---
title: "Gbase 8a jdbc"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Gbase_8a_jdbc"
---

This article describes how to integrate Gbase 8a jdbc to create a dataset.

<span id="eb83be77"></span>
# Prerequisites

Before connecting to the data, contact the database administrator to collect the following information:


* The IP address and port number of the server where the database is located

* The username and password for the database


<span id="1f149a55"></span>
# Preparation

In Gbase 8a jdbc, add to the allowlist. Enter the "DataWind public IP for access" in the allowlist settings area to grant this IP address permission to access the Gbase 8a jdbc service. The "DataWind public IP for access" can be found in [Data connection overview](https://www.volcengine.com/docs/4726/47756).

<span id="61622038"></span>
# Create from data connection


1. Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select Gbase 8a jdbc on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/203593af58b8474c9e57d851d37ba490~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and test the connection. After a successful connection, click Save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5c9d756441941afa4dc1b20445c94b7~tplv-goo7wpa0wc-image.image) </span>


* The configuration instructions for the SaaS version connection method are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, gbase_8a_jdbc_20250707140533.<br><br>The name can be modified. Please enter a standardized name. Only combinations of Chinese characters, English letters, numbers, and underscores are allowed, and there must be no spaces at the beginning or end. |
   |Connection method |IP/Port<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52767a6be50345b0be19920e7d29e64a~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The public network address of gbase_8a_jdbc. To obtain it, refer to [Gbase Documentation](https://www.gbase.cn/docs/gbase-8a/%E4%BA%A7%E5%93%81%E6%89%8B%E5%86%8C/doc-introduction/). |
   |Port |The instance port of gbase_8a_jdbc. To obtain it, refer to [Gbase Documentation](https://www.gbase.cn/docs/gbase-8a/%E4%BA%A7%E5%93%81%E6%89%8B%E5%86%8C/doc-introduction/). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   

* The configuration instructions for the self\-hosted version connection method are as follows:

   
   |Parameters |Configuration description |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, gbase_8a_jdbc_20250707140533.<br><br>The name can be modified. Please enter a valid name. Only Chinese characters, English letters, digits, and underscores are allowed, and spaces are not permitted at the beginning or end. |
   |Connection method |* IP/Port: Suitable for general scenarios.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52767a6be50345b0be19920e7d29e64a~tplv-goo7wpa0wc-image.image) </span><br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe3dd5a37de4429fb55fdcdd185d2b68~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The public network address of gbase_8a_jdbc. To obtain it, refer to [Gbase Documentation](https://www.gbase.cn/docs/gbase-8a/%E4%BA%A7%E5%93%81%E6%89%8B%E5%86%8C/doc-introduction/). |
   |Port |The instance port of gbase_8a_jdbc. To obtain it, refer to [Gbase Documentation](https://www.gbase.cn/docs/gbase-8a/%E4%BA%A7%E5%93%81%E6%89%8B%E5%86%8C/doc-introduction/). |
   |JDBC connection string |JDBC connection string. To obtain it, refer to [Gbase Documentation](https://www.gbase.cn/docs/gbase-8a/%E4%BA%A7%E5%93%81%E6%89%8B%E5%86%8C/doc-introduction/) |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel of the corresponding engine. |
   


<span id="5ac3de84"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 in **Create from data connection**. After completing the configuration, you will remain in the pop\-up window for selecting a data connection for the dataset, where you can proceed directly to the next step of dataset creation.


<span id="a337091b"></span>
# Next step: Create a dataset


1. Use the previously created data connection to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the dropdown the previously created data connection.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da00fc59da9b4b8986d5e66ff9ba23c5~tplv-goo7wpa0wc-image.image" width="424px" /></div>


&nbsp;
