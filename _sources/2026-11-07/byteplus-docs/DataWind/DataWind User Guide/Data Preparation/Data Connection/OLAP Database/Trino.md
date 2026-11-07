---
title: "Trino"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Trino"
---

This article introduces how to connect Trino to create datasets.

<span id="af4bb01a"></span>
# Prerequisites

Before connecting to the data, contact the database administrator to collect the following information:


* The IP address and port number of the server where the database is located

* The username and password for the database


<span id="5fc4dac3"></span>
# Preparation

In Trino, perform the add allowlist operation, enter the "DataWind public IP for access" in the allowlist settings area, and grant this IP address permission to access the Trino service. The "DataWind public IP for access" can be viewed at [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview).

<span id="13f9f18a"></span>
# Create from data connection


1. Go to BytePlus, enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select Trino on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e786b9e20c964e6a9435856729ca0b86~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and after a successful connection, click Save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62bce6c5bb974f599789ee41539c21b9~tplv-goo7wpa0wc-image.image) </span>


* The configuration instructions for the SaaS version connection method are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Trino_20250703144958.<br><br>The name can be modified. Please enter a standardized name, which can only contain Chinese characters, English letters, numbers, and underscores, and cannot have spaces at the beginning or end. |
   |Connection method |IP/Port<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2daaed571e734924bb4a38e10d828536~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The public network address of Trino. To obtain this information, refer to the [Trino official documentation](https://trino.io/docs/current/). |
   |Port |The instance port of Trino. To obtain this information, refer to the [Trino official documentation](https://trino.io/docs/current/). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
   |Database |The database name created in Trino. |
   |vpcMode |Select "Yes" if the user needs to connect via the BytePlus internal network; otherwise, select "No". Select "No" here. |
   

* The configuration instructions for the self\-hosted version connection method are as follows:

   
   |Parameter |Configuration description |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish between different database connections in the system. For example, Trino_20250703144958.<br><br>The name can be modified. Please enter a valid name. Only Chinese characters, English letters, digits, and underscores are allowed, and spaces are not permitted at the beginning or end. |
   |Connection method |* IP/Port: Suitable for general scenarios.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2daaed571e734924bb4a38e10d828536~tplv-goo7wpa0wc-image.image) </span><br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7176a17a4b8f406ca8ce8d15834cbab4~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The public network address of Trino. To obtain this information, refer to the [Trino official documentation](https://trino.io/docs/current/). |
   |Port |The instance port of Trino. To obtain this information, refer to the [Trino official documentation](https://trino.io/docs/current/). |
   |JDBC connection string |JDBC connection string. To obtain this information, refer to the [Trino official documentation](https://trino.io/docs/current/). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
   |Database |The database name created in Trino. |
   


<span id="3247394d"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting the data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 in **Create from data connection** above. After completing the configuration, you will remain in the pop\-up window for selecting a data connection for the dataset, where you can proceed directly to the next step of dataset creation.


<span id="7ba107a0"></span>
# Next step: Create a dataset


1. Use the previously created data connection to create a dataset: click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the drop\-down list the data connection that was previously created.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43187a5d86d648e9987b5c43562ddf8a~tplv-goo7wpa0wc-image.image" width="450px" />   </div>
   


&nbsp;
