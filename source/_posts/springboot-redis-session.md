---
title: springboot redis 实现 session 共享
date: 2018-12-20 03:29:48
categories:
- Java
- SpringBoot
tags:
- java
- springboot
- redis
---

<!-- more -->

## springboot 版本
选择 springboot 2.x 的第一个 GA 版本：2.0.7.RELEASE
``` xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.0.7.RELEASE</version>
  <relativePath />
</parent>
```

## 添加依赖
``` xml
<dependency>
  <groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework.session</groupId>
	<artifactId>spring-session-data-redis</artifactId>
</dependency>
```

## application.yml
``` yaml
spring:
  application:
    name: springboot
  session:
    store-type: redis
  redis:
    host: 127.0.0.1
    port: 6379
    password:

server:
  port: 8080
```

## Java Config
``` java
@Configuration
@EnableRedisHttpSession(maxInactiveIntervalInSeconds = 1800)
public class RedisSessionConfig {

}
```
