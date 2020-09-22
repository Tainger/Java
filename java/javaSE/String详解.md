## String类可以被继承吗？



String类在声明时使用final关键字修饰，被final关键字修饰的类无法被继承。



接下来我们可以看一下String类的源代码片段：

```java
public final class String
    implements java.io.Serializable, Comparable<String>,CharSequence {
    /** The value is used for character storage. */
    private final char value[];

    /** Cache the hash code for the string */
    private int hash; // Default to 0

    /** use serialVersionUID from JDK 1.0.2 for interoperability */
    private static final long serialVersionUID = -6849794470754667710L;
```



- **为什么Java语言的开发者，把String类定义为final的呢？**

因为只有当字符串是不可变的，字符串池才有可能实现。字符串池的实现可以在运行时节约很多heap空间，因为不同的字符串变量都指向池中的同一个字符串。但如果字符串是可变的，那么String interning将不能实现，因为这样的话，如果变量改变了它的值，那么其它指向这个值的变量的值也会一起改变。如果字符串是可变的，那么会引起很严重的安全问题。譬如，数据库的用户名、密码都是以字符串的形式传入来获得数据库的连接，或者在socket编程中，主机名和端口都是以字符串的形式传入**。因为字符串是不可变的，所以它的值是不可改变的，否则黑客们可以钻到空子，改变字符串指向的对象的值，造成安全漏洞**。

 

因为字符串是不可变的，所以是多线程安全的，同一个字符串实例可以被多个线程共享。这样便不用因为线程安全问题而使用同步。字符串自己便是线程安全的。

 

因为字符串是不可变的，所以在它创建的时候HashCode就被缓存了，不需要重新计算。这就使得字符串很适合作为Map中的键，字符串的处理速度要快过其它的键对象。这就是HashMap中的键往往都使用字符串。



- **字符串常量池的设计意图是什么？**



字符串的分配，和其他的对象分配一样，耗费高昂的时间与空间代价，作为最基础的数据类型，大量频繁的创建字符串，极大程度地影响程序的性能。



JVM为了提高性能和减少内存开销，在实例化字符串常量的时候进行了一些优化。

1. 为字符串开辟一个字符串常量池，类似于缓存区。
2. 创建字符串常量时，首先坚持字符串常量池是否存在该字符串。
3. 存在该字符串，返回引用实例，不存在，实例化该字符串并放入池中。



实现的基础

1. 实现该优化的基础是因为字符串是不可变的，可以不用担心数据冲突进行共享。不会存在多个句柄（引用）指向一个String对象，其中一个引用改变了对象，导致数据异常。
2. 运行时实例创建的全局字符串常量池中有一个表，总是为池中每个唯一的字符串对象维护一个引用,这就意味着它们一直引用着字符串常量池中的对象，所以，在常量池中的这些字符串不会被垃圾收集器回收。



代码：从字符串常量池中获取相应的字符串

![image-20200922212928051](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922212928051.png)



- 字符串常量池在哪里？

在分析字符串常量池的位置时，首先了解一下jvm内存模型：

![image-20200922213617552](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922213617552.png)



堆

- 存储的是对象，每个对象都包含一个与之对应的class。
- JVM只有一个堆区(heap)被所有**线程共享**，堆中不存放基本类型和对象引用，只存放对象本身。
- 对象的由垃圾回收器负责回收，因此大小和生命周期不需要确定。

栈

- 每个线程包含一个栈区，栈中只保存基础数据类型的对象和自定义对象的引用(不是对象)。
- 每个栈中的数据(原始类型和对象引用)都是私有的。
- 栈分为3个部分：基本类型变量区、执行环境上下文、操作指令区(存放操作指令)。
- 数据大小和生命周期是可以确定的，当没有引用指向数据时，这个数据就会自动消失。

方法区

- 静态区，跟堆一样，被所有的线程共享。
- 方法区中包含的都是在整个程序中永远唯一的元素，如class，static变量。



**字符串常量池则存在于方法区**



代码：堆栈方法区存储字符串

![image-20200922214623883](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922214623883.png)

![image-20200922214639259](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922214639259.png)

**字符串对象的创建**

面试题：String str4 = new String(“abc”) 创建多少个对象？

1. 在常量池中查找是否有"abc"对象

   ​	a. 有则返回对应的引用实例，常量池中的每个实例都有一个引用引用，所以才一直不会gc回收。

   ​	b.没有则创建对应的实例对象。

2. 在堆中new一个String("abc") 对象。

3. 将对象地址赋值给str4,创建一个引用。

所以，常量池中没有“abc”字面量则创建两个对象，否则创建一个对象，以及创建一个引用。

**操作字符串常量池的方式**

- JVM实例化字符串常量池时

![image-20200922215508654](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922215508654.png)

- String.intern()

通过new操作符创建的字符串对象不指向字符串池中的任何对象，但是可以通过使用字符串的intern()方法来指向其中的某一个。java.lang.String.intern()返回一个保留池字符串，就是一个在全局字符串池中有了一个入口。如果以前没有在全局字符串池中，那么它就会被添加到里面。

![image-20200922215546348](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922215546348.png)

**字面量和常量池初探**

字符串对象内部是用字符数组存储的，那么看下面的例子：

![image-20200922215614177](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922215614177.png)



1. 会分配一个11长度的char数组，并在常量池分配一个由这个char数组组成的字符串，然后由m去引用这个字符串。
2. 用n去引用常量池里边的字符串，所以和n引用的是同一个对象。
3. 生成一个新的字符串，但内部的字符数组引用着m内部的字符数组。
4. 同样会生成一个新的字符串，但内部的字符数组引用常量池里边的字符串内部的字符数组，意思是和u是同样的字符数组。
5. 使用图来表示的话，情况就大概是这样的(使用虚线只是表示两者其实没什么特别的关系)：
6. ![image-20200922215911116](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922215911116.png)

测试demo：

![image-20200922215932868](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200922215932868.png)



结论：

- m和n是同一个对象；
- m,u,v都是不同的对象
- m,u,v,n但都使用了同样的字符数组，并且用equal判断的话也会返回true。

































