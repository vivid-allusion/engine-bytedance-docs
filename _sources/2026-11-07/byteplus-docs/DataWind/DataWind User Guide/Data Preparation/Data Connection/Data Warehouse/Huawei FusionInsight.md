---
title: "Huawei FusionInsight"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Huawei_FusionInsight"
---

<span id="_1-产品概述"></span>
# 1. Product overview

Intelligent Data Insight supports multiple data connection methods and currently offers compatibility with more than 40 types of data sources. This document introduces the Huawei FusionInsight database connection. Users can connect to this data source in V2.56.1 and later versions to create datasets and perform visual queries and analysis.

**Prerequisites**

Before connecting to the database, collect the following information:


* Database connection method;

* The IP address and port number of the server where the database is hosted;

* Database username and password;


For information on how to obtain the server's IP address and port number, refer to [Connect BI](https://www.volcengine.com/docs/6492/101901).

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Go to BytePlus, click a specific project to enter it, click Data Preparation, then select Data Connection from the drop\-down list.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) On the page, select Huawei FusionInsight.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3c66fae1297467fa22fc9dcdc3edca9~tplv-goo7wpa0wc-image.image) </span>

(3) Enter the required basic information and test the connection. Once the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d978ac04b324597819ff041f7be92bd~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection is established.

(5) You can use this connection as a data source to create a dataset: Click Data Preparation \-\-\> Dataset, then click the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search for or scroll through the existing connections and select the data source you just created.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Go to BytePlus, click Data Preparation \-\-\> Dataset, then click the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1** above. After the upload is complete, you will remain in the pop\-up window to select a data connection for the dataset, where you can proceed directly to the next step of dataset creation.
