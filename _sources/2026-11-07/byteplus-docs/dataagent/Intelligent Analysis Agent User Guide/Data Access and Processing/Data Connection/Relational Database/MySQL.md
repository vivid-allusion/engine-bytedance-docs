---
title: "MySQL"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/MySQL"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to a MySQL database to create datasets.

<span id="_2-快速入门"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter Volcano Engine, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select the MySQL connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8943b05d0c8443da2fe0c4d75952b9f~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90a505ae3e614174af485bdbc0d47f69~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64a8d9f0e58643d3b4e1abd07d8f3c7e~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search for or select from the dropdown an existing connection, and choose the data source created earlier.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b498cfa6613a4d1f9542d716e6eacf2d~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter Volcano Engine, click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, you will stay on the pop\-up window for selecting a data connection for the dataset, and can proceed directly to the next step of dataset creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8943b05d0c8443da2fe0c4d75952b9f~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b498cfa6613a4d1f9542d716e6eacf2d~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-功能详解"></span>
# 3. Feature details


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, MYSQL.<br><br>The name can be modified. Please enter a standard name. Do not use special characters, and do not include spaces at the beginning or end. |
|Server |The IP address where the MySQL database is deployed |
|Port |The instance port of MYSQL. |
|Username |The username for accessing the MYSQL database. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
|Password |The password for accessing the MYSQL database. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
|Permission mode |Supports both read and write modes |
|vpcMode |Support is available in two ways: yes or no. If the database you want to connect to is Volcano Engine RDS or a Volcano Engine ECS self\-built MySQL service, and it is located in the same region as DataWind, you can use the VPC internal network connection mode to access the database via internal IP. |
|VPC ID |For instructions on obtaining the VPC ID, refer to the document "[获取数据库 VPC ID](https://www.volcengine.com/docs/4726/1418732#_2-2-%E8%8E%B7%E5%8F%96%E6%95%B0%E6%8D%AE%E5%BA%93%E5%B1%80%E5%9F%9F%E7%BD%91-ip-%E4%B8%8E-vpc-id)". |
