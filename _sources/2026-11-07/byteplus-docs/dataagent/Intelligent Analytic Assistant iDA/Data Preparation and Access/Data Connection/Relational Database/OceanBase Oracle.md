---
title: "OceanBase Oracle"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/OceanBase_Oracle__"
---

<span id="6c3039a9"></span>
# Overview

The agent supports a variety of data connection methods, and currently supports more than 40 data sources. This article will introduce you to OceanBase Oracle database connection. After connecting the data, users can further create datasets for visualized query and analysis.

<span id="fd03b159"></span>
# Quick Start

There are two ways to connect to the OceanBase Oracle database. One is to create a new one from the "Data Connection" module, and the other is to create a new one from the "Dataset" module. The following is a specific introduction for you.

<span id="63b9f99c"></span>
## New from data connection


1. Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

2. Select the OceanBase Oracle file on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95eb9e5fd5ef4906a3c41bef5c3635f8~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f731f3917e9a426ebc38919e73103fd4~tplv-goo7wpa0wc-image.image) </span>

4. After confirming that the basic information of the data connection is correct, the data connection is completed.

5. You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

6. Search for or drop down an existing connection and select the newly created data source.


<span id="f4aa330b"></span>
## Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>


(2) When selecting Data Connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with steps (2) and (3) of 2.1 above. After the upload is completed, it will stop in the pop\-up box of Dataset Select Data Connection, and you can directly proceed to the next step of Dataset Creation.

<span id="3e819404"></span>
# Term explanation


|Name |Describe |
|---|---|
|display name |The display name of the data source configuration list. A name consists of a combination of characters, numbers, letters, underscores (_) or dashes (\-). |
|database address |Deploy the intranet address of the OceanBase Oracle database. At this time, the intranet address is the intranet address corresponding to the ECS instance that purchased the database. |
|Port |Deploy the intranet port corresponding to the OceanBase Oracle database intranet address. |
|database |Customized database name when deploying OceanBase Oracle database. |
|Username and password |The username and password to log in to the OceanBase Oracle database. |
