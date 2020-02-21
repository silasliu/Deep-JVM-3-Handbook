[为什么java中调用final方法是用invokevirtual指令而不是invokespecial?](https://www.zhihu.com/question/45131640)

## 方法调用的字节码指令
Java 虚拟机支持以下五种字节码指令以实现方法调用
* invokestatic
* invokespecial
* invokevirtual
* invokeinterface
* invokedynamic


? 解析调用  和 分派调用中的静态调用的差异是?


## 栈帧
栈帧（Stack  Frame）是用于支持虚拟机进行方法调用和方法执行的数据结构，它是虚拟机运行时数据区中的虚拟机栈（Virtual  Machine  Stack）的栈元素。
### 栈帧组成
1. 局部变量表 Local Variables Table
2. 操作数栈 Operand Stack 
3. 动态连接 Dynamic Linking
4. 方法返回地址 Return Address
5. 附加信息
345统称栈帧信息.

