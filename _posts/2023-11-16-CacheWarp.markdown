---
layout:     post
title:      "CacheWarp —— AMD CPUs上的新漏洞"
subtitle:   ""
date:       2023-11-16 02:01:00
author:     "luobobo"
header-img: "img/timewarp-log.jpg"
tags:
    - paper
---


## CacheWarp Attack —— AMD CPU中的时空旅行

这周三，我们披露了新的AMD CPU漏洞 —— CacheWarp (CVE-2023-20592) ! 攻击者可以在一分钟内直连进Victim VM并且完成权限提升为root账户。

欢迎在我们的[网站](https://cachewarpattack.com/)上查看上传的Demo视频，完整的学术论文，以及已开源的全部代码。

CacheWarp攻击的是SEV (Secure Encrypted Virtualization)这一功能。AMD希望通过SEV，云用户(guest VM)可以信任云服务商(Hypervisor)，因为每一个guest VM都会分配到一个由芯片单独生成的key并用此加密，没有其他人可以读/更改。SEV在近几年进行过两次安全升级，分别为SEV-ES与SEV-SNP。在去年，Google Project Zero和Google Cloud Security一起为SEV-SNP做了安全审计，AMD宣称SEV-SNP保护了Guest VM的完整性，没有人可以篡改其数据。

然而，CacheWarp, 利用INVD指令，就可以”隐秘地““抹除”guest VM对内存的任何修改，并让guest VM以旧数据的值继续执行。**这一攻击在SEV, SEV-ES, SEV-SNP上全部适用。**目前，AMD已经在第三代EPYC CPUs上对SEV-SNP进行了修复，并不再对第一代和第二代EPYC CPU上的 SEV/SEV-ES进行修复。

### TimeWarp --- 时间穿梭

我们提出的第一种攻击方法，是攻击CALL这一指令。

在x86上，CALL可拆分为一个PUSH+一个JMP，返回地址将被Push至栈上。然而，在被更新回内存(Main Memory)之前，所有的值都会先在缓存(Cache)中被更改或取用。而INVD指令，会丢弃所有缓存中的值，像橡皮擦一样将缓存完全清空了。



![timewarp_toy](../img/timewarp_toy.jpg)

上图代码展示了我们为TimeWarp设计的一个toy example，while循环中判断函数ret1()的返回值是否为0 (当然不是)，之后再调用函数ret0()。理论上来说，这个函数永远也执行不了puts("WIN")。



执行ret1 (对应着汇编代码的Line5) 之前，返回地址(Line6)会被保存至栈上。在执行ret0 (Line12) 之前，返回地址(Line13)会被保存至栈上同一位置，覆盖原来的返回地址(Line6)。 但在它还在缓存中时，INVD把它抹去了。CPU将以ret0的返回值，跳转回到执行完ret1后返回的位置。

0=0，bingo，我们在命令行上看到“WIN”。

![timewap-toy-work](../img/timewap-toy-work.jpg)

看到我post的图之后，Youheng风风火火地从隔壁赶来跟我"Give me Five!"



一番讨论后，我们第一个要测的strcmp，理论上来说它很常用且相当好attack。有了TimeWarp以后我们可以轻松地让任意两个字符串完全匹配。可惜在现实中strcmp都因为optimization被编译器优化掉了。我们不得不找新的Gadgets.



#### OpenSSH - "Works"

![timewarp-openssh](../img/timewarp-openssh.jpg)

Maybe是几杯咖啡下肚，或者是去买饮料的路上呼吸的新鲜空气，我们很快找到了新的Gadget。

既然strcmp不行， 我们在Line 9执行xcrypt后使用Timewarp，时间回到Line 5，*pw_password指向了新的地址——xcrypt(password, salt)，也就是后文中与encrypted_password相同的值。

无需得知ssh的密码，Attacker就能登进你的VM！



### DropForge --- 锻造

第二种方法，可以对缓存进行操作，并重置guest对数据所做的更改

![dropforge-toy](../img/dropforge-toy.jpg)

上图为另一个toy example，理论上说只要1*10+1 == 11，循环就不会被打破。但任何Memory writes，包括由编译器引入的参数传递，局部变量，返回值，只要写在内存中，都有可能会在缓存阶段被抹除。

#### sudo

```assembly
mov rax, 0x66
syscall  (get_uid)
ret
mov [MEM], rax <-- TARGET
```

上图是sudo binary中的一段代码，若是由root账户调用，get_uid将返回0，反之则不是。

在最后一行，sudo将get_uid的返回值 (%rax) 写回Memory中，攻击者将这一write抹除，得到的是一个stale value。有趣的是，在这之前，sudo会将这一段memory初始化为0。

就这样轻松地成为了root。

![sudo-happy](img/sudo-happy.jpg)



### 其他

以上的PoC都有一个assumption，就是需要在正确的时间执行INVD指令。为此，我们实现了一套稳定的中断框架，利用APIC Timer，单步执行guest VM的每一个指令。此外，结合另一个方法，我们还可以知道VM中执行到的具体是哪一段指令...详细内容请读我们的paper，在此不再深入讨论。



- [Ruiyi Zhang](https://zhangruiyi.me/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Lukas Gerlach](https://roots.ec/people/lukas-gerlach/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Daniel Weber](https://roots.ec/people/daniel-weber/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Lorenz Hetterich](https://roots.ec/people/lorenz-hetterich/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)
- [Youheng Lü](https://www.linkedin.com/in/youheng-lü-a799ba227/)  (Independent)
- [Andreas Kogler](https://andreaskogler.com/)  [(Graz University of Technology)](https://www.iaik.tugraz.at/)
- [Michael Schwarz](https://misc0110.net/)  [(CISPA Helmholtz Center for Information Security)](https://cispa.de/)