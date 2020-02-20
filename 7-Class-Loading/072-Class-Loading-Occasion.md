

?接口初始化的时机

## 类初始化时机
主动引用
1. 遇到 new、getstatic、putstatic、invokestatic 这四条字节码指令时.
2. 使用 Java.lang.refect 包的方法对类进行反射调用时.
3. 子类初始化触发父类初始化
4. 当虚拟机启动时，虚拟机会初始化主类(main 方法)。
5. java.lang.MethodHandle实例的最后解析结果为REF_getStatic,REF_putStatic,REF_invoke,REF_newInvokeSpecial四种类型的方法句柄时.
6. 定义了默认方法的接口的实现类会触发该接口的初始化.
被动引用
1. 子类引用父类的静态变量,子类不会被初始化
2. 创建类的数组
3. 访问类的常量

?必须字符串常量吗

## 陷阱
### 注意区分"类加载过程"与"加载"
类加载过程是指虚拟机将Class文件转化成内存中能直接使用的Java类型的过程.
在类加载过程中,涉及到"加载"这个阶段.