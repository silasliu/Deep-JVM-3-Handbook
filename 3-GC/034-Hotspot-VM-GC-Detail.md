---
title: 034-Hotspot-VM-GC-Detail
top: false
cover: false
toc: true
mathjax: true
tags: JVM
categories: Deep-JVM-3-Handbook
date: 2020-01-12 13:37:15
password:
summary:
---
## 用来提高GC效率的技术细节

### 并发
对于三色算法在concurrent的时候可能产生的漏标记问题，SATB在marking阶段中，对于从gray对象移除的目标引用对象标记为gray，对于black引用的新产生的对象标记为black；由于是在开始的时候进行snapshot，因而可能存在Floating Garbage

原文網址：https://kknews.cc/code/pp4q2m2.html


SATB仅仅对于在marking开始阶段进行"snapshot"(marked all reachable at mark start)；在marking阶段中，对于从gray对象移除的目标引用对象标记为gray，对于black引用的新产生的对象标记为black；由于是在开始的时候进行snapshot，因而可能存在Floating Garbage

原文網址：https://kknews.cc/code/pp4q2m2.html

### others 
OopMap 用于记录引用对象引用存放位置,快速完成GC Roots 枚举

Safepoint 安全点  >> 生成OopMap的指令位置,线程到达安全点才能停顿下来进行GC

线程进行gc的中断方法

1. 抢先式中断 Preemptive Suspension
2. 主动式中断 Voluntary Suspension

安全局域 >>> 指在一段代码中,引用关系不会发生变化