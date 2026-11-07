---
title: "LAS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/LAS"
---

<span id="_1-概述"></span>
# 1. Overview

The agent supports integration with the Lakehouse Analysis Service (LAS) to obtain data, create datasets, and perform further analysis. Data connections support either direct access or extraction from LAS data sources.

Before connecting to LAS, please collect the following information:


* The IP address and port number of the server where LAS is located;

* The username and password for LAS;


For information on how to obtain the server's IP address and port number, refer to [Connect BI](https://www.volcengine.com/docs/6492/101901).

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Log in to Volcano Engine, navigate to a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select LAS on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a3f5f2193f4d43aa6159de8f71c551~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4b831c19fe841e1bae48b63df0e7418~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information for the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Log in to Volcano Engine, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After the upload is completed, the pop\-up window for selecting a data connection for the dataset will remain open, allowing you to proceed directly to the next step of dataset creation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The LAS connection adds a new extraction link (requires product version V2.58.0 or above)</div>


In the LAS connection for data connections, a new extraction link has been added. The LAS extraction link no longer uses JDBC and instead directly unloads data to CDP HDFS. The following diagram illustrates the comparison between the old and new links:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0ab87ea059345309f3a6f72c3003125~tplv-goo7wpa0wc-image.image) </span>
