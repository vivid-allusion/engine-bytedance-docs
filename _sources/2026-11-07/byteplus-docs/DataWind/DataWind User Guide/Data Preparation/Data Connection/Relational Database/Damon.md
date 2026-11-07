---
title: "Damon"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Damon"
---

<span id="_1-概述"></span>
# 1. Overview

Intelligent Data Insight supports multiple data connection methods and currently supports more than 40 types of data sources. This document introduces Dameng database connections. After connecting to the data, users can further create datasets for visual queries and analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

There are two ways to create a Dameng database connection: one is to create a new connection from the "Data Connection" module, and the other is to create a new connection from the "Dataset" module. The following provides a detailed introduction.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select the Dameng file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e33aaf7939d464e912d02da0d3ccdf0~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8f181ef67d34da5a1560c97a4d0ce29~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) This connection can be used as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1 above. After the upload is complete, you will remain on the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-名词解释"></span>
# 3. Glossary


|Name |Description |
|---|---|
|Display name |The display name of the data source configuration list. The name can consist of Chinese characters, digits, letters, underscores (_), or hyphens (\-). |
|Database address |The internal network address of the deployed Dameng database. At this time, the internal network address refers to the internal network address of the ECS instance purchased for the database. |
|Port |The internal network port corresponding to the internal network address of the deployed Dameng database. |
|Database |The database name customized during the deployment of the Dameng database. |
|Username and password |The username and password for logging in to the Dameng database. |
