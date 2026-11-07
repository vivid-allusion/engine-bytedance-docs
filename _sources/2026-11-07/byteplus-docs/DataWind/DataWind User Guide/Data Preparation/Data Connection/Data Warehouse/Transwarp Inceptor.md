---
title: "Transwarp Inceptor"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Transwarp_Inceptor"
---

<span id="_1-概述"></span>
# 1. Overview

You can connect to the Transwarp Inceptor database to create datasets. Data connections support either direct connection or extraction from Transwarp Inceptor data sources. (Extraction is supported in product version V2.52.0 and above; direct connection is supported in product version V2.75.0 and above)

Before connecting to the database, please collect the following information:


* The database connection method;

* The IP address and port number of the server where the database is located;

* The username and password for the database;

* The database authentication method (username and password, Kerberos)


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Transwarp Inceptor.

(3) Fill in the required basic information, then you can choose either username and password or Kerberos as the authentication method. After filling in the information (or uploading the corresponding file), test the connection. Once the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53e4fb4ab95c47e99b202815d3fea55b~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search for or scroll through existing connections, and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in 2.1 above. After uploading is complete, you will remain in the popup window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="fc22bec1"></span>
# 3. Feature description

The basic information to note when configuring a data connection is described as follows.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Transwarp ArgoDB.<br><br>The name can be modified. Please enter a valid name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Supports two connection methods: IP/Port and JDBC connection string |
|Server |The public network address of Inceptor.<br><br>For information, refer to the official Inceptor documentation "[Connection method](https://www.transwarp.cn/doc/inceptor/9.3.3/connect-to-inceptor--connect-ways)" |
|Port |The instance port of Inceptor.<br><br>For information, refer to the official Inceptor documentation "[Connection method](https://www.transwarp.cn/doc/inceptor/9.3.3/connect-to-inceptor--connect-ways)" |
|Username |The username for database access. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
|Password |The password for database access. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
|JDBC connection string |JDBC connection string. For details on how to obtain it, refer to the [documentation](https://www.transwarp.cn/doc/inceptor/9.3.3/application-development--development-jdbc) |
|Authentication method |Supported authentication methods: username and password, and Kerberos. |
|Keytab file |The method for obtaining Kerberos authentication\-related files or information (Keytab file, krb5 file, principal, kuser) varies depending on the Inceptor version. It is recommended to contact Inceptor operations personnel or after\-sales support. |
|Krb5 file ||
|Principal ||
|kuser ||
|Permission mode |Supports two modes: read and write |
|nameNode |Permission\-related information. For details on how to obtain it, refer to the [documentation](https://www.transwarp.cn/doc/inceptor/9.3.3/manage-permission-and-resource--manage-dcl--sql-manage-hdfs-acl) |
|storageLocationPrefix ||
|hdfsPrincipal ||
|hdfsKeytab ||
|hdfsKrb5 ||
