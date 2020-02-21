---
title: ZGC
top: false
cover: false
toc: true
mathjax: true
tags: JVM
categories: Deep-JVM-3-Handbook
date: 2020-02-13 22:49:07
password:
summary:
---

## 定义
ZGC是基于动态Region内存布局，（暂时）不设年龄分代，使用了读屏障、染色指针和内存多重映射等技术来实现可并发的标记-整理算法的收集器。 

## 动态Region 
三种类型Region:  
1. 小型Region(small region) ,容量=2M ,存放小于256KB的对象
2. 中性Region(medium region),容量=32M,存放256KB~4MB的对象
3. 大型Region(large region),容量不固定(2M整数倍),存放单个4M以上对象,不会被重分配

## 染色指针
?? 2020年02月13日23:17:18 具体还是不清晰

## ZGC工作过程
### 1. 并发标记(Concurrent Mark)
可达性分析  
标记在染色指针上  
### 2. 并发预备重分配(Concurrent Prepare for Relocate)
重分配->复制到新Region中   
统计出重分配集(Relocation Set)  
### 3. 并发重分配(Concurrent Relocate)
将重分配集中每个Region并发复制到新Region,并为每个Region维护转发表(Forward Table)
此时初次访问旧对象发生"指针自愈"(转发到新的副本上)
### 4. 并发重映射(Concurrent Remap)
修正整个堆中指向重分配集中旧对象的所有引用  
被合并到下一次并发标记过程中(节省一次堆对象的遍历)

## 评价
###  存在对象分配速率的问题  
*完整并发收集时间长->新对象全部存活(浮动垃圾)->留给新对象可分配的空间不够多*  
解决办法:引入分代收集  