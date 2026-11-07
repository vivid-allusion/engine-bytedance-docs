---
title: "VastBase"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/VastBase__"
---

<span id="fef6ce44"></span>
# Overview

Support access to VastBase to create datasets. Data connections support direct connection or extraction of VastBase data sources.

Before you connect to the data, please collect the following information:


* The IP address and port number of the server where the database is located

* The username and password of the database

* Database connection method (IP/Port, JDBC connection string)


<span id="3db75b21"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="b581b032"></span>
## New from data connection


1. Enter the Volcano Engine, click to enter a specific project, click Data Preparation, find the data connection in the drop\-down list, and create a new data connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Select VastBase on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4efab661f8442d782bbd4ff82614623~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/282b34b50093455da8e483b7682f0a17~tplv-goo7wpa0wc-image.image) </span>

4. After confirming that the basic information of the data connection is correct, the data connection is completed.

5. You can use this connection to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

6. Enter a keyword search and select the newly created data connection.


<span id="cb0c9be1"></span>
## Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. When selecting Data Connection, click the Other button.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


The following steps are consistent with steps (2) and (3) of 2.1 above. After completing the configuration, it will stop in the pop\-up box of Dataset Select Data Connection, and you can directly proceed to the next step of Dataset Creation.

<span id="78d39179"></span>
# Function introduction

The basic information to be concerned about when connecting data is described below.


|Name |Describe |
|---|---|
|data connection name |The name of the new data connection used to distinguish connections to different databases in the system. For example, VastBase.<br><br>The name can be modified. Please enter the standard name, do not use special characters, and do not include spaces before and after. |
|connection method |Support IP/Port and JDBC connection string two connection methods |
|server |VastBase's public network address<br><br>For information, please refer to the official VastBase document "[Connection Settings](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/7e7074bd293a4a56b32610562bf1169e#bbec8c33-4038-420a-a545-4b72dc08e91d)" |
|Port |VastBase instance port<br><br>For information, please refer to the official VastBase document "[Connection Settings](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/7e7074bd293a4a56b32610562bf1169e#bbec8c33-4038-420a-a545-4b72dc08e91d)" |
|database |The name of the database created in VastBase. |
|user name |Database access username, if you don't know how to get it, it is recommended to contact the operation and maintenance staff of the corresponding engine to get it. |
|password |If you don't know how to obtain the database access password, it is recommended to contact the operation and maintenance personnel of the corresponding engine to obtain it. |
|JDBC connection string |JDBC connection string, get the way to refer to the [document](https://docs.vastdata.com.cn/zh_CN/VastbaseG100/V3.0.8/1/1dd7384ace1f431c911173c2561847c4) |
