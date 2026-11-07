---
title: "ByteHouse CE"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ByteHouse_CE"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to the ByteHouse CE database to create datasets.

**Prerequisites**: Requires [ByteHouse CE Enterprise Edition](https://www.byteplus.com/en/product/bytehouse);

**Preparatory work**:

(1) Apply for a [BytePlus account](https://console.byteplus.com/auth/signup). Enterprise users need to visit the BytePlus official website to apply for a primary BytePlus account and complete account verification. For steps, refer to ["BytePlus Account Registration and Verification Guide"](https://www.volcengine.com/docs/6261/64925)

(2) Complete real\-name authentication. For steps, refer to Real\-name authentication.

(3) Activate [ByteHouse CE Enterprise Edition](https://www.byteplus.com/en/product/bytehouse).

The steps for creating databases and tables in ByteHouse CE can be referenced as follows:

(1) Create a new cluster.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a4a51c5fa0f4b058433b47ad1fff3cd~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9aba52dc5460490db709394db3b8d517~tplv-goo7wpa0wc-image.image) </span>

(2) Select the previously created cluster and click to create a database.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/804d1e07a025451cb6b853d40c6d7d03~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6d23963bd3c4af6bb3538ff2118d1ab~tplv-goo7wpa0wc-image.image) </span>

(3) Import data as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5bc02747bdf459294b3b98fe1ebb683~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

The following introduces two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, navigate to a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select ByteHouse CE on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dbf20c4e1844bfe8ed776e60bd82d77~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after a successful connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/997b2574219548f193ac6ef74de77c4d~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/621d6230b6214562820c149ce7b25eec~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After completing the upload, you will remain in the popup window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-常见问题"></span>
# 3. Frequently asked questions

<span id="c03689f1"></span>
## 3.1 Real\-name authentication

If real\-name authentication is not completed, you will not be able to access the BytePlus ByteHouse Enterprise Edition console normally. You need to complete real\-name authentication.

<span id="f82cf149"></span>
## 3.2 **Obtain the database LAN IP and VPC ID**

Note: Obtaining the database LAN IP and VPC ID is only necessary when connecting via LAN IP in VPC mode and the data source region is North China 2. Two methods are provided for this purpose.

Method 1: Query by pinging the LAN domain name.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/830b77b909e743349305e2c3e179b4ba~tplv-goo7wpa0wc-image.image" width="1178px" /></div>


Method 2: View through network interface management under the VPC. The following steps use MySQL as an example (the process is similar for other products, such as PostgreSQL, load balancing, ECS, and databases deployed in these environments).

(1) Go to the MySQL instance list page and click to view "Instance information".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3cd4e9dd83341e1953467dbe0498b2d~tplv-goo7wpa0wc-image.image) </span>

(2) Copy the "ID" in the "Basic information" section as shown below.

(3) Enter the copied "ID" in the A "VPC ID" field on the data connection page (as shown below).

(4) Go to the network interface page, and you can view the LAN IP in the private IP address field.

(5) Copy the LAN IP.

(6) Enter this IP in the B "Server" field on the data connection page.

&nbsp;
