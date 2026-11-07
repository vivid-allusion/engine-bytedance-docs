---
title: "Amazon Redshift"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Amazon_Redshift"
---

<span id="_1-概述"></span>
# 1. Overview

Intelligent Data Insight supports connecting to Amazon Redshift databases to retrieve data, create datasets, and perform further analysis. Data connections support both direct connection and extraction from Amazon Redshift data sources. Extraction from Redshift data sources now additionally supports fields of type text and super. (Support for new fields requires product version V2.58.0 or above)

Before connecting to the data, please collect the following information:


* The IP address and port number of the server where the database is located;

* The name of the database;

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

The following describes two ways to create a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, go to a specific project, click Data Preparation, find Data Connection in the dropdown list, and select it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Amazon Redshift.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ad7251516bd4d7bd5be585d58b1aba6.png) </span>

(3) Fill in the required basic information, test the connection, and click Save after a successful connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db9d174e66b54ed7b62aa8cc60ba1100~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, you have completed the data connection.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search for or select from the dropdown an existing connection, and choose the data source created earlier.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, you will remain in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.
