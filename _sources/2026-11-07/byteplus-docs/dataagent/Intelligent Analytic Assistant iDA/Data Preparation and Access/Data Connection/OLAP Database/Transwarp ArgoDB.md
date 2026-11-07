---
title: "Transwarp ArgoDB"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/TranswarpArgoDB"
---

<span id="f1bbc2d6"></span>
# Overview

The data connection module supports access, and the Transwarp ArgoDB is used to create datasets. The data connection method supports direct connection or extraction.

Description:

Before you connect to the data, collect the following information:


* The IP address and port number of the server where the database is located

* The username and password of the database

* Database connection method (IP/Port, JDBC connection string)


<span id="2d0ed6f5"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="4fcdd9ca"></span>
## New from data connection


1. Enter the Volcano Engine, click to enter a specific project, click Data Preparation, find the data connection in the drop\-down list, and create a new data connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Select ArgoDB from the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be01fbed6a0d4d1a8943c88c54572c09~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00e4e0dafd52483a9f210479e080c5c3~tplv-goo7wpa0wc-image.image) </span>

4. After confirming that the basic information of the data connection is correct, the data connection is completed.

5. You can use this connection to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

6. Enter a keyword search and select the newly created data connection.


<span id="7628e85d"></span>
## Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. When selecting Data Connection, click the Other button.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


The following steps are consistent with steps (2) and (3) of 2.1 above. After completing the configuration, it will stop in the pop\-up box of Dataset Select Data Connection, and you can directly proceed to the next step of Dataset Creation.

<span id="20c41dee"></span>
# Function introduction

The basic information to be filled in during data connection is described as follows.


|Name |Describe |
|---|---|
|data connection name |The name of the new data connection used to distinguish connections to different databases in the system. For example, Transwarp ArgoDB.<br><br>The name can be modified. Please enter the standard name, do not use special characters, and do not include spaces before and after. |
|connection method |Support IP/Port and JDBC connection string two connection methods |
|server |The public network address of ArgoDB<br><br>For information, please refer to the official ArgoDB document " [Connection Overview ](https://www.transwarp.cn/doc/argodb/6.0/developer-guide--connect-to-argodb--overview)" |
|Port |Instance port of Starring ArgoDB<br><br>For information, please refer to the official ArgoDB document " [Connection Overview ](https://www.transwarp.cn/doc/argodb/6.0/developer-guide--connect-to-argodb--overview)" |
|user name |Database access username, if you don't know how to get it, it is recommended to contact the operation and maintenance staff of the corresponding engine to get it. |
|password |Database access password, if you don't know how to get it, it is recommended to contact the operation and maintenance staff of the corresponding engine to get it. |
|JDBC connection string |JDBC connection string, get the way can refer to ArgoDB official document ["based on JDBC development"](https://www.transwarp.cn/doc/argodb/6.0/developer-guide--application-development--development-jdbc) |
