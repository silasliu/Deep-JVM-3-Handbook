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
## 对象在堆内存的布局
1. 对象头 Header
   1. 运行时数据
   2. 类型指针
   3. (对象为数组时)数组长度数据
2. 实例数据 Instance Data
3. 对齐填充 Padding
## 对象的访问方式
对象的访问方式是指如何在栈中使用本地变量表的reference类型变量来操作堆上的具体对象.
虚拟机的对象访问方式有以下两种:
* 句柄访问
* 直接访问


