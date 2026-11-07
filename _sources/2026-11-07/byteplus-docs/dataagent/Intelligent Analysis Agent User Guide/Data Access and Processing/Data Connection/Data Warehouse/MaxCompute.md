---
title: "MaxCompute"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/MaxCompute"
---

<span id="_1-概述"></span>
# 1. Overview

Supports integration with MaxCompute to create datasets.

Before connecting data, confirm the following information:


* A MaxCompute project has been created.

* The Endpoint for the region where the target MaxCompute project is located has been obtained.

* The AccessKey ID and AccessKey Secret with access to the MaxCompute project have been obtained.

* The Project Name of the target MaxCompute project has been obtained.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select MaxCompute on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d99af3ef23f47dd84ee5e1d85f87437~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47ea7f595c3849a59975b1f162c2c615~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create datasets: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After the upload is complete, the pop\-up window to select a data connection for the dataset will remain open, and you can proceed directly to the next step of dataset creation.

<span id="_3-功能介绍"></span>
# 3. Feature description

The following is the basic information of the data connection.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, MaxCompute. The name can be modified. Please enter a standardized name. Do not use special characters, and do not include spaces at the beginning or end. |
|Server |The Endpoint for the region where the target MaxCompute project is located. For Endpoint information in each region, see [Endpoint](https://help.aliyun.com/zh/maxcompute/user-guide/endpoints#concept-m2j-h1y-5db). |
|Access ID |The AccessKey ID with permission to access the target MaxCompute project. |
|Access Secret |The AccessKey Secret corresponding to the AccessKey ID. |
|Project Name |The name of the target MaxCompute project. This refers to the MaxCompute project name, not the workspace name. You can log in to the MaxCompute console, switch the region in the upper left corner, and then view the corresponding MaxCompute project name on the project management tab. |
