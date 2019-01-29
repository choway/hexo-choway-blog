---
title: JVM 内存区域
date: 2018-12-11 09:23:46
categories:
- Java
- JVM
tags:
- java
- jvm
- hotspot
---

Java 虚拟机（JVM）在执行 Java 程序时会把它管理的内存划分为多个不同的数据区域。这些区域各有用途，以及创建和销毁的时间。有些内存区域随着虚拟机进程的启动而存在，有些区域则依赖用户线程的启动和结束而建立和销毁。

<!-- more -->

## 程序计数器（Program Counter Register）
由于 JVM 的多线程是通过线程切换并分配处理器执行时间的方式来实现的，所以在任何一个时刻，一个处理器（多核CPU的一个内核）都只会执行一条线程，线程切换后为了确保每个线程能恢复到正确的执行位置，每个线程都需要有个独立的程序计数器。
* 线程私有；
* 唯一一个在 JVM 规范中没有规定任何 OutOfMemoryError 的区域；

## JVM 栈（JVM Stacks）
Java 方法在执行时会创建一个栈帧（Stack Frame）用于存储局部变量表、操作数栈、动态链接、方法出口等信息；
每个方法从调用到执行结束，对应一个栈帧在 JVM 栈中的入栈到出栈过程；
如果线程请求的栈深度大于 JVM 所允许的深度，将抛出 StackOverflowError；
如果 JVM 栈可以动态扩展，如果扩展时无法申请到足够的内存，就会抛出 OutOfMemoryError；
* 线程私有；
* 在 JVM 规范会抛出 StackOverflowError、OutOfMemoryError；

#### 栈溢出（StackOverflowError）
在 HotSpot 虚拟机中并不区分虚拟机栈和本地方法栈，栈容量使用 -Xss 参数设定；


## JVM 堆（JVM Heap）
JVM 堆是被所有线程共享的内存区域，在虚拟机启动时创建；
JVM 规范：所有的对象实例以及数组都在堆上分配；
堆是垃圾回收器管理的主要区域，因此也被称为 GC 堆；
如果在堆中没有内存完成实例分配，并且堆也无法扩展，则抛出 OutOfMemoryError；
* 线程共享；
* 在 JVM 规范会抛出 OutOfMemoryError；

#### 堆溢出（OutOfMemoryError，简称 OOM）
* -Xms 设定堆最小值，即初始化堆大小；
* -Xmx 设定堆最大值，当堆内存不够时，堆大小会自动扩展，直到达到堆最大值；
-Xms 和 -Xmx 设置一样可避免堆自动扩展；

## 方法区（Method Area）
方法区用于存储已被 JVM 加载的类信息、常量、静态变量、即使编译器编译后的代码等数据，各个线程共享；
该区域的内存回收目标主要针对常量池的回收和类型卸载；
* 线程共享；
* 在 JVM 规范中，当方法区无法满足内存分配，则抛出 OutOfMemoryError；

#### 运行时常量池（Runtime Constant Pool）
常量池是方法区的一部分，也会抛出 OutOfMemoryError；
Class 文件除了有类的版本、字段、方法、接口等描述信息外，还有常量池用户存放编译期的各种字面量和符合引用，这些内容在类加载后进入方法区的运行时常量池中存放。

#### 方法区、常量池溢出
-XX:PermSize 和 -XX:MaxPermSize 设定方法区大小；


## 直接内存（Direct Memory）
直接内存不是 JVM 运行时数据的一部分，也不是 JVM 规范中定义的内存。
在 JDK 1.4 中新加入了 NIO（New Input/Output）类，引入了一种基于通道（Channel）与缓冲区（Buffer）的 IO 方式，它可以直接使用 Native 库直接分配堆外内存。
* -XX:MaxDirectMemorySize 参数指定直接内存大小；
* 如果不指定，默认与 -Xmx 值一样；