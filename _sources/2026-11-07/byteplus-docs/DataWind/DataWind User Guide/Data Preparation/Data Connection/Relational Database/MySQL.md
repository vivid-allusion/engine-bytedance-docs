---
title: "MySQL"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/MySQL"
---

This article describes how to connect MySQL to create datasets.

<span id="a20aeec8"></span>
# Prerequisites

Before connecting to the data, contact the database administrator to collect the following information:


* The IP address and port number of the server where the database is located

* The username and password for the database

* The name of the database


<span id="f4674a52"></span>
# Preparation

SaaS users must add an entry to the allowlist in MySQL by entering the "DataWind public IP address for access" in the allowlist settings area and granting this IP address permission to access the MySQL service. The "DataWind public IP address for access" can be viewed at [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">SaaS users who select the vpcMode connection mode must also add the IP address "<a href="http://100.64.0.0/10">100.64.0.0/10</a>" to the allowlist configuration of the corresponding database (using MySQL as an example here), otherwise the connection will fail.</div>


<span id="_2-1-从数据连接新建"></span>
# Create from data connection


1. Log in to BytePlus, enter a specific project, go to Data Preparation, find Data Connection in the dropdown list, and select it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select MySQL on the page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef6e004fb88b45ae97ba6ba9617fd860~tplv-goo7wpa0wc-image.image) </span>


3. Fill in the required basic information, test the connection, and click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91bdac71f3c0484190c5caa1f18cced3~tplv-goo7wpa0wc-image.image) </span>

   
   |Name |Description |
   |---|---|
   |Data connection name |The name of the newly created data connection, used to distinguish connections to different databases in the system. You can customize it as needed.<br><br>Please enter a valid name. Do not use special characters, and do not include spaces at the beginning or end. |
   |Server |The IP address where the MySQL database is deployed. If you are using the MySQL service provided by BytePlus, refer to [Access Regions and BytePlus Intranet Connection](https://docs.byteplus.com/docs/DataWind/Access_Regions_and_BytePlus_Intranet_Connection) for instructions on how to obtain it. |
   |Port |The instance port of MySQL. If you are using the MySQL service provided by BytePlus, refer to [View instance connection information](https://www.volcengine.com/docs/6313/81188?lang=en) for instructions on how to obtain it. |
   |Username |The username for accessing the MySQL database. If you do not know how to obtain it, contact the operations personnel for the corresponding engine. |
   |Password |The password for accessing the MySQL database. If you do not know how to obtain it, contact the operations personnel for the corresponding engine. |
   |Permission mode |Both read and write modes are supported. |
   |vpcMode and VPC ID |Whether to use VPC mode (private network mode). Only the SaaS version needs to fill in these two parameters.<br><br>The usage scenarios are described as follows:<br><br><br>* **Enable VPC mode**: If your data source is a **BytePlus database or data warehouse product**, **it is recommended to use VPC mode**. You need to set vpcMode to **Yes** and provide the VPC ID. For instructions on how to obtain the VPC ID, see [Obtain the VPC ID](https://docs.byteplus.com/docs/DataWind/Access_Regions_and_BytePlus_Intranet_Connection#06269f9c).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use VPC mode for BytePlus products to ensure data security and avoid additional data transfer costs.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If users choose to connect using vpcMode, they need to add the IP address "<a href="http://100.64.0.0/10">100.64.0.0/10</a>" to the allowlist configuration of the corresponding database; otherwise, the connection will fail.   </div><br>   <br><br>* **Disable VPC mode**: If your data source has already enabled public network access, you do not need to set vpcMode; you can set it to No. |
   

4. After confirming that the basic information for the data connection is correct, the connection is complete.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72736db20c5f419e82ae79bdf8b5bb8f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-从数据集新建"></span>
# Create from dataset


1. Log in to BytePlus, go to Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting the data connection, click Create Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 in section 2.1 above. After the upload is complete, you will remain in the popup window for selecting the data connection for the dataset, and you can proceed directly to the next step of dataset creation.


<span id="36e50b79"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: Go to Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select the previously created data connection from the dropdown.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c59a6e09468402ca3dd8a7e64adc175~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
