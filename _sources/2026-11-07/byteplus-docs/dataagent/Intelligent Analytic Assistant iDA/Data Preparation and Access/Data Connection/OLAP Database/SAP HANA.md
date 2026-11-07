---
title: "SAP HANA"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/SAP_HANA__"
---

<span id="c4650495"></span>
# 1. Overview

Support access to SAP HANA to create datasets.

Before you connect to the data, collect the following information:


* The IP address and port number of the server where the database is located.

* The username and password for the database.


<span id="51d1f8a3"></span>
# 2. Quick start

Here are two ways to create a data connection.

<span id="4b35fae8"></span>
## 2.1 Create a new data connection

(1) Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select SAP HANA on the page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_318f880d64d018e07861931d7ea59489.png) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f18f11f92f646ecbc199c634b2eb2fb~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or drop down an existing connection and select the newly created data source.

<span id="988df581"></span>
## 2.2 Creating a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting Data Connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea96f8456c3e4008953014a269bac69e~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.
