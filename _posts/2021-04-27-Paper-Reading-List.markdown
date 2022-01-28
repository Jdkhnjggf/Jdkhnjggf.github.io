---
layout:     post
title:      "Paper-Reading-List"
subtitle:   " Security Papers"
date:       2022-01-29 00:41:02
author:     "luobobo"
header-img: "img/post1.jpg"
tags:
    - paper
---

> “Learn to read papers and develop my taste.”


[How to Read a Paper](https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf)

The THREE-PASS APPROACH
1. The first pass [about 5-10 min]
	- title, abstract, and introduction
	- section and sub-section headings
	- conclusions
2. The second pass [about one hour]
	- read carefully, ignore details such as proof
	- figures, diagrams, and illustrations
	- mark unread references
3. The third pass [about four to five hours for beginner]
	- virtually re-implement the paper
    - identify and challenge every assumption in every statement


**TODO**
* [(22 SP)BLACKSMITH: Scalable Rowhammering in the Frequency Domain](https://comsec.ethz.ch/wp-content/files/blacksmith_sp22.pdf)
* [(22 USENIX) Rapid Prototyping for Microarchitectural Attacks](https://misc0110.net/files/rapid_prototyping_sec22.pdf)
* [(21 USENIX) SMASH: Synchronized Many-sided Rowhammer Attacks from JavaScript](https://www.usenix.org/system/files/sec21-de-ridder.pdf)
* [(16 ACSAC) Amplifying Side Channels Through Performance Degradation](https://eprint.iacr.org/2015/1141.pdf)
* [(21 SP) PLATYPUS: Software-based Power Side-Channel Attacks on x86](https://platypusattack.com/platypus.pdf)


**Microarchitecture & Side-Channel Attack:**
* ~~[(17 USENIX) Telling Your Secrets Without Page Faults: Stealthy Page Table-Based Attacks on Enclaved Execution](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-van_bulck.pdf)
* ~~[(17 USENIX) Prime+Abort: A Timer-Free High-Precision L3 Cache Attack using Intel TSX](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-disselkoen.pdf)
* ~~[AMD SEV-SNP](https://www.amd.com/system/files/TechDocs/SEV-SNP-strengthening-vm-isolation-with-integrity-protection-and-more.pdf)~~
* ~~[(21 CCS) CROSS LINE: Breaking “Security-by-Crash” based Memory Isolation in AMD SEV](https://arxiv.org/pdf/2008.00146.pdf)~~
* ~~[(21 USENIX) Lord of the Ring(s): Side Channel Attacks on the CPU On-Chip Ring Interconnect Are Practical](https://www.usenix.org/system/files/sec21-paccagnella.pdf)~~
* ~~[(21 USENIX) CipherLeaks: Breaking Constant-time Cryptography on AMD SEV via the Ciphertext Side Channel](https://www.usenix.org/system/files/sec21-li-mengyuan.pdf)~~
* ~~[(21 CCS) SmashEx: Smashing SGX Enclaves Using Exceptions](https://arxiv.org/pdf/2110.06657.pdf)~~
* ~~[(18 SPACE) Tutorial: Uncovering and Mitigating Side-Channel Leakage in Intel SGX Enclaves](https://jovanbulck.github.io/files/space18-tutorial.pdf)~~
* ~~[(17 SysTEX) SGX-Step: A Practical Attack Framework for Precise Enclave Execution Control](https://core.ac.uk/download/pdf/129863707.pdf)~~
* ~~[(17 DIMVA) Malware Guard Extension: Using SGX to Conceal Cache Attacks](https://arxiv.org/pdf/1702.08719.pdf)~~
* ~~[(19 SP) Attack Directories, Not Caches:Side-Channel Attacks in a Non-Inclusive World](https://people.csail.mit.edu/mengjia/data/sp19.pdf)~~
* ~~[(16 DIMVA) Flush+Flush: A Fast and Stealthy Cache Attack](https://gruss.cc/files/flushflush.pdf)~~
* ~~[(22 USENIX) AMD Prefetch Attacks through Power and Time](https://misc0110.net/files/amd_prefetch_sec22.pdf)~~
* ~~[(17 ESORICS) Practical Keystroke Timing Attacks in Sandboxed JavaScript](https://misc0110.net/files/keystroke_js.pdf)~~
* ~~[(21 CCS) Prime+Scope: Overcoming the Observer Effect for High-Precision Cache Contention Attacks](https://www.esat.kuleuven.be/cosic/publications/article-3405.pdf)~~
* ~~[(15 SP) Prime+Probe: Last-Level Cache Side-Channel Attacks are Practical](http://palms.ee.princeton.edu/system/files/SP_vfinal.pdf)~~
* ~~[(16 DIMVA) Rowhammer.js: A Remote Software-Induced Fault Attack in JavaScript](https://gruss.cc/files/rowhammerjs.pdf)~~
* ~~[(17 FC) Fantastic Timers and Where to Find Them: High-Resolution Microarchitectural Attacks in JavaScript](https://misc0110.net/files/timers.pdf)~~
* ~~[(22 SP) Spook.js: Attacking Chrome Strict Site Isolation via Speculative Execution](https://www.spookjs.com/files/spook-js.pdf)~~
* ~~[(21 SP) CROSSTALK: Speculative Data Leaks Across Cores Are Real](https://download.vusec.net/papers/crosstalk_sp21.pdf)~~
* ~~[(21 SP) CacheOut: Leaking Data on Intel CPUs via Cache Evictions](https://cacheoutattack.com/files/CacheOut.pdf)~~
* ~~[(21 USENIX) ExpRace: Exploiting Kernel Races through Raising Interrupts](https://www.usenix.org/system/files/sec21-lee-yoochan.pdf)~~ 
* ~~[(21 USENIX) Rage Against the Machine Clear: A Systematic Analysis of Machine Clears and Their Implications for Transient Execution Attacks](https://www.usenix.org/system/files/sec21-ragab.pdf)~~ 
* ~~[(19 SP) RIDL: Rogue In-Flight Data Load](https://mdsattacks.com/files/ridl.pdf)~~ 
* ~~[(19 CCS) Fallout: Leaking Data on Meltdown-resistant CPUs](https://mdsattacks.com/files/fallout.pdf)~~ 
* ~~[(21 EuroSec) Transient Execution of Non-Canonical Accesses](https://saidganim.github.io/pdfs/AMD_NCTE.pdf)~~
* ~~[(20 FC) Speculative Dereferencing: Reviving Foreshadow (Extended Version)](https://misc0110.net/files/specderef.pdf)~~  
* ~~[Intel SGX Explained](https://eprint.iacr.org/2016/086.pdf)~~
* ~~[(21 USENIX) Frontal Attack: Leaking Control-Flow in SGX via the CPU Frontend](https://arxiv.org/pdf/2005.11516.pdf)~~
* ~~[(20 USENIX) Medusa: Microarchitectural Data Leakage via Automated Attack Synthesis](https://www.usenix.org/system/files/sec20-moghimi-medusa.pdf)~~
* ~~[(20 SP) LVI: Hijacking Transient Execution through Microarchitectural Load Value Injection](https://lviattack.eu/lvi.pdf)~~
* ~~[(19 CCS) ZombieLoad: Cross-Privilege-Boundary Data Sampling](https://zombieloadattack.com/zombieload.pdf)~~
* ~~[(17 Blackhat) Breaking the x86 ISA](https://www.blackhat.com/docs/us-17/thursday/us-17-Domas-Breaking-The-x86-Instruction-Set-wp.pdf)~~
* ~~[(21 USENIX) Osiris: Automated Discovery of Microarchitectural Side Channels](https://publications.cispa.saarland/3431/1/main.pdf)~~
* ~~[(18 USENIX) Spectre Attacks: Exploiting Speculative Execution](https://spectreattack.com/spectre.pdf)~~
* ~~[(19 SP) Meltdown: Reading Kernel Memory from User Space](https://meltdownattack.com/meltdown.pdf)~~
* ~~[(18 EuroSec) SEVered: Subverting AMD’s Virtual Machine Encryption](https://arxiv.org/pdf/1805.09604.pdf)~~
* ~~[(20 SP) SEVurity: No Security Without Integrity Breaking Integrity-Free Memory Encryption with Minimal Assumptions](https://arxiv.org/pdf/2004.11071.pdf)~~
* ~~[(14 USENIX) FLUSH+RELOAD: a High Resolution, Low Noise, L3 Cache Side-Channel Attack](https://eprint.iacr.org/2013/448.pdf)~~
* ~~[(15 USENIX) Cache Template Attacks: Automating Attacks on Inclusive Last-Level Caches](https://gruss.cc/files/cta.pdf)~~


**Software Security:**
* ~~[ObliCheck: Efficient Verification of Oblivious Algorithms with Unobservable State](https://www.usenix.org/system/files/sec21-son.pdf)~~

**Seminar Task (Selected Topics in Automated Testing and Debugging):**
* ~~[FormatFuzzer: Effective Fuzzing of Binary File Formats](https://dl.cispa.de/s/3q2PyqP7rqZzrNn)~~
* ~~[Smart Greybox Fuzzing (AFLSmart)](https://arxiv.org/pdf/1811.09447.pdf)~~
* ~~[MultiSE: Multi-Path Symbolic Execution using Value Summaries (MultiSE)](https://people.eecs.berkeley.edu/~ksen/papers/multise.pdf)~~
* ~~[Compiler Validation via Equivalence Modulo Inputs (EMI)](https://www.cs.ucdavis.edu/~su/publications/emi.pdf)~~
* ~~[A review of reverse debugging (Time-travel Debugging) Engblom](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.338.3420&rep=rep1&type=pdf)~~
* ~~[Mining Input Grammars from Dynamic Control Flow](https://publications.cispa.saarland/3101/1/fse2020-mimid.pdf)~~
* ~~[Dynamically discovering likely program invariants to support program evolution](https://homes.cs.washington.edu/~mernst/pubs/invariants-tse2001.pdf)~~
* ~~[Input Algebras](https://publications.cispa.saarland/3208/7/gopinath2021input.pdf)~~
* ~~[Learning the Language of Error](http://www.cprover.org/learning-errors/learning-the-language-of-error-including-a-proof-supplement.pdf)~~
* ~~[Simplifying and Isolating Failure-Inducing Input](https://hiper.cis.udel.edu/lp/lib/exe/fetch.php/courses/other-delta-zellertse.pdf)~~
* ~~[Abstracting Failure-Inducing Inputs](https://publications.cispa.saarland/3103/7/issta2020-language-of-failure.pdf)~~
* ~~[When does my Program do this? Learning Circumstances of Software Behavior](https://publications.cispa.saarland/3107/7/fse2020-alhazen.pdf)~~
* ~~[Simplifying and isolating failure-inducing input](https://www.st.cs.uni-saarland.de/papers/tse2002/tse2002.pdf)~~

<!-- 
* [Constraint-guided Directed Greybox Fuzzing](https://www.usenix.org/conference/usenixsecurity21/presentation/lee-gwangmu)
* [Android SmartTVs Vulnerability Discovery via Log-Guided Fuzzing](https://www.usenix.org/conference/usenixsecurity21/presentation/aafer)
* [ExpRace: Exploiting Kernel Races through Raising Interrupts](https://www.usenix.org/conference/usenixsecurity21/presentation/lee-yoochan)
* [CANARY - a reactive defense mechanism for Controller Area Networks based on Active RelaYs](https://www.usenix.org/conference/usenixsecurity21/presentation/groza)
* [MAZE: Towards Automated Heap Feng Shui](https://www.usenix.org/conference/usenixsecurity21/presentation/wang-yan)
* [Breaking Through Binaries: Compiler-quality Instrumentation for Better Binary-only Fuzzing](https://www.usenix.org/conference/usenixsecurity21/presentation/nagy)
* [VScape: Assessing and Escaping Virtual Call Protections](https://www.usenix.org/conference/usenixsecurity21/presentation/chen-kaixiang)
* [PTAuth: Temporal Memory Safety via Robust Points-to Authentication](https://www.usenix.org/conference/usenixsecurity21/presentation/mirzazade)
* [Finding Bugs Using Your Own Code: Detecting Functionally-similar yet Inconsistent Code](https://www.usenix.org/conference/usenixsecurity21/presentation/ahmadi)
* [SHARD: Fine-Grained Kernel Specialization with Context-Aware Hardening](https://www.usenix.org/conference/usenixsecurity21/presentation/abubakar)
* [Preventing Use-After-Free Attacks with Fast Forward Allocation](https://www.usenix.org/conference/usenixsecurity21/presentation/wickman)
* [IJON: Exploring Deep State Spaces via Fuzzing](https://www.ei.ruhr-uni-bochum.de/media/emma/veroeffentlichungen/2020/02/27/IJON-Oakland20.pdf)
* [xMP: Selective Memory Protection for Kernel and User Space](https://www3.cs.stonybrook.edu/~sghavamnia/papers/xmp.sp20.pdf)
* [Temporal System Call Specialization for Attack Surface Reduction](https://www.usenix.org/system/files/sec20-ghavamnia.pdf)
* [(Mostly) Exitless VM Protection from Untrusted Hypervisor through Disaggregated Nested Virtualization](https://www.usenix.org/system/files/sec20summer_mi_prepub.pdf)
* [EcoFuzz: Adaptive Energy-Saving Greybox Fuzzing as a Variant of the Adversarial Multi-Armed Bandit](https://www.usenix.org/conference/usenixsecurity20/presentation/yue)
* [ParmeSan: Sanitizer-guided Greybox Fuzzing](https://www.usenix.org/conference/usenixsecurity20/presentation/osterlund)
* [SoK: Benchmarking Flaws in Systems Security](https://ieeexplore.ieee.org/document/8806739)
* [SoK: Eternal War in Memory](https://people.eecs.berkeley.edu/~dawnsong/papers/Oakland13-SoK-CR.pdf)
* [SoK: Using Dynamic Binary Instrumentation for Security](https://www.diag.uniroma1.it/~delia/papers/asiaccs2019.pdf)
* [SoK: Sanitizing for Security](https://arxiv.org/pdf/1806.04355.pdf)
* [One Engine to Fuzz ’em All: Generic Language Processor Testing with Semantic Validation](https://faculty.ist.psu.edu/wu/papers/polyglot.pdf)
* [STOCHFUZZ: Sound and Cost-effective Fuzzing of Stripped Binaries by Incremental and Stochastic Rewriting](https://www.cs.purdue.edu/homes/zhan3299/res/SP21b.pdf)
* [A novel dynamic analysis infr el dynamic analysis infrastructur astructure to instrument untrusted o instrument untrusted execution flow across user-kernel spaces](https://ink.library.smu.edu.sg/cgi/viewcontent.cgi?article=6613&context=sis_research)
* [A Secure and Formally Verified Linux KVM Hypervisor](http://www.cs.columbia.edu/~nieh/pubs/ieeesp2021_kvm.pdf)
* [DIANE: Identifying Fuzzing Triggers in Apps to Generate Under-constrained Inputs for IoT Devices](https://conand.me/publications/redini-diane-2021.pdf)
* [DIFFUZZ: Differential Fuzzing for Side Channel Analysis](https://arxiv.org/pdf/1811.07005.pdf)
* [Fuzzing: Challenges and Reflections](https://www.comp.nus.edu.sg/~abhik/pdf/IEEE-SW-Fuzzing.pdf)
* [Industrial Oriented Evaluation of Fuzzing Techniques (ICST 2021)](http://www.wingtecher.com/themes/WingTecherResearch/assets/papers/icst21.pdf)
* [An Empirical Study of OSS-Fuzz Bugs (MSR 2021)](https://squareslab.github.io/materials/DingOSSFuzz21.pdf)
* [UNIFUZZ: A Holistic and Pragmatic Metrics-Driven Platform for Evaluating Fuzzers](https://arxiv.org/pdf/2010.01785.pdf )
* [A Feature-Oriented Corpus for understanding, Evaluating and Improving Fuzz Testing](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/ASIACCS19_Feature-Oriented.pdf)
* [RetroWrite: Statically Instrumenting COTS Binaries for Fuzzing and Sanitization (S&P 2020)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/SP20_RetroWrite.pdf)
* [Antifuzz: impeding fuzzing audits of binary executables (USENIX Security2019)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/USENIX19_Antifuzz.pdf)
* [FUZZIFICATION: Anti-Fuzzing Technique (USENIX Security2019)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/USENIX19_FUZZIFICATION.pdf)
* [Hydra: An Extensible Fuzzing Framework for Finding Semantic Bugs in File Systems (SOSP 2019)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/SOSP19_Hydra.pdf)
* [A Priority Based Path Searching Method for Improving Hybrid Fuzzing (Computers & Security 2021)](https://www.sciencedirect.com/science/article/pii/S0167404821000663?casa_token=OUEFq5TSDv0AAAAA:jDit2FK_0vPqynepfWH__-mPOAQwfZaRP7Qv9G19x_t22z20N6C293JaNz2I16W2djytcOEFHrGM)
* [HFL: Hybrid Fuzzing on the Linux Kernel (NDSS 2020)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/NDSS20_HFL.pdf)
* [PANGOLIN: Incremental Hybrid Fuzzing with Polyhedral Path Abstraction (S&P 2020)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/SP20_PANGOLIN.pdf)
* [SAVIOR: Towards Bug-Driven Hybrid Testing (S&P 2020)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/SP20_SAVIOR.pdf)
* [PathAFL: Path-Coverage Assisted Fuzzing (ASIA CCS 2020)](https://dl.acm.org/doi/abs/10.1145/3320269.3384736)
* [Not All Coverage Measurements Are Equal: Fuzzing by Coverage Accounting for Input Prioritization (NDSS 2020)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/NDSS20_Prioritization.pdf)
* [Matryoshka: fuzzing deeply nested branches (CCS 2019)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/CCS19_Matryoshka.pdf)
* [REDQUEEN: Fuzzing with Input-to-State Correspondence (NDSS2019)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/NDSS19_REDQUEEN.pdf)
* [Typestate-Guided Fuzzer for Discovering Use-after-Free Vulnerabilities (ICSE 2020)](https://www.scedt.tees.ac.uk/s.qin/papers/icse2020-uafl.pdf)
* [Binary-level Directed Fuzzing for Use-After-Free Vulnerabilities (RAID 2020)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/Arxiv20_BinaryUAF.pdf)
* [MemFuzz: Using Memory Accesses to Guide Fuzzing (ICST 2019)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/ICST19_MemFuzz.pdf)
* [MemLock: Memory Usage Guided Fuzzing (ICSE2020)](https://wcventure.github.io/pdf/ICSE2020_MemLock.pdf)
* [MOPT: Optimize Mutation Scheduling for Fuzzers (USENIX Security2019)](https://github.com/wcventure/FuzzingPaper/blob/master/Paper/USENIX19_MOPT.pdf)
* [FuzzGen: Automatic Fuzzer Generation (USENIX Security2020)](https://www.usenix.org/system/files/sec20fall_ispoglou_prepub.pdf) -->