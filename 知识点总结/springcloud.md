# springcloud

### Feign

- Feign把request请求隐藏，伪装成类似于SpringMVC的controller类，URL的参数拼接交于Feign自动完成

- 步骤

  - 注解： 在启动类上加 @EnableFeignClients

  - 创建Feign客户端：接口类上加 @FenginClient("服务名称")

    ~~~ java
    @FeignClient("user-services")
    Public interface UserClient{
    	@GetMapping("user/{id}")
    	User querbyid(@pathvariable Long id);//调用该方法时会自动拼接为“http：//user-												services/user/{id}”去查询数据
    }
    ~~~

  - 创建处理器

    ~~~ java
    @RerstController
    @RuqestMapping("/cf")
    Public class FeignController{
        @Authouired
        private UserClient userclient; //自动注入Feign客户端
       
        @GetMapping("/{id}")
        Public User querybyid(@pathvariable Long id){
            return userclient.querbyid(id);
        }
    }
    ~~~



###  FEIGN中的负载均衡和熔断

- 负载均衡：feign中本身集成了ribbon依赖，因此不需要引入依赖及创建RestTemplate对象

  - 在FEIGN配置（消费者工程下的APPLICATION.xml）中加入

    ~~~ xml
    ribbon:
    	ReadTimeout:2000 #读取超时时长
    	ConnectTimeout:1000 #建立连接超时时长
    	MaxAutoRetries: 0 #当前服务器的重连次数
    	MaxAutoRetriesNextSercer：0 # 重连多少次服务
    	OKtoRetryOnAllOperations： false #是否对所有的请求方式都重试
    ~~~

- hystrix

  ~~~ xml
  feign：
  	hystrix：
  		enabled：true #开启熔断器功能
  ~~~



### Gateway网关

- gateway组件的核心是**过滤器**，通过这些过滤器将客户端的请求**路由**（转发）到对应的微服务。

![image-20200223110608399](C:\Users\金鑫\AppData\Roaming\Typora\typora-user-images\image-20200223110608399.png)

 

- 核心概念

  ![image-20200223110911639](C:\Users\金鑫\AppData\Roaming\Typora\typora-user-images\image-20200223110911639.png)





### 总结

- 

  ![image-20200228093829848](C:\Users\金鑫\AppData\Roaming\Typora\typora-user-images\image-20200228093829848.png)