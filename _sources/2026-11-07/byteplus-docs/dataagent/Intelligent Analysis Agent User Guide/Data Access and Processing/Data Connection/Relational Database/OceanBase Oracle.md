---
title: "OceanBase Oracle"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/OceanBase_Oracle"
---

<span id="_1-概述"></span>
# 1. Overview

The agent supports multiple data connection methods and currently supports more than 40 data sources. This document introduces OceanBase Oracle database connections. After connecting to the database, users can further create datasets for visual query and analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

There are two ways to connect to an OceanBase Oracle database: one is to create a new connection from the "Data Connection" module, and the other is to create a new connection from the "Dataset" module. The following sections provide a detailed introduction.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select the OceanBase Oracle option on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68907538f88e49bfa9b49e19a11c4f9e~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/645cd889c00541f0abccd1f522892318~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After the configuration is uploaded, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68907538f88e49bfa9b49e19a11c4f9e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-名词解释"></span>
# 3. Glossary


|Name |Description |
|---|---|
|Display name |The display name in the data source configuration list. The name consists of Chinese characters, numbers, letters, underscores (_), or hyphens (\-). |
|Database address |The internal network address where the OceanBase Oracle database is deployed. At this time, the internal network address is the internal address corresponding to the purchased database's ECS instance. |
|Port |The internal network port corresponding to the internal network address where the OceanBase Oracle database is deployed. |
|Database |The custom database name specified when deploying the OceanBase Oracle database. |
|Username and password |The username and password for logging in to the OceanBase Oracle database. |
