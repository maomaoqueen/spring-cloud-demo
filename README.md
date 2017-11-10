# 1. Spring Cloud Config

# 1.1 Spring Cloud Config 服务端配置

- 服务端需引入`spring-cloud-onfig-server`依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

- 设置配置仓库地址

```yml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/maomaoqueen/spring-cloud-config-repo #配置的git仓库地址
```

- 启动config server

在SpringBoot的启动类上添加`@EnableConfigServer`注解

# 1.2 Spring Cloud Config 客户端配置

- 客户端需引入`spring-cloud-starter-config`依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

- 设置Spring Cloud Config服务端uri

```yml
spring:
  cloud:
   config:
     uri: http://localhost:8888
```

- 获取远程配置中心的属性值

`server.port`为属性名,通过`@Value`注解获取属性值

```java
@Value("${server.port}")
    private String port;
```

> 在config client启动时,会获取远程配置中心的属性值,如果在本地也有设置则本地的属性值会被覆盖  

例如:  

本地`bootstrap.yml`中

```yml
server:
  port: 8888
```

远程配置中心的`application.properties`中
```properties
server.port=7777
```

则本地tomcat启动端口会修改为7777
