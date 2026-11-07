---
title: "AnalyticDB for MySQL 3.0"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/AnalyticDB_for_MySQL_3_0"
---

<span id="_1-概述"></span>
# 1. Overview

Integration with AnalyticDB for MySQL 3.0 is supported for creating datasets.

Before connecting to the database, collect the following information:


* The IP address and port number of the server where the database is located.

* The database username and password.


<span id="_2-快速入门"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create a dataset from a data connection

(1) Log in to BytePlus, enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select AnalyticDB for MySQL 3.0.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/091615150e8e45b88321f5c41568355a~tplv-goo7wpa0wc-image.image) </span>

(3) Enter the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd6145533ad14967abb790e507389613~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create a dataset from a new data connection

(1) Log in to BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After completing the previous steps, you will remain on the pop\-up window to select a data connection for the dataset, where you can proceed directly to the next step of dataset creation.
