---
title: "MongoDB"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/MongoDB"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to MongoDB to create datasets.

Before connecting to the database, collect the following information:


* The IP address and port number of the server where the database is located;

* The name of the database;

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1从数据连接新建"></span>
## 2.1 Create from data connection

(1) Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select MongoDB.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47c63c2c95844c8babe1babb48da8882~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e8092cf0e8f49e89d9c9bc9c536c14d~tplv-goo7wpa0wc-image.image) </span>

(4) Once you have confirmed that the basic information for the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4405ef3ea4d140d3bf141a0e22f7acb4~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections, and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1eed57e950a438b93b3662ae3f291d5~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Go to BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, you will remain on the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1eed57e950a438b93b3662ae3f291d5~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature introduction


|Name |Description |
|---|---|
|Server |The address where the MongoDB BI Connector (Mongosqld service) is deployed. |
|Port |The port of the MongoDB service. |
|Database |The custom database name specified when deploying the MongoDB database. |
|Username and password |The username and password for logging in to the MongoDB database. |
