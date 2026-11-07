---
title: "VastBase"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/VastBase"
---

<span id="441e4f0e"></span>
# 1. Overview

Supports connecting to VastBase to create datasets. Data connections support direct connection or extraction from VastBase data sources.

Please collect the following information before establishing a data connection:


* The IP address and port number of the server where the database is located

* The username and password of the database

* The connection method for the database (IP/Port, JDBC connection string)


<span id="515e18df"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="8df03836"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and create a new data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) On the page, select VastBase.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/906a53ba546742b3b19e5729318520fc~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d80b8ed51d7b4ad3ab26235d7989100e~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Enter keywords to search and select the previously created data connection.

<span id="e764d628"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in 2.1 above. After completing the configuration, you will remain on the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="a9bac7e4"></span>
# 3. Feature description

The basic information to pay attention to when establishing a data connection is described as follows.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, VastBase.<br><br>The name can be modified. Please enter a standard name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Supports two connection methods: IP/Port and JDBC connection string |
|Server |The public network address of VastBase<br><br>For more information, refer to the VastBase official documentation "[Connection Settings](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/7e7074bd293a4a56b32610562bf1169e#bbec8c33-4038-420a-a545-4b72dc08e91d)" |
|Port |The instance port of VastBase<br><br>For information, refer to the VastBase official documentation "[Connection settings](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/7e7074bd293a4a56b32610562bf1169e#bbec8c33-4038-420a-a545-4b72dc08e91d)" |
|Database |The name of the database created in VastBase. |
|Username |If you do not know how to obtain the username, it is recommended to contact the operations personnel for the corresponding engine. |
|Password |If you do not know how to obtain the password, it is recommended to contact the operations personnel for the corresponding engine. |
|JDBC connection string |JDBC connection string. For information on how to obtain it, refer to the [documentation](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/1dd7384ace1f431c911173c2561847c4) |
