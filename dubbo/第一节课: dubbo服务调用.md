#  Dubbo

## 一 分布式架构的发展历史与背景

### 架构的发展史

#### 单体式架构

![image-20210905210829901](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905210829901.png)

#### 垂直架构

![image-20210905211101756](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905211101756.png)

#### 分布式架构



![image-20210905193740649](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905193740649.png)

#### 微服务架构

分布式架构粒度更小



### 分布式架构所带来的成本与风险

#### 分布式事务

分布式事务指一个操作，分成几个小操作在多个服务器上执行，要么都成功，要么都失败。

#### 不允许服务有状态

无状态服务是指对单次请求处理，不依赖其他请求，每次请求都是独立的一次请求。也就是处理一次请求所需要的信息要么都包含在这个请求里，要么可以从外部获取到，比如redis（session共享），服务器本省不存储任何信息。

#### 服务依赖关系复杂

服务A--->B--->C 那服务C的修改就可能影响B和C，事实上当服务越来越多的时候，C的变动就越来越困难。

链路追踪技术。 

#### 部署运维成本增加

不用说了，相比之前几个节点，运维成本增加必须的。

#### 源码管理成本增加：

原本一套或几套源码现在拆分成几十个源码库，其中分支，tag都要进行相应管理

#### 如何保证系统的伸缩性

伸缩性是指，当前服务器硬件升级后新增服务器处理能力就能相对应的提升。

#### 分布式会话：

为了解决服务存在状态的问题，我们不能将session存储在一个服务器上。

#### 分布式Job

通常一个定时任务在一台sever上执行，分布式情况下，不能在每台服务器上都能执行，所以我们通过分布式job进行选举一个任务执行。

- zookeeper进行选举，选出一台master服务器执行elasticJob
- 专门抽一台服务器去执行elasticJob





## 二 如何选型分布式架构

### 1. 分布式架构的背景



大家知道的有哪些远程调用的方式？拿几个大家比较熟悉的来举例：RMI，Web Service， Http

| 协议        | 描述 | 优点 | 缺点 |
| ----------- | ---- | ---- | ---- |
| RMI         | Java |      |      |
| Web Service |      |      |      |
| Http        |      |      |      |

![image-20210905194720346](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905194720346.png)

RMI 的缺点：

![image-20210905195551979](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905195551979.png)

- 不支持跨语言
- 负载均衡：这么多个机器调用哪一台？
- 服务发现：增加一台新的服务器，客户端怎么发现？
- 健康检测： 服务宕机或恢复后怎么办？
- 容错： 如果调用其中一台出错了怎么办？

### 2. 分布式架构的三种解决方案

1. 基于反向代理的集中式分布式架构
2. 嵌入应用内部的去中心化架构
3. 基于独立代理进程的Service Mesh架构

####  1）基于反向代理的集中式分布式架构



![image-20210905200529698](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905200529698.png)

轻量级分布式架构

![image-20210905200813069](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905200813069.png)

Http+Nginx 方案总结：

优点: 简单快速，几乎没有学习成本，对业务没有什么侵入性

使用场景：轻量级分布式系统，局部分布式架构。

瓶颈：Nginx 中心负载， Http传输，JSON序列化，开发效率，运维效率。多了一层Nginx调用。

  

#### 2）嵌入应用内部的去中心化架构

![image-20210905202530224](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905202530224.png)

给你封装一个jar包，这个jar包能够定时去从注册中心去获取servers这些信息。 在client调用server 会先调用jar包，这个jar包会提供一些负载均衡功能，然后client拿到信息会直接调用服务器。

##### 和一代比特点：

- 去中心化，客户端直连服务端，不需要和第一代那样多一次nginx,消息体积更小。
- 动态注册和发现服务
- 高效稳定的网络传输
- 透明代理。感知不到注册中心

##### 目前两种实现方式dubbo和springCloud

- dubbo是基于二进制流调用server1，server2，server3 长度为12字节
- http调用的话就是 18M

##### 如果注册中心挂掉了，会影响服务吗？

LB   Invoker 会将注册中心server注册信息缓存下来，如果注册中心暂时挂掉了，短暂来说是不影响服务调用的。





#### 3）基于独立代理进程的Service Mesh架构

这种做法是上面两种模式的一个折中，代理既不是独立集中部署，也不嵌入在客户应用的程序中，而是作为独立进程部署在每一个主机上，一个主机上的多个消费者应用可以共用这个代理，实现服务发现和负载均衡，如下图所示。这个模式一般需要独立的服务注册中心组件配合，作用同第二代架构。

![image-20210905210134601](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905210134601.png)

### 3. 三种架构的比较

![image-20210905210613851](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905210613851.png)

## 三 Dubbo架构与设计说明

### 1.dubbo架构简要讲解

![image-20210905223542611](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905223542611.png)

#### 1）流程说明

1. Provider(提供者)绑定指定端口并启动服务。
2. 服务提供者连接注册中心，并发本机IP，端口，应用信息和提供服务信息发送至注册中心存储。
3. Consumer(消费者)，连接注册中心，并发送应用信息，所想获得服务信息至注册中心。
4. 注册中心根据消费者所求服务信息匹配对应的提供者列表发送至Consumer应用缓存。
5. Consumer在发起远程调用时基于缓存的消费者列表择其一发起调用。
6. Provider状态变更会实时通知注册中心，在由注册中心实时推送至Consumer。

#### 2）这么设计的意义

1. Consumer与Provider 解耦，双方都可以横向增加节点数。
2. 注册中心对本身可做对等集群，可动态增减节点，并且任意一台宕掉后，将自动切换到另一台。
3. 去中心化，双方不直接依赖注册中心，即使注册中心全部宕机短时间也不会影响服务的调用。
4. 服务提供者无状态，任意一台宕掉后，不影响使用。

### 2. Dubbo整体设计

#### 1）整体设计

![image-20210905215726991](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905215726991.png)

- config 配置层: 对外配置接口，以ServiceConfig，ReferenceConfig为中心，可以直接初始化配置类。

  ![image-20210905220018879](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905220018879.png)

![image-20210905220134819](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905220134819.png)

#### 2）调用流程

![image-20210905233101440](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimgimage-20210905233101440.png)

### 3.Dubbo中的SPI机制

![image-20210905220612417](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905220612417.png) 

#### 1）演示Java SPI 机制





#### 2）演示Dubbo SPI 机制

