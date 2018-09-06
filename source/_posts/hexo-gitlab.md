title: Hexo + Gitlab光速搭建博客并实现Git服务器自动部署
cover_picture: /images/hexo.jpg
tags: []
categories:
  - 玩转框架
date: 2018-08-29 20:20:00
---
** {{ title }}：** <Excerpt in index | 首页摘要>
分布式系统不是万能，不能解决所有痛点。在高可用，一致性，分区容错性必须有所权衡。
<!-- more -->
<The rest of contents | 余下全文>

#### 第一步：安装node.js
##### 1、Windows下安装node
   Windows下安装直接下载软件包，执行就好。
   安装完成后，在Windows环境下，请打开命令提示符，然后输入node -v，如果安装正常，你应该看到v7.6.0这样的输出：
   
![upload successful](\images\hexo\pasted-1.png)

其实npm已经在Node.js安装的时候顺带装好了。我们在命令提示符或者终端输入npm -v，应该看到类似的输出：

![upload successful](\images\hexo\pasted-2.png)

##### 2、Linux下安装node
（1）下载nodejs程序包
网址：https://nodejs.org/en/download/

![upload successful](\images\hexo\pasted-3.png)

 （2）把程序包上传到服务器

![upload successful](\images\hexo\pasted-4.png)

（3）加压压缩包
	tar -xvf node-v10.8.0-linux-x64.tar.xz

（4）重命名文件夹
	mv node-v10.8.0-linux-x64 nodejs
    
 （5）建立软链接，配置全局环境变量

	ln -s /usr/local/node/nodejs/bin/npm /usr/local/bin/

	ln -s /usr/local/node/nodejs/bin/node /usr/local/bin/

 （6）检查是否配置成功
	node -v

	npm -v

2.把程序包上传到服务器

#### 第二步：安装hexo并初始化项目

    npm install -g hexo-cli

  安装成功后切换到你想要创建博客的目录，然后执行

    hexo init <folder>
     cd <folder>
     npm install
  其中folder为博客目录名称，换成你想要的名称即可
  至此，第一步已经完成。得到如下源文件：
  
![upload successful](\images\hexo\pasted-0.png)

#### 第三步：安装git

#### 第四步：上传项目到gitlab上

#### 第五步：Gitlab-CI实现
 ##### 1、名词解释
  （1）Gitlab-CI
 Gitlab-CI是GitLab Continuous Integration（Gitlab持续集成）的简称。
 
 从Gitlab的8.0版本开始，gitlab就全面集成了Gitlab-CI,并且对所有项目默认开启。
 
 只要在项目仓库的根目录添加.gitlab-ci.yml文件，并且配置了Runner（运行器），那么每一次合并请求（MR）或者push都会触发CI pipeline。
 
  （2）Gitlab-runner
   
   Gitlab-runner是.gitlab-ci.yml脚本的运行器，Gitlab-runner是基于Gitlab-CI的API进行构建的相互隔离的机器（或虚拟机）。GitLab Runner 不需要和Gitlab安装在同一台机器上，但是考虑到GitLab Runner的资源消耗问题和安全问题，也不建议这两者安装在同一台机器上。

Gitlab Runner分为两种，Shared runners和Specific runners。
Specific runners只能被指定的项目使用，Shared runners则可以运行所有开启 Allow shared runners选项的项目。

（3）Pipelines
Pipelines是定义于.gitlab-ci.yml中的不同阶段的不同任务。
我把Pipelines理解为流水线，流水线包含有多个阶段（stages），每个阶段包含有一个或多个工序（jobs），比如先购料、组装、测试、包装再上线销售，每一次push或者MR都要经过流水线之后才可以合格出厂。而.gitlab-ci.yml正是定义了这条流水线有哪些阶段，每个阶段要做什么事。

（4）Badges
徽章，当Pipelines执行完成，会生成徽章，你可以将这些徽章加入到你的README.md文件或者你的网站。

 ##### 2、安装配置
 这里跳过Gitlab的安装
 
 ##### 安装gitlab-ci-multi-runner
 （1）添加Gitlab的官方源
 
     #ForCentOS
     curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.rpm.sh | sudo bash
 （2）安装
    
    sudo yum install gitlab-ci-multi-runner
 
 （3）注册Runner
 
 Runner需要注册到Gitlab才可以被项目所使用，一个gitlab-ci-multi-runner服务可以注册多个Runner
     ## http://gitlab.capd.net/
     ## jgbar32kmvaafJvoNH2o
     
     sudo gitlab-ci-multi-runner register
     
     Running in system-mode.                            
                                                        
     Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
     http://gitlab.capd.net/
     Please enter the gitlab-ci token for this runner:
     jgbar32kmvaafJvoNH2o
     Please enter the gitlab-ci description for this runner:
     [host-10-1-241-33]: mytest
     Please enter the gitlab-ci tags for this runner (comma separated):
     test
     Whether to run untagged builds [true/false]:
     [false]: true
     Whether to lock Runner to current project [true/false]:
     [false]: 
     Registering runner... succeeded                     runner=jgbar32k
     Please enter the executor: docker, docker-ssh, parallels, ssh, docker-ssh+machine, shell, virtualbox, docker+machine, kubernetes:
     shell
     Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded! 
  （4）更新Runner
  如果需要更新Runner，只需要执行以下脚本： 
    
    #For CentOS
    sudo yum update
    sudo yum install gitlab-ci-multi-runner
 
 （5）Runner高级配置
  通过gitlab-ci-multi-runner register注册的Runner配置会存储在/etc/gitlab-runner/config.toml中，如果需要修改可直接编辑该文件

    concurrent = 1
    check_interval = 0
    [[runners]]
      name = "matesr"
      url = "http://gitlab.capd.net/"
      token = "977bec174e00a0960f6b3133d7f3c3"
      executor = "shell"
      [runners.cache]
    
    [[runners]]
      name = "hexO"
      url = "http://gitlab.capd.net/"
      token = "75e82f2298901dfb7aec37a47bacae"
      executor = "shell"
      [runners.cache]
    
    [[runners]]
      name = "asiainfo-hexo"
      url = "http://gitlab.capd.net/"
      token = "6765a30042ecdc79e41c2b085f2999"
      executor = "shell"
      [runners.cache]
    
    [[runners]]
      name = "hexo-jiacy"
      url = "http://10.1.241.33/"
      token = "d9034efa87b159c7c98794cfad9f8f"
      executor = "shell"
      [runners.cache]
    ~     
    到这里我们的Runner就安装配置好了，接下来是对项目根目录中.gitlab-ci.yml进行配置。               
 ##### （2）配置构建任务

   （1）在项目根目录添加.gitlab-ci.yml文件
   
    image: node:8.11.2
    
    pages:
      cache:
        paths:
        - node_modules/
    
      script:
      - npm install hexo-cli -g
      - npm install
      - hexo deploy
      artifacts:
        paths:
        - public
      only:
      - master
      
  （2）在项目根目录添加.gitlab-ci.yml文件
  
![upload successful](\images\hexo\pasted-5.png)

这样整个CI流程就配置完了，项目是hexo，就会生产我们的页面，在Pages中查看：

![upload successful](\images\hexo\pasted-6.png)

之后每次push到git仓库代码的时候都会执行项目对应的任务：

![upload successful](\images\hexo\pasted-7.png)