# java知识点

### 内部类

- 成员内部类

  成员内部类是最普通的内部类，它的定义为位于另一个类的内部

- 局部内部类

  局部内部类是定义在一个方法或者一个作用域里面的类，它和成员内部类的区别在于局部内部类的访问仅限于方法内或者该作用域内（不能有 public、protected、private 以及 static 修饰符的）

- 匿名内部类

  

- 静态内部类

  关键字static，静态内部类是不需要依赖于外部类的，它不能使用外部类的非static成员变量或者方法

### 抽象类和接口

- 抽象类可实现公共的方法给子类继承；实现接口需实现接口定义的所有方法，抽象类只重载你需要的方法，代码更加简洁。

- 抽象类
  - 抽象类是用来捕捉子类的通用特性的 ，它不能被实例化，只能被用作子类的超类
  - 可以有构造器，main方法，速度更快
- 接口
  - 接口是抽象方法的集合，如果一个类实现了某个接口，那么它就继承了这个接口所有抽象方法
  - 没有构造器，不能有main方法
  - 增加新方法时，必须要修改所有引用过该接口的所有代码



### 子类赋值给父类

~~~ jva
Prent test= new child();
~~~

调用公有方法时，如果子类重写了方法则使用子类重写的方法，如果没有重写就使用父类的方法。

调用公有属性时，当子类和父类都有相同属性时，用的是父类属性。

赋值只是赋值给引用具有父类方法和公有属性的变量而已，内存里还是指向子类的对象，保存的是子类的对象。



### final、finally、finalize的区别

- final
  - final修饰的class，代表不可以继承扩展
  - final的方法也是不可以重写的
  - final修饰的变量是不可以修改的（对于基本类型不可修改，引用类型来说不能重新赋值）
- finally
  - try-catch-finally  保证重要代码一定被执行的语句
- finalize
  - finalize 该方法已经被抛弃，阻碍了jvm的回收机制。



### 序列化和反序列化

- 序列化：将对象转化为字节序列，便于存储。实现对象的“持久性”（即对象的生命周期不取决于程序）

  - Serializeable接口（隐式序列化，自动将**非STATIC和transient**修饰的成员变量序列化）
- Externalizable接口（显示序列化）



### Collection

- SET

  - 构造方法

    ~~~ java
    Set<E> set = new hashSet<E>(); //hashSET、treeSet
    ~~~

  - 方法

    add（），集合中加元素。

    remove（），删除集合中某元素。

    iterator(), 用于递归集合，返回一个Iterator（）对象。

- List

  - 构造方法

    ~~~java
    List<E> list = new linkedlist<E>();
    ~~~

  - 方法

    ~~~java
    add(int i,Object obj) //在位置i处插入元素obj
    remove(int i)   //删除I处的元素
    get(int i)  //获得I处的元素
    indexof(Object obj)  //返回元素obj的第一次出现的位置
    listIterator(int i)  //获得i（包含i）以后的所有元素的ListIterator实列对象
    ~~~

- Vector（线程安全）

  - 构造方法

    ~~~java
    Vector v1 = new Vector();
    ~~~

  - 常用方法

    ~~~java
    //插入
    //增加元素（末尾）
    public final synchronized void adddElement(Object obj)
    //设置指定位置元素（覆盖）
    public final synchronized void setElementAt(Object obj,int index)
    //插入指定位置元素，后续元素移动
    public final synchronized void insertElementAt(Object obj,int index)
    
    //删除
    public final synchronized void removeElement(Object obj) 
    public final synchronized void removeAllElement(); 
    public fianl synchronized void removeElementAt(int index) 
        
    //查询
    public final int indexOf(Object obj)
        //从指定位置开始向后查询
    public final synchronized int indexOf(Object obj,int index)
        //逆向查询
    public final int lastindexOf(Object obj)
    ~~~

    

- Map

  - 构造方法

    ~~~java
    Map<E,E> map = new hashMap<E,E>();
    ~~~

  - 方法

    ~~~  java
    put(k,v)  //插入键值对k:v
    get(k)    //获得键值K对应的V值
    remove(K) 
    iterator()   //返回Iterator实列对象
    ~~~

