---
title: Java 虚拟机之垃圾回收器
date: 2019-01-29 14:28:17
categories:
- Java
- JVM
tags:
- java
- jvm
---

Java 虚拟机在进行垃圾回收之前，需要判断识别哪些对象为垃圾对象，再针对不同年代的对象，运用不同的回收算法对垃圾对象进行回收；

<!-- more -->

## 判断垃圾对象
