---
title: centos7 安装 docker
date: 2018-12-14 05:09:03
categories:
- DevOps
- Docker
tags:
- docker
- centos
---

Docker 是开发人员和系统管理员使用容器开发，部署和运行应用程序的平台，用于轻松部署应用程序。Docker 可以将应用程序与基础架构分离，以便快速交付软件；可以像管理应用程序一样管理基础架构。通过利用 Docker 的方法快速发送，测试和部署代码，显著减少编写代码和在生产中运行代码之间的延迟。

<!-- more -->

## 系统要求
* centos 7
* centos-extras库必须启用

## 卸载旧版本
较旧版本的Docker被称为docker或docker-engine。如果已安装这些，请卸载它们以及相关的依赖项。
``` bash
$ sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-selinux docker-engine-selinux docker-engine
```

## 使用存储库安装
1. 安装所需的包

``` bash
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

2. 使用以下命令设置稳定存储库

``` bash
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

3. 安装 docker ce

``` bash
$ sudo yum install docker-ce
``` 
Docker已安装但尚未启动。该docker组已创建，但没有用户添加到该组。

4. 启动Docker

``` bash
$ sudo systemctl start docker
```

5. 运行hello-world 映像验证是否已正确安装

``` bash
$ sudo docker run hello-world
```