---
title: "ClickHouse"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ClickHouse"
---

<span id="_1-概述"></span>
# 1. Overview

Supports using ClickHouse as a data source to create datasets.

Before connecting to the database, please confirm the following information:


* The IP address and port number of the server hosting the database.

* The username and password for the database.

* The required database connection method.


<span id="_2-快速入门"></span>
# 2. Quick start

The following introduces two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select the ClickHouse file on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53067b5578cf42d18414e4132abceda3~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4561bd08622a445798a57489257d281b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2df4e2094b23436db56112f77bbfbc1e~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58510146ffea49a9891bd674a671107f~tplv-goo7wpa0wc-image.image) </span>

Note: The default protocol here is Http.

(5) This connection can be used as a data source to create datasets: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee93914c405f4d459cf79e5d6b746fd4~tplv-goo7wpa0wc-image.image" width="633px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After the upload is completed, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b974c5bf2c4e2962d1a41627cf3eb568.png) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee93914c405f4d459cf79e5d6b746fd4~tplv-goo7wpa0wc-image.image" width="633px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature introduction


|Name |Description |
|---|---|
|Server |The public address of the host where the ClickHouse database is deployed. At this time, the public address is the host's IP address. |
|Port |The port number corresponding to the public address where the ClickHouse database is deployed. |
|Username and password |The username and password for logging in to the ClickHouse database. |
|Protocol |The default protocol is Http. |
