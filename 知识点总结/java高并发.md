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

### Redis

- 什么是redis

  - nosql数据库，单线程

- 基本类型

  - String、list、hash、set、sset

- redis持久化

  - 将内存中数据异步写入磁盘、rdb、aof

  - rdb

    通过bgsave命令，父进程fork（）一个子进程，由子进程创建rdb文件（根据父进程内存生成临时的快照文件），将原文件（磁盘内）进行原子替换。

  - aof

    redis每执行一个操作后，都会把该命令添加到aof文件中

- redis为什么快

  - 单线程，无线程竞争
  - 数据的处理都是在内存上
  - 多路复用，不需要阻塞等待

- 如何保持一致性

- 分布式锁

  - setnx+expire
  - setnx

- Scan

  - ```java
    //scanParams 实现redis模糊查询
    ScanParams sp = new ScanParams();
    sp.match("*"+key+"*");
    //每次查询100个数据
    sp.count(100);
    
    //cursor 游标默认从0开始，每次执行Scan会返回查询结果和游标的位置，当返回游标为0才代表查询结束
    //scan()   return new ScanResult(newcursor, results)
    ScanResult<String> ret = jedis.scan(cursor, sp);
    ```



### RabbitMQ

- 基于高级消息队列协议的（AMQP）开源的消息代理的队列服务器

- 作用：

  - 异步：消息发送者只需要发送消息进队列即可，不需要等待消费者
  - 削峰：当队列满了后将会拒绝后面的请求
  - 解耦：消费者和生产者的代码完全解开，只需要设置QUEUE的订阅发布

- 基本对象

  - connectionFactory  connect的制造工厂
  - connection    MQ的Socket链接
  - channel    与MQ交互接口（定义QUEUE、exchange，绑定queue，发布消息等）
  - queue
  - exchange
    - fanout 把消息路由到所有与其绑定的队列中
    - direct  把消息发送到bind_key与route—key匹配的队列中
    - topic    加上模糊查询的direct，2个KEY用.来分，根据业务的不同模糊查询去不同的队列

- 特点

  - 消息都是存放在消息队列中，消费者每次消费消息都需要发送一个回执，MQ收到回执才会从队列中删除该消息，如没有收到并检测到链接断开（注意没有timeout），将该消息给其它消费者处理。
  - durable 持久化  mq事物
  - 生产者将消息交给exchange（指定rout-key，用来规定路由规则），由交换器来决定消息给哪个队列（或删除）

- 结构

  ![image-20200427222236560](C:\Users\jinxin\AppData\Roaming\Typora\typora-user-images\image-20200427222236560.png)

  - bind-key 和route-key匹配，消息送到对应队列

