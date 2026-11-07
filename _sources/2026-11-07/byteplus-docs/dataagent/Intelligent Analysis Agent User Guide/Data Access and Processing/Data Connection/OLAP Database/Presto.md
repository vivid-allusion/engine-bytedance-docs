---
title: "Presto"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Presto"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to the Presto database to create datasets.

Before connecting to the data, please collect the following information:


* The IP address and port number of the server where the database is located;

* The name of the database;

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Click New Data Connection in the upper left corner, and select Presto on the page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e25498249799c09a0f892432edcf582.png) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e70a888d5efb49089e7973c918d28040~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62f53375b66b47efa9f438f824612c7c~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create datasets: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections, and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a68f602a145f4ff09cfa797a587d7e8d~tplv-goo7wpa0wc-image.image" width="595px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) of 2.1**. After completing the upload, you will stay in the popup window for selecting a data connection for the dataset, and can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a68f602a145f4ff09cfa797a587d7e8d~tplv-goo7wpa0wc-image.image" width="595px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-鉴权方式"></span>
## 3.1 Authentication methods

There are two authentication methods: username and password, and Kerberos.

If Kerberos is selected as the authentication method


* The server, port, Keytab, and Krb5 are provided by the data source party.

* Principal


Here, Principal refers to a user\-level principal. It can generally be viewed through the Keytab file. The command is (using dlcdp.Keytab as an example):


* mac：`ktutil --Keytab=dlcdp.Keytab list`

* linux：`klist -kt dlcdp.Keytab`


Execution result on the mac platform:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6e66626280e497b9e02549af01cd9da~tplv-goo7wpa0wc-image.image) </span>

As shown above, the Principal for the dlcdp.Keytab file is dlcdp@CDH.COM.

If you choose to authenticate using username and password, simply enter them directly.

<span id="_3-2-连接方式"></span>
## 3.2 Connection methods

The following JDBC URL formats are supported:

`jdbc:presto://host:port jdbc:presto://host:port/catalog jdbc:presto://host:port/catalog/schema`

For example, use the following URL to connect to Presto running on `example.net` at the specified port, with catalog and schema:

`jdbc:presto://example.net:8080/hive/sales`

You can use the URL above to create a connection:

`String url = "jdbc:presto://example.net:8080/hive/sales"; Connection connection = DriverManager.getConnection(url, "test", **null**);`
