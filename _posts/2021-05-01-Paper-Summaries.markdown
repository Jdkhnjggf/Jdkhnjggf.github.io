---
layout:     post
title:      "Paper-Summaries"
subtitle:   " Security Papers"
date:       2021-07-02 21:30:00
author:     "luobobo"
header-img: "img/post2.jpg"
tags:
    - paper
---

> “The better you understand a subject, the easier it is to explain it thoroughly and briefly.”

My English writing is so bad... I am taking a seminar lecture this semester and am required to write paper summaries every week. Here I record some summaries of papers I've read as a way to practice writing skill.

[**How to Summarize a Research Article**](https://writingcenter.uconn.edu/wp-content/uploads/sites/593/2014/06/How_to_Summarize_a_Research_Article1.pdf)


### Smart Greybox Fuzzing
[**Paper**](https://arxiv.org/pdf/1811.09447.pdf)  *2021-07-02*

**Summary:**
 Coverage-guided fuzzing (CGF) is a genetic algorithm where natural selection is based on achieving unique code coverage. However, there is a well-known limitation in CGF that its mutation operators work on the bit-level representation of inputs. At the same time, more and more target processes and libraries process highly structured inputs today. This paper proposes smart greybox fuzzing (SGF), which provides high-level structural mutation operators working on the virtual file structure of the representation of inputs. The virtual structure, containing the structural information of the input, is constructed by a file format specification and a parser component. In this way, SGF is more likely to generate seeds with maintaining the validity to pass the parsing state of the program. SGF also introduces a novel validity power schedule to assign more energy to seed with a higher degree of validity. Moreover, SGF starts to construct virtual structure only when exploring the new path slows down, which avoids sacrificing its efficiency to crack virtual structure for every seed. Eventually, based on these techniques, SGF can explore the target program's state deeper within limited time budgets.


### MultiSE: Multi-Path Symbolic Execution using Value Summaries
[**Paper**](https://people.eecs.berkeley.edu/~ksen/papers/multise.pdf)  *2021-06-27*

**Summary:**
 Compared to pure symbolic execution, concolic testing combines concrete execution and symbolic execution to reduce executed time significantly. However, concolic testing still does not scale to large programs for their huge program states. In order to cut down the paths to be explored, the conventional state merging mechanism introduces an auxiliary value to represent the merged value.  There is a problem that when the auxiliary variable has a floating-point predicate, the constraints solver may not support such calculation. The MultiSE merges state incrementally without using auxiliary variables based on an alternative representation of symbolic execution state. Its key point is to organize the symbolic state by variables' values instead of organizing by paths. Specifically, MultiSE proposes a new concept —— guarded symbolic expression. It is a pair that contains variables' symbolic expression and the corresponding distinct path constraint.  A set of guarded symbolic expressions is a value summary. MultiSE incrementally updates the value summary, avoiding scanning merged states at join points. Moreover, merging states without the auxiliary variable, MultiSE is proven to run faster than conventional state merging mechanisms in evaluation.


### Compiler Validation via Equivalence Modulo Inputs
[**Paper**](https://www.cs.ucdavis.edu/~su/publications/emi.pdf)  *2021-06-19*

**Summary:**
 Compilers are always regarded as secure to generate correct programs. However, the possible miscompilitation leads to unexpected behavior, which could potentially result in damage. The paper introduces equivalence modulo inputs (EMI), a methodology for validating the compiler's optimization. Based on EMI, the author presents a tool, Orion, to generate EMI-variants of a program with a set of test inputs. Given a program P and an input set, the P's EMI-variants behave the same on the same input set. The key idea is that first tracks the program's execution information and outputs of a given input. Next, the tool randomly deletes the unexecuted code statements indicated by the last step to generate a collection of programs (EMI-variants). Later, the tool feeds the collection of programs and the original program's output to the targeted compilers with various configurations. If there are inconsistencies between a new compiled output and the original output, the compiler may have a miscompilitation bug. 


### Spectre Attacks: Exploiting Speculative Execution
[**Paper**](https://spectreattack.com/spectre.pdf)  *2021-06-11*

**Summary:**
 Spectre is similar to Meltdown, against memory isolation between kernel address and user address based on exploiting the side effect of out-of-order execution. After the impact of the transient instructions is reverted at the architecture level, the micro-architecture state remains changed, which can be leveraged to leak sensitive information. Spectre makes these instructions executed by mistraining branch predictor or poisoning indirect branches. The mechanism of conditional branch prediction is based on the previous results that attackers can manipulate. An attacker can also poison indirect branches with malicious destinations. Then the attacker needs to locate a particular gadget that allows access to memory at the attacker-chosen address. Eventually, Spectre can expose the attacker-chosen address via a broad range of convert channels.


### Osiris: Automated Discovery of Microarchitectural Side Channels
[**Paper**](https://publications.cispa.saarland/3431/1/main.pdf) *2021-06-09*
TO SUMMARY 


### Mining Input Grammars from Dynamic Control Flow
[**Paper**](https://publications.cispa.saarland/3101/1/fse2020-mimid.pdf)  *2021-06-07*

**Summary:**
 This paper presents an algorithm, mimid, to recover program input grammar from the dynamic control flow. The algorithm consists of three steps: tracking control flows, gaining parse trees from traces, and inferring grammar from parse trees. First, the mimid algorithm instruments the parsing functions by adding trackers on the entry and exit of these methods and the entry and exit of control flow structures, e.g., if, loop in these methods. Each tracker is associated with an identifier. Next, the mimid algorithm assigns specific indexes of input to a particular tracker. It uses a strategy that the last method (or control flow structure) accessed a character directly consumes that character. Afterward, the corresponding method call directly owns the index range of input. Then, the indexes are added as leaf nodes to the method or control flow structure. The mimid algorithm then identifies where the nodes can be replaced with another to prune these parse trees. The algorithm regards a node as replaceable with another that the new generated string can be parsed correctly, named as compatible nodes. Although, Compatible is not transitive if check parse validity, mimid assume transitivity of compatibility since it rarely breaks and its effect on accuracy is minor, which is revealed in their evaluation. Eventually, the parse trees are well labeled to infer input grammar. Mimid algorithm traverses each parse tree, marks the non-character node as non-terminal. Then, non-character children of the node will be transformed as a rule of the non-terminal's expansion. In contrast, a character node will be placed as terminal. After traversing all the parse trees, the mimid algorithm generalizes regular expressions for terminals.

### Input Algebras
[**Paper**](https://publications.cispa.saarland/3208/7/gopinath2021input.pdf)  *2021-05-17*

### Learning the Language of Error*
[**Paper**](http://www.cprover.org/learning-errors/learning-the-language-of-error-including-a-proof-supplement.pdf)  *2021-05-17*

**Summary:**
 The paper presents a grammar transformer, Evogram, that combines the input grammar with some specific user-defined patterns, to obtain a combined grammar. 
Within this grammar, users can produce test inputs satisfying a set of specific patterns, which greatly improves the flexibility and practicality of grammar-based test generators.
At first, authors regards the given constraint as an abstract pattern, called evocative pattern, which is actually a specific string representation of non-terminals. Subsequently, authors connect the original grammar with a reaching grammar to guarantee the inputs generated with end grammar contain at least one instance of evocative pattern. Eventually, authors provide formal proofs of a series of algebra of grammar specializations, ensuring the accuracy of the combined grammar they derive.
In contrast, another paper presents a method based on the $L^*$ algorithm.
It automatically determines what program behavior towards some specific program failure.
This approach instruments the program to get the conditions for generating an event, and the program behavior is composed of a series of events.
Through multiple rounds of queries with the feedback obtained, this method can automatically learn a DFA with specific properties, which helps to visualise the cause of program's error.


### FLUSH+RELOAD: a High Resolution, Low Noise, L3 Cache Side-Channel Attack
[**Paper**](https://eprint.iacr.org/2013/448.pdf)  *2021-05-13*

**Summary:**
 In this paper, the authors present FLUSH+RELOAD, a new cache side-channel attack technique that exploits the side effects of the copy-on-write technique. 
Copy-on-write contributes to page-sharing but introduces a significant time delay. So an attacker can spy this time difference to speculate the secret value in the cache. 
Compared to prior cache side-channel attacks, FLUSH+RELOAD focuses on the Last-Level Cache.
Consequently, the attacker and victim can not be in the same processor. Moreover, FLUSH+RELOAD allows cross-VM attacks in a virtual environment.


### Meltdown: Reading Kernel Memory from User Space
[**Paper**](https://meltdownattack.com/meltdown.pdf)  *2021-05-11*

**Summary:**
 The paper presents a new attack, Meltdown, against memory isolation between kernel address and user address.
Meltdown allows an adversary to dump the entire kernel address by exploiting the side effects of Out-of-order execution.
Modern processors prioritize the execution of operations with available input data to prevent idleness and achieve high performance. 
However, Meltdown makes the CPU execute originally unreachable instructions to change micro-architectural state with a secret value. 
Subsequently, Meltdown uses Flush+Reload, a cache attack technique, to transfer micro-architectural state change into architectural state and speculates the secret value.
Eventually, by repeating the above steps, an attacker can dump the kernel memory without accessible privileges.
This attack applies to many operating systems,  e. g. Linux, Windows, Android, and could cause damage to a large number of users.


### [Seminar] Abstracting Failure-Inducing Inputs
[**Paper**](https://publications.cispa.saarland/3103/7/issta2020-language-of-failure.pdf)  *2021-05-09*

### [Seminar] When does my Program do this? Learning Circumstances of Software Behavior
[**Paper**](https://publications.cispa.saarland/3107/7/fse2020-alhazen.pdf)  *2021-05-09*

**Summary:**
 Given an input grammar, the DDSet algorithm automatically generates an abstract pattern of a failure-inducing input, greatly helps developers locate, fix bugs, and validate patches.
DDSet regards a failing-test input as a derivation tree and reduces the given input into a 1-minimal input at first, which means none of its nodes can be empty to reproduce the failure still. Next, DDSet determines which parts of the given input can be abstracted as an expression, and the remaining should be kept still to fail the test. Then DDSet isolates causes of failure by verifying the abstract node independently, moreover, establishes combinations of sharing abstraction.   
Rather than generate a set of related failure-inducing tests, the Alhazen approach automatically determines what inputs lead to a particular software behavior (also can be a failure) take place. Alhazen parses inputs by using grammar and feeds several selected features to a decision tree learner. In each iteration, the learner removes prohibited production and eliminates infeasible predicate sets to produce inputs for next iteration.
After re-testing with the generated inputs repeatedly, Alhazen can predict the program behavior by learning the decision rules inferred from previous testing results.


### [Seminar] Simplifying and Isolating Failure-Inducing Input
[**Paper**](https://hiper.cis.udel.edu/lp/lib/exe/fetch.php/courses/other-delta-zellertse.pdf)  *2021-05-01*

**Summary:**
 Developers of popular open-source software usually need to deal with a large number of bug reports. The ability to quickly clarify and classify the cause of bugs is vital. 
The paper implemented two algorithms — ddmin, dd. ddmin automatically minimizes the failure-inducing input by partitioning it into subsets and test each. The granularity of subsets is default two. ddmin increases granularity when none of these subsets is the failing test. When a test fails, ddmin recursively partitions this subset into smaller subsets and test each until ddmin can not increase the granularity. ddmin finds a minimal test case that satisfies two conditions: fails in the test and removing any part of it will make it not fail in the test. Correspondingly, dd adds two rules to ddmin. Likewise, dd partitions the difference between test failing cases and test passing cases. Moreover, each subset of changes is added to the test passing case and tested again. While a new test passes the test, dd recursively partitions the difference between the failure-inducing input. Eventually, the difference between a passing and failing test case is isolated. 
Experiments have shown that Delta Debugging algorithms achieve promising results in simplifying and isolating failure-inducing inputs automatically. The method has been applied to streamline the failing test inputs, including GCC, Mozilla, and fuzz inputs. Furthermore, Delta Debugging algorithms can be applied in users’ interactions and program invocations. 
Overall, Delta Debugging algorithms propose for the first time to combine debugging with re-testing to automatically minimize failure test cases and isolate the cause of failure.