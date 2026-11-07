---
title: "Transwarp ArgoDB"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Transwarp_ArgoDB"
---

<span id="54c2dd18"></span>
# 1. Overview

The data connection module supports connecting to Transwarp ArgoDB to create datasets. The data connection methods support direct connection or data extraction.

Note:

Before connecting to the data, collect the following information:


* The IP address and port number of the server where the database is located

* The username and password for the database

* The database connection method (IP/Port, JDBC connection string)


<span id="be233ea1"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="e359917f"></span>
## 2.1 Create a new data connection

(1) Enter BytePlus, navigate to a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) On the page, select Transwarp ArgoDB.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcdd26bdd98744b7b617c93f909bc6da~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d85281c25c684aef8ec548dabc3e643a~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection to create datasets: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Enter keywords to search and select the previously created data connection.

<span id="05cab0fb"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting the data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After completing the configuration, you will stay in the pop\-up window for selecting the data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="707624e6"></span>
# Feature overview

The basic information required when creating a data connection is described as follows.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Transwarp ArgoDB.<br><br>The name can be modified. Please enter a valid name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Supports two connection methods: IP/Port and JDBC connection string |
|Server |The public network address of Transwarp ArgoDB<br><br>For information, refer to the ArgoDB official documentation "[Connection overview](https://www.transwarp.cn/doc/argodb/6.0/developer-guide--connect-to-argodb--overview)" |
|Port |Instance port of Star Ring ArgoDB<br><br>For information, refer to the ArgoDB official documentation "[Connection overview](https://www.transwarp.cn/doc/argodb/6.0/developer-guide--connect-to-argodb--overview)" |
|Username |Database access username. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|Password |Database access password. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|JDBC connection string |JDBC connection string. For information on how to obtain it, refer to the ArgoDB official documentation ["JDBC-based development"](https://www.transwarp.cn/doc/argodb/6.0/developer-guide--application-development--development-jdbc) |
