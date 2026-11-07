---
title: "VastBase"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/VastBase"
---

<span id="441e4f0e"></span>
# 1. Overview

Supports connecting to VastBase to create datasets. Data connections support direct connection or extraction from VastBase data sources.

Before connecting to the data, please collect the following information:


* The IP address and port number of the server where the database is located

* The username and password for the database

* The connection method for the database (IP/Port, JDBC connection string)


<span id="515e18df"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="8df03836"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click a specific project to enter it, click Data Preparation, find Data Connection in the drop\-down list, and create a new data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) On the page, select VastBase.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90698e61b99248c988b2eacd3b29cac6~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c682350554240429755a3aa821abd8f~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is established.

(5) You can use this connection to create a dataset: click Data Preparation, then Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Enter keywords to search and select the previously created data connection.

<span id="e764d628"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation, then Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1 above. After completing the configuration, you will stay in the pop\-up window for selecting the data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="a9bac7e4"></span>
# 3. Feature description

The basic information to pay attention to when connecting to data is described as follows.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, VastBase.<br><br>The name can be modified. Please enter a valid name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Supports two connection methods: IP/Port and JDBC connection string |
|Server |The public network address of VastBase<br><br>For more information, refer to the VastBase official documentation "[Connection Settings](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/7e7074bd293a4a56b32610562bf1169e#bbec8c33-4038-420a-a545-4b72dc08e91d)" |
|Port |The instance port of VastBase<br><br>For information, refer to the VastBase official documentation "[Connection settings](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/7e7074bd293a4a56b32610562bf1169e#bbec8c33-4038-420a-a545-4b72dc08e91d)" |
|Database |Name of the database created in VastBase. |
|Username |Database access username. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
|Password |Database access password. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
|JDBC connection string |JDBC connection string. For details on how to obtain it, refer to the [documentation](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/1dd7384ace1f431c911173c2561847c4) |
