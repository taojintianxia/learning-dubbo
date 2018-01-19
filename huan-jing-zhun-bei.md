github上可以找到dubbo官网的一些例子 : [dubbo project](https://github.com/alibaba/dubbo)

环境需求 :  

* JDK: version 6 or higher  
* Maven: version 3 or higher

Maven依赖 : (最新版的dubbo为2.6.0) 

```
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dubbo</artifactId>
    <version>${dubbo.version}</version>
</dependency>
```
2.定义服务接口 :
鉴于服务端与客户端都依赖相同的接口, 这里强烈建议将接口放在一个单独的模块中, 这样可以给供provider跟consumer共享.  

```
package com.alibaba.dubbo.demo;

public interface DemoService {
    String sayHello(String name);
}

```
3.实现service provider

```
package com.alibaba.dubbo.demo.provider;
import com.alibaba.dubbo.demo.DemoService;

public class DemoServiceImpl implements DemoService {
    public String sayHello(String name) {
        return "Hello " + name;
    }
}

```
3.配置service provider
下面的一小段代码展示了如何通过spring来配置dubbo的service provider, 这也是比较推荐的方式.当然了, 你也可以通过[API configuration](https://dubbo.gitbooks.io/dubbo-user-book/content/configuration/api.html)的方式来配置.

```
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">
    <dubbo:application name="demo-provider"/>
    <dubbo:registry address="multicast://224.5.6.7:1234"/>
    <dubbo:protocol name="dubbo" port="20880"/>
    <dubbo:service interface="com.alibaba.dubbo.demo.DemoService" ref="demoService"/>
    <bean id="demoService" class="com.alibaba.dubbo.demo.provider.DemoServiceImpl"/>
</beans>
```


