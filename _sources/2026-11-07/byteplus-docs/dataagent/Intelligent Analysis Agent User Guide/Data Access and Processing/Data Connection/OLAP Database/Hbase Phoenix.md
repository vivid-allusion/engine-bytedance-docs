---
title: "Hbase Phoenix"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Hbase_Phoenix"
---

<span id="_1-概述"></span>
# 1. Overview

Supports integrating HBase Phoenix to create datasets.

Before connecting to the database, collect the following information:


* The IP address and port number of the server where the database is located;

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select HBase Phoenix on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46782e8c02714303b78e9da753dbf02a~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b9889f0dca9468aa44b765d32e52685~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04e4e55f5714432db2ea550badb566b2~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection is established.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6473d0706e614012bb9e9a21a4e9ab93~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create datasets: click Data Preparation \-\-\> Dataset, and select the 'Create' button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections, and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bff56ee85b14b71bd8ad69ce6efb261~tplv-goo7wpa0wc-image.image" width="648px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the 'Create' button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After completing the upload, the popup window for selecting a data connection for the dataset will remain open, and you can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bff56ee85b14b71bd8ad69ce6efb261~tplv-goo7wpa0wc-image.image" width="648px" /></div>
