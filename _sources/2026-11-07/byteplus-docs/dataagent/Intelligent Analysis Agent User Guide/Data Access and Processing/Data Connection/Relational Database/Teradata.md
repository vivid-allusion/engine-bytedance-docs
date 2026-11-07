---
title: "Teradata"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Teradata"
---

<span id="_1-概述"></span>
# 1. Overview

The agent supports multiple data connection methods and currently supports more than 40 data sources. This document introduces how to connect to a Teradata database. After connecting to the database, users can further create datasets and perform visual queries and analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

There are two ways to connect to a Teradata database: one is to create a new connection from the "Data Connection" module, and the other is to create a new connection from the "Dataset" module. The following sections provide detailed instructions.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select the Teradata file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e64ba517c824c969c8da9ac2bf6e276~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff0becc85d0d4303b488a2d28abf67f7~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After the upload is complete, the process will remain at the pop\-up window for selecting a data connection for the dataset, allowing you to proceed directly to the next step of dataset creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f4586cb05da437983e7e0191efd3f56~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-名词解释"></span>
# 3. Terminology


|Name |Description |
|---|---|
|Display name |The display name in the data source configuration list. The name consists of a combination of Chinese characters, numbers, letters, underscores (_), or hyphens (\-). |
|Database address |The internal network address where the Teradata database is deployed. At this time, the internal network address refers to the internal address of the purchased database's ECS instance. |
|Port |The internal network port corresponding to the internal network address where the Teradata database is deployed. |
|Database |The custom database name specified when deploying the Teradata database. |
|Username and password |Username and password for logging in to the Teradata database. |
