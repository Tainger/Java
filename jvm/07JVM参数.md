 #JVM参数

#### JVM 的堆内存, 是通过下面两个参数控制的。
- Xms 最小堆的大小，也就是当你的虚拟机启动后，就会分配这么大的堆内存给你。
- Xmx 是最大堆的大小。 
- -XX:+HeapDumpOnOutOfMMemoryError 在OOM的时候自动dum p当时的内存信息。

当最小堆占满后，会尝试进行GC，如果GC之后还不能得到足够的内存(GC未必会收集到所有当前可用内存)，分配新的对象，那么就会扩展堆，如果-Xmx设置的太小，扩展堆就会失败，导致OutOfMemoryError错误提示。

#### JVM常用命令
##### jps 查看java进程

##### jconsole

##### jstat 主要是查看内存的

###### jstat -gc pid  毫秒；

![image-20210905013019244](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905013019244.png)

S0C：年轻代中第一个survivor（幸存区）的容量 (字节)     

S1C：年轻代中第二个survivor（幸存区）的容量 (字节)     

S0U：年轻代中第一个survivor（幸存区）目前已使用空间 (字节)     

S1U：年轻代中第二个survivor（幸存区）目前已使用空间 (字节)     

EC：年轻代中Eden（伊甸园）的容量 (字节)     

EU：年轻代中Eden（伊甸园）目前已使用空间 (字节)     

OC：Old代的容量 (字节)     

OU：Old代目前已使用空间 (字节) 

MC：元空间的容量（字节）

MU：元空间的使用容量(字节)

CCSC：compressed class Space 的容量（字节）

CCSU:  compressed class Space 的使用空间 （字节）

YGC:  年轻代GC的次数

YGCT: 年轻代GC所花费的时间

FGC： full GC的次数

FGCT: full GC 所花费的次数

GCT：从应用程序启动到采样时gc用的总时间(s)

- ​	jstat -gcnew 5666

![image-20210905021247669](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905021247669.png)

- jstat -gcold 5666

![image-20210905021414103](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905021414103.png)

##### jstack

##### jmap

- jmap -dump:file=a 5666
- jmap -heap 5666

打印出内存信息，jstat也可以打印出内存信息，但是不太好观看出来。



##### visual VM的内存信息

因为有的时候linux是无界面纯命令行的，所以只能dump当时的内存文件，然后用visual VM查看。

· 

