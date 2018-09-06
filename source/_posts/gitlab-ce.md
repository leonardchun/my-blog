title:  Gitlab服务器搭建
cover_picture: /images/hexo.jpg
tags: []
categories:
  - 研发工具
date: 2018-08-29 20:20:00
---
** {{ title }}：** <Excerpt in index | 首页摘要>
GitLab 是一个用于仓库管理系统的开源项目，使用Git作为代码管理工具，并在此基础上搭建起来的web服务。
<!-- more -->
<The rest of contents | 余下全文>

#### 一：安装步骤
##### 1、安装
    ##安装
    sudo yum install gitlab-ce
    
    #配置itLab
    sudo gitlab-ctl reconfigure
    ##gitlab-ctl reconfigure
    ##出现：ruby_block[supervise_redis_sleep] action run，会一直卡无法往下进行
    ##解决方案：
    ##1. 按住CTRL+C强制结束
    ##2. 运行：sudo systemctl restart gitlab-runsvdir
    ##3. 再次执行：sudo gitlab-ctl reconfigure
    
    ##启动Gitlab服务
    sudo gitlab-ctl restart
 ##### 2、修改配置   

    vi /etc/gitlab/gitlab.rb
    
    ## 修改客户端访问地址，配置域名
    ## GitLab URL
    ##! URL on which GitLab will be reachable.
    ##! For more details on configuring external_url see:
    ##! https://docs.gitlab.com/omnibus/settings/configuration.html#configuring-the-external-url-for-gitlab
    external_url 'http://gitlab.capd.net'
    
    
    ## 更改代码仓库的默认目录
    ### For setting up different data storing directory
    ###! Docs: https://docs.gitlab.com/omnibus/settings/configuration.html#storing-git-data-in-an-alternative-directory
    ###! **If you want to use a single non-default directory to store git data use a
    ###!   path that doesn't contain symlinks.**
    git_data_dirs({
      "default" => {
        "path" => "/aifs/gitlab/git-data"
       }
    })
    
    ###### 
    #git_data_dir has been deprecated since 8.10 and was removed in 11.0. Use git_data_dirs instead.
    ######
    
    ################################################################################
    ## gitlab.yml configuration
    ##! Docs: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/gitlab.yml.md
    ################################################################################
    
    ### Email Settings
    gitlab_rails['gitlab_email_enabled'] = true
    gitlab_rails['gitlab_email_from'] = 'cuc-tc-capd@asiainfo.com'
    gitlab_rails['gitlab_email_display_name'] = 'CUC TC-CAPD ADMIN'
    gitlab_rails['gitlab_email_reply_to'] = 'cuc-tc-capd@asiainfo.com'
    gitlab_rails['gitlab_email_subject_suffix'] = ''
    
    ### GitLab email server settings
    ###! Docs: https://docs.gitlab.com/omnibus/settings/smtp.html
    ###! **Use smtp instead of sendmail/postfix.**
    
    gitlab_rails['smtp_enable'] = true
    gitlab_rails['smtp_address'] = "mail.asiainfo.com"
    gitlab_rails['smtp_port'] = 25
    gitlab_rails['smtp_user_name'] = "cuc-tc-capd@asiainfo.com"  ##必须是邮箱名
    gitlab_rails['smtp_password'] = "Gl123456"
    gitlab_rails['smtp_domain'] = "asiainfo.com"
    gitlab_rails['smtp_authentication'] = "login"
    gitlab_rails['smtp_enable_starttls_auto'] = true
    gitlab_rails['smtp_tls'] = false
    
    vi /var/opt/gitlab/gitlab-rails/etc/gitlab.yml
    
    ##域名配置
    ## Web server settings (note: host is the FQDN, do not include http://)
    host: gitlab.capd.net
    
    ## Email settings
    # Uncomment and set to false if you need to disable email sending from GitLab (default: true)
    #email_from: gitlab@gitlab.capd.net
    email_from: cuc-tc-capd@asiainfo.com
    
 #### 二：卸载步骤
     ## 停止gitlab
     sudo gitlab-ctl stop
     ## 卸载gitlab
     sudo rpm -e gitlab-ce
     ## 查看gitlab进程
     ps -ef|grep gitlab
     
     ## 杀掉第一个守护进程
     kill -9 6031
     # 再次查看gitlab进程是否存在
     ps -ef|grep gitlab
     
     ## 删除gitlab文件
     #  删除所有包含gitlab的文件及目录
     find / -name gitlab|xargs rm -rf

修改gitlab.rb、gitlab.yml需重启服务

    sudo gitlab-ctl reconfigure
    sudo gitlab-ctl restart
    sudo gitlab-ctl status
