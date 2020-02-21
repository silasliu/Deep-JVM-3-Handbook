## 特点  
* 目标:无论任何堆内存大小下都可以吧垃圾收集的停顿时间控制在10毫秒以内  
* 并发垃圾标记,并发整理  
* 使用Brooks Point [一种转发指针(Forwarding Pointer)]实现引用修正
* Shenandoah使用转发指针和读屏障来实现并发整理(p113)
## 评价
吞吐量下降明显  
停顿时间未达到十毫秒以内的目标  

## G1的继任者  
与G1的区别:
1. 可以在整理阶段,与用户线程并发执行  
2. 默认不使用分代收集
3. 使用连接矩阵(Connection Matrix)维护跨Region引用关系  



## 收集过程
### 过程图示  
![](https://oss.silas.fun/markdown/20200211104226.png)
### 三个主要步骤
Three major phases:  
1. Snapshot-at-the-beginning concurrent mark  
并发标记
2. Concurrent evacuation  
并发回收
3. Concurrent update references   (optional)  
并发引用更新  

## 缺陷和改进  
* Brooks Pointer 带来的对象访问的线程安全问题
  * 写操作->复制对象生成副本后,引用更新前,对旧对象进行了写操作
  * 


* 改进方法
  * 写操作 -> CAS 操作表征
  * 读操作 -> 在读/写屏障中都加入了额外的转发处理??


## 参考文献  
https://shipilev.net/talks/devoxx-Nov2017-shenandoah.pdf