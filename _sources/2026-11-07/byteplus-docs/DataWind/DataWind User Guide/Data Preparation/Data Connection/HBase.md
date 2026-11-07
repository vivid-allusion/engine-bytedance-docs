---
title: "HBase"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/HBase"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to HBase to create datasets.

Before connecting to the database, collect the following information:


* The IP address and port number of the server where the database is located.

* The database's rootdir and zk.znode.parent.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Go to BytePlus, select a specific project to enter it, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) On the page, select HBase.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6abead8c80e4338aca86665715f4f25~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8caa20d735ac4fbd9dc702ae763a1b6f~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection setup is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or select from the drop\-down list of existing connections, and choose the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Go to BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After uploading is complete, the pop\-up window to select a data connection for the dataset will remain open, allowing you to proceed directly to the next step of dataset creation.
