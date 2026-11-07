---
title: "OpenGauss"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/OpenGauss"
---

<span id="_1-概述"></span>
# 1. Overview

The platform supports multiple data connection methods and currently supports more than 40 data sources. This document introduces how to connect to an OpenGauss database. After connecting to the data, users can further create datasets for visual query and analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

There are two ways to create an OpenGauss database connection: one is to create a new connection from the "Data Connection" module, and the other is to create a new connection from the "Dataset" module. The following sections provide detailed instructions.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select the OpenGauss file on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aa9a3c755ba4dc3beaa5970bb9f050a~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef77ced802334d08bcba7b2b2f8d403b~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93c0f250499d49ebbe999249e8154295~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9087416a7ae14b1c8dabc51f3ae75bc4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After the upload is complete, you will remain in the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aa9a3c755ba4dc3beaa5970bb9f050a~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9087416a7ae14b1c8dabc51f3ae75bc4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-名词解释"></span>
# 3. Terminology


|Name |Description |
|---|---|
|Display name |The display name in the data source configuration list. The name consists of Chinese characters, numbers, letters, underscores (_), or hyphens (\-). |
|Database address |The internal network address where the OpenGauss database is deployed. In this case, the internal network address refers to the internal network address of the ECS instance purchased for the database. |
|Port |The internal network port corresponding to the internal network address where the OpenGauss database is deployed. |
|Database |The database name defined when deploying the OpenGauss database. |
|Username and password |The username and password for logging in to the OpenGauss database. |
