---
title: "ClickHouse"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ClickHouse__"
---

<span id="0cc2025c"></span>
# Overview

Support ClickHouse as a data source to create datasets.

Before connecting to the database, please clarify the following information:


* The IP address and port number of the server where the database is located.

* The username and password of the database.

* The database method that needs to be connected.


<span id="6d6be205"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="785260f9"></span>
## New from data connection

(1) Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select ClickHouse file on the page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a94abf46b7b8f2286e49968ec142f5a4.png) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac5266db4e434b51a39404442de2ae27~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb49431d4bf647c7bd35dde6520bc694~tplv-goo7wpa0wc-image.image) </span>

Description: The protocol here defaults to the HTTP protocol.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or drop down an existing connection and select the newly created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e9c004c27d9487baca190ee4366c4f6~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="0ae350d7"></span>
## Create a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting Data Connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/061245f89a764ef38851e9e3cfbc1a4b~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b974c5bf2c4e2962d1a41627cf3eb568.png) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e9c004c27d9487baca190ee4366c4f6~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="511ebf04"></span>
# Function introduction


|Name |Describe |
|---|---|
|server |Deploy ClickHouse the public address of the database host, which is the host IP address. |
|Port |Deploy ClickHouse the port number corresponding to the database public network address. |
|Username and password |Login ClickHouse username and password for the database. |
|agreement |The default is the HTTP protocol. |
