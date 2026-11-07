---
title: "Amazon Athena"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Amazon_Athena"
---

<span id="_1-概述"></span>
# 1. Overview

Starting from version V2.44.0, Amazon Athena integration is supported for creating datasets.

<span id="_2-快速入门"></span>
# 2 Quick start

The following describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Amazon Athena.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6582bbd2c36d03630b29fa7499fd63e4.png) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7bec9d3451d40abba5e1b2f9718069d~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection setup is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Go to BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After completing these steps, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-ak-和-sk"></span>
## 3.1 AK and SK

The Access Key ID and Secret Access Key in the basic information of the data connection are Amazon's AK and SK information:


* You can log in to Amazon, then click "[My Security Credentials](https://console.amazonaws.cn/iam/home#/security_credentials)" under your profile.

* Click Amazon IAM credentials, find [**Access Key ID**] (choose any), and **the corresponding SK generated when creating this ID** (the information saved when generating the AK).

* Enter [**Access Key ID**] in Access Key ID, and [**the SK corresponding to this ID**] in Secret Access Key.


<span id="_3-2-区域（region）"></span>
## 3.2 Region

Use the above account to access the S3 to be connected. The Region information of the data source can be obtained from the URL, for example, https://console.amazonaws.cn/s3/buckets?region=cn\-north\-1, where the Region is cn\-north\-1.

You can enter this Region information in the data connection information.

<span id="_3-3-s3-暂存目录（s3outputlocation）"></span>
## 3.3 S3 temporary directory (S3OutputLocation)


* Since Athena is a SQL engine, intermediate calculation results need to be stored, so this space is required.

* Users can define a location on their own S3. Caution: The current account in use must have read and write permissions for that directory.
