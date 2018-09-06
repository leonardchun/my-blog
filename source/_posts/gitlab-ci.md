title:  Gitlab-CI安装
cover_picture: /images/hexo.jpg
tags: []
categories:
  - 研发工具
date: 2018-08-29 20:20:00
---
** {{ title }}：** <Excerpt in index | 首页摘要>
GitLab持续集成（CI）：是一种软件开发实践，即团队开发成员经常集成它们的工作，通过每个成员每天至少集成一次，也就意味着每天可能会发生多次集成。每次集成都通过自动化的构建（包括编译，发布，自动化测试）来验证，从而尽早地发现集成错误
<!-- more -->
<The rest of contents | 余下全文>

#### 一：安装步骤

#### 1、安装
    sudo yum install gitlab-runner
    
    ##查看runner配置信息
    gitlab-runner list
    #也可以直接打开配置文件进行查看 
    vi /etc/gitlab-runner/config.toml
    
    ##部分GitLab-Runner常用命令
    1. gitlab-runner帮助：gitlab-runner –help
    2. gitlab-runner指定命令帮助：gitlab-runner <commond> –help
    3. 注册runner：gitlab-runner register
    4. 注销runner：gitlab-runner unregister
    5. 当前运行的runner：gitlab-runner list
    6. 启动runner：gitlab-runner start
    7. 停止runner：gitlab-runner stop
    8. 重启runner：gitlab-runner restart
    9. 查询runner状态：gitlab-runner status
    其他runner命令可以查询官网介绍：
    https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/commands/README.md

##### 2.注册runner
    sudo gitlab-runner register

 #### 二：卸载步骤
    rpm -qa|grep +你安装的名字 搜索不到证明你没有安装成功
    rpm -ql +你安装程序的名字 这能搜索到你安装成功的程序位置。
    rpm -e --noscripts ** 不考虑依赖卸载
    
    rpm -qa|grep gitlab-runner
    
    rpm -e gitlab-runner-11.2.0-1.x86_64
    
     #删除相关文件
     find / -name gitlab-runner
     find / -name gitlab-runner|xargs rm -rf
    