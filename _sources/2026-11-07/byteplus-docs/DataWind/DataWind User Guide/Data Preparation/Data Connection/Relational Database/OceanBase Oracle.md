---
title: "OceanBase Oracle"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/OceanBase_Oracle"
---

This article describes how to connect OceanBase Oracle to create datasets.

<span id="9b1fbc54"></span>
# Feature overview

Supports connecting OceanBase Oracle data sources to create datasets. Data connections support offline extraction of OceanBase Oracle data sources.

<span id="47c62c59"></span>
# Prerequisites

Before connecting to the data, contact the database administrator to collect the following information:


* The IP address and port number of the server where the database is located

* The username and password of the database


<span id="d7bb621a"></span>
# Preparation

SaaS users need to perform the add allowlist operation in OceanBase Oracle, enter the "DataWind public IP for access" in the allowlist settings area, and grant this IP address permission to access the OceanBase Oracle service. The "DataWind public IP for access" can be viewed at [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If SaaS users choose to connect using vpcMode, they also need to add the IP address "<a href="http://100.64.0.0/10">100.64.0.0/10</a>" to the allowlist configuration of the corresponding database (using MySQL as an example here), otherwise the connection will fail.</div>


<span id="9430a6fe"></span>
# Create from data connection


1. Go to BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select OceanBase Oracle on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/087d192618064deb89deabf94266d15f~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after the connection is successful.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16bed03d1bc14bcdb1d77b4be4f3c343~tplv-goo7wpa0wc-image.image) </span>


* The configuration instructions for connecting in the SaaS version are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish between different database connections in the system. For example, OceanBase_Oracle_20250723142047.<br><br>The name can be modified. Please enter a standardized name. Only combinations of Chinese characters, English letters, digits, and underscores are allowed. Spaces are not allowed at the beginning or end. |
   |Server |The public network address of OceanBase Oracle. For how to obtain it, refer to [OceanBase official documentation](https://www.oceanbase.com/docs/oceanbase-database-cn). |
   |Port |The instance port of OceanBase Oracle. For how to obtain it, refer to [OceanBase official documentation](https://www.oceanbase.com/docs/oceanbase-database-cn). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The username entered for the OceanBase data connection should be in the format "user@tenant_name#cluster_name".</div><br> |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   |Permission mode |Both read and write modes are supported.<br><br><br>* Read: Only retrieves data from the data source and cannot modify, add, or delete data.<br><br>* Write: Users need to write data to the data connection through visual modeling and must have data operation permissions. |
   |vpcMode |Select "Yes" if the user needs to connect via the BytePlus intranet; otherwise, select "No". |
   |VPC ID |When vpcMode is "Yes", this field must be filled in. For how to obtain it, refer to [Access Regions and BytePlus Intranet Connection](https://docs.byteplus.com/docs/DataWind/Access_Regions_and_BytePlus_Intranet_Connection).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the user selects the vpcMode connection mode, they need to add the IP address "<a href="http://100.64.0.0/10">100.64.0.0/10</a>" to the allowlist configuration of the corresponding database; otherwise, the connection will fail.</div><br> |
   

* The configuration instructions for connecting in the private deployment version are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish between different database connections in the system. For example, OceanBase_Oracle_20250723142840.<br><br>The name can be modified. Please enter a standardized name. Only combinations of Chinese characters, English letters, digits, and underscores are allowed. Spaces are not allowed at the beginning or end. |
   |Server |The public network address of OceanBase Oracle. For how to obtain it, refer to [OceanBase official documentation](https://www.oceanbase.com/docs/oceanbase-database-cn). |
   |Port |The instance port of OceanBase Oracle. For how to obtain it, refer to [OceanBase official documentation](https://www.oceanbase.com/docs/oceanbase-database-cn). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The username entered for the OceanBase data connection should be in the format "user@tenant_name#cluster_name".</div><br> |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   |Permission mode |Both read and write modes are supported.<br><br><br>* Read: Only data from the data source can be retrieved; data cannot be modified, added, or deleted.<br><br>* Write: The user must use visual modeling to write data to the data connection and must have permission to operate the data. |
   


<span id="c9e26ab8"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 of **Create from data connection** above. After completing the configuration, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.


<span id="110a6106"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the dropdown the previously created data connection.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e4864cf9a874e09b2a4bb51094c9487~tplv-goo7wpa0wc-image.image" width="450px" /></div>
