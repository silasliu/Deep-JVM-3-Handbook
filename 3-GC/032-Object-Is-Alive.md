---
title: 032-Object-Is-Alive
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

## GC Roots对象
大致分成两大类:
1. 全局性引用(例如常量和静态属性)
2. 执行上下文(例如栈帧中的本地变量表)

在Java体系里面，固定可以作为GC Roots的对象有如下几种：
1. 在虚拟机栈（栈帧中的本地变量表）中引用的对象，譬如各个线程被调用的方法栈中使用到的参数、局部变量、临时变量等。
2. 在方法区中类静态变量引用的对象
3. 在方法区中常量引用的对象，譬如字符串常量池里的引用
4. 在本地方法栈中JNI（Native方法）引用的对象
5. Java虚拟机内部的引用，如基本数据类型对应的class对象,一些常驻的异常对象(NullPointException,OutOfMemoryError 等),还有系统类加载器
6. 所有被同步锁(Syncharonized)持有的对象
7. 反映Java虚拟机内部使用情况的JMXBean、JVMTI中注册的回调、本地代码缓存等。
