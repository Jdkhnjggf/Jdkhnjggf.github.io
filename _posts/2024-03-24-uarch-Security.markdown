---
layout:     post
title:      "Microarchitecture Security 研究方向（中文向）"
subtitle:   "微架构安全"
date:       2024-04-27 02:01:00
author:     "luobobo"
header-img: "img/paper-note-bg.jpg"
tags:
    - paper
---

这篇博客本来只是随手记录的一些笔记，但貌似由于过于biased而产生了不好的影响。
再加上距上次更新也有大半年过去了，我的认知又丰富了一点 ;) 所以打算重新整理一下。

声明：我的研究方向主要在x86上的side-channels attacks & architectural attacks，如果对其他方向 (ARM/Rowhammer/GPU/ML-Based/...)，其他会议/期刊(非四大安全会/期刊/体系结构会议如MICRO/ISCA/HPCA/...) 的papers有忽略，欢迎提醒/指正/补充。Just drop me a mail (ruiyi.zhang [AT] cispa.de) or open an issue. 感谢.

只是入门的话，并不需要看完每一篇paper，只需要对某一方向有大致的了解就可以了。

Opinions (and lack of them) are my own :)

# 微架构安全有哪些研究方向：

## 处理器(CPU):


**按时间线分类**

侧信道(side channels) -> 瞬态执行攻击(Transient Execution Attacks) -> 架构安全(Architectural Security)

**按victim分类**

可信执行环境(Trusted Execution Environment - TEE), 加密算法(Cryptography)

**按attacker分类**

TEE (Attacker可以是privileged的hypervisor) <- side channels / transient execution attacks 需要普通用户的执行权限 -> Microarchitectural Attacks from browser (需要的权限最少)

**防御**

### 侧信道:

侧信道泄露metadata而不是直接泄露data，例如侧信道可以让攻击者知道内存里的某个地址是否刚刚被access了，而不能直接知道这个地址里的值具体是多少。

#### 跟缓存(Cache)相关的

