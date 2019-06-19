title:   配置中心
tags: []
categories: [研发工具]
date: 2019/5/17 9:39
---
** {{ title }}：** <Excerpt in index | 首页摘要>
各种功能的开关、参数的配置、服务器的地址...配置修改后实时生效，灰度发布，分环境、分集群管理配置，完善的权限、审核机制...
<!-- more -->
<The rest of contents | 余下全文>

### 一、有哪些开源配置中心

* spring-cloud/spring-cloud-config
https://github.com/spring-cloud/spring-cloud-config
spring出品，可以和spring cloud无缝配合

* 淘宝 diamond
https://github.com/takeseem/diamond
已经不维护

* disconf
https://github.com/knightliao/disconf
java开发，蚂蚁金服技术专家发起，业界使用广泛

* ctrip apollo
https://github.com/ctripcorp/apollo/
Apollo（阿波罗）是携程框架部门研发的开源配置管理中心，具备规范的权限、流程治理等特性。

### 二、配置中心对别

### 三、技术路线兼容性
| 功能点 | 优先级 |  spring-cloud-config  |  ctrip apollo  |  disconf  | 
| :----: | :----: | :----: | :----: | :----: |
| SpringBoot支持 | 高 |  原生支持 |  支持 |  disconf  |   
| SpringCloud支持 | 高 | 原生支持  |  支持  |  disconf  |    
| 客户端支持 | 低 |  Java  |  Java、.Net  |  Java  |  备注  |
| 业务系统侵入性 | 高 | 侵入性弱  |  侵入性弱  |  侵入性弱 ，支持注解及xml方式	  | 
| 依赖组件 | 高 |  Eureka  |  Eureka  |  zookeeper  |  
### 四、可用性与易用性
