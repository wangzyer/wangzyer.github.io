---
date: 2020/9/20 20:00:25
categories:
- 容器
tags:
- Docker
- NodeJs
---

# 容器
### 虚拟化技术
#### 云计算
当我们把各种计算机资源集中起来放到一个地方，这个地方我们就称之为云端，云计算就是对这些与那段的计算机资源进行弹性管理、分配。我们常听到的阿里云、腾讯云等都是为我们提供云计算服务。
#### 分配资源
我们平时的个人电脑cpu、内存、硬盘等都是我们买单个的硬件组装起来使用。但是如果我们从阿里云申请一台主机，他们会用一个个的硬件为我们组装起来么？显然不可能，因为不同服务对资源的要求是不一样的，并且如此多的硬件组合对资源的浪费也是庞大的。虚拟化技术在这里起到了举足轻重的地位。
<!--more-->
#### 什么是虚拟化
虚拟化很好理解就是在一台硬件服务器上，分隔出多个虚拟服务器运行，这种虚拟服务器也叫虚拟机，这些虚拟机之前不会相互影响，每台虚拟机都有自己的内存、cpu、硬盘空间这些都是共享物理机的硬件，并且分配给每个虚拟机的硬件是相互隔离的（资源隔离），在虚拟化的时候按需求分配给各个虚拟机（资源限制）。

![91e9fe536a5a95af02c5c348bdca7ff2.jpeg](en-resource://database/537:1)
### 虚拟机和容器
在使用上述的虚拟技术使用过程中会出现一些问题。如果用户只想运行一个很小的服务，为了隔离只能分隔出一个虚拟机，这个过程是比较费时的，而且如果想要迁移服务就只能迁移整个虚拟机。这时就引入了“容器”。

容器也是虚拟化，但是相对于虚拟机的虚拟化更加的轻量和快速。虚拟机是操作系统级别的隔离，同一台物理设备的虚拟机都有各自的操作系统。而容器是进程上的资源分配，还是运行在物理机的操作系统上，通过对不同进程资源的管理、分配、隔离来实现虚拟化。

![ceae9f0bc8d350e464a9352e5b8dca65.jpeg](en-resource://database/541:1)


从虚拟化方式的不同就可以看出容器的虚拟化速度要比虚拟机快很多。我们常听说的Docker，就是创建容器的工具，是应用容器引擎。


![7054f2da73cfa36741f88db4479ca166.jpeg](en-resource://database/538:1)

### docker概念
- Docker daemon（ Docker守护进程）：Docker daemon是一个运行在宿主机（ DOCKER-HOST）的后台进程。可通过 Docker客户端与之通信。
- Client（ Docker客户端）：Docker客户端是 Docker的用户界面，它可以接受用户命令和配置标识，并与 Docker daemon通信。图中， docker build等都是 Docker的相关命令。
- Images（ Docker镜像）：Docker镜像是一个只读模板，它包含创建Docker容器的说明。它和系统安装光盘有点像，使用系统安装光盘可以安装系统，同理，使用Docker镜像可以运行 Docker镜像中的程序。
- Container（容器）：容器是镜像的可运行实例。镜像和容器的关系有点类似于面向对象中，类和对象的关系。可通过 Docker API或者 CLI命令来启停、移动、删除容器。

### docker工作原理
![cc31c1c36bf747967b53c6de65cfa486.jpeg](en-resource://database/540:1)
![8ee39b2707ac30be624db89eb3563072.jpeg](en-resource://database/539:1)

### docker的使用
#### 常用命令
##### 镜像相关
- docker search jdk 搜索java相关镜像
- docker pull fund-node 下载最新镜像
- docker pull fund-node:1.0.0 下载指定版本的镜像
- docker images 列出当前已经下载的镜像
- docker rmi fund-node:1.0.0 删除镜像
- docker commit -m="update" -a="wangzhiyong"  e218edb10161 fund-node:v1.0.1
- docker save fund-node:v1.0.1 > fund-node.tar 导出镜像
- docker load < fund-node.tar 导入镜像
##### 容器相关
- docker run -itd -v /data:/data node12  /bin/bash 根据指定镜像创建容器
-d: 后台运行
-p: 是容器内部端口绑定到指定的主机端口
-it: 为容器重新分配一个伪输入终端
-v: 本地和容器建立文件映射
- docker ps：列出运行中的容器
-a: 列出所有的容器
-l:  查询最后一次创建的容器
- docker stop 容器id：停止容器
- docker kill 容器id：强制停止容器
- docker start 容器id：启动已停止的容器
- docker restart 容器id：重启停止的容器
- docker inspect 容器id：查看容器的所有信息
- docker top 容器id：查看容器里的进程
- exit：退出容器
- docker rm 容器id：删除已停止的容器
- docker rm -f 容器id：删除正在运行的容器
- docker container ls 列出所有的容器
- docker container ls -a 列出所有的容器（包括已停止的）
- docker container logs 容器id：查看容器日志
- docker container exec -it 容器id /bin/bash：在运行的容器中执行命令
-i: 交互式操作
-t: 终端
- docker attach 容器ID：进入容器，退出时会停止容器（与exec功能类似）
- docker export 容器id > some.tar 导出容器
- docker import > some.tar 导入容器
- docker port 容器id：查看容器端口映射

### k8s