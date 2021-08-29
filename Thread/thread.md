# 多线程

### 创建线程的几种方式？
- 继承Thread类，重写run方法
- 实现Runnable接口创建线程
- 使用 Callable 和 FutureTask 创建线程
- 通过线程池创建线程

### 线程的状态
- java中线程的状态
 ```java
 public enum State {
        
        //线程被创建
        NEW,
        // 等待cpu调度
        RUNNABLE,
        //没有获得锁进入阻塞队列中
        BLOCKED,
        //线程进入等待状态，等待一个线程唤醒或者执行完。
        // 比如 等待唤醒 Object#wait() Object.wait，比如执行完 join 
        WAITING,
        //Thread.sleep， 
        // Object#wait(long) Object.wait} with timeout， 
        // #join(long) Thread.join} with timeout
        //LockSupport#parkNanos LockSupport.parkNanos
        // LockSupport#parkUntil LockSupport.parkUntil
        TIMED_WAITING,
        // 线程执行完的结束状态
        TERMINATED;
    }
```
- 操作系统中线程的状态
    创建线程， 就绪， 运行， 阻塞， 终结 


### ForkJoin 的理解


