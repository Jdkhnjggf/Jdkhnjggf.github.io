---
layout:     post
title:      "CacheWarp —— AMD CPUs上的芯片漏洞"
subtitle:   ""
date:       2023-11-16 02:01:00
author:     "luobobo"
header-img: "img/timewarp-logo.jpg"
tags:
    - paper
---


## CacheWarp Attack

2023年11月15日凌晨，来自CISPA亥姆霍兹信息安全中心和格拉茨科技大学的研究员公布了存在于AMD EPYC CPUs上的芯片漏洞 —— CacheWarp (CVE-2023-20592)。攻击者可以恶意地使用INVD指令抹去任意写入内存的操作，从而破坏内存保护机制，并在云虚拟机中实现远程代码执行或权限提升。研究人员们已经在论文中详细描述了漏洞的原理和攻击方法，并公布了[相关代码](https://github.com/cispa/CacheWarp)和[演示视频](https://cachewarpattack.com/#demo)。多家安全媒体如DarkReading, The Hacker News, SecurityWeek, Cyber Security News, BNN, The Register, Gigazine等已经对此进行了报道。

![timewarp_toy](/img/cw_author.jpg)

### 背景

AMD的EPYC系列芯片从2016年开始加入了SEV (Secure Encrypted Virtualization) 功能,用于加密内存，提高云服务的安全性。云用户可以在不受信任的管理程序 (Hypervisor) 中部署虚拟机。

AMD在近几年针对SEV功能进行过两次安全升级，分别为SEV-ES (Encrypted State) 与SEV-SNP (Secure Nested Paging)。在2022年，Google Project Zero团队和Google Cloud Security团队一起为SEV-SNP做了安全审计，AMD宣称SEV-SNP保护了Guest VM的完整性，没有攻击者可以篡改其数据。

但CacheWarp证明，即便是最新的安全措施SEV-SNP也存在安全风险。AMD已经对第三代EPYC CPU进行了修复，但第一二代的EPYC CPU将不提供修复。


### INVD - Invalidate Internal Caches

INVD 是x86中的一个特权指令，用于清空CPU的缓存。攻击者可以通过特定的方式使用这个指令，破坏正常的内存操作。默认情况下，AMD芯片上的INVD指令会被转换为WBINVD - Wribe back and invalidate cache，确保了内存一致性。但通过配置Model Specific Register (MSR)，攻击者可将这个转换功能关闭，进而抹除victim对内存的任意写操作。在Intel芯片上，当SGX/TDX功能开启时，执行INVD指令将触发#GP错误。

由于INVD指令是特权指令，攻击者不能只是普通用户。这种特殊的要求却恰好符合TEE的攻击场景，因为攻击者是不受信任的Hypervisor。

### TimeWarp

程序使用内存不仅仅是存储全局变量和结构，还包括使用堆栈来记录函数返回地址等。在x86上，函数调用指令CALL可拆分为一个PUSH+一个JMP，CPU将返回地址存在栈上，之后再跳转到被执行的函数地址。

CacheWarp的第一种攻击方法TimeWarp，就是攻击CALL这一指令，替换当前函数的返回值为后续待执行函数的返回值。下图代码展示了我们为TimeWarp设计的一个toy example，while循环中判断函数ret1()的返回值是否为0 (当然不是)，之后再调用函数ret0()。理论上来说，这个函数永远也执行不了puts(“WIN”)。

![timewarp_toy](/img/timewarp_toy.jpg)

程序在执行函数ret1 (对应着汇编代码的Line5) 之前，返回地址(Line6)会被保存至栈上。在执行函数ret0 (Line12) 之前，返回地址(Line13)会被保存至栈上同一位置，覆盖原来的返回地址(Line6)。然而，所有对内存读写的数据会先存于缓存中。攻击者通过结合INVD以及WBINVD指令，将旧返回地址(Line6)写回内存，并把新返回地址(Line13)抹除。CPU将以函数ret0的返回值，跳转回到执行完函数ret1后返回的位置，就像函数ret1返回了0一样。

![timewap-toy-work](/img/timewap-toy-work.jpg)

看到我post的图之后，Youheng风风火火地从隔壁赶来跟我"Give me Five!"

一番讨论后，我们第一个要测的strcmp，理论上来说它很常用且相当好attack。有了TimeWarp以后我们可以轻松地让任意两个字符串完全匹配。因为，我们可以用任一后续函数的返回值作为strcmp的结果，也就是匹配成功。

可惜在现实中strcmp都因为optimization被编译器优化掉了。我们不得不找新的Gadgets.


#### OpenSSH - "Works"

攻击者可以使用TimeWarp攻击 OpenSSH的密码验证。 sys_auth_passwd 函数检查用户是否输入了正确的密码。当函数返回 1 时，表明用户已通过身份验证。

![timewarp-openssh](/img/timewarp-openssh.jpg)

攻击者只需要在执行xcrypt函数后使用TimeWarp，程序将返回至Line5，并重用xcrypt的返回值：

```
pw_password = xcrypt(password, salt);
encrypted_password = xcrypt(password, salt);
```

由此，攻击者可通过任意密码登陆进AMD-SEV虚拟机。


### DropForge

这种方法通过重置内存中的数据，让攻击者能够控制程序的行为。

![dropforge-toy](/img/dropforge-toy.jpg)

上图为另一个toy example，victim(1,1)理论上说只要1*10+1 == 11，循环就不会被打破。但任何Memory writes，包括由编译器引入的参数传递，局部变量，返回值，只要是写在内存而非寄存器中，都有可能会在缓存阶段被抹除。

#### sudo

在成功攻击OpenSSH得到任意代码执行之后，权限提升自然而然成了下一个攻击目标。通过DropForge方法，攻击者可以使sudo命令误认为攻击者拥有root权限。

下图是sudo中的一段代码。这段代码通过getuid()的返回值来判断调用者是否具有管理者权限。若是由root账户调用，get_uid将返回0，反之则不是。

```assembly
mov rax, 0x66
syscall  (get_uid)
ret
mov [MEM], rax <-- TARGET
```

在最后一行，sudo将get_uid的返回值存入中，攻击者将这一指令抹除，将得到的是一个初始化的值。巧合的是，在这之前，sudo会将这一段memory初始化为0。攻击者就这样成为了root。

![sudo-happy](/img/sudo-happy.jpg)

### 单步执行

上述攻击都有个前提，那就是攻击者需要在正确的时间执行INVD指令。

为此作者开源了一套稳定的中断框架，利用APIC Timer，单步执行Guest VM的每一个指令。类似的方法最早由鲁汶大学的Jo Van Bulck提出。Jo公开的工具，sgx-step[1]，可以单步执行SGX Enclave中的指令。之后，Mengyuan Li et al.[2] 测试了APIC-Timer中断在AMD-SEV中实现单步执行的可能性。由于AMD-SEV中上下文切换所带来的噪音高于SGX，单步执行并未在AMD-SEV中完全实现。CacheWarp的作者们利用WBINVD指令在每次上下文切换前实现缓存状态的一致性，大幅降低了噪音，实现了稳定的单步执行功能。由Luca Wilke et al. [3]提出的同期工作sev-step也实现了稳定的单步执行功能。

### 其他

CacheWarp还可以与Cache Eviction结合，攻击者可以有选择性地保留缓存中的值。此外，INVD的行为竟与官方手册的描述不符，作者们在论文中详细地分析了这一指令。更多内容请在paper中一探究竟吧～

相关代码：https://github.com/cispa/CacheWarp
演示视频：https://cachewarpattack.com/#demo
论文下载：https://www.usenix.org/system/files/sec24summer-prepub-742-zhang-ruiyi.pdf

### 参考链接

[1] J. Van Bulck, F. Piessens, and R. Strackx, “SGX-Step: A Practical Attack Framework for Precise Enclave Execution Control,” in Workshop on System Software for Trusted Execution, 2017.

[2] M. Li, Y. Zhang, H. Wang, K. Li, and Y. Cheng, “Cipherleaks: Breaking constant-time cryptography on amd sev via the ciphertext side channel,” in USENIX Security Symposium, 2021.

[3] L. Wilke, J. Wichelmann, A. Rabich, and T. Eisenbarth, “Sev-step: A single-stepping framework for amd-sev,” 2023.


- [Ruiyi Zhang](https://zhangruiyi.me/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Lukas Gerlach](https://roots.ec/people/lukas-gerlach/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Daniel Weber](https://roots.ec/people/daniel-weber/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Lorenz Hetterich](https://roots.ec/people/lorenz-hetterich/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Youheng Lü](https://www.linkedin.com/in/youheng-lü-a799ba227/)  (Independent)
- [Andreas Kogler](https://andreaskogler.com/)  [(Graz University of Technology)](https://www.iaik.tugraz.at/)
- [Michael Schwarz](https://misc0110.net/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)