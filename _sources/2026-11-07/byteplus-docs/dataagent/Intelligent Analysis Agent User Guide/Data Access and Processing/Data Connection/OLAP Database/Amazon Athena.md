---
title: "Amazon Athena"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Amazon_Athena"
---

<span id="_1-概述"></span>
# 1. Overview

Supports integration with Amazon Athena to create datasets.

<span id="_2-快速入门"></span>
# 2 Quick start

The following introduces two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Amazon Athena.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66de18f3eabf4bea9a1caec95d93a911~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04207e554a0c46deb5157bc6d93a791c~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-ak-和-sk"></span>
## 3.1 AK and SK

The Access Key ID and Secret Access Key in the basic information of the data connection are Amazon's AK and SK information:


* You can log in to Amazon, then click "[My Security Credentials](https://console.amazonaws.cn/iam/home#/security_credentials)" under your profile.

* Click Amazon IAM credentials, find [**Access Key ID**] (choose any), and **the corresponding SK generated when this ID was created** (information saved when generating the AK).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b982d547c0ce4f92900d9af745767cfc~tplv-goo7wpa0wc-image.image) </span>


* Enter [**Access Key ID**] in Access Key ID, and [**SK corresponding to this ID**] in Secret Access Key.


<span id="_3-2-区域（region）"></span>
## 3.2 Region

Use the above account to access the S3 to be connected. The Region information of the data source can be obtained from the URL, for example, https://console.amazonaws.cn/s3/buckets?region=cn\-north\-1, where the Region is cn\-north\-

You can enter this Region information in the data connection information.

<span id="_3-3-s3-暂存目录（s3outputlocation）"></span>
## 3.3 S3 staging directory (S3OutputLocation)


* Since Athena is a SQL engine, intermediate calculation results need to be stored, so this space is required.

* The user can define a location on their own S3. Caution: The account currently in use must have read and write permissions for that directory.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c3660b27964c976931030e5bcbdc8b0.png) </span>
