title: Zookeeper安装部署手册
cover_picture: /images/zook.jpg
tags: []
categories:
  - 玩转框架
date: 2018-08-29 20:20:00
---
** {{ title }}：** <Excerpt in index | 首页摘要>
分布式系统不是万能，不能解决所有痛点。在高可用，一致性，分区容错性必须有所权衡。
<!-- more -->
<The rest of contents | 余下全文>

## Zookeeper安装部署手册
### 一、环境配置

### 二、操作步骤
#### 1、下载zookeeper安装包
    
#### 2、将安装包上传解压到服务器指定目录
    
#### 3、对默认配置文件进行重命名
    
#### 4、修改zoo.cfg配置文件
    
    #发送心跳的间隔时间，单位：毫秒
    tickTime=2000
    #zookeeper保存数据的目录
    dataDir=/modules/zookeeper-3.4.5-cdh5.11.1/data
    #日志目录
    dataLogDir=/modules/zookeeper-3.4.5-cdh5.11.1/dataLog
    #端口
    clientPort=2181
    #leader和follower初始化连接时最长能忍受多少个心跳时间的间隔数
    initLimit=5
    #leader和follower之间发送消息，请求和英达时间长度，最长不能超过多少个tickTime的时间长度
    syncLimit=2
    #zookeeper机器列表，server.order这里的Order依据集群的机器个数依次进行递增，这里的server1、server2、server3表示机器IP地址
    server.1=server1:2888:3888
    server.2=server2:2888:3888
    server.3=server3:2888:3888
    
#### 5、新建myid文件
    
    在server1机器中，在上面配置的data目录下，新建一个名为 myid的文件，文件内容填写 1，对的，没有听错，文件中只保留一个数字 1。
    zookeeper是根据该文件来决定zookeeper集群各个机器的身份分配。
    
#### 6、将配置好的zookeeper分发到集群的所有机器
    经过上面的五个步骤zookeeper已经配置完毕，然后将其依次拷贝的集群的其他机器中。快捷一点可以使用 scp 命令来做这件事
    然后修改data目录的下的myid 文件中的数字，在这里即为将server2的myid内容修改为2，将server3的myid内容修改为3。对于不同的集群，根据需要进行修改，与配置文件中的order保持一致。
    
#### 7、启动zookeeper服务
    
    修改完成后，在每台机器上依次使用bin/zkServer.sh start来启动zookeeper服务，
    待启动完成后使用 bin/zkServer.sh status来查看该机器的身份 
    
#### 8、启动zookeeper客户端检验服务是否可用
    使用 bin/zkCli.sh来检验zookeeper是否可以连接成功，若出现如下提示，则表示zookeeper服务已经安装成功。