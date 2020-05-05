## Spring

### AOP

- 通过代理来实现对原来方法的功能增强

- 实现原理

  - 动态代理：对实现接口的类的代理

  - CGLIB代理：对没有实现接口的类的代理（实际上是生成目标类的子类来完成代理）

    - Enhancer可以为非接口类型创建一个java代理，动态的创建给定类的子类并拦截代理类的所有方法。

      ~~~java
      final LinkManDao linkManDao = new LinkManDao();
              // 创建cglib核心对象
              Enhancer enhancer = new Enhancer();
              // 设置父类
              enhancer.setSuperclass(linkManDao.getClass());
              // 设置回调
              enhancer.setCallback(new MethodInterceptor() {
                  /**
                   * 当你调用目标方法时，实质上是调用该方法
                   * intercept四个参数：
                   * proxy:代理对象
                   * method:目标方法
                   * args：目标方法的形参
                   * methodProxy:代理方法
                  */
                  @Override
                  public Object intercept(Object proxy, Method method, Object[] args, MethodProxy methodProxy)
                          throws Throwable {
                      System.out.println("记录日志");
                       Object result = method.invoke(linkManDao, args);
                      return result;
                  }
              });
              // 创建代理对象
              LinkManDao proxy = (LinkManDao) enhancer.create();
              proxy.save();
      ~~~



### IOC  java反射

- 原理：

  - 反转控制  现在对象的生命周期和对象间的关系将交由SPRING来控制，控制方不再是引用它的对象。
  - 依赖注入  动态的向某个对象提供它所需的其他对象。我们只需要在使用的时候从IOC容器中获取即可，不在是在代码中NEW一个新对象，这样也降低了耦合度。

- 总体阶段

  - 容器启动阶段
    - 注入： 构造方法注入、setter注入（用XML或者注解方式告知Spring）
    - 分类：
      - beanfactory   基础IOC容器，在访问某个受管对象时才开始对该对象进行初始化和依赖注入
      - ApplicationContext  容器启动后即把所有依赖和对象初始化完成

  - bean的注册过程
    - XMLbeandefiniton读取Xml中对应bean对象的信息映射到对应的beandefinition对象
    - 通过beanfactory在需要该对象时从beandefinitong中读取信息并实例化

- bean的生命周期

  - 实例化
  - 赋值
  - 初始化
  - 使用
  - 销毁

