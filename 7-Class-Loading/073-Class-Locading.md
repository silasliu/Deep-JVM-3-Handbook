## Java 类的加载阶段的工作.
1通过一个类的全限定名来获取定义的此类二进制字节流。
2将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构。
3在Java堆中生成一个代表这个类的java.lang.Class对象，作为对方法区中这些数据的访问入口。