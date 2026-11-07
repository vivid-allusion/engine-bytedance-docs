---
title: "Oracle"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Oracle__"
---

<span id="36b6a5f2"></span>
# Overview

Support access to Oracle to create datasets. Data connection supports direct connection or extraction of Oracle data sources. (Direct connection requires privatization of product version V2.75.0 and above)

Before you connect to the data, collect the following information:


* The IP address and port number of the server where the database is located.

* The name of the database.

* The username and password for the database.


<span id="69668f8c"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="2b43d683"></span>
## New from data connection


1. Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

2. Select Oracle on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01ca68246acbc5a15aedf78ce7aa0127.png) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a636c6d556445df9ded94888e920eae~tplv-goo7wpa0wc-image.image) </span>

4. After confirming that the basic information of the data connection is correct, the data connection is completed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9163c4ff62194ef899f9ae87b7cb4643~tplv-goo7wpa0wc-image.image) </span>

5. You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

6. Search for or drop down an existing connection and select the newly created data source.


<span id="cc3fe488"></span>
## Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.
