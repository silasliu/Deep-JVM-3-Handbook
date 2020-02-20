## 运行时常量池
位于方法区中,用于存放编译器生成的各种字面量和符号引用(从class文件的常量池表Constant Pool Table中载入) p47

# 垃圾回收
## Minor GC
新生代垃圾回收-Young GC
## Major GC 
老年代垃圾回收-Old GC
## Full GC
收集整个Java堆和方法区的垃圾回收
注意:Full GC 有时候也指代老年代GC p97
## Mixed GC
收集整个新生代及部分老年代的垃圾回收
## Partial GC
不完整收集整个Java的垃圾回收
包括Minor Gc,Major GC,Mixed GC
## STW
等同于Stop The World
暂停全部用户线程以进行垃圾回收
## Stop The World
暂停全部用户线程以进行垃圾回收
## 吞吐量
吞吐量 = 运行用户代码时间 / ( 运行用户代码时间 + 运行垃圾收集时间 )
## -XX:MaxGCPauseMillis
使用Parallel Scavenge收集器时控制(单次)最大垃圾收集停顿时间,单位:秒.
一定情况下,该值设置越小,垃圾收集越频繁.(收集越频繁,单次收集新生代越少,能降低最大停顿时间)
## -XX:GCTimeRatio
使用Parallel Scavenge收集器时控制吞吐量大小.
> [Java 8 官方文档](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gc-ergonomics.html)  
> -XX:GCTimeRatio=nnn
> A hint to the virtual machine that it's desirable that not more than 1 / (1 + nnn) of the application execution time be spent in the collector.

吞吐量 = 运行用户代码时间 / ( 运行用户代码时间 + 运行垃圾收集时间 )
吞吐量 = GCTimeRatio / ( 1 + GCTimeRatio )
GCTimeRatio = 运行用户代码时间 / 运行垃圾收集时间
GCTimeRatio = ( 1 / 吞吐量 ) - 1 

## 方法区垃圾收集
这个区域垃圾收集的目标主要是针对(运行时)常量池的回收和类型的卸载. p46
# Class文件常量池
## CONSTANT_Utf8_info
UTF-8编码的字符串
## CONSTANT_Integer_info
整型字面量
## CONSTANT_Float_info
浮点型字面量
## CONSTANT_Long_info
长整型字面量
## CONSTANT_Double_info
双精度浮点型字面量
## CONSTANT_Class_info
## CONSTANT_String_info
## CONSTANT_Fieldref_info
## CONSTANT_Methodref_info
## CONSTANT_InterfaceMethodref_info

# 类加载
## 类加载 
**Class Loading**
指"类加载"Class Loading的过程,包括以下步骤
* 加载 Loading
* 链接 Linking
  * 验证 Verification
  * 准备 Preparation
  * 解析 Resolution
* 初始化 Initialization
* 使用 Using
* 卸载 Unloading


# 虚拟机字节码执行引擎
## 符号引用
Symbolic References
符号引用以一组符号来描述所引用的目标，符号可以是任何形式的字面量，只要使用时能无歧义地定位到目标即可。 
## 直接引用
Direct References
直接引用可以是直接指向目标的指针、相对偏移量或是一个能间接定位到目标的句柄。
## 字节码
* 语义1:一个字节长度,代表着某种特定操作含义的数字
* 语义2:指的是已经经过编译，但与特定机器代码无关，需要解释器转译后才能成为机器代码的中间代码.即class文件所储存的内容.

## 字节码指令
以操作码Opcode和零至多个操作数Operand(参数)的形式构成的单个虚拟机操作.
> 在计算机技术中，指令是由指令集架构定义的单个的CPU操作。[Wiki](https://zh.wikipedia.org/wiki/%E6%8C%87%E4%BB%A4)  
> Java虚拟机采用面向操作数栈的架构.

## 操作码Opcode
字节码指令集中定义的一个字节长度,代表着某种特定操作含义的数字

## 虚拟机指令
等同于字节码指令

## 字节码指令集
一系列字节码的集合

## 动态分派
动态分派是指在运行去根据实际类型确定方法执行版本的分派过程.
