---
layout:     post
title:      "Paper-Summaries"
subtitle:   " Security Papers"
date:       2021-05-11 00:00:00
author:     "luobobo"
header-img: "img/post2.jpg"
tags:
    - paper
---

> “The better you understand a subject, the easier it is to explain it thoroughly and briefly.”

My writing is so bad... I am taking a seminar lecture this semester and am required to write paper summaries every week. Here I record some summaries of papers I've read as a way to practice.

[**How to Summarize a Research Article**](https://writingcenter.uconn.edu/wp-content/uploads/sites/593/2014/06/How_to_Summarize_a_Research_Article1.pdf)


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