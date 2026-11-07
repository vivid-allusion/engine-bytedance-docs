---
title: "Teradata"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Teradata"
---

<span id="_1-概述"></span>
# 1. Overview

Intelligent Data Insight supports multiple data connection methods and currently supports more than 40 types of data sources. This article introduces the Teradata database connection. After connecting to the data, users can further create datasets and perform visual queries and analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

There are two ways to connect to a Teradata database: one is to create a new connection from the "Data connection" module, and the other is to create a new connection from the "Dataset" module. The following sections provide detailed instructions.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data preparation, find Data connection in the drop\-down list, and click Data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select the Teradata file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a87a24d5effd4d66872dd6b834b8b002~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4594968a69a4cdabc0fddb86c89ed7d~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click Create configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1 above. After uploading is complete, you will remain in the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-名词解释"></span>
# 3. Glossary


|Name |Description |
|---|---|
|Display name |The display name in the data source configuration list. A name consists of Chinese characters, digits, letters, underscores (_), or hyphens (\-). |
|Database address |The internal network address for deploying the Teradata database. At this time, the internal network address is the internal network address of the purchased ECS instance corresponding to the database. |
|Port |The internal network port corresponding to the internal network address for deploying the Teradata database. |
|Database |The database name customized during the deployment of the Teradata database. |
|Username and password |The username and password for logging in to the Teradata database. |
