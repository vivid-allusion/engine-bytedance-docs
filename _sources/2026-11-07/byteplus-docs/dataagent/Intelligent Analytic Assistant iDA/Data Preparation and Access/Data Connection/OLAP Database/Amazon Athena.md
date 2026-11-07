---
title: "Amazon Athena"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Amazon_Athena__"
---

<span id="f09efd38"></span>
# Overview

Support for accessing Amazon Athena to create datasets.

<span id="fafe46ab"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="d570ada4"></span>
## New from data connection

(1) Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select Amazon Athena on the page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6582bbd2c36d03630b29fa7499fd63e4.png) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61990c693dd9474fb9c3a91537b543f4~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or drop down an existing connection and select the newly created data source.

<span id="83993695"></span>
## Create a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting Data Connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<span id="235437e7"></span>
# Function introduction

<span id="1aff99a6"></span>
## AK and SK

The Access Key ID and Secret Access Key in the basic information of the data connection are Amazon's AK and SK information:


* You can log in to Amazon, and then click " [My Security Credentials ](https://console.amazonaws.cn/iam/home#/security_credentials)" under the avatar

* Click on the Amazon IAM certificate, find [ **Access Key ID** ] (choose one), and **generate the ID corresponding to SK** (generate AK generated when the self\-saved information)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b982d547c0ce4f92900d9af745767cfc~tplv-goo7wpa0wc-image.image) </span>

* Fill in [ **Access Key ID** ] on the Access Key ID (Access Key ID), and fill in [ **This ID corresponds to SK** ] on the Access Key (Secret Access Key)


<span id="e5744e54"></span>
## Region

Use the above account to click to enter the S3 to be docked, and get the Region information of the data source on the URL. For example, https://console.amazonaws.cn/s3/buckets?region=cn\-north\-1, its Region is cn\-north\-1.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eb7727395b64a6ea752ffd241827280~tplv-goo7wpa0wc-image.image) </span>

You can fill in the Region information into the data connection information

<span id="784607da"></span>
## S3 Temporary Directory (S3OutputLocation)


* Since Athena is a SQL engine, intermediate computation results need to be stored, so this space is required

* Users can define the location on their S3. Note that the current user account needs to have read and write permissions to this directory.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c3660b27964c976931030e5bcbdc8b0.png) </span>
