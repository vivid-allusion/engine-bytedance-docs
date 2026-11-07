---
title: "Doris"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Doris"
---

<span id="_1-概述"></span>
# 1. Overview

The agent supports multiple data connection methods and currently supports more than 40 types of data sources. This article introduces Doris database connections. Currently, both direct connection and extraction methods are supported. After connecting to the data, users can further create datasets for visualized queries and analysis.

Before establishing a data connection, please collect the following information:


* The IP address and port number of the server where the database is located;

* The username and password of the database;


<span id="_2-快速入门"></span>
# 2. Quick start

The following introduces two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

**Create a data connection — Enter connection information — Create a dataset — Select the connected data source file — Complete**

(1) Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select the Doris file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73a064bf3f29496e9d1db89c6c10419a~tplv-goo7wpa0wc-image.image) </span>

(3) Enter the required basic information and test the connection. Once the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a099f0cf2cc4292b3e0854a5b9423e0~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f857040a3214b6f8e8cc491d0d747f7~tplv-goo7wpa0wc-image.image) </span>

(5) This connection can be used as a data source to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2b1faac68f74a01a93a657b78bdb63c~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

**Create a dataset — Create a configuration — Select the data source file — Enter connection information — Select the connected data source file — Complete**

(1) Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner, and create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After uploading is complete, you will remain in the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2b1faac68f74a01a93a657b78bdb63c~tplv-goo7wpa0wc-image.image" width="610px" /></div>