- Stack

  - 构造方法

    ~~~java
    Stack stack = new Stack();
    ~~~

  - 方法

    ~~~java
    push(obj) //入栈
    pop() //栈顶元素出栈
    peek() //取栈顶元素，不出栈
    ~~~

    

- Queue

  - 构造方法

    ~~~java
    Queue<E> queue = new LinkedList();
    ~~~

  - 方法

    ~~~java
    offer(obj)  //元素入队
    poll()  //队头元素出队
    peek()  //获取队头元素，不出队
    ~~~




### JVM

- 内存

  ![image-20200329105442427](https://github.com/moodsjinxin/moods/raw/master/images/image-20200329105442427.png)

  ![image-20200329111204416](https://github.com/moodsjinxin/moods/raw/master/images/image-20200329111204416.png)

  ![image-20200428091753078](https://github.com/moodsjinxin/moods/raw/master/images/image-20200428091753078.png)

- 类加载过程  加载、验证、解析、初始化

  ![image-20200326165230161](https://github.com/moodsjinxin/moods/raw/master/images/image-20200326165230161.png)

  - 验证：确保加载的类信息符合JVM规范，无安全方面的问题
- 解析： 将类的二进制数据中的符号引用替换为直接引用
  - 初始化：先初始化其父类（祖父类），再依次初始化

- 类加载器

  - Bootstrap ClassLoader：根类（启动、引导类加载器）加载器：负责加载java的核心类，由原生C++实现

  - Extension classloader： 扩展类加载器   负责加载JRE的扩展目录

  - Application classloader： 系统类加载器  负责加载应用类

  - ![image-20200428093245039](https://github.com/moodsjinxin/moods/raw/master/images/image-20200428093245039.png)

  - 双亲委派机制： 类的创建都是交由父类加载器来完成，一层层向上申请，直接到启动类加载器，顶层加载器不能完成，在交由子类加载器完成。

    - 避免了类的重复加载

    - 使相同类名加载出来的类都是相同的

      

- 堆和栈的区别

  - 栈

    - 先进后出，为一个线程独有；由编译器创建和释放。内存空间连续；

    - 第一个进栈的是主函数下一条指令的地址，然后是函数的各个参数，局部变量，基本数据类型

  - 堆

    - 由程序员分配和释放，链接；速度慢
    - 内容：new 对象，引用类型

- 垃圾回收的算法思想

  - 引用计数
  - 标记清除（碎片多）
  - 复制算法（不容易产生碎片、代价高昂、空间分半）
  - 标记整理清除法
  - 分代收集算法
    - 新生代：复制算法
    - 老年代：标记整理清除

- GCroot 可达性分析 （从GCroot的对象为起始点进行搜索，寻找可达对象，所有不可达对象作为垃圾回收）

  - GCROOT的可能
    - 虚拟机栈（栈帧中的局部变量区）中引用的对象
    - 方法区中类静态属性引用的对象
    - 方法区中常量引用的对象
    - 本地方法栈中JNI（native方法）引用的对象

- 垃圾回收器详解（回收算法的落地）

  - 垃圾回收方法

    - Serial 串行 ： 为单线程环境设计的只用一个线程进行垃圾回收，回收时暂停用户程序
    - Parallel 并行 ： 多个垃圾回收线程并行工作，此时用户进程暂停
    - CMS 并发：用户线程和收集线程可以同时执行（不一定并行，可能并发），不需要停顿用户程序
    - G1： 将堆内存分割成不同区域然后并发进行垃圾回收 

  - 垃圾收集器种类

    ![image-20200326164404921](https://github.com/moodsjinxin/moods/raw/master/images/image-20200326164404921.png)

    - serial / serialold  单线程串行

    - Parnew    多线程并行计算

    - Parallel Scavenge /parallel old多线程收集器（并行），不需要暂停用户

    - CMS 并发收集器 采用mark算法

    - G1

      - 偏向服务端，更高性能，更大内存

      - 和应用程序并发执行

      - 与CMS相比 不会产生很多内存碎片、在停顿时间上增加了预测机制，用户可以指定停顿的时间

      - 老年代和新生代不再是连续的空间，内存区域划分为大小一样的区块，分属于老年代和新生代

      - 整体上采用标记整理算法，局部通过复制，没有碎片

        

  - 使用情况

    - ![image-20200326164545891](https://github.com/moodsjinxin/moods/raw/master/images/image-20200326164545891.png)
    - 

- JVM调优

  - 参数类型： 标配 x参数 xx参数**

  - 参数

    ~~~
    -XMS	初始堆空间
    -XMX	堆的最大值
    -XSS    初始栈空间
    
    xx参数类型：boolean\ kv \ jinfo
    jps 查看java的后台进程
    jinfo 查看正在运行程序的信息
    	例如：jinfo -flag 参数名	进程标识号
    修改参数：
    	boolean:	-xx:+(-)参数名
    	kv：			-XX: K = V 
    *** 如何盘看家底参数cmd中	java -xx：+printflagsinitial
    
    ~~~

    









### java反射机制

- java类型信息的获取

  - RTTI（Run-TIME Type Identification）
  - java反射机制

- 定义

  - 动态获取信息或动态调取方法的功能称为java反射机制

    对于任意的类，都能知道该类的属性和方法；对于任意对象，都能调用它的方法和属性。

- 利用CLASS类来创建实列

  ![image-20200226224513419](https://github.com/moodsjinxin/moods/raw/master/images/image-20200226224513419.png)



- 利用Method类中的invoke（）方法实现反射

  ![image-20200226225216830](https://github.com/moodsjinxin/moods/raw/master/images/image-20200226225216830.png)

- java代理

  - 静态代理

    - 创建共同接口（抽象类）

    - 创建真实对象继承共同接口

    - 创建代理对象继承共同接口

      类属性引用了真实对象

    - 在客户端创建共同接口的抽象类对象（实例对象为代理对象）

    - 调用共同接口的方法

  

  - 动态代理

    - java.long.Proxy类 

      是java动态代理机制的主类，它提供一组静态的方法为一组接口动态的完成代理类及其对象

      ~~~ java
      //用于获取关联于指定类加载器和一组接口的动态代理类的类对象
      static class getProxyClass(ClassLoader loader,class[] interfaces) 
       //用于获取指定代理对象所关联的调用处理器
      static invocationHandler getInvocationHandler(Object proxu)
       //判定指定的类是否是一个动态代理类
      static boolean isProxyClass(Class cl)
      ~~~

    - 创建抽象角色

      ~~~ java
      public interface Subjectrole {
          public void request();
      }
      ~~~

    - 创建真实角色

      ~~~java
      //创建真实的角色
      public class Realrole implements Subjectrole {
          public void request(){
              System.out.println("我是真实对象");
          }
      }
      ~~~

    - 创建代理角色

      ~~~java
      import java.lang.reflect.InvocationHandler;
      import java.lang.reflect.Method;
      
      //代理角色，必须继承InvocationHandler
      public class Prorole implements InvocationHandler {
          private Object object;
          public Prorole(Object obj){
              object=obj;
          }
      
          @Override
          public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
              System.out.println("代理操作前的操作");
              method.invoke(object,args);
              System.out.println("代理操作后的操作");
              return null;
          }
      }
      ~~~

    - 创建测试客户端

      ~~~ java
      public class Clienttest {
          public static void main(String[] args) throws Throwable {
              //指定被代理的类
              Realrole realrole = new Realrole();
              InvocationHandler ds = new Prorole(realrole);
              Class cl = realrole.getClass();
              //一下是一次性生成代理
              Subjectrole subjectrole = (Subjectrole) Proxy.newProxyInstance(cl.getClassLoader(),cl.getInterfaces(),ds);
              subjectrole.request();
          }
      }
      ~~~

      

    



### Volatile

- java提供的轻量级的同步机制

- 特性：

  - 内存可见性（线程工作内存、主内存、修改共有变量时及时通知其它线程）

  - **不保证原子性**

    解决方法：sychronized(太重，不推荐)、AtomicInteger(与cas相关)

  - 禁止指令重排

- JMM（内存模型，抽象非实体）
  - 可见性、原子性、有序性
  - ![image-20200303163438670](https://github.com/moodsjinxin/moods/raw/master/images/image-20200303163438670.png)

- 使用场景
  
  - 单例模式



### CAS(比较并交换、CompareAndSwap)

- 源码分析

  ~~~java
  //5是初始值，假设从主内存中取得的初始值是5
  AtomicInteger atomicInteger = new AtomicInteger(5);
  //5是期望值，即最初拿到的值，判断主内存的值是否被人动过，2019是本次线程更新所得的值，返回值为boolean
  atomicInteger.compareAndSet(5,2019);
  ~~~

  ~~~java
  public final boolean compareAndSet(int expect, int update) {
      //valueofset 内存地址偏移量
          return unsafe.compareAndSwapInt(this, valueOffset, expect, update);
      }
  ~~~

  ~~~
  unsafe类jdk的最初代源码在jre的runtime.sun.misc包内
  是CAS的核心类，因为java无法直接访问底层系统，需要native方法来访问，Unsafe相当于和底层交互的接口，基于该类可以直接对本地内存进行操作。
  UNSAFE类中的方法都是用native修饰的，这些方法可以直接调用操作系统底层资源
  ~~~

  ~~~java
  底层比较并交换的代码
  int var ;
  do{
      //取当前变量的最新值
  var = this.getIntVolatile(obj,valueoffset);
  }while(//当不被接受时，继续循环取最新值，直到被接受
      !this.compareAndSwapInt(obj,valueoffset,var,update))
  return var;//返回本次更新前的最新值
  ~~~

  do-while也称为自旋锁

- CAS是cpu的并发原语，具有原子性

- 缺点

  - 可能产生死循环，时间开销大
  
  - 只能完成一个共享变量的原子操作
  
  - 引发ABA问题（A-B-A,其它线程无法判断中间发生了什么）
  
    - 原子引用，AtomicReference接口时间类的原子声明。（类似于AtomicInteger）
  
      ~~~java
    AtomicReference<Myclass> atomic = new AtomicReference<>(初始值);
      ~~~
    
      
    
      ![image-20200304174229639](https://github.com/moodsjinxin/moods/raw/master/images/image-20200304174229639.png)
    
    - 原子引用解决ABA（时间戳的原子引用）
    
      ~~~java
      AtomicstampReference<Myclass> atomic = new AtomicStampReference<>(初始值，初始时间戳);
      ~~~
    
      ~~~java
      new Thread(new Runable() ->{
      atomic.compareandswap(excetVal,updateVal,exceptTimestamp,updaTimestamp);
      },"thread4").start();
      ~~~



### 集合类的不安全现象（MAP、LIST、SET）

- ConcurrentModificationException异常

  - 原因：

  - 解决方法：

    - Collections类

    ~~~java
    	//构建一个线程安全的集合类，collections是collection的辅助方法类	
    	List<String> list = new Collections.synchronizedList(new ArrayList());
    ~~~

    - juc的copyOnWriteArrayList<E>类 ——写时复制

      ~~~java
      List<String> list = new CopyOnWriteArrayList<>();
      ~~~

      - 读写分离、写时复制

### HASHMAP && ConcurrentHash Map

- HashMap

  - 

    默认加载因子： 0.75

    链转红黑树的阈值：8  
  
  

### CountDownLatch

- 

  ~~~java
  CountDownLatch countdownlatch = new CountDownLatch(int count);
  .....
      //计数器值减一
      countdownlatch.countdown();
  	//等待count==0
  	countdownlatch.await();
  ~~~

- CyclicBarrier(与CountDownLatch相反)

  ~~~java
   //public CyclicBarrier(int parties, Runnable barrierAction),parties计数值，barrierAction 线程
          CyclicBarrier cyclicBarrier = new CyclicBarrier(7, new Runnable() {
              @Override
              public void run() {
                  System.out.println("jiqilongzhu");
              }
          });
  for(int i=0;i<7;i++){
              int finalI = i;
              new Thread(new Runnable() {
                  @Override
                  public void run() {
                      System.out.println(Thread.currentThread().getName()+"收集到第"+ finalI +"棵龙珠");
                      try {
                          //本线程等待值到达7
                          cyclicBarrier.await();
                      } catch (InterruptedException e) {
                          e.printStackTrace();
                      } catch (BrokenBarrierException e) {
                          e.printStackTrace();
                      }
                  }
              },String.valueOf(i)).start();
  ~~~

- Semaphore(信号量)

  ~~~java
  public static void main(String[] args) {
          //public Semaphore(int permits, boolean fair),permits 计数，fair （公平与不公平）默认false,不公平
          Semaphore semaphore =new Semaphore(3); //3个资源
          for(int i=0;i<6;i++){              //6个线程去争夺
              new Thread(new Runnable() {
                  @Override
                  public void run() {
                      try {
                          semaphore.acquire();
                          System.out.println(Thread.currentThread().getName()+"抢到资源");
                          TimeUnit.MILLISECONDS.sleep(2000);
                          System.out.println(Thread.currentThread().getName()+"占用2秒后释放");
                      } catch (InterruptedException e) { e.printStackTrace(); }
                      finally {
                          //不管是线程挂掉 或者 运行完成 都要释放semaphore
                          semaphore.release();
                      }
                  }
              },String.valueOf(i)).start();
          }
      }
  ~~~


### BlockingQueue

- 构造方法

  ~~~java
   BlockingQueue queue = new LinkedBlockingDeque();
   BlockingQueue queue =new ArrayBlockingQueue(3); //3为队列的最大量，有界性
   BlockingQueue queue = new SynchronousQueue();//同步阻塞队列 必须有人take才会进行put
  ~~~

- 常用方法

  ![image-20200311152002377](https://github.com/moodsjinxin/moods/raw/master/images/image-20200311152002377.png)



### Synchronized 和Lock的区别

- Syn底层编译处用的是monitor ，lock用的是new 对象
- syn自动释放锁，lock必须手动释放，若不释放容易发生死锁
- syn不可中断，lock可以中断被阻塞（调用interrupt（）方法中断）
- syn非公平锁，lock根据构造方法的boolean参数来确定
- syn没有condition（要么唤醒一个，要么全部唤醒），lock可以构造多个condition精准唤醒，部分唤醒



### Thread_Pool

- 构造方法

  ~~~java
  ExecutorService threadpool = Executors.newCachedThreadPool();  多线程池
  ExecutorService threadpool = Executors.newFixedThreadPool(6);     固定数量的线程池
  ExecutorService threadpool = Executors.newSingleThreadExecutor(); //一池一线程
  ~~~

- 常用方法

  ~~~
  //
  submit(Callable<T> task);
  submit(Runnable task, T result);  //带结果的runable类的实现方法
  submit(Runnable task);
  
  //配套使用
  execute(Runable task);
  shutdown();
  ~~~

- 底层原理

  ~~~java
  public static ExecutorService newSingleThreadExecutor() {
          return new FinalizableDelegatedExecutorService
              (new ThreadPoolExecutor(1, 1,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>()));
      }
  
  public static ExecutorService newCachedThreadPool() {
          return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                        60L, TimeUnit.SECONDS,
                                        new SynchronousQueue<Runnable>());
      }
  ~~~

- 拒绝策略
  - 丢弃任务并抛出异常
  - 丢弃任务
  - 丢弃队列最前的任务，然后提交被拒绝的任务
  - 直接处理该线程


### OOM

- 种类

  ![image-20200326145431318](https://github.com/moodsjinxin/moods/raw/master/images/image-20200326145431318.png)

- 后四种类型

  - GC overhead limit ：程序大量的资源用来做GC或者多次	GC却只回收了2%的极端情况。
  - Direct buffer memory：元空间的new对象直接new在直接内存空间中，GC无法回收，极端情况下直接内存慢了，抛出错误（很严重）
  - unable to create  new native thread:
    - 一个应用进程创建了多个线程，超出系统承载极限
    - 服务器不允许应用程序创建多线程
    - 解决方法：1.降低创建的线程数量  2.修改操作系统的配置参数
  - metaspace：元空间溢出

  
