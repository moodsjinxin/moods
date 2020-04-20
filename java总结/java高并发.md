### 线程池

#### 引用

~~~ java
import java.util.concurrent.lockes.ExecutorService
~~~

#### 实现方法

1.实现类：

    ThreadPoolExecutor
    ScheduleThreadPoolExecutor
2.工厂类：Executors

~~~ txt
1. newCachedThreadPool 创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。
2. newFixedThreadPool 创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。
3. newScheduledThreadPool 创建一个定长线程池，支持定时及周期性任务执行。
4. newSingleThreadExecutor 创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。
~~~

3.实现举例

~~~
ExecutorService executorService01 = new ThreadPoolExecutor();

ExecutorService executorService02 = Exectors.newScheduledThreadPool();
~~~

#### 使用方法

  假设： executorService 是 ExecutorService 类的实例化对象

ExecutorService类有如下方法：

~~~
- execute(Runnable)  
- submit(Runnable)
- submit(Callable)
- invokeAny(...)
- invokeAll(...)
~~~

举例：

~~~java
executorService.execute(new Runnable(){public void run(){  //代码 
}});
~~~





### 线程间并行

#### 同步

1.Synchronized（对象）  对象锁

2.java.util.concurrent 下的Lock类

  ~~~java
Lock lock = new ReentrantLock();
lock.lock();  //加锁
lock.unlock(); //解锁

Java.util.concurrent.Condition condition1=lock.newCondition(); //创建条件锁
lock.lock();
condition.await(); //条件枷锁
condition.singal(); //条件上锁
  ~~~

#### 异步

 



### Raft

- https://blog.csdn.net/daaikuaichuan/article/details/98627822
- Leader选举、日志复制、安全性、日志压缩
- 

