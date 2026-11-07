---
title: "KingbaseES"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/KingbaseES"
---

<span id="04fc92b4"></span>
# 1. Overview

Intelligent Data Insight supports connecting KingbaseES to create datasets.


* Supports V2.91.0 and later versions;

* Supported database version: v9 full market edition – MySQL\-compatible mode;

* Supports creating datasets with custom SQL. For guidance, see [Custom SQL](https://docs.byteplus.com/docs/DataWind/110006).


Before connecting to the database, collect the following information:


* The IP address and port number of the server where the database is located;

* The database username and password;

* The name of the database.


<span id="54318a15"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="97de4739"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, go to a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select KingbaseES.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61d56b5447c640c39b7deff3191d59c2~tplv-goo7wpa0wc-image.image) </span>

(3) Enter the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27e21708597d4f289f6241d00ae07841~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection to create datasets: click Data Preparation → Dataset, then click the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Enter keywords to search and select the previously created data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d7321af4dee4b0b80790c225ff5f165~tplv-goo7wpa0wc-image.image" width="450px" /></div>


<span id="a5a14744"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation → Dataset, then click the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After completing the configuration, you will remain in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.
