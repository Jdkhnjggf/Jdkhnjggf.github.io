---
layout:     post
title:      "Paper-Reading-List"
subtitle:   " Security Papers"
date:       2023-07-01 01:01:00
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

**Side-Channel Attacks (Cache)**
1.  [(22 S&P) Adversarial Prefetch: New Cross-Core Cache Side Channel Attacks](https://arxiv.org/pdf/2110.12340.pdf)
2.  [(21 CCS) Prime+Scope: Overcoming the Observer Effect for High-Precision Cache Contention Attacks](https://www.esat.kuleuven.be/cosic/publications/article-3405.pdf)
3.  [(17 USENIX) Prime+Abort: A Timer-Free High-Precision L3 Cache Attack using Intel TSX](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-disselkoen.pdf)
4.  [(15 S&P) Prime+Probe: Last-Level Cache Side-Channel Attacks are Practical](http://palms.ee.princeton.edu/system/files/SP_vfinal.pdf)
5.  [(16 DIMVA) Flush+Flush: A Fast and Stealthy Cache Attack](https://gruss.cc/files/flushflush.pdf)
6.  [(14 USENIX) FLUSH+RELOAD: a High Resolution, Low Noise, L3 Cache Side-Channel Attack](https://eprint.iacr.org/2013/448.pdf)
7.  [(15 USENIX) Cache Template Attacks: Automating Attacks on Inclusive Last-Level Caches](https://gruss.cc/files/cta.pdf)

**Side-Channel Attacks (Other)**
1.  [(19 S&P) Attack Directories, Not Caches:Side-Channel Attacks in a Non-Inclusive World](https://people.csail.mit.edu/mengjia/data/sp19.pdf)
2.  [(16 USENIX) DRAMA: Exploiting DRAM Addressing for Cross-CPU Attacks](https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_pessl.pdf)
3.  [(21 USENIX) Lord of the Ring(s): Side Channel Attacks on the CPU On-Chip Ring Interconnect Are Practical](https://www.usenix.org/system/files/sec21-paccagnella.pdf)
4.  [(22 USENIX) AMD Prefetch Attacks through Power and Time](https://misc0110.net/files/amd_prefetch_sec22.pdf)

**Fuzzing-Based**
1.  [(22 S&P) Finding and Exploiting CPU Features using MSR Templating](https://misc0110.net/files/msrtemplate_sp22.pdf)
2.  [(21 USENIX) Osiris: Automated Discovery of Microarchitectural Side Channels](https://publications.cispa.saarland/3431/1/main.pdf)
3.  [(17 Blackhat) Breaking the x86 ISA](https://www.blackhat.com/docs/us-17/thursday/us-17-Domas-Breaking-The-x86-Instruction-Set-wp.pdf)

**Reverse-engineer Microarchitecture**
1.  [(22 USENIX) TLB;DR: Enhancing TLB-based Attacks with TLB Desynchronized Reverse Engineering](https://download.vusec.net/papers/tlbdr_sec22.pdf)
2.  BHI
3.  RETBLEED
4.  Attack Directories
5.  Lord of the Rings

**Meltdown & Variants**
1.  [(22 USENIX) Repurposing Segmentation as a Practical LVI-NULL Mitigation in SGX](https://publications.cispa.saarland/3493/1/lvi_null_sec22.pdf)
2.  [(20 S&P) LVI: Hijacking Transient Execution through Microarchitectural Load Value Injection](https://lviattack.eu/lvi.pdf)
3.  [(21 EuroSec) Transient Execution of Non-Canonical Accesses](https://saidganim.github.io/pdfs/AMD_NCTE.pdf)
4.  [(20 USENIX) Medusa: Microarchitectural Data Leakage via Automated Attack Synthesis](https://www.usenix.org/system/files/sec20-moghimi-medusa.pdf)
5.  [(19 S&P) Meltdown: Reading Kernel Memory from User Space](https://meltdownattack.com/meltdown.pdf)

**Spectre & Variants**
1. [(22 USENIX) RETBLEED: Arbitrary Speculative Code Execution with Return Instructions](https://www.usenix.org/system/files/sec22-wikner.pdf) 
3. [(22 USENIX) Branch History Injection: On the Effectiveness of Hardware Mitigations Against Cross-Privilege Spectre-v2 Attacks](https://download.vusec.net/papers/bhi-spectre-bhb_sec22.pdf)
4. [(19 USENIX) A Systematic Evaluation of Transient Execution Attacks and Defenses](https://www.usenix.org/system/files/sec19-canella.pdf)
4.	[(18 CCS) ret2spec: Speculative Execution Using Return Stack Buffers](https://arxiv.org/pdf/1807.10364.pdf)
5.  [(18 USENIX) Spectre Attacks: Exploiting Speculative Execution](https://spectreattack.com/spectre.pdf)

**Other Transient Execution Attacks**
1.  [(21 USENIX) Rage Against the Machine Clear: A Systematic Analysis of Machine Clears and Their Implications for Transient Execution Attacks](https://www.usenix.org/system/files/sec21-ragab.pdf) 
2.  [(21 S&P) CROSSTALK: Speculative Data Leaks Across Cores Are Real](https://download.vusec.net/papers/crosstalk_sp21.pdf)
3.  [(19 S&P) RIDL: Rogue In-Flight Data Load](https://mdsattacks.com/files/ridl.pdf) 
4.  [(19 CCS) Fallout: Leaking Data on Meltdown-resistant CPUs](https://mdsattacks.com/files/fallout.pdf) 
5.  [(20 FC) Speculative Dereferencing: Reviving Foreshadow (Extended Version)](https://misc0110.net/files/specderef.pdf)  
6.  [(19 CCS) ZombieLoad: Cross-Privilege-Boundary Data Sampling](https://zombieloadattack.com/zombieload.pdf)
7.  [(21 S&P) CacheOut: Leaking Data on Intel CPUs via Cache Evictions](https://cacheoutattack.com/files/CacheOut.pdf)

**DVFS-Based**
1.  [(22 USENIX) Hertzbleed: Turning Power Side-Channel Attacks Into Remote Timing Attacks on x86](https://www.hertzbleed.com/hertzbleed.pdf)
2.  [(22 USENIX) Minefield: A Software-only Protection for SGX Enclaves against DVFS Attacks](https://www.usenix.org/system/files/sec22fall_kogler.pdf)
3.  [(20 S&P) Plundervolt: Software-based Fault Injection Attacks against Intel SGX](https://plundervolt.com/doc/plundervolt.pdf)
4.  [(21 S&P) PLATYPUS: Software-based Power Side-Channel Attacks on x86](https://platypusattack.com/platypus.pdf)

**Rowhammer**
1.	[(20 IEEE Trans. Comput.)RowHammer: A Retrospective](https://people.inf.ethz.ch/omutlu/pub/RowHammer-Retrospective_ieee_tcad19-official.pdf)

**AMD TEE (SEV):**
1. [(23 USENIX) Cipherfix: Mitigating Ciphertext Side-Channel Attacks in Software](https://www.usenix.org/system/files/sec23fall-prepub-614-wichelmann.pdf)
2. [(22 S&P) A Systematic Look at Ciphertext Side Channels on AMD SEV-SNP](https://ieeexplore.ieee.org/document/9833768)
3. [AMD SEV-SNP](https://www.amd.com/system/files/TechDocs/SEV-SNP-strengthening-vm-isolation-with-integrity-protection-and-more.pdf)
4. [(21 USENIX) CipherLeaks: Breaking Constant-time Cryptography on AMD SEV via the Ciphertext Side Channel](https://www.usenix.org/system/files/sec21-li-mengyuan.pdf)
5.  [(21 CCS) CROSS LINE: Breaking “Security-by-Crash” based Memory Isolation in AMD SEV](https://arxiv.org/pdf/2008.00146.pdf)
6. [(18 EuroSec) SEVered: Subverting AMD’s Virtual Machine Encryption](https://arxiv.org/pdf/1805.09604.pdf)
7. [(20 S&P) SEVurity: No Security Without Integrity Breaking Integrity-Free Memory Encryption with Minimal Assumptions](https://arxiv.org/pdf/2004.11071.pdf)

**Intel TEE (SGX):**
1.  [ÆPIC Leak: Architecturally Leaking Uninitialized Data from the Microarchitecture](https://aepicleak.com/aepicleak.pdf)
2.  [(21 CCS) SmashEx: Smashing SGX Enclaves Using Exceptions](https://arxiv.org/pdf/2110.06657.pdf)
3.  [(21 USENIX) Frontal Attack: Leaking Control-Flow in SGX via the CPU Frontend](https://arxiv.org/pdf/2005.11516.pdf)
4.  [(17 USENIX) Telling Your Secrets Without Page Faults: Stealthy Page Table-Based Attacks on Enclaved Execution](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-van_bulck.pdf)
5.  [(18 SPACE) Tutorial: Uncovering and Mitigating Side-Channel Leakage in Intel SGX Enclaves](https://jovanbulck.github.io/files/space18-tutorial.pdf)
6.  [(17 SysTEX) SGX-Step: A Practical Attack Framework for Precise Enclave Execution Control](https://core.ac.uk/download/pdf/129863707.pdf)
7.  [Intel SGX Explained](https://eprint.iacr.org/2016/086.pdf)
8.  [(17 DIMVA) Malware Guard Extension: Using SGX to Conceal Cache Attacks](https://arxiv.org/pdf/1702.08719.pdf)

**Microarchitectural Attack in Browsers**
1.  [(22 S&P) Spook.js: Attacking Chrome Strict Site Isolation via Speculative Execution](https://www.spookjs.com/files/spook-js.pdf)
2.  [(17 ESORICS) Practical Keystroke Timing Attacks in Sandboxed JavaScript](https://misc0110.net/files/keystroke_js.pdf)
3.  [(16 DIMVA) Rowhammer.js: A Remote Software-Induced Fault Attack in JavaScript](https://gruss.cc/files/rowhammerjs.pdf)
4.  [(17 FC) Fantastic Timers and Where to Find Them: High-Resolution Microarchitectural Attacks in JavaScript](https://misc0110.net/files/timers.pdf)

**Defence**
1.  [(16 RAID) CloudRadar: A Real-Time Side-Channel Attack Detection System in Clouds](https://yinqian.org/papers/raid16.pdf)
2.  [(16 ESSoS) HexPADS: a platform to detect “stealth” attacks](http://www.nebelwelt.net/publications/files/16ESSoS.pdf)

**Others & SoK:**
1.  [(22 USENIX) Rapid Prototyping for Microarchitectural Attacks](https://misc0110.net/files/rapid_prototyping_sec22.pdf)
2.  [(13 S&P) SoK: Eternal War in Memory](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6547101&casa_token=r-r6lLBi480AAAAA:8dchTr9PsYNFhSkC-E3Q3KtbNOERNuOr1s5OYf6KdVdNxn4BpoCE3yoCVpJ0Nb2EGTHmTWuY4vtHRg)
3.  [(21 USENIX) ExpRace: Exploiting Kernel Races through Raising Interrupts](https://www.usenix.org/system/files/sec21-lee-yoochan.pdf) 


<!-- **Software Security:**
* [ObliCheck: Efficient Verification of Oblivious Algorithms with Unobservable State](https://www.usenix.org/system/files/sec21-son.pdf)

**Seminar Task (Selected Topics in Automated Testing and Debugging):**
1. [FormatFuzzer: Effective Fuzzing of Binary File Formats](https://dl.cispa.de/s/3q2PyqP7rqZzrNn)
2. [Smart Greybox Fuzzing (AFLSmart)](https://arxiv.org/pdf/1811.09447.pdf)
3. [MultiSE: Multi-Path Symbolic Execution using Value Summaries (MultiSE)](https://people.eecs.berkeley.edu/~ksen/papers/multise.pdf)
4. [Compiler Validation via Equivalence Modulo Inputs (EMI)](https://www.cs.ucdavis.edu/~su/publications/emi.pdf)
5. [A review of reverse debugging (Time-travel Debugging) Engblom](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.338.3420&rep=rep1&type=pdf)
6. [Mining Input Grammars from Dynamic Control Flow](https://publications.cispa.saarland/3101/1/fse2020-mimid.pdf)
7. [Dynamically discovering likely program invariants to support program evolution](https://homes.cs.washington.edu/~mernst/pubs/invariants-tse2001.pdf)
8. [Input Algebras](https://publications.cispa.saarland/3208/7/gopinath2021input.pdf)
9. [Learning the Language of Error](http://www.cprover.org/learning-errors/learning-the-language-of-error-including-a-proof-supplement.pdf)
10. [Simplifying and Isolating Failure-Inducing Input](https://hiper.cis.udel.edu/lp/lib/exe/fetch.php/courses/other-delta-zellertse.pdf)
11. [Abstracting Failure-Inducing Inputs](https://publications.cispa.saarland/3103/7/issta2020-language-of-failure.pdf)
12. [When does my Program do this? Learning Circumstances of Software Behavior](https://publications.cispa.saarland/3107/7/fse2020-alhazen.pdf)
13. [Simplifying and isolating failure-inducing input](https://www.st.cs.uni-saarland.de/papers/tse2002/tse2002.pdf) -->
