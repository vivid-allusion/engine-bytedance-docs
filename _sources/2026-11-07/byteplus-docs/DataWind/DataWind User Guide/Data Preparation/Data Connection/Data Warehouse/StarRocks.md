---
title: "StarRocks"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/StarRocks"
---

This article describes how to connect StarRocks to create a dataset.

<span id="f0384f78"></span>
# Prerequisites

Before connecting to the data, collect the following information:


* The IP address and port number of the server where the database is located.

* The username and password for the database.


<span id="9e4848a4"></span>
# Create a dataset from a data connection


1. Go to BytePlus, enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Select StarRocks on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55f80573525144818afdab6c44a470f5~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after the connection is successful.

   * The parameter configuration instructions for the SaaS version are as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38fa46a8d24446e7995d200593064c81~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  | | | \
  |Parameters |Configuration instructions |
  |---|---|
  | | | \
  |Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. The default is StarRocks_timestamp. You can modify the name, but please enter a valid name. Only Chinese characters, English letters, numbers, and underscores are allowed, and there must be no spaces at the beginning or end. |
  | | | \
  |Server |The public network address of StarRocks. For details, refer to the [StarRocks official documentation](https://docs.starrocks.io/docs/introduction/StarRocks_intro/). |
  | | | \
  |Port |The instance port of StarRocks. For details, refer to the [StarRocks official documentation](https://docs.starrocks.io/docs/introduction/StarRocks_intro/). |
  | | | \
  |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
  | | | \
  |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
  | | | \
  |Connection method |The SaaS version provides the IP/Port connection method. |\
  | |![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d80721094f1b4ff8875ea049e5c73480~tplv-goo7wpa0wc-image.image =426x) |
  | | | \
  |externalCatalog |This field must be filled in when querying external data sources (such as Hive, Iceberg, Hudi, Delta Lake, JDBC, Elasticsearch, Paimon, and more) through an external catalog. Enter the database name as in "catalog name.database name". (For example: my_catalog.hive_db1, enter hive_db1 here) |
  | | | \
  |Permission mode |Both read and write modes are supported. |\
  | | |\
  | |* Read: Only retrieves data from the data source; data cannot be modified, added, or deleted. |\
  | |* Write: The user needs to write data to the data connection through visual modeling and must have permission to operate the data. |
  | | | \
  |vpcMode and VPC ID |* vpcMode: Select "Yes" if the user needs to connect via the BytePlus intranet; select "No" in all other cases. |\
  | |   :::warning |\
  | |   Currently, VPC internal network connections are only supported in the North China region. |\
  | |   ::: |\
  | |* VPC ID: Required when vpcMode is set to "Yes". For how to obtain it, see [Preparation](https://www.volcengine.com/docs/4726/171360#_1-%E6%A6%82%E8%BF%B0). |
```



* The parameter configuration instructions for the on\-premises version are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38fa46a8d24446e7995d200593064c81~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration description |
   |---|---|
   |Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. The default is StarRocks_timestamp. The name can be modified, but please enter a standardized name. Only Chinese characters, English letters, digits, and underscores are allowed, and spaces are not permitted at the beginning or end. |
   |Server |The public network address of StarRocks. For details, refer to the [StarRocks official documentation](https://docs.starrocks.io/docs/introduction/StarRocks_intro/). |
   |Port |The instance port of StarRocks. For details, refer to the [StarRocks official documentation](https://docs.starrocks.io/docs/introduction/StarRocks_intro/). |
   |Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
   |Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel responsible for the corresponding engine. |
   |Connection method |The private deployment version provides two connection methods: IP/Port and JDBC connection string.<br><br><br>* IP/Port: Suitable for general scenarios.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d80721094f1b4ff8875ea049e5c73480~tplv-goo7wpa0wc-image.image) </span><br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97114d662d91401f8f74e81c9742a97a~tplv-goo7wpa0wc-image.image) </span> |
   |externalCatalog |When querying external data sources (such as Hive, Iceberg, Hudi, Delta Lake, JDBC, Elasticsearch, Paimon, and more) through an external catalog, this field is required. Enter the database name from “catalog name.database name”. (For example: my_catalog.hive_db1; enter hive_db1 here.) |
   |JDBC connection string |For the JDBC connection string, refer to the [StarRocks official documentation](https://docs.starrocks.io/docs/introduction/StarRocks_intro/) for details on how to obtain it. |
   |Permission mode |Both read and write modes are supported.<br><br><br>* Read: Only retrieves data from the data source; modification, addition, or deletion of data is not allowed.<br><br>* Write: To write data to the data connection through visual modeling, the user must have data operation permissions. |
   


<span id="38ae78c0"></span>
# Create a dataset from a dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 in **Create a dataset from a data connection**. After completing the configuration, the pop\-up window for selecting a data connection for the dataset will remain open, allowing you to proceed directly to the next step: creating the dataset.


<span id="95669f09"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the drop\-down list the data connection you created earlier.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29dcf4fb97fb4e51b5c11905acba414e~tplv-goo7wpa0wc-image.image" width="610px" /></div>
