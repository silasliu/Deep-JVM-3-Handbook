---
title: 033-GC-Algorithm
top: false
cover: false
toc: true
mathjax: true
tags: JVM
categories: Deep-JVM-3-Handbook
date: 2020-01-12 13:35:53
password:
summary:
---

## 垃圾回收算法
有以下几种算法:
* 分代收集理论Generational Collection
* 标记-清除算法Mark-Sweep
Concurrent Mark Sweep(CMS)
* 标记-复制算法Copying
Serial,ParNew,Parallel Scavenge
* 标记-整理算法Mark-Compact
Serial Old,Parallel Old

### 标记-清除算法Mark-Sweep
#### 应用
Concurrent Mark Sweep(CMS)

### 标记-复制算法Copying
#### 应用
Serial,ParNew,Parallel Scavenge

### 标记-整理算法Mark-Compact
#### 应用
Serial Old,Parallel Old

## 分代收集理论
分代收集理论名为一种理论,实际更为一种经验法则,他建立在以下假说之上
1. 强分代假说 Weak Generational Hypothesis
2. 弱分代假说 Strong Generational Hypothesis
3. 跨代引用假说  Intergenerational Reference Hypothesis

## JVM经典垃圾收集器
指JDK 7 Update4 ~ JDK 11 前 HotSpot 虚拟机中全部可用的垃圾收集器
可按照连线形式搭配:
![](https://oss.silas.fun/image/20200116225405.png?x-oss-process=style/watermark)

## Serial 垃圾收集器
* 单线程的复制算法
* 简单高效
* Stop The World
* Client模式默认回收算法 

## ParNew 垃圾收集器
* Serial的多线程版本
* Stop The World
默认开启与处理器核心数量相同数量的线程用于垃圾收集

## Parallel Scavenge 收集器
* 追求可控制的吞吐量

### 参数
使用 -XX:MaxGCPauseMillis 控制最大停顿时间.
使用 -XX:GCTimeRatio 控制吞吐量.
> [Java 8 官方文档](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gc-ergonomics.html)  
> -XX:GCTimeRatio=nnn
> A hint to the virtual machine that it's desirable that not more than 1 / (1 + nnn) of the application execution time be spent in the collector.

注:此处<深入Java虚拟机 第三版>中的表述与官方文档有出入,以官方文档为准.
吞吐量 = 运行用户代码时间 / ( 运行用户代码时间 + 运行垃圾收集时间 )
吞吐量 = GCTimeRatio / ( 1 + GCTimeRatio )
GCTimeRatio = 运行用户代码时间 / 运行垃圾收集时间
GCTimeRatio = ( 1 / 吞吐量 ) - 1 

