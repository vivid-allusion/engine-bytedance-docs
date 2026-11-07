---
title: "MaxCompute"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/MaxCompute"
---

<span id="_1-概述"></span>
# 1. Overview

Supports connecting to MaxCompute to create datasets.

Before connecting to the data source, confirm the following information:


* A MaxCompute project has been created.

* The Endpoint for the region where the target MaxCompute project resides has been obtained.

* The AccessKey ID and AccessKey Secret for accessing the MaxCompute project have been obtained.

* The Project Name of the target MaxCompute project has been obtained.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) On the page, select MaxCompute.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c36293f61983e92a1d3d5c2cfcbe0f8a.png) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e9d260e38874267a70c4be88f7e3049~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After uploading is complete, you will remain in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-功能介绍"></span>
# 3. Feature description

The following is the basic information for the data connection.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, MaxCompute. The name can be modified. Please enter a valid name. Do not use special characters, and do not include spaces at the beginning or end. |
|Endpoint |The Endpoint for the region where the target MaxCompute project resides. For Endpoint information for each region, see [Endpoint](https://www.alibabacloud.com/help/en/maxcompute/user-guide/endpoints?spm=a2c63.l28256.help-menu-27797.d_2_0_2.2a9065ffhr6GTO). |
|Access ID |AccessKey ID with access permissions to the target MaxCompute project. |
|Access Secret |The AccessKey Secret corresponding to the AccessKey ID. |
|Project Name |The name of the target MaxCompute project. This refers to the MaxCompute project name, not the workspace name. You can log in to the MaxCompute console, switch regions in the upper left corner, and view the corresponding MaxCompute project name on the Project Management tab. |
