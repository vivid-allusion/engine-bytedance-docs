---
title: "StarRocks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/StarRocks"
---

<span id="_1-概述"></span>
# 1. Overview

Supports integration with StarRocks to create datasets.

> The StarRocks data source currently supports extraction mode; direct connection mode will be available soon.

> VPC intranet connection is currently supported only in the North China region.


Before connecting to the data, please collect the following information:


* The IP address and port number of the server where the database is located

* The username and password of the database


<span id="_2-快速入门"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create via data connection

(1) In BytePlus, access a specific project, go to Data Preparation, find Data Connection in the dropdown list, and click it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select StarRocks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e0b74455c3b4c2bb8c288ae90d53d3c~tplv-goo7wpa0wc-image.image) </span>

(3) Enter the required basic information, test the connection, and after a successful test, click Save.

```Plain Text
  **VPC intranet connection is currently supported only in the North China region.*
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f509fdd753745af86d99e26ea1ba4c2~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection setup is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a4bc0d52660466c93142e99dc37a8e3~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: go to Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or select from the dropdown of existing connections, and choose the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2dad55d9077548febbfaede21537d953~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create via dataset

(1) In BytePlus, go to Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After completing the upload, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.
