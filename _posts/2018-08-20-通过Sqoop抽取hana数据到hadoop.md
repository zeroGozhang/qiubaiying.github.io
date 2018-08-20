---
layout:     post
title:      通过Sqoop抽取数据到hana
subtitle:   TDH对接Hana
date:       2018-08-20  
author:     zeroGoZhang
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Blog
---

# 前期准备
1、 进入客户端sqoop目录µ
   cd /mnt/disk1/softwares/TDH-Client/sqoop

2、 拷贝ngdbc.jar包到TDH-Client/sqoop/libs目录下

# Sqoop获取Hana数据命令
```
parameter:
  hana_ip       : hana数据库IP地址
  hana_port     : hana数据库端口
  hana_users    : hana数据库用户名
  hana_password : hana数据库密码
```
* 列出表格
./bin/sqoop list-tables --username $hana_users --password $hana_password --connect jdbc:sap://$hana_ip:hana_port/ --driver com.sap.db.jdbc.Driver

* 把数据从hana导入hdfs
./bin/sqoop import --username p520214 --password 1q3DCa@ws --connect jdbc:sap://$hana_ip:hana_port?currentschema=SYS  --driver com.sap.db.jdbc.Driver --query 'select USER_ID,USER_NAME,USER_MODE from SYS.USERS WHERE $CONDITIONS' --delete-target-dir  --target-dir=/user/sqoop/USERS --split-by USER_ID --num-mappers 1

# inceptor 建立外表验证抽取到hadoop数据
1、在inceptor里建立外表
create external table hana_users (
USER_ID string,
USER_NAME string,
USER_MODE string
)
row format delimited fields terminated by ','
location '/user/sqoop/USERS'

# 通过beeline验证查询

select * from hana_users;
