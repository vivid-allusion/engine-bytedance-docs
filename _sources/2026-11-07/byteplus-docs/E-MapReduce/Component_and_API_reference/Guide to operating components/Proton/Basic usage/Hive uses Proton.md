---
title: "Hive uses Proton"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_uses_Proton"
---

<span id="_1-概述说明"></span>
## 1 Overview

Volcano Engine E\-MapReduce (EMR) has supported the Proton SDK since EMR\-3.1.1 (corresponding to Hadoop 3.x and Hive 3.x) and EMR\-2.2.0 (corresponding to Hadoop 2.x and Hive 2.x). This document describes how to use the Proton SDK to read and write TOS data in Hive on Volcano EMR or in Hive on a self\-built Hadoop cluster.

<span id="_2-火山-emr"></span>
## 2 Volcano EMR

<span id="_2-1-认证配置"></span>
### 2.1 Authentication configuration

For details on Volcano Engine EMR authentication configuration, see: [Hadoop 使用 Proton - 认证配置](https://docs.byteplus.com/docs/E-MapReduce/109384#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE).

<span id="_3-自建-hadoop-集群"></span>
## 3 Self\-built Hadoop cluster

<span id="_3-1-配置-hadoop-环境"></span>
### 3.1 Configure the Hadoop environment

Download the corresponding Proton package according to the Proton version. For details, see: [Hadoop 使用 Proton - 下载依赖](https://docs.byteplus.com/docs/E-MapReduce/109384#_2-1-hadoop3-%E7%B3%BB%E5%88%97), and configure the Hadoop environment.

<span id="_3-2-配置-hive"></span>
### 3.2 Configure Hive

There are two methods to configure Hive:

<span id="_3-2-1-修改-hive-site-xml"></span>
#### 3.2.1 Modify hive\-site.xml

Add the following configuration:

```xml
<property>
   <name>hive.blobstore.optimizations.enabled</name>
   <value>true</value>
</property>

<property>
   <name>hive.blobstore.supported.schemes</name>
   <value>s3,s3a,s3n,tos</value>
</property>

<property>
   <name>hive.blobstore.use.blobstore.as.scratchdir</name>
   <value>false</value>
</property>
```


<span id="_3-2-2-在-sql-中设置"></span>
#### 3.2.2 Set in SQL

```sql
set hive.blobstore.optimizations.enabled=true;
set hive.blobstore.supported.schemes=s3,s3a,s3n,tos;
set hive.blobstore.use.blobstore.as.scratchdir=false;
```


<span id="_4-使用-tos"></span>
## 4 Use TOS

When creating a Hive table, set the value of the location field to the TOS address so that you can analyze TOS data. For example:

```SQL
CREATE EXTERNAL TABLE `palmplay_log_pv_csv`(  
  `meta_id` STRING,   
  `brand` STRING,   
  `channel` STRING,   
  `countrycode` STRING )  
PARTITIONED BY (dt String)  
LOCATION  
  'tos://您的tos bucket name/palmplay_log_pv_csv';
```
