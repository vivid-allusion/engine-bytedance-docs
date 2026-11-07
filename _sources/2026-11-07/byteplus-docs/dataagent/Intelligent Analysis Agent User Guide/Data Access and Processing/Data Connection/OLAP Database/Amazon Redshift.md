---
title: "Amazon Redshift"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Amazon_Redshift"
---

<span id="_1-概述"></span>
# 1. Overview

The agent supports connecting to the Amazon Redshift database to retrieve data, enabling the creation of datasets for further analysis. Data connections support either direct access or extraction from Amazon Redshift data sources. Support for fields of the text and super types has been added in Redshift data source extraction.

Before connecting to the data, collect the following information:


* The IP address and port number of the server hosting the database;

* The name of the database;

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, navigate to a specific project, click Data Preparation, locate Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Amazon Redshift.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32fc7148abe44870a396e631b771690e~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ac409780ec2406c901fea30a624e7f9~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a815a9b74bba46d68145a261fceed1ac~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/076ca62be91849a08825f9c578434dfa~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or scroll through existing connections, and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67fb279709b84126b273457869c4b3f8~tplv-goo7wpa0wc-image.image" width="586px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3244389cc7145bd8b1663a2ae326811~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67fb279709b84126b273457869c4b3f8~tplv-goo7wpa0wc-image.image" width="586px" /></div>
