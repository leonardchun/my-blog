title: Phoenix操作hbase语句
author: Leonard
cover_picture: /images/docker.jpg
tags: []
categories: [玩转框架,大数据]
date: 2018-08-30 11:26:00
---
** {{ title }}：** <Excerpt in index | 首页摘要>
hbase 提供很方便的shell脚本，可以对数据表进行 CURD 操作，但是毕竟是有一定的学习成本的，基本上对于开发来讲，
sql 语句都是看家本领，那么，有没有一种方法可以把 sql 语句转换成 hbase的原生API呢？ 这样就可以通过普通平常的 sql 来对hbase 进行数据的管理，使用成本大大降低。Apache Phoenix 组件就完成了这种需求
<!-- more -->
<The rest of contents | 余下全文>


创建表：

    CREATE TABLE "TEST" (
    "ROW" VARCHAR PRIMARY KEY,
    "ORDER_LINE_ID" VARCHAR,
    "ORDER_ID" VARCHAR,
    "IN_MODE_CODE" VARCHAR
    )

表赋值：

    upsert into TEST values('000027effafe62a196bd8012b0dd439ad1b0294a15000','NY','NewYork','8143197');

删除表：
    
    drop table TEST；

删除记录：

    delete from TEST where ORDER_ID='NewYork';

查找表：
    
    SELECT * FROM TEST LIMIT 1;

添加表字段：

    ALTER TABLE TEST ADD PRODUCT_ID VARCHAR;

删除表字段：
    
    ALTER TABLE TEST  DROP COLUMN PRODUCT_ID;