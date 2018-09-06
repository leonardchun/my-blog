title: Centos7上安装Docker
author: Leonard
cover_picture: /images/docker.jpg
tags: []
categories:
  - 研发工具
date: 2018-08-30 11:26:00
---
** {{ title }}：** <Excerpt in index | 首页摘要>
分布式系统不是万能，不能解决所有痛点。在高可用，一致性，分区容错性必须有所权衡。
<!-- more -->
<The rest of contents | 余下全文>

#### 一、What is Docker? 
正如[Docker官网](https://docs.docker.com/)介绍的那样：

	Docker is the world’s leading software containerization platform.
 

Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从Apache2.0协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

#### 二、Centos7安装Docker

1、Docker 要求 CentOS 系统的内核版本高于 3.10 ，查看本页面的前提条件来验证你的CentOS 版本是否支持 Docker 。

通过 uname -r 命令查看你当前的内核版本

    $ uname -r
2、使用 root 权限登录 Centos。确保 yum 包更新到最新。

    $ sudo yum update
3、卸载旧版本(如果安装过旧版本的话)

    $ sudo yum remove docker  docker-common docker-selinux docker-engine
4、安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的

    $ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
5、设置yum源

    $ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

![upload successful](\images\docker\pasted-1.png)
6、可以查看所有仓库中所有docker版本，并选择特定版本安装

    $ yum list docker-ce --showduplicates | sort -r
![upload successful](\images\docker\pasted-0.png)

7、安装docker

    $ sudo yum install docker-ce  #由于repo中默认只开启stable仓库，故这里安装的是最新稳定版17.12.0
    $ sudo yum install <FQPN>  # 例如：sudo yum install docker-ce-17.12.0.ce
    
![upload successful](\images\docker\pasted-2.png)

8、启动并加入开机启动

    $ sudo systemctl start docker
    $ sudo systemctl enable docker
9、验证安装是否成功(有client和service两部分表示docker安装启动都成功了)

    $ docker version
       
![upload successful](\images\docker\pasted-3.png)