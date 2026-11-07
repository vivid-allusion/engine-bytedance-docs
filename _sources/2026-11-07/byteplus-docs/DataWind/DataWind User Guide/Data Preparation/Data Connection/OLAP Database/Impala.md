---
title: "Impala"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Impala"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to Impala to create datasets.

<span id="_2-快速入门"></span>
# 2. Quick start

This section describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Go to BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select Impala.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_923b5363fe34ab26a812a09eefeddbac.png) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a40f0ba4a679403cbe0757c39741f295~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87c2dec9ac4c423db433251db28bba61~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e086ea2d3310478cae52d984c42d8973~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2082d1102684eaea42687cdb7fc5865~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Go to BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, you will remain in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36372883d0ad4c358d868e5456b45562~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature description

<span id="鉴权方式"></span>
## Authentication methods

There are two authentication methods available. You can choose to log in using a username and password, or use Kerberos for authentication, depending on your requirements.

To use Kerberos, you need to upload the Keytab file and the Krb5 file, and enter the Principal.


* If the authentication method is Kerberos

* The server, port, Keytab, and Krb5 should be provided by the data source provider.

* Principal


Here, Principal refers to the user\-level principal, which can generally be viewed through the Keytab file. The command is (using dlcdp.Keytab as an example):


* mac：`ktutil --Keytab=dlcdp.Keytab list`

* linux：`klist -kt dlcdp.Keytab`


Execution result on mac platform:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cb7117463f5428984e1a2854b088548~tplv-goo7wpa0wc-image.image) </span>

As shown above, the Principal corresponding to the dlcdp.Keytab file is dlcdp@CDH.COM.
