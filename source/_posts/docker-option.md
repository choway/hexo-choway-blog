---
title: docker 基本操作
date: 2018-12-18 14:37:09
categories:
- DevOps
- Docker
tags:
- docker
---

<!-- more -->

## 查看 docker 环境
``` bash
$ docker -v
$ docker version
$ docker info
```

## docker 设置镜像加速
1. [centos] 在 /etc/docker/ 目录下建立 daemon.json 文件

``` json
{
  "registry-mirrors": ["https://mirror-id.mirror.aliyuncs.com"]
}
```

2. 然后执行

``` bash
$ systemctl daemon-reload
$ systemctl restart docker
```

## 镜像操作
##### 从仓库获取镜像
``` bash
$ docker pull
$ docker pull --help
```

##### 列出本地镜像
``` bash
$ docker image ls
$ docker images
```

##### 删除本地镜像
``` bash
$ docker image rm IMAGE_ID
$ docker rmi IMAGE_ID
```

## 容器操作
##### 查看容器
``` bash
$ docker ps 查看启动的容器
$ docker ps -a 查看所有容器，包括已停止的容器
```

##### 创建并启动容器
``` bash
$ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
OPTIONS 常用选项：
-p 将本地端口和容器端口进行映射，如 -p 80:8080；
-d 后台运行容器；
-i 将容器的标准输入一直打开；
-t 让容器分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上；
-v 挂载数据卷：将本地目录和容器目录进行映射，从而达到多容器实例之间共享数据目录；

##### 停止容器
``` bash
$ docker stop CONTAINER
```

##### 启动一个停止的容器
``` bash
$ docker start CONTAINER
```

##### 重启容器
``` bash
$ docker restart CONTAINER
```

##### 删除容器
``` bash
$ docker rm CONTAINER
```

##### 获取容器的输出信息
``` bash
$ docker logs CONTAINER
```

##### 进入容器
``` bash
$ docker exec -i -t CONTAINER /bin/bash
```

##### 容器拷贝（本地）文件
``` bash
$ docker cp
```
