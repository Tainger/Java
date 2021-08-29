# Java技术栈

### 总结：
- 面试应主动把内容说详细，有详有略去描述，把控面试， 告诉面试官你擅长哪一块，你的优势在哪？
- 不满足说出来，别人都知道我也知道，而且我知道的更详细。
### JAVA 基础
- == equals区别，如果hashcode相等代表equals相等吗？



### JAVA 容器
- hashmap实现，线程安全？为什么会造成不安全，currenthashmap怎么实现线程安全的
- concurrenthashmap如何保证线程安全，说说你的理解
- arraylist linkedlist 使用场景
- hashmap底层实现方式『tableSizeFor，hash』？，1.8相比1.7为什么头插变尾插？
- 什么时候变成红黑树？双哈希表？「这些其实讲到了源码层面，initTable，resize，tryPresize，Thread.yield，ForwardingNode。」
- 线程安全的map有哪些？为什么用concurrenthashmap？底层实现是什么？
- 什么时候变成红黑树？双哈希表？「这些其实讲到了源码层面，initTable，resize，tryPresize，Thread.yield，ForwardingNode。」



### [多线程](https://github.com/jiazhiyuans/Java/blob/master/Thread/thread.md)
- 创建线程的几种方式？
- java中线程的状态 和 理论上线程模型对比
- 本地线程和守护线程的区别，Thread.setDemon();
- synchronized？mute lock怎么实现的
- 线程池好处？多创线程就怎么了？压测的时候创建几千个线程才几毫秒这点儿开销有必要节省吗？内存开销，时间开销？线程池参数，execute执行流程，work？没有工作会删除吗？睡眠状态？idl怎么配置的？最大线程满了之后？
- 有哪些Map？还有啥Map？用的jdk几？说一下HashMap数据结构，put值散列冲突怎么解决？链表树化转移数量？为什么是8为什么是6？？为什么数组要是二次幂？怎么扩容的？扩容rehash的流程？
- concurrentHashMap的散列流程？concurrentHashMap怎么实现的线程安全？CAS什么意思，怎么实现的？Unsafe怎么实现？concurrentHashMap什么时候用到CAS？并发情况下两个线程都到之后怎么插入的？初始化的时候两个线程都检测到需要初始化了，然后怎么做的？
- volatile讲一下，MESI？
- 线程池思想 介绍了线程池execute，submit中适配的思想
- [原子类](/Thread/21 原子类:无锁工具类的典范.md)

### jvm
- jvm运行时数据区，哪些线程私有，哪些会发生内存溢出，内存溢出和内存泄漏，怎么判断对象可回收，gc算法
- 类加载， 双亲委派类加载， 线程上下文加载， spi机制
- Java垃圾收集器知道哪些？高并发情况下用哪个？


### Hive
- hive是怎样将sql转化为mr任务的？
- hive中四种排序的区别（sort by/ order by/ distributed by/ cluster by），你在什么场合下用过这些排序函数？
- 遇到数据倾斜怎么解决

### redis
- redis数据类型
- redis持久化的方式，rdb和aof区别
- redis长度过长怎么优化？哪个api，数据量超过多少效率会变低？ 
- MySQL做过哪些优化？覆盖索引？limit两个参数区别？MySQL分页优化的其他方法
- string底层实现，跳表复杂度？
- redis集群部署方式？主从和哨兵的区别？
- redis 分布式锁的实现方式？
- redis 数据结构有哪些，zset 底层数据结构是什么，讲一下？
- redis分布式锁解决了什么问题？ 
- redis为什么能支持分布式锁？使用方式有哪些？



### 计算机网络
- tcp三次握手，四次挥手为什么是4次？



### mysql
- mysql聚簇索引和非聚簇索引，导致索引失效的场景
- 4种事务隔离级别和分别的问题？
- SQl调优你怎么做的？




### kafka
- Kafka分区分配的策略

### 面经常见的算法题

- 两数之和
- coins硬币
- 二叉树中序遍历，递归非递归实现

### 应用题
- 编写一个转账接口


### 业务功能实现
- 限流怎么做的？令牌桶的算法实现？限流还有哪些方式？
- 缓存穿透，雪崩，击穿讲下你的理解。雪崩问题的解决方案？
- redis解决客户端session共享信息怎么解决的。



### http 
- http1.1 http1.0 http2.0 区别 （+2）

### Spring
- Spring IOC，AOP你的理解讲一下？
- Spring注入方式知道哪些？
- bean是线程安全的吗？
- Spring循环依赖怎么解决？


### Linux
- Linux命令用的多吗？awk用过吗？

### 设计模式
- 单例模式

### 场景设计题
- 从一个目录中，找出所有文件里面单词出现top100





