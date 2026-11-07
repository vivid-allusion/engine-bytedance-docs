---
title: "Doris"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Doris"
---

<span id="_1-概述"></span>
# 1. Overview

Intelligent Data Insights supports multiple data connection methods and currently supports more than 40 data sources. This document introduces how to connect to Doris databases. Currently, both direct connection and extraction modes are supported. After connecting to the data, users can further create datasets for visual queries and analysis.

Before connecting to the data, please gather the following information:


* The IP address and port number of the server where the database is located;

* The username and password for the database;


<span id="_2-快速入门"></span>
# 2. Quick start

The following introduces two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create a data connection

**Create a new data connection — Enter connection information — Create a new dataset — Select the connected data source file — Complete**

(1) Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select the Doris file.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d567e5e4229b407fad02bb7df9823457.png) </span>

(3) Fill in the required basic information and test the connection. After a successful connection, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76235948d6d1493fba86c19dfc465e74~tplv-goo7wpa0wc-image.image) </span>

(4) Once you have confirmed that the basic information for the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create a dataset

**Create a new dataset — Create a new configuration — Select the data source file — Enter connection information — Select the connected data source file — Complete**

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After uploading, you will stay in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.
