---
title: "Presto"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Presto__"
---

<span id="8fc27517"></span>
# Overview

Support accessing the Presto database to create datasets.

Before you connect to the data, collect the following information:


* The IP address and port number of the server where the database is located.

* The name of the database.

* The username and password for the database.


<span id="8609b50e"></span>
# Quick Start

<span id="0c6392a8"></span>
## New from data connection


1. Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

2. Click New Data Connection in the upper left corner and select Presto on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e25498249799c09a0f892432edcf582.png) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78efbadd4f6c4653ad50a0353e5a2849~tplv-goo7wpa0wc-image.image) </span>


4. After confirming that the basic information of the data connection is correct, the data connection is completed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e5f00e316044c6fba451ea204b11f8a~tplv-goo7wpa0wc-image.image) </span>


5. You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

6. Search for or drop down an existing connection and select the newly created data source.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7620d0e9b273489b9313522a05de6c98~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="a0795bf9"></span>
## Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7620d0e9b273489b9313522a05de6c98~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="94eeabff"></span>
# Function introduction

<span id="a3c46d0d"></span>
## Authentication method

There are two authentication methods: username and password, Kerberos

If the authentication method is selected Kerberos


* Server, port, Keytab, Krb5 are provided by the data source.

* Principal


The Principal here refers to the user level, which can generally be viewed through the Keytab file. The command is (take dlcdp. Keytab as an example):


* mac：`ktutil --Keytab=dlcdp.Keytab list`

* linux：`klist -kt dlcdp.Keytab`


The execution result of the Mac platform:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6e66626280e497b9e02549af01cd9da~tplv-goo7wpa0wc-image.image) </span>

As can be seen from the figure above, the Principal corresponding to the file dlcdp. Keytab is dlcdp@CDH.COM.

If you choose the form of username + password for verification, just enter it directly.

<span id="6f138a5b"></span>
## Connection method

The following JDBC URL formats are supported:

`jdbc:presto://host:port jdbc:presto://host:port/catalog jdbc:presto://host:port/catalog/schema`

For example, use the following URL to connect to Presto running on a `example.net`port with a directory and schema:

`jdbc:presto://example.net:8080/hive/sales`

You can use the URL above to create a connection.

`String url = "jdbc:presto://example.net:8080/hive/sales"; Connection connection = DriverManager.getConnection(url, "test", **null**);`
