---
layout:     post
title:      "Microarchitecture Security Paper Note（中文向）"
subtitle:   ""
date:       2023-08-01 02:01:00
author:     "luobobo"
header-img: "img/post1.jpg"
tags:
    - paper
---

在过去十年间，越来越多的测信道(side channel)攻击被研究人员发现。在2017年Meltdown和Spectre的出现之后，Microarchitecture安全这一领域在工业界和学术界都受到了更广泛的关注。新的防御措施和攻击变种交替更迭，硬件上频频更新的优化策略又会带来哪些安全问题？只要各家芯片厂商的官方文档一天不完全公开 (Intel Manual虽有5000+页但还是冰山一角)，只要researcher还得将CPU们当作一个个“可信”的黑盒，那这个领域就还有很多安全问题值得探究 :)

在选"Software-based Microarchitecture Attacks"作为PhD的研究方向之后，我花了很长时间才真正入门(读Manual，读各个小方向的paper，复现，and 被老板和同事们带xD)。这一方面是因为这些过于底层的细节确实晦涩，二是中文互联网上有用的信息较少。本文打算尽可能简短地(我很懒)概括我读过的一些paper，做一点小小的贡献。

PS: 以防各位天才们通过side channel分析出我/我们组正在under review / TODO 的ideas，相关的paper**可能**会被跳过。



[[14 USENIX] FLUSH+RELOAD: a High Resolution, Low Noise, L3 Cache Side-Channel Attack](https://eprint.iacr.org/2013/448.pdf)
   
经典side channel，理解modern CPU的Cache Architecture的好机会。Attacker需要有跟victim的shared memory。Attacker用clflush指令flush一个cache line，等待，再timing一次这个address的memory access，通过这个时间差异(cache hit/miss)来判断victime有没有在waiting period access the cache line。

[[15 S&P] Prime+Probe: Last-Level Cache Side-Channel Attacks are Practical](http://palms.ee.princeton.edu/system/files/SP_vfinal.pdf)

跟F+R相比，P+P不需要shared memory，不需要clflush指令，用在cloud env里更方便。相反它需要提前构建一个eviction set，access其中的所有address来把目标cacheline“挤”出去。但构建eviction set，需要理解如何计算phys addr => cache index & cache slice。

[[16 DIMVA] Flush+Flush: A Fast and Stealthy Cache Attack](https://gruss.cc/files/flushflush.pdf)

Target在或不在cache中，对flush的timing也有影响。有一点像F+R的替代版，但更stealthy。

[[15 USENIX] Cache Template Attacks: Automating Attacks on Inclusive Last-Level Caches](https://gruss.cc/files/cta.pdf)

教你如何将上述三种side channels用于实践。去复现。

[[16 USENIX] DRAMA: Exploiting DRAM Addressing for Cross-CPU Attacks](https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_pessl.pdf)

不仅cache有hit/miss，DRAM的shared across processors的row buffer也有hit/miss。本文presents了一个很快的covert channel，还给了一个逆向dram arch的工具。读完还能理解下rowhammer。
【去读。(1) Open Source! (2) 我乐于找机会给老板涨citation】

[[17 USENIX] Prime+Abort: A Timer-Free High-Precision L3 Cache Attack using Intel TSX](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-disselkoen.pdf)

相比于P+P，P+A依赖于Intel的TSX，可以理解成blockchain里的transaction。当victim event发生后，transaction abort，不然就commit。这样可以不依赖timer。但TSX这个功能因为安全性问题太多已经被Intel弃用。

[[19 S&P] Meltdown: Reading Kernel Memory from User Space](https://meltdownattack.com/meltdown.pdf)

Meltdown & Spectre之前大家对于side channel还只是停留在break cryptography，transient execution attacks之后开启了一个新研究纪元。 因CPU的out-of-order execution特性，指令会被乱序执行，依序retired(commit, visible)。 当访问inaccessible的memory时，CPU需要去检查权限(读页表等等)。这一步骤对于CPU来说很慢，所以CPU会假设它能够读到这个value，并以此接着执行，当权限结果返回时(报错)，所有状态回滚，user没法architecturally看见不可访问的数据(registers/memory...)，但这个traces会留在microarchitecture(e.g., cache)里。 Attacker可以用side channel作为building block将这个值泄漏出来。作者们把这类攻击叫做transient execution attack。【去读。(1) nb! (2) 我乐于找机会给老板涨citation】

[[18 USENIX] Spectre Attacks: Exploiting Speculative Execution](https://spectreattack.com/spectre.pdf)

相比于out-of-order execution, Spectre attack speculative execution。例如当CPU遇到in/direct branch，*确定判断条件*这个步骤很慢，CPU需要预测一个branch来执行(根据一些microarchitectural elements)。所以Spectre需要找到特定的gadget, 在错误预测分支后，leak secret，revert，再用side channel 读出secret。【去读。(1) nb! (2) 我乐于找机会给老板涨citation】

[[19 USENIX] A Systematic Evaluation of Transient Execution Attacks and Defenses](https://www.usenix.org/system/files/sec19-canella.pdf)

标题总结完了。各种variants和defenses。有个mind map https://transient.fail/
【去读/复现。(1) open source! (2) 我乐于找机会给老板涨citation】

MDS的众多paper暂且跳过(懒)。

[[19 S&P] Attack Directories, Not Caches:Side-Channel Attacks in a Non-Inclusive World](https://people.csail.mit.edu/mengjia/data/sp19.pdf)

Intel的server CPU还有AMD的CPU一般用的是non-inclusive L3 cache，这样有些cache attacks没有办法简单地port过来。作者逆向了一个directory的结构，成功在non-inclusive caches实现了cache attacks。 Solid work.

[[21 USENIX] Osiris: Automated Discovery of Microarchitectural Side Channels](https://publications.cispa.saarland/3431/1/main.pdf)

找新的side channel是个枯燥的工作，一般需要researcher读很多手册，做实验测试，很麻烦。Osiris是一个fuzzing-based的框架，自动地找x86 instruction里的timing side channel。
【去读/复现。(1) 很好复现!really good work！ (2) 都xx鸽们.jpg】

[[21 CCS] Prime+Scope: Overcoming the Observer Effect for High-Precision Cache Contention Attacks](https://www.esat.kuleuven.be/cosic/publications/article-3405.pdf)

P+P每次都得access一长串addrs怎么办？P+S可以把它简化到每次reset只需要access一个地址。作者还开源了一个工具来自动寻找这样的prime pattern (for P+P & P+S)。结果。 Novel work!

[[21 USENIX] Lord of the Ring(s): Side Channel Attacks on the CPU On-Chip Ring Interconnect Are Practical](https://www.usenix.org/system/files/sec21-paccagnella.pdf)

L3 cache 是multi-processors共享的，可以把它们看成一个环。作者present了一种由ring之间contention引起的timing-based side channel。

[(22 S&P) Adversarial Prefetch: New Cross-Core Cache Side Channel Attacks](https://arxiv.org/pdf/2110.12340.pdf)

Prefetch instructions 也可以用来做side channel attacks。文中还分析了各种prefetch指令与cache coherence state之间的关系。

[(22 USENIX) AMD Prefetch Attacks through Power and Time](https://misc0110.net/files/amd_prefetch_sec22.pdf)

Prefetch instructions 可以用来infer TLB state，Timing和Power上都有差距。

[(22 USENIX) Rapid Prototyping for Microarchitectural Attacks](https://misc0110.net/files/rapid_prototyping_sec22.pdf)

一个很好的框架/库来实施各种各样的microarchitectural attacks。

未完待续(下次更TEE，DVFS)