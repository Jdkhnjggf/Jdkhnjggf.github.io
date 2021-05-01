---
layout:     post
title:      "Paper-Summaries"
subtitle:   " Security Papers"
date:       2021-05-01 22:00:00
author:     "luobobo"
header-img: "img/post2.jpg"
tags:
    - paper
---

> “The better you understand a subject, the easier it is to explain it thoroughly and briefly.”

My writing skills are abysmal... I am taking a seminar lecture this semester and am required to write paper summaries every week. Here I record some summaries of papers I've read as a way to practice.

[How to Summarize a Research Article ](https://writingcenter.uconn.edu/wp-content/uploads/sites/593/2014/06/How_to_Summarize_a_Research_Article1.pdf)


### [Seminar] Simplifying and Isolating Failure-Inducing Input

[Paper](https://hiper.cis.udel.edu/lp/lib/exe/fetch.php/courses/other-delta-zellertse.pdf)

**Summary:**
Developers of popular open-source software usually need to deal with a huge number of bug reports. The ability to quickly clarify the classify the cause of bugs is vital. 
The paper implemented two algorithms — ddmin, dd. ddmin automatically minimizes the failure-inducing input by partitioning it into subsets and test each. The granularity is default two. ddmin increases granularity when none of these subsets is the failing test. When the test fails, ddmin recursively partitions this subset into smaller subsets and test each until the granularity can not be increased. A minimal test case is found that satisfies two conditions: (1) fails in the test and removing any part of it will make it not fail in the test. dd adds two rules to ddmin. Likewise, dd partitions the difference between test failing cases and test passing cases. Moreover, each subset of changes is added to the test passing case and tested again. While a new test case pass, dd recursively partitions the difference between the Failure-Inducing Input and it until the granularity can not be increased. The difference between a passing and failing test case is isolated. 
Experiments have shown that Delta Debugging algorithms achieve promising results in simplifying and isolating Failure-inducing inputs automatically. The method has been applied to simplify the failing test inputs, including GCC, Mozilla, and fuzz input. Furthermore, Delta Debugging algorithms can be applied in users’ interactions and program invocations. 
Overall, Delta Debugging algorithms propose for the first time to combine debugging with re-testing to automatically minimize failure test cases and isolate the cause of failure.