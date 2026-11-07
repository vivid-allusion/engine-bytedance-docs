---
title: "Hetu"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Hetu__"
---

<span id="7875b050"></span>
# Overview

The data connection module supports accessing Hetu to create datasets. Data connection supports direct connection or extraction of Hetu 3.3 data sources.

Description:

Before you connect to the data, please collect the following information:


* The IP address and port number of the server where the database is located

* The username and password of the database

* Database connection method (IP/Port, JDBC connection string)

* Database authentication method (username, password, Kerberos)


<span id="871b1cd2"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="c9534a1e"></span>
## New from data connection


1. Enter the Volcano Engine, click to enter a specific project, click Data Preparation, find the data connection in the drop\-down list, and create a new data connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Select Hetu on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f158f6ab36944afba0b140fcd764169a~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5697d52286e46b886f41785b37475f3~tplv-goo7wpa0wc-image.image) </span>

4. After confirming that the basic information of the data connection is correct, the data connection is completed.

5. You can use this connection to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

6. Enter a keyword search and select the newly created data connection.


<span id="5d1d446e"></span>
## Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. When selecting Data Connection, click the Other button.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


The following steps are consistent with steps (2) and (3) of 2.1 above. After completing the configuration, it will stop in the pop\-up box of Dataset Select Data Connection, and you can directly proceed to the next step of Dataset Creation.

<span id="bda8710b"></span>
# Function introduction

The basic information to be concerned about during the data connection process is described below.


|Name |Describe |
|---|---|
|data connection name |The name of the new data connection used to distinguish connections to different databases in the system. For example, Hetu.<br><br>The name can be modified. Please enter the standard name, do not use special characters, and do not include spaces before and after. |
|connection method |IP/Port and JDBC connection strings |
|server |Hetu's public network address<br><br>For information, please refer to the official Hetu documentation. |
|Port |Hetu instance port<br><br>For information, please refer to the official Hetu documentation. |
|Authentication method |Authentication method supports username password, and Kerberos two ways |
|user name |If you don't know how to get the username created in the database engine, it is recommended to contact the operation and maintenance staff of the corresponding engine to get it. |
|password |If you don't know how to obtain the password created in the database engine, it is recommended to contact the operation and maintenance staff of the corresponding engine to obtain it. |
|Keytab file |The files or information related to kerberos certification (keytab, krb5, pricinpal, jks) are usually in the hetu engine installation directory. It is recommended to contact the relevant operation and maintenance personnel or Hetu after\-sales service to obtain them. |
|Krb5 file ||
|Principal ||
|jks ||
|database |The name of the database created in Hetu. |
