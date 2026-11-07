---
title: "GreenPlum"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/GreenPlum"
---

<span id="_1-概述"></span>
# 1. Overview

Supports integration with GreenPlum to create datasets.

Before connecting to the database, collect the following information:


* The IP address and port number of the server where the database is located.

* The name of the database.

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, go to a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select GreenPlum.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_88d79e2c123b0ab7f3ca76434005c4d1.png) </span>

(3) Enter the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/025300d30f8846b490a139e87165263e~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection setup is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e1b9421e53d485e801aca8044a49110~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or browse existing connections and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c2ebd31493c4912918055fe58889bb4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in **2.1** above. After the upload is complete, you will remain on the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2126f7794e0245b0a7efaf39d6d81b55~tplv-goo7wpa0wc-image.image" width="610px" /></div>
