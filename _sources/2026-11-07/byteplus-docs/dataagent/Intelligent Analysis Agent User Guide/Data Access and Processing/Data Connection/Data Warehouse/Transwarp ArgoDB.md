---
title: "Transwarp ArgoDB"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Transwarp_ArgoDB_"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to the Transwarp Inceptor database to create datasets. Data connections support direct connection or extraction from Transwarp Inceptor data sources.

Before connecting to the database, please collect the following information:


* The connection method of the database;

* The IP address and port number of the server where the database is located;

* The username and password of the database;

* The database authentication method (username and password, Kerberos)


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Transwarp Inceptor.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22166512c80b43b3830a8bb7dfc14409~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, then choose either username and password or Kerberos as the authentication method. After filling in the information (or uploading the corresponding file), test the connection. After a successful connection, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/093baffa9465464dad6a75706352a631~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) This connection can be used as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1 above. After uploading is complete, you will remain in the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="fc22bec1"></span>
# 3. Feature description

The basic information to note when connecting to data is described as follows.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Transwarp ArgoDB.<br><br>The name can be modified. Please enter a standard name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Supports two connection methods: IP/Port and JDBC connection string. |
|Server |The public network address of Transwarp Inceptor.<br><br>For information, refer to the official Inceptor documentation "[Connection methods](https://www.transwarp.cn/doc/inceptor/9.3.3/connect-to-inceptor--connect-ways)" |
|Port |The instance port of Transwarp Inceptor.<br><br>For information, refer to the official Inceptor documentation "[Connection methods](https://www.transwarp.cn/doc/inceptor/9.3.3/connect-to-inceptor--connect-ways)" |
|Username |Database access username. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|Password |Database access password. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|JDBC connection string |JDBC connection string. For information on how to obtain it, refer to the [documentation](https://www.transwarp.cn/doc/inceptor/9.3.3/application-development--development-jdbc) |
|Authentication method |The authentication method supports two options: username and password, and Kerberos. |
|Keytab file |Kerberos authentication\-related files or information (keytab file, krb5 file, principal, kuser) vary depending on the Transwarp version. It is recommended to contact Transwarp operations personnel or after\-sales support to obtain them. |
|Krb5 file ||
|Principal ||
|kuser ||
|Permission mode |Supports two modes: read and write. |
|nameNode |Permission\-related information. For information on how to obtain it, refer to the [documentation](https://www.transwarp.cn/doc/inceptor/9.3.3/manage-permission-and-resource--manage-dcl--sql-manage-hdfs-acl) |
|storageLocationPrefix ||
|hdfsPrincipal ||
|hdfsKeytab ||
|hdfsKrb5 ||
