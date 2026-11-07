---
title: "Transwarp ArgoDB"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/TranswarpArgoDB__"
---

<span id="_1-概述"></span>
# 1. Overview

This feature supports connecting to the Transwarp Inceptor database to create datasets. You can establish a data connection either directly or by extracting data from Transwarp Inceptor data sources.

Before connecting to the database, please collect the following information:


* The method for connecting to the database;

* The IP address and port number of the server where the database is located;

* The username and password for the database;

* The database authentication method (username and password, Kerberos)


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter Volcano Engine, navigate to a specific project, click Data Preparation, locate Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select Transwarp Inceptor on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22166512c80b43b3830a8bb7dfc14409~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, then choose either username and password or Kerberos as the authentication method. After entering the information (or uploading the corresponding file), test the connection. Once the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff62207f8d414fe9886ff6fb6ec5867d~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create datasets: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or select from existing connections, and choose the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter Volcano Engine, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After uploading is complete, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="fc22bec1"></span>
# 3. Feature introduction

The basic information to note when establishing a data connection is described as follows.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases within the system. For example, Transwarp ArgoDB.<br><br>The name can be modified. Please enter a standardized name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Supports two connection methods: IP/Port and JDBC connection string |
|Server |The public network address of StarRings Inceptor.<br><br>For information, refer to the official Inceptor documentation "[Connection methods](https://www.transwarp.cn/doc/inceptor/9.3.3/connect-to-inceptor--connect-ways)" |
|Port |The instance port of StarRings Inceptor.<br><br>For information, refer to the official Inceptor documentation "[Connection methods](https://www.transwarp.cn/doc/inceptor/9.3.3/connect-to-inceptor--connect-ways)" |
|Username |The database access username. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|Password |The database access password. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|JDBC connection string |JDBC connection string. For information on how to obtain it, refer to the [documentation](https://www.transwarp.cn/doc/inceptor/9.3.3/application-development--development-jdbc) |
|Authentication method |The authentication method supports two options: username/password and Kerberos. |
|Keytab file |The method for obtaining Kerberos authentication\-related files or information (keytab file, krb5 file, principal, kuser) varies depending on the StarRings version. It is recommended to contact StarRings operations personnel or after\-sales support to obtain them. |
|Krb5 file ||
|Principal ||
|kuser ||
|Permission mode |Supports two modes: read and write |
|nameNode |Permission\-related information. For information on how to obtain it, refer to the [documentation](https://www.transwarp.cn/doc/inceptor/9.3.3/manage-permission-and-resource--manage-dcl--sql-manage-hdfs-acl) |
|storageLocationPrefix ||
|hdfsPrincipal ||
|hdfsKeytab ||
|hdfsKrb5 ||
