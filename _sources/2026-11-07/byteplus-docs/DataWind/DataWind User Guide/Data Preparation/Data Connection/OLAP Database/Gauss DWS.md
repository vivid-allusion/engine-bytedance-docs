---
title: "Gauss DWS"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Gauss_DWS"
---

This article describes how to connect to Gauss DWS to create a dataset.

<span id="dfa3d283"></span>
# Prerequisites

Before connecting to the data, contact the database administrator to collect the following information:


* The IP address and port number of the server where the database is hosted

* The username and password for the database


<span id="f4f2f826"></span>
# Preparation

In Gauss DWS, perform the add allowlist operation. Enter the "DataWind public IP address" in the allowlist settings area to grant this IP address permission to access the Gauss DWS service. The "DataWind public IP address" can be viewed at [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview).

<span id="a3150fc3"></span>
# Create from data connection


1. Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select Gauss DWS on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8a183fb3b304668b240484862549531~tplv-goo7wpa0wc-image.image) </span>

3. Enter the required basic information and test the connection. After the connection is successful, click Save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35f71dcb0e2a4afebc58cea73603fd68~tplv-goo7wpa0wc-image.image) </span>


* The configuration instructions for connecting to the SaaS version are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Gauss_DWS_20250703151659.<br><br>The name can be modified. Please enter a valid name. Only Chinese characters, English letters, numbers, and underscores are allowed, and spaces are not allowed at the beginning or end. |
   |Connection method |IP/Port<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bf44b7dc62e48b899d1691012e3c389~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The public network address of Gauss DWS. For details, refer to [Gauss DWS](https://support.huaweicloud.com/wtsnew-dws/index.html) |
   |Port |The instance port of Gauss DWS. For details on how to obtain it, see [Gauss DWS](https://support.huaweicloud.com/wtsnew-dws/index.html). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the administrator of the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the administrator of the corresponding engine. |
   |Database |The database name created in Gauss DWS. |
   

* The configuration instructions for connecting to the on\-premises version are as follows:

   
   |Parameter |Configuration description |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish between different database connections in the system. For example, Gauss_DWS_20250703151659.<br><br>The name can be modified. Enter a valid name. Only Chinese characters, English letters, digits, and underscores are allowed. Leading and trailing spaces are not permitted. |
   |Connection method |* IP/Port: Suitable for general scenarios.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5b5c9ff6407419780cdadae90be4919~tplv-goo7wpa0wc-image.image) </span><br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cd70642005d4efba2a8a7ff93015f99~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The public network address of Gauss DWS. For details on how to obtain it, see [Gauss DWS](https://support.huaweicloud.com/wtsnew-dws/index.html). |
   |Port |The instance port of Gauss DWS. For details on how to obtain it, see [Gauss DWS](https://support.huaweicloud.com/wtsnew-dws/index.html). |
   |JDBC connection string |JDBC connection string. For details on how to obtain it, see [Gauss DWS](https://support.huaweicloud.com/wtsnew-dws/index.html). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the administrator of the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the administrator of the corresponding engine. |
   |Database |The database name created in Gauss DWS. |
   


<span id="0109b647"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6753b4124394ae8aec91b6d92e22524~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click Create new configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 in **Create from data connection** above. After completing the configuration, the pop\-up window for selecting a data connection for the dataset will remain open, allowing you to proceed directly to the next step of dataset creation.


<span id="c8a6acdd"></span>
# Next steps: Create a dataset


1. Use the previously created data connection to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select the previously created data connection from the drop\-down list.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/129707d473674d809f6fb6041b70039c~tplv-goo7wpa0wc-image.image" width="610px" /></div>
