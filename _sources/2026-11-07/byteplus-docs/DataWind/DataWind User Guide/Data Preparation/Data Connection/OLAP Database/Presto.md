---
title: "Presto"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Presto"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to Presto databases to create datasets.

Before connecting to the data, collect the following information:


* The IP address and port number of the server where the database is located.

* The name of the database.

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) In BytePlus, select a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Click New Data Connection in the upper left corner, and select Presto on the page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e25498249799c09a0f892432edcf582.png) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a97f8d06ada34949a4d3b75cc32ab803~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/871ae2a7fe6e487e899fee3da6d9ce3f~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe9a273c1640413e8652525a735fb6e9~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) In BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After completing the upload, you will remain in the pop\-up window for selecting a data connection for the dataset, and can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe9a273c1640413e8652525a735fb6e9~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-功能介绍"></span>
# 3. Features

<span id="_3-1-鉴权方式"></span>
## 3.1 Authentication methods

There are two authentication methods: username and password, or Kerberos.

If Kerberos is selected as the authentication method,


* the server, port, Keytab, and Krb5 are provided by the data source provider.

* Principal


Here, Principal refers to the user\-level Principal, which can generally be viewed through the Keytab file. The command is (using dlcdp.Keytab as an example):


* mac：`ktutil --Keytab=dlcdp.Keytab list`

* linux：`klist -kt dlcdp.Keytab`


Execution result on mac platform:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6e66626280e497b9e02549af01cd9da~tplv-goo7wpa0wc-image.image) </span>

As shown above, the Principal corresponding to the dlcdp.Keytab file is dlcdp@CDH.COM.

To authenticate using username and password, enter them directly.

<span id="_3-2-连接方式"></span>
## 3.2 Connection methods

The following JDBC URL formats are supported:

`jdbc:presto://host:port jdbc:presto://host:port/catalog jdbc:presto://host:port/catalog/schema`

For example, use the following URL to connect to Presto running on `example.net` with a catalog and schema:

`jdbc:presto://example.net:8080/hive/sales`

You can use the above URL to create a connection:

`String url = "jdbc:presto://example.net:8080/hive/sales"; Connection connection = DriverManager.getConnection(url, "test", **null**);`
