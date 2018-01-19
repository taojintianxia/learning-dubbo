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
  


