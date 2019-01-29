---
title: Dockerfile 编写
date: 2018-12-14 07:12:39
categories:
- DevOps
- Docker
tags:
- docker
---

Docker 通过从 Dockerfile 包含所有命令的文本文件中读取指令来自动构建镜像 ，按顺序构建镜像。Docker 镜像由只读层组成，每个层都代表一个Dockerfile 指令。这些层是堆叠的，每一层都是前一层变化的增量。

<!-- more -->

## Dockerfile 指令
**FROM** 引用的基础镜像
**LABEL** 为镜像添加标签
**RUN** 执行任何命令并提交结果
**CMD** 用于运行图像包含的软件以及任何参数
**EXPOSE** 容器监听的端口并可以暴露容器外部使用
**ENV** 设置环境变量
**COPY** 将本地文件复制到容器中