[[14 USENIX] FLUSH+RELOAD: a High Resolution, Low Noise, L3 Cache Side-Channel Attack](https://eprint.iacr.org/2013/448.pdf)

[[15 S&P] Prime+Probe: Last-Level Cache Side-Channel Attacks are Practical](http://palms.ee.princeton.edu/system/files/SP_vfinal.pdf)

[[16 DIMVA] Flush+Flush: A Fast and Stealthy Cache Attack](https://gruss.cc/files/flushflush.pdf)

[[21 CCS] Prime+Scope: Overcoming the Observer Effect for High-Precision Cache Contention Attacks](https://www.esat.kuleuven.be/cosic/publications/article-3405.pdf)

[[22 S&P] Adversarial Prefetch: New Cross-Core Cache Side Channel Attacks](https://arxiv.org/pdf/2110.12340.pdf)

[[22 USENIX] HyperDegrade: From GHz to MHz Effective CPU Frequencies](https://www.usenix.org/system/files/sec22-aldaya.pdf)


#### 跟某一指令相关的

**TSX**

[[17 USENIX] Prime+Abort: A Timer-Free High-Precision L3 Cache Attack using Intel TSX](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-disselkoen.pdf)

**Software Prefetcher**

[[22 USENIX] AMD Prefetch Attacks through Power and Time](https://misc0110.net/files/amd_prefetch_sec22.pdf)

**UMWAIT**

[[23 USENIX] (M)WAIT for It: Bridging the Gap between Microarchitectural and Architectural Side Channels](https://publications.cispa.saarland/3769/1/mwait_sec23.pdf)

#### 跟其他结构相关的

**Directory**

[[19 S&P] Attack Directories, Not Caches:Side-Channel Attacks in a Non-Inclusive World](https://people.csail.mit.edu/mengjia/data/sp19.pdf)

**Ring**

[[21 USENIX] Lord of the Ring(s): Side Channel Attacks on the CPU On-Chip Ring Interconnect Are Practical](https://www.usenix.org/system/files/sec21-paccagnella.pdf) 

**TLB**

[[22 USENIX] Binoculars: Contention-Based Side-Channel Attacks Exploiting the Page Walker](https://www.usenix.org/system/files/sec22-zhao-zirui.pdf)

[[22 USENIX] TLB;DR: Enhancing TLB-based Attacks with TLB Desynchronized Reverse Engineering](https://download.vusec.net/papers/tlbdr_sec22.pdf)

**ROB**

[[22 USENIX] SecSMT: Securing SMT Processors against Contention-Based Covert Channels](https://www.usenix.org/system/files/sec22summer_taram.pdf)

**Mesh**

[[22 USENIX] Don’t Mesh Around: Side-Channel Attacks and Mitigations on Mesh Interconnects](https://www.usenix.org/system/files/sec22-dai.pdf)

**Prefetcher**

[[23 USENIX] BunnyHop: Exploiting the Instruction Prefetcher](https://www.usenix.org/system/files/usenixsecurity23-zhang-zhiyuan-bunnyhop.pdf)

**Execution Port**

[[22 ESORICS] CPU Port Contention Without SMT](https://misc0110.net/files/portcontention_esorics22.pdf)

#### Linux Kernel
[[22 NDSS] Remote Memory-Deduplication Attacks](https://martinschwarzl.at/media/files/remote_dedup.pdf)

[[23 S&P] SQUIP: Exploiting the Scheduler Queue Contention Side Channel](https://martinschwarzl.at/media/files/squip.pdf)

#### Power / Hertz

[[21 S&P] Platypus: Software-based Power Side-Channel Attacks on x86](https://platypusattack.com/platypus.pdf)

[[22 USENIX] Hertzbleed: Turning Power Side-Channel Attacks Into Remote Timing Attacks on x86](https://www.hertzbleed.com/hertzbleed.pdf)

[[23 S&P] DVFS frequently leaks secrets: Hertzbleed attacks beyond SIKE, cryptography, and CPU-only data](https://www.hertzbleed.com/2h2b.pdf)

#### 其他架构 RISC-V / ARM

[[23 S&P] A Security RISC: Microarchitectural Attacks on Hardware RISC-V CPUs](https://misc0110.net/files/riscv_attacks_sp23.pdf)

[[23 USENIX] Synchronization Storage Channels (S2C): Timer-less Cache Side-Channel Attacks on the Apple M1 via Hardware Synchronization Instructions](https://www.usenix.org/system/files/usenixsecurity23-yu-jiyong.pdf)

#### Fuzzing side-channels

[[20 NDSS] ABSynthe: Automatic Blackbox Side-channel Synthesis on Commodity Microarchitectures](https://comsec.ethz.ch/wp-content/files/absynthe_ndss20.pdf)

[[21 USENIX] Osiris: Automated Discovery of Microarchitectural Side Channels](https://publications.cispa.saarland/3431/1/main.pdf)

#### Hardware Fuzzers

[[23 Usenix] HyPFuzz: Formal-Assisted Processor Fuzzing](https://www.usenix.org/system/files/usenixsecurity23-chen-chen.pdf)

[[23 USENIX] MorFuzz: Fuzzing Processor via Runtime Instruction Morphing enhanced Synchronizable Co-simulation](https://www.usenix.org/system/files/usenixsecurity23-xu-jinyan.pdf)

[[24 USENIX] Cascade: CPU Fuzzing via Intricate Program Generation](https://comsec.ethz.ch/wp-content/files/cascade_sec24.pdf)

[[24 Usenix] WhisperFuzz: White-Box Fuzzing for Detecting and Locating Timing Vulnerabilities in Processors](https://arxiv.org/pdf/2402.03704.pdf)

### Leak Data (但不是transient-execution)

[[22 S&P] Augury: Using Data Memory-Dependent Prefetchers to Leak Data at Rest](https://www.prefetchers.info/augury.pdf)


[[23 USENIX] Collide+Power: Leaking Inaccessible Data with Software-based Power Side Channels](https://collidepower.com/paper/Collide+Power.pdf)


### Transient Execution Attacks:

> 侧信道作为TEA的building block，直接leak data

[[19 S&P] Meltdown: Reading Kernel Memory from User Space](https://meltdownattack.com/meltdown.pdf)

[[18 USENIX] Spectre Attacks: Exploiting Speculative Execution](https://spectreattack.com/spectre.pdf)

**Microarchitectural Data Sampling (MDS)** 

跟Meltdown / Spectre 相比，MDS Attacks leak的是in-flight data (就是这个data正在被其他user/hyperthreading使用，存在某一个element里，如line-fill buffer / load buffer / store buffer...)

[[18 USENIX] FORESHADOW: Extracting the Keys to the Intel SGX Kingdom with Transient Out-of-Order Execution](https://foreshadowattack.eu/foreshadow.pdf)

[[19 S&P] RIDL: Rogue In-Flight Data Load](https://mdsattacks.com/files/ridl.pdf)

[[19 CCS] Fallout: Leaking Data on Meltdown-resistant CPUs](https://misc0110.net/files/fallout.pdf)

[[19 CCS] ZombieLoad: Cross-Privilege-Boundary Data Sampling](https://zombieloadattack.com/zombieload.pdf)

[[19 USENIX] A Systematic Evaluation of Transient Execution Attacks and Defenses](https://www.usenix.org/system/files/sec19-canella.pdf)

[[20 S&P] LVI: Hijacking Transient Execution through Microarchitectural Load Value Injection](https://lviattack.eu/lvi.pdf) 他们的[预告片](https://www.youtube.com/watch?v=baKHSXeIIaI&t=1s)很有趣

[[21 USENIX] Rage Against the Machine Clear: A Systematic Analysis of Machine Clears and Their Implications for Transient Execution Attacks](https://www.vusec.net/projects/fpvi-scsb/)


**GDS**

[[23 USENIX] Downfall: Exploiting Speculative Data Gathering](https://downfall.page/media/downfall.pdf)

**RFDS**
[RFDS-Intel](https://www.intel.com/content/www/us/en/security-center/advisory/intel-sa-00898.html) 

**More Spectre..** 

Varients请查transient.fall

**绕过Spectre Mitigation** 


[[20 CCS] Speculative Probing: Hacking Blind in the Spectre Era](https://comsec.ethz.ch/wp-content/files/blindside_ccs20.pdf)

[[21 CCS] Exorcising Spectres with Secure Compilers](https://dl.acm.org/doi/pdf/10.1145/3460120.3484534)

[[22 USENIX] Branch History Injection: On the Effectiveness of Hardware Mitigations Against Cross-Privilege Spectre-v2 Attacks](https://download.vusec.net/papers/bhi-spectre-bhb_sec22.pdf)

[[22 USENIX] Retbleed: Arbitrary Speculative Code Execution with Return Instructions](https://comsec.ethz.ch/wp-content/files/retbleed_sec22.pdf)

[[23 USENIX] Breaking and Fixing Speculative Load Hardening](https://zhangzhiyuan.me/publication/uslh.pdf)

[[23 USENIX] Inception: Exposing New Attack Surfaces with Training in Transient Execution](https://comsec.ethz.ch/wp-content/files/inception_sec23.pdf)

[[24 USENIX] GhostRace: Exploiting and Mitigating Speculative Race Conditions](https://download.vusec.net/papers/ghostrace_sec24.pdf)

**找Spectre Gadgets** 

[[21 NDSS] SpecTaint: Speculative Taint Analysis for Discovering Spectre Gadgets](https://www.cs.ucr.edu/~heng/pubs/SpecTaint.pdf)

[[22 NDSS] Kasper: Scanning for Generalized Transient Execution Gadgets in the Linux Kernel](https://comsec.ethz.ch/wp-content/files/kasper_ndss22.pdf)

[[24 USENIX] InSpectre Gadget: Inspecting the Residual Attack Surface of Cross-privilege Spectre v2](https://download.vusec.net/papers/inspectre_sec24.pdf)

### Architectual Vulnerability:

芯片厂商把这些**内部发现的**bugs叫做Errata

[[22 USENIX] ÆPIC Leak: Architecturally Leaking Uninitialized Data from the Microarchitecture](https://aepicleak.com/aepicleak.pdf)

[Zenbleed](https://lock.cmpxchg8b.com/zenbleed.html) & [Reptar](https://lock.cmpxchg8b.com/reptar.html) by GPZ的Tavis Ormandy

[[24 USENIX] CacheWarp: Software-based Fault Injection using Selective State Reset](https://cachewarpattack.com/paper.pdf)

**Fault Attacks**

[[19 CCS / 20 Asian HOST] VoltJockey: Breaching TrustZone by Software-Controlled Voltage Manipulation over Multi-core Frequencies](https://dl.acm.org/doi/abs/10.1145/3319535.3354201)

[[20 S&P] Plundervolt: Software-based Fault Injection Attacks against Intel SGX](https://plundervolt.com/doc/plundervolt.pdf)

[[20 USENIX] V0LTpwn: Attacking x86 Processor Integrity from Software](https://www.usenix.org/system/files/sec20-kenjar.pdf)

### 可信执行环境(TEE)

TEE是芯片厂商设计的一种安全功能。 与加密算法一样，是Side Channels常见的攻击对象。此外，TEE的threadt model允许attacker具有priviledge权限，所以有一些新的攻击面。

这里不推荐paper了。

对于Intel SGX，推荐阅读SGX-STEP作者Dr. Jo Van Bulck的[PhD Thesis - Microarchitectural Side-Channel Attacks for Privileged Software Adversaries](https://jovanbulck.github.io/files/phd-thesis.pdf) 

对于AMD SEV，推荐阅读Dr. Mengyuan Li的[PhD Thesis - Understanding and Exploiting Design Flaws of AMD Secure Encrypted Virtualization](https://etd.ohiolink.edu/acprod/odb_etd/ws/send_file/send?accession=osu1658413600898645&disposition=inline)

我对ARM TEE并不熟悉，但SUSTech 张锋巍老师的组好像有不少[相关工作](https://compass.sustech.edu.cn/publications_en.html)

### 加密算法

To mitigate side-channels attacks, many cryptographic libraries have to implement a constant-time version.

[[23 CCS] A Systematic Evaluation of Automated Tools for Side-Channel Vulnerabilities Detection in Cryptographic Libraries](https://cmaurice.fr/pdf/ccs23_geimer.pdf)

[[24 USENIX] GoFetch: Breaking Constant-Time Cryptographic Implementations Using Data Memory-Dependent Prefetchers](https://gofetch.fail/files/gofetch.pdf)

### 防御

[[20 NDSS] ConTExT: A Generic Approach for Mitigating Spectre](https://misc0110.net/files/context.pdf)

[[21 USENIX]ScatterCache: Thwarting Cache Attacks via Cache Set Randomization](https://misc0110.net/files/scattercache.pdf)

还有一些用PMC/Power Consumption来检测攻击的paper

### Formal Methods

[Prof. JAN REINEKE](https://embedded.cs.uni-saarland.de/reineke.php) 和 [Prof. Marco Guarnieri](https://mguarnieri.github.io/)做了不少这个方向的工作。

[[20 S&P] SPECTECTOR: Principled Detection of Speculative Information Flows](https://spectector.github.io/papers/spectector.pdf)

[[21 S&P] Hardware-Software Contracts for Secure Speculation](https://spectector.github.io/papers/hwsw-contracts.pdf)

[[22 CCS] Automatic Detection of Speculative Execution Combinations](https://mguarnieri.github.io/publication/ccs2022/ccs2022.pdf)

[[23 S&P] Hide and Seek with Spectres: Efficient discovery of speculative information leaks with random testing](https://mguarnieri.github.io/publication/sp2023/sp2023.pdf)

[[23 CCS] Specification and Verification of Side-channel Security for Open-source Processors via Leakage Contracts](https://arxiv.org/pdf/2305.06979.pdf)

### Attack from browser
[[19 NDSS] JavaScript Template Attacks: Automatically Inferring Host Information for Targeted Exploits](https://misc0110.net/files/jstemplate.pdf)

[[18 NDSS] JavaScript Zero: Real JavaScript and Zero Side-Channel Attacks](https://misc0110.net/files/jszero.pdf)

[[17 ESORICS] Practical Keystroke Timing Attacks in Sandboxed JavaScript](https://misc0110.net/files/keystroke_js.pdf)

[[17 FC] Fantastic Timers and Where to Find Them: High-Resolution Microarchitectural Attacks in JavaScript](https://misc0110.net/files/timers.pdf)

[[16 DIMVA] Rowhammer.js: A Remote Software-Induced Fault Attack in JavaScript](https://gruss.cc/files/rowhammerjs.pdf)

[[15 ESORICS] Practical Memory Deduplication Attacks in Sandboxed Javascript](https://gruss.cc/files/dedup.pdf)
## 内存(DRAM):

#### 侧信道

[[16 USENIX] DRAMA: Exploiting DRAM Addressing for Cross-CPU Attacks](https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_pessl.pdf)

#### Rowhammer

不是很熟，看过一些，没复现过。

[[14 ISCA] Flipping Bits in Memory Without Accessing Them: An Experimental Study of DRAM Disturbance Errors](https://users.ece.cmu.edu/~yoonguk/papers/kim-isca14.pdf)

[[16 CCS] Drammer: Deterministic Rowhammer Attacks on Mobile Platforms](https://vvdveen.com/publications/drammer.pdf)

[[16 USENIX] Flip Feng Shui: Hammering a Needle in the Software Stack](https://download.vusec.net/papers/flip-feng-shui_sec16.pdf)

[[18 S&P] Another Flip in the Wall of Rowhammer Defenses](https://misc0110.net/files/another_flip.pdf)

[19 RowHammer: A Retrospective](https://arxiv.org/pdf/1904.09724.pdf)

[[20 S&P] TRRespass: Exploiting the Many Sides of Target Row Refresh](https://download.vusec.net/papers/trrespass_sp20.pdf)

[[21 USENIX] SMASH: Synchronized Many-sided Rowhammer Attacks From JavaScript](https://download.vusec.net/papers/smash_sec21.pdf)

[[22 S&P] BLACKSMITH: Scalable Rowhammering in the Frequency Domain](https://comsec.ethz.ch/wp-content/files/blacksmith_sp22.pdf)

[[24 USENIX] ZenHammer: Rowhammer Attacks on AMD Zen-based Platforms](https://comsec.ethz.ch/wp-content/files/zenhammer_sec24.pdf)

## 图形处理器(GPU):

感觉GPU上目前主要还是侧信道攻击，但我对这个方向不太了解


# OLD VERSION

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

MDS的众多paper暂且跳过(懒)。可查 https://mdsattacks.com/

[[19 S&P] Attack Directories, Not Caches:Side-Channel Attacks in a Non-Inclusive World](https://people.csail.mit.edu/mengjia/data/sp19.pdf)

Intel的server CPU还有AMD的CPU一般用的是non-inclusive L3 cache，这样有些cache attacks没有办法简单地port过来。作者逆向了一个directory的结构，成功在non-inclusive caches实现了cache attacks。 Solid work.

[[21 USENIX] Osiris: Automated Discovery of Microarchitectural Side Channels](https://publications.cispa.saarland/3431/1/main.pdf)

找新的side channel是个枯燥的工作，一般需要researcher读很多手册，做实验测试，很麻烦。Osiris是一个fuzzing-based的框架，自动地找x86 instruction里的timing side channel。
【去读/复现。(1) 很好复现!really good work！ (2) 都xx鸽们.jpg】

[[21 CCS] Prime+Scope: Overcoming the Observer Effect for High-Precision Cache Contention Attacks](https://www.esat.kuleuven.be/cosic/publications/article-3405.pdf)

P+P每次都得access一长串addrs怎么办？P+S可以把它简化到每次reset只需要access一个地址。作者还开源了一个工具来自动寻找这样的prime pattern (for P+P & P+S)。结果。 Novel work!

[[21 USENIX] Lord of the Ring(s): Side Channel Attacks on the CPU On-Chip Ring Interconnect Are Practical](https://www.usenix.org/system/files/sec21-paccagnella.pdf)

L3 cache 是multi-processors共享的，可以把它们看成一个环。作者present了一种由ring之间contention引起的timing-based side channel。

[[22 USENIX]Don’t Mesh Around: Side-Channel Attacks and Mitigations on Mesh Interconnects](https://www.usenix.org/system/files/sec22-dai.pdf)

Contention-based attacks on the on-chip mesh interconnect used in server-class Intel processors. 

[[22 S&P] Adversarial Prefetch: New Cross-Core Cache Side Channel Attacks](https://arxiv.org/pdf/2110.12340.pdf)

Prefetch instructions 也可以用来做side channel attacks。文中还分析了各种prefetch指令与cache coherence state之间的关系。

[[22 USENIX] AMD Prefetch Attacks through Power and Time](https://misc0110.net/files/amd_prefetch_sec22.pdf)

Prefetch instructions 可以用来infer TLB state，Timing和Power上都有差距。

[[22 USENIX] Rapid Prototyping for Microarchitectural Attacks](https://misc0110.net/files/rapid_prototyping_sec22.pdf)

一个很好的框架/库来实施各种各样的microarchitectural attacks。

### TEE
Trusted Execution Attacks拥有一个更强大的threat model —— 攻击者可以是hypervisor。意味着攻击者可以执行privileged code。

[[17 SysTEX] SGX-Step: A Practical Attack Framework for Precise Enclave Execution Control](https://people.cs.kuleuven.be/~jo.vanbulck/systex17.pdf)

Interrupt-based的一个框架，通过一个合适的APIC interval根据攻击场景实现zero-step或single-step。这篇主要是介绍了下框架。

[[18 CCS] Nemesis: Studying Microarchitectural Timing Leaks in Rudimentary CPU Interrupt Logic](https://people.cs.kuleuven.be/~jo.vanbulck/ccs18.pdf)

SGX-Step的作者展示了如何用这个框架infer instruction-granular execution state (Observe the timing of step)。

[[20 USENIX] COPYCAT: Controlled Instruction-Level Attacks on Enclaves](https://www.usenix.org/system/files/sec20-moghimi-copycat.pdf)

Nemesis加强版，结合page-level，能更大力度的infer control flow。

[[21 USENIX] Frontal Attack: Leaking Control-Flow in SGX via the CPU Frontend](https://www.usenix.org/system/files/sec21-puddu.pdf)

在Code Fetch的阶段，当相同的代码位于不同的offset时(mod 16bytes), single-step的latency可观测到不一样。

[[22 USENIX] AEPIC Leak: Architecturally Leaking Uninitialized Data from the Microarchitecture](https://www.usenix.org/system/files/sec22-borrello.pdf)

APIC是一个MMIO page，包含了众多registers。但目前有用(有记录)的只占其中一小部分。作者发现在Intel的新架构下，直接访问未记载的部分可以直接leak superqueue(一个L2和L3之间的buffer)
中的数据。

[[19 CCS / 20 Asian HOST] VoltJockey: Breaching TrustZone by Software-Controlled Voltage Manipulation over Multi-core Frequencies](https://dl.acm.org/doi/abs/10.1145/3319535.3354201)

不同的指令对CPU所提供的电压需求不同，CPU有接口可以动态调整自己的电压/频率/能量消耗。作者调整电压，inject fault，还原AES/RSA密钥。第一次在Arm上，后Intel。

[[20 S&P] Plundervolt: Software-based Fault Injection Attacks against Intel SGX](https://plundervolt.com/doc/plundervolt.pdf)

同上 attack Intel SGX。

[[21 S&P] Platypus: Software-based Power Side-Channel Attacks on x86](https://platypusattack.com/platypus.pdf)

CPU在当时可以从userspace读取power consumption，作者发现当CPU执行不同的指令，甚至相同指令处理不同操作数时，能量消耗不同。可以结合zero-step进行攻击。

[[22 USENIX](Hertzbleed: Turning Power Side-Channel Attacks Into Remote Timing Attacks on x86)](https://www.hertzbleed.com/hertzbleed.pdf)

作者发现Platypus Attack中指令对power consumption的影响，同样适用于CPU Frequency上。而且Frequency是userspace可读的。

[[21 CCS]CrossLine: Breaking "Security-by-Crash" based Memory Isolation in AMD SEV](https://dl.acm.org/doi/pdf/10.1145/3460120.3485253)

[[21 Usenix]CipherLeaks: Breaking Constant-time Cryptography on AMD SEV via the Ciphertext Side Channel](https://www.usenix.org/system/files/sec21-li-mengyuan.pdf)

[[22 S&P]A Systematic Look at Ciphertext Side Channels on AMD SEV-SNP](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9833768)

[[23 USENIX]Cipherfix: Mitigating Ciphertext Side-Channel Attacks in Software](https://www.usenix.org/system/files/usenixsecurity23-wichelmann.pdf)

[SEV-Step A Single-Stepping Framework for AMD-SEV](https://arxiv.org/pdf/2307.14757.pdf)

[[24 USENIX]CacheWarp: Software-based Fault Injection using Selective State Reset](https://cachewarpattack.com/paper.pdf)

未完待续，欢迎补充/纠错。