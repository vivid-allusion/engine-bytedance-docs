---
title: "Hologres"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Hologres__"
---

<span id="997f22a1"></span>
# **Product Overview**

The agent supports accessing the Hologres database to obtain data, and then creates a dataset for further analysis. Data connections support direct connection or extraction of Hologres data sources.

**Description** :

Before you connect to the data, collect the following information:


* The database has been created in Hologres.

* The public network address of the Hologres instance has been obtained.

* The instance port for Hologres has been obtained.

* The AccessKey ID and AccessKey Secret for accessing the Hologres project have been obtained.


<span id="6dcb87a2"></span>
# **Conditions of use**

The user needs to have **the Data Preparation \- New Data Connection permission for the current project** .

<span id="68faa788"></span>
# **Operation steps**


1. Click **Data Preparation \> Data Connection** . 2. In the upper left corner of the data connection directory, click the **New Data Connection** button and select **OLAP\-Hologres** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/160b3ad0ef5d443392ac4b75d43f7108~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d77106f66a8454b80178edff7bae844~tplv-goo7wpa0wc-image.image) </span>

3. Make a **test connection, and** click **Save** after prompting that the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54a8bd3fa14c480d923f9e3a289d1bab~tplv-goo7wpa0wc-image.image) </span>


<span id="d379ea99"></span>
# Function introduction

Here is the basic information about the data connection.


|Name |Describe |
|---|---|
|data connection name |The name of the new data connection used to distinguish connections to different databases in the system. For example, Hologres.<br><br>The name can be modified. Please enter the standard name, do not use special characters, and do not include spaces before and after. |
|server |The public network address of the Hologres instance.<br><br>You can go to the instance details page of the Hologres Management Console and get the public network address from the Network Information area. |
|Port |The instance port for Hologres.<br><br>You can go to the instance details page of the Hologres Management Console and get the port from the Network Information area. |
|user name |The AccessKey ID of the current Alibaba Cloud account.<br><br>You can obtain the AccessKey ID in the AccessKey management of Alibaba Cloud. |
|password |AccessKey Secret for the current Alibaba Cloud account.<br><br>You can obtain the AccessKey Secret in the AccessKey management of Alibaba Cloud. |
|database |The name of the database created in Hologres. |
|session parameters |Parameter name is required, parameter value can be empty. Parameter acquisition See Hologres' official document ["GUC Parameters"](https://help.aliyun.com/zh/hologres/developer-reference/guc-parameters?spm=a2c4g.11186623.help-menu-113622.d_5_3_1.3b29d106YzTF9W&scm=20140722.H_382261._.OR_help-T_cn-DAS-zh-V_1) |
