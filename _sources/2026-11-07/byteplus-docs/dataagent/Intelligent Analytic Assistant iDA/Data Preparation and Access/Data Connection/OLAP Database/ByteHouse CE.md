---
title: "ByteHouse CE"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ByteHouseCE__"
---

<span id="7cdb7a2c"></span>
# 1. Overview

Support access to ByteHouse CE database to create datasets.

**Prerequisites** : [ByteHouse CE Enterprise Edition ](https://www.byteplus.com/en/product/bytehouse)is required;

**Preliminary preparations** :

(1) Apply for a [BytePlus account ](https://console.byteplus.com/auth/signup); enterprise users need to go to the Volcano Engine official website to apply for a Volcano Engine main account and complete the account authentication. Please refer to the steps ["Volcano Engine Account Registration and Authentication Operation Guide"](https://www.volcengine.com/docs/6261/64925)

(2) For real\-name authentication, please refer to [real-name authentication](https://www.volcengine.com/docs/6261/64935)

(3) Activate [ByteHouse CE Enterprise Edition](https://www.byteplus.com/en/product/bytehouse)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fb87ed9f2a84789acf76f0477d87e82~tplv-goo7wpa0wc-image.image) </span>

The steps to create a database and data table in ByteHouse CE can refer to the following operations:

(1) Create a new cluster.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35277a6588d341e5af9e6519817c2d2b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/741ee6ef18a14156b16ef16bfc86590c~tplv-goo7wpa0wc-image.image) </span>

(2) Select the previously created cluster and click Create Database.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bed21de268842ab918d54e680b04dde~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9bc5b5089794a1eb6a0a1a4b846ea62~tplv-goo7wpa0wc-image.image) </span>

(3) Just import the data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a92e1fe08dc641bb974b4dfa3170ccba~tplv-goo7wpa0wc-image.image) </span>

Click OK and submit the information.

<span id="9b5e5cef"></span>
# 2. Quick start

Here are two ways to create a data connection.

<span id="034c6af6"></span>
## 2.1 Create a new data connection

(1) Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select ByteHouse CE on the page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_233d47bf2b221ecf5bb79c2cb4a116d0.png) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3056f3f0f9c44aca2e14b5cab703ad5~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b05d57c358a481c914cce2c9c25f1d2~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or drop down an existing connection and select the newly created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47d4849d01034c59b5bcb51d0e2a86c4~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="32d9f2b4"></span>
## 2.2 Creating a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting Data Connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47d4849d01034c59b5bcb51d0e2a86c4~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="2c33e4fd"></span>
# 3. Frequently Asked Questions

<span id="55b8f88f"></span>
## 3.1 Real\-name authentication

Without real\-name authentication, you will not be able to access the Volcano Engine ByteHouse Enterprise Edition console normally, and you need to complete [real-name authentication ](https://www.volcengine.com/docs/6261/64935).

<span id="7b7ad661"></span>
## 3.2 **Obtain database LAN IP and VPC ID**

Description: If you need to use the LAN IP connection through VPC mode, and the connected data source region is North China 2, you need to pay attention to obtaining the database LAN IP and VPC ID. We provide you with two ways to obtain it.

The first way: query by pinging the LAN domain name.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/830b77b909e743349305e2c3e179b4ba~tplv-goo7wpa0wc-image.image" width="1178px" /></div>


The second way: through the VPC network interface card management view. The following is an example of MySQL for step\-by\-step instructions (the same is true for databases built in other products, such as PostgreSQL, load balance, ECS, etc.).

(1) Enter the instance list interface of MySQL and click to view "instance information".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d9805478ecf4b10901b1d78d4ab406d~tplv-goo7wpa0wc-image.image) </span>

(2) Copy the "ID" in the "Basic Information" shown in the figure below;

(3) Fill in the copied "ID" into the A "VPC ID" column of the data connection interface (as shown below);

(4) Enter the network interface card interface, in the private network Internet Protocol Address column, you can check the LAN IP;

(5) Copy the LAN IP;

(6) Fill in this IP address into the B "Server" column in the data connection interface.
