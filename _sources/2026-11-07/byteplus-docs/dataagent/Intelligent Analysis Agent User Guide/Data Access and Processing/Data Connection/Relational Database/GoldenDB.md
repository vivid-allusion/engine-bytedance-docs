---
title: "GoldenDB"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/GoldenDB"
---

<span id="_1-概述"></span>
# 1. Overview

The intelligent agent supports multiple data connection methods and currently supports more than 40 types of data sources. This document introduces GoldenDB database connections. After connecting to the database, users can further create datasets for visual queries and analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

There are two ways to create a GoldenDB database connection: one is to create a new connection from the "Data Connection" module, and the other is to create a new connection from the "Dataset" module. The following sections provide detailed instructions.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Log in to BytePlus, navigate to a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select the GoldenDB file on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd8f02e69c414f25b023d07c80af9d9c~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2c68a2aebef42ebbeb9eed408b2b330~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or scroll through existing connections, and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Log in to BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After completing the upload, you will remain in the pop\-up window for selecting a data connection for the dataset, and can proceed directly to the next step of dataset creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd8f02e69c414f25b023d07c80af9d9c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-名词解释"></span>
# 3. Terminology


|Name |Description |
|---|---|
|Display name |The display name in the data source configuration list. The name consists of Chinese characters, numbers, letters, underscores (_), or hyphens (\-). |
|Database address |The internal network address where the GoldenDB database is deployed. The internal network address corresponds to the internal address of the purchased ECS instance. |
|Port |The internal network port corresponding to the internal network address where the GoldenDB database is deployed. |
|Database |The custom database name specified when deploying the GoldenDB database. |
|Username and password |The username and password for logging in to the GoldenDB database. |
