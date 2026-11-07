---
title: "Impala"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Impala__"
---

<span id="e607ccae"></span>
# Overview

Support access to Impala to create datasets.

<span id="3fbb00e6"></span>
# Quick Start

Here are two ways to create a data connection.

<span id="5c766689"></span>
## New from data connection

(1) Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select Impala on the page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_923b5363fe34ab26a812a09eefeddbac.png) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62e91b1f44ca456289ac4094af7138d6~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f28960ff4ac44d8f930bf0c024151f94~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a31054eb794ae19da0bfb24aaddd2e~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or drop down an existing connection and select the newly created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5393d6c1e99a468d89dcb299f792a091~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="f2e5c83d"></span>
## Create a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting Data Connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/861343d49496452488a8af1194d14000~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with **steps (2) and (3) of 2.1** above. After the upload is completed, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5393d6c1e99a468d89dcb299f792a091~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="612e7466"></span>
# Function introduction

<span id="d049a874"></span>
## Authentication method

There are two authentication methods, you can choose to log in to verify by way of username + password according to your needs, or you can choose Kerberos for verification.

If you choose Kerberos, you need to upload the Keytab file and Krb5 file and fill in Principal.


* If the authentication method is selected Kerberos.

* Server, port, Keytab, Krb5 are provided by the data source.

* Principal.


The Principal here refers to the user level, which can generally be viewed through the Keytab file. The command is (take dlcdp. Keytab as an example):


* mac：`ktutil --Keytab=dlcdp.Keytab list`

* linux：`klist -kt dlcdp.Keytab`


The execution result of the Mac platform:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cb7117463f5428984e1a2854b088548~tplv-goo7wpa0wc-image.image) </span>

As can be seen from the figure above, the Principal corresponding to the file dlcdp. Keytab is dlcdp@CDH.COM.
