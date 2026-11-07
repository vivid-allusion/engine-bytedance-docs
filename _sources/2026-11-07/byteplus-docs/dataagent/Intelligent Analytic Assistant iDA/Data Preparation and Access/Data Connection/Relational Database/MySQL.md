---
title: "MySQL"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/MySQL__"
---

<span id="1f700d37"></span>
# Overview

Support access to MySQL database to create datasets.

<span id="28b52a67"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="c6a8a969"></span>
## New from data connection


1. Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

2. Select the MySQL file on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e683944934dd4ddeb16d8fbe0fba95fd~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecb1113648c2486b9b970fed85681c32~tplv-goo7wpa0wc-image.image) </span>

4. After confirming that the basic information of the data connection is correct, the data connection is completed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb964f81205e4229a73a9c857302aef0~tplv-goo7wpa0wc-image.image) </span>

5. You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

6. Search for or drop down an existing connection and select the newly created data source.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b380cdb96faf423da7be4c638c9ba914~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="4894ca83"></span>
## Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b22873443e644ef28e1b1ae176f90c0e~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b380cdb96faf423da7be4c638c9ba914~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="f0057a3c"></span>
# Detailed function explanation


|Name |Describe |
|---|---|
|data connection name |The name of the new data connection used to distinguish connections to different databases in the system. For example, MySQL.<br><br>The name can be modified. Please enter the standard name, do not use special characters, and do not include spaces before and after. |
|server |The IP address for deploying the MySQL database |
|Port |MYSQL instance port. |
|user name |MYSQL database access username, if you don't know how to get it, it is recommended to contact the operation and maintenance staff of the corresponding engine to get it. |
|password |If you don't know how to get the MYSQL database access password, it is recommended to contact the operation and maintenance staff of the corresponding engine to get it. |
|permission mode |Supports both reading and writing |
|vpcMode |Support yes or no. If the database you want to connect to is Volcano Cloud RDS, or Volcano Cloud ECS self\-built MySQL service, and belongs to the same region as DataWind, you can use the VPC intranet connection mode to access the database through the intranet IP |
|VPC ID |To get the VPC ID, please refer to the document " [Get Database VPC ID ](https://www.volcengine.com/docs/4726/1418732#%E8%8E%B7%E5%8F%96vpc-id)" |
