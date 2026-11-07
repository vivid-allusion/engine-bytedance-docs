---
title: "Hologres"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Hologres"
---

<span id="_1-产品概述"></span>
# **1. Product overview**

DataWind supports connecting to the Hologres database to obtain data, create datasets, and perform further analysis. Data connections support direct connection or extraction from Hologres data sources. (Direct connection requires product version V2.58.0 or above)

**Note**:

Before connecting to the data, collect the following information:


* A database has been created in Hologres.

* The public network address of the Hologres instance has been obtained.

* The instance port of Hologres has been obtained.

* The AccessKey ID and AccessKey Secret for accessing the Hologres project have been obtained.


<span id="_2-使用条件"></span>
# **2. Usage requirements**

The user must have the **Data Preparation \- Create Data Connection** permission for the current project.

<span id="_3-操作步骤"></span>
# **3. Operation steps**


1. Click **Data Preparation \> Data Connection**. 2. In the upper left corner of the data connection directory, click the **Create Data Connection** button.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. On the page, select Hologres.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef7f9bdc415147d281ad2add3c1e7ad6~tplv-goo7wpa0wc-image.image) </span>

3. Enter the required basic information.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3db8c42e1174447685aafabd6d32fa7c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>



4. Perform **Test Connection,**  and after the connection is successful, click **Save**.

    &nbsp;


<span id="_4-feature-description"></span>
# 4. Feature description

The following are the basic information fields for the data connection.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Hologres.<br><br>The name can be modified. Please enter a valid name. Do not use special characters, and do not include spaces at the beginning or end. |
|Server |The public network address of the Hologres instance.<br><br>You can go to the instance details page in the Hologres management console and obtain the public network address from the network information section. |
|Port |The instance port of Hologres.<br><br>You can go to the instance details page in the Hologres management console and obtain the port from the network information section. |
|Username |The AccessKey ID of the current Alibaba Cloud account.<br><br>You can obtain the AccessKey ID in the AccessKey management section of Alibaba Cloud. |
|Password |The AccessKey Secret of the current Alibaba Cloud account.<br><br>You can obtain the AccessKey Secret in the AccessKey management section of Alibaba Cloud. |
|Database |The name of the database created in Hologres. |
|Session parameters |The parameter name is required; the parameter value can be empty. For parameter acquisition, see the official Hologres documentation ["GUC Parameters"](https://help.aliyun.com/zh/hologres/developer-reference/guc-parameters?spm=a2c4g.11186623.help-menu-113622.d_5_3_1.3b29d106YzTF9W&scm=20140722.H_382261._.OR_help-T_cn-DAS-zh-V_1). |
