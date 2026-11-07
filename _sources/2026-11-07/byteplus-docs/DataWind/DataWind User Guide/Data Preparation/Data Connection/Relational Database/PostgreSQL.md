---
title: "PostgreSQL"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/PostgreSQL"
---

This article describes how to integrate PostgreSQL to create datasets.

<span id="65ed5f9f"></span>
# Feature overview

Supports integrating PostgreSQL databases to create datasets. Data connections support direct connection or offline extraction of PostgreSQL data sources.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Direct connection requires product version V2.58.0 or above.</div>


<span id="65dd284d"></span>
# Prerequisites

Before connecting to the data, contact the database administrator to collect the following information:


* The IP address and port number of the server where the database is located

* The database username and password

* The database name

* Driver information (generally defaults to org.postgresql.Driver, no modification required)


<span id="884fd9f3"></span>
# Preparation

SaaS users need to add an allowlist entry in PostgreSQL by entering the "DataWind public IP for access" into the allowlist settings area, granting this IP address permission to access the PostgreSQL service. The "DataWind public IP for access" can be viewed at [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If SaaS users choose to connect using vpcMode, they must also add the IP address "<a href="http://100.64.0.0/10">100.64.0.0/10</a>" to the allowlist configuration of the corresponding database (using MySQL as an example here), otherwise the connection will fail.</div>


<span id="78196cfc"></span>
# Create from data connection


1. Go to BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select PostgreSQL on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c80f96f8c08425ba0bed5ee9049ca63~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after a successful connection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60315acc74c8430d97001b49e099f5e1~tplv-goo7wpa0wc-image.image) </span>


* The configuration instructions for SaaS version connection methods are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |Name of the new data connection, used to distinguish between different database connections in the system. For example, PostgreSQL_20250710163110.<br><br>The name can be modified. Please enter a valid name. Only combinations of Chinese characters, English letters, numbers, and underscores are allowed. Leading and trailing spaces are not permitted. |
   |Server |The public network address of PostgreSQL. For details, refer to the [PostgreSQL official documentation](https://www.postgresql.org/docs/). If you are using the PostgreSQL service provided by BytePlus, refer to [Obtain the database local area network IP](https://docs.byteplus.com/docs/DataWind/Access_Regions_and_BytePlus_Intranet_Connection#de8ed400) for details on how to obtain it. |
   |Port |The instance port of PostgreSQL. For details, refer to the [PostgreSQL official documentation](https://www.postgresql.org/docs/). If you are using the PostgreSQL service provided by BytePlus, refer to [View instance connection information](https://www.volcengine.com/docs/6438/81179?lang=en) for details on how to obtain it. |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   |Database |Name of the database created in PostgreSQL. |
   |Driver |Usually defaults to org.postgresql.Driver. No modification is required. |
   |vpcMode and VPC ID |Whether to use VPC mode (private network mode). Only the SaaS version requires these two parameters to be filled in.<br><br>The usage scenarios are as follows:<br><br><br>* **Enable VPC mode**: If your data source is a **BytePlus database or data warehouse product**, **it is recommended to use VPC mode**. Set vpcMode to **Yes** and enter the VPC ID. For details on how to obtain the VPC ID, see [Obtain the VPC ID](https://docs.byteplus.com/docs/DataWind/Access_Regions_and_BytePlus_Intranet_Connection#06269f9c).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use VPC mode for BytePlus products to ensure data security and avoid additional data transfer costs.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If users choose to connect using vpcMode, the IP address "<a href="http://100.64.0.0/10">100.64.0.0/10</a>" must be added to the allowlist configuration of the corresponding database; otherwise, the connection will fail.   </div><br>   <br><br>* **Disable VPC mode**: If your data source has public network access enabled, there is no need to set vpcMode. You can set it to No. |
   


<span id="f344d0e6"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 in **Create from data connection** above. After completing the configuration, you will remain in the pop\-up window for selecting a data connection for the dataset, where you can proceed directly to the next step of dataset creation.


<span id="1c6dbef9"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the dropdown the previously created data connection.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bb793b360184edcb1d46d73ca62edc9~tplv-goo7wpa0wc-image.image" width="610px" /></div>


&nbsp;
