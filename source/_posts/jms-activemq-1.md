---
title: JMS 之 ActiveMQ
date: 2018-12-29 13:55:10
categories:
- DevOps
- ActiveMQ
tags:
- jms
- activemq
---

Apache ActiveMQ 是一款开源的，基于 JMS（Java Message Service） 标准的消息中间件（Message Oriented Middleware，MOM），实现 JMS Provider，用来实现高可用、高性能、可伸缩、易用和安全的企业级面向消息服务的系统。

<!-- more -->

## JMS 消息结构
JMS 消息由消息头、消息属性、消息体组成；
**消息头**
**Message ID** 消息的唯一标识；
**Destination** 消息发送的目的地，Queue 和 Topic；
**DeliveryMode** 传送模式：持久模式和非持久模式；持久化的消息在jms provider出现故障后不会消失，它会在服务器恢复之后再次传递；非持久化的消息最多被传送一次，服务器出现故障后，该消息永远消失；
**Expiration** 设置为0表示消息永不过期；
**Priority** 消息优先级：0-4是普通消息，5-9是加急消息，默认是4；
**Timestamp** 消息发送的时间戳；
**Correlation ID** 用来连接到另外一个消息，常用在回复消息中连接到原消息；
**Reply To** 设置回复本消息的消息目的地；
**Type** 消息类型；
**Redelivered** 是否重新传递：true 或 false；

## ActiveMQ 消息存储
ActiveMQ 提供了一个插件式的消息存储，主要实现：
1. 基于文件存储；
2. KahaDB 消息存储：提供了容量提升和恢复能力，是现在默认的存储方式；
3. JDBC 消息存储；
4. Memory 消息存储：基于内存存储；