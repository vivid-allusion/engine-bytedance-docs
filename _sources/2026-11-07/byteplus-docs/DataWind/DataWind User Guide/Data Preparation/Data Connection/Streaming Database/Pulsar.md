---
title: "Pulsar"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Pulsar"
---

<span id="_1-概述"></span>
# 1. Overview

You can connect to Pulsar to create datasets.

<span id="_2-快速入门"></span>
# 2. Quick start

This section describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create a data connection

(1) In Byteplus, enter a specific project, click Data Preparation, select Data Connection from the drop\-down list, and click it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Pulsar.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_886ed74eb27188dc262576392e3c4315.png) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2af7d3d249274e9285235ee24cdbdaa6~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through the existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create a dataset

(1) In Byteplus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click "New Configuration".

The subsequent steps are the same as **steps (2) and (3) of 2.1**. After the upload is complete, you will remain on the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-功能介绍"></span>
# 3. Feature overview

(1) Obtaining the SERVICE HTTP URL

This refers to the web service URL of Pulsar, which can be specified when deploying Pulsar. If the user does not modify it, the default is http://{IP address or domain name}:8080

(2) Obtaining the namespace

The user topic format is usually {persistent|non\-persistent}://tenant/namespace/topic, so the namespace is tenant/namespace.

For example, if the topic is persistent://my\-tenant/my\-namespace/my\-topic, then the namespace should be written as my\-tenant/my\-namespace.
