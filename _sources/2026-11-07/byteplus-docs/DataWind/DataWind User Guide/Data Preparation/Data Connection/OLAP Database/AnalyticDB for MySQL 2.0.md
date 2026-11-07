---
title: "AnalyticDB for MySQL 2.0"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/AnalyticDB_for_MySQL_2_0"
---

<span id="_1-概述"></span>
# 1. Overview

You can connect to AnalyticDB for MySQL 2.0 to create datasets.

Before connecting to the database, collect the following information:


* The IP address and port number of the server where the database is located;

* The name of the database;

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

The following introduces two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create a dataset from a data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select AnalyticDB for MySQL 2.0.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c66ecdf21d004e959bff824177bac39d~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b51bb193e9654d3d81e9ce5346432c77~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create a data connection from a dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner, and create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, you will remain in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.
