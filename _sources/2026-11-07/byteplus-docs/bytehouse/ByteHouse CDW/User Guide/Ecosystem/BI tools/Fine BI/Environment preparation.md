---
title: "Environment preparation"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/fine-bi-env-preparation"
---

FineBI, launched by Fanruan Software Co., Ltd., is a business intelligence product that provides professional solutions for difficulties encountered in corporate informatization.

<span id="4b4b2007"></span>
## Prerequisites


1. Install FineBI. Follow the installation and deployment instructions according to the system requirements [here](https://help.fanruan.com/finebi-en/).

2. Obtain the driver for connecting to ByteHouse. You may choose one of the following:

   1. MySQL JDBC Driver5

   2. [MySQL JDBC Driver8](https://mvnrepository.com/artifact/mysql/mysql-connector-java)

   3. [ClickHouse JDBC Driver](https://github.com/ClickHouse/clickhouse-java/releases)

   4. [ByteHouse JDBC Driver](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/): Download the latest version.

   5. [ByteHouse HTTP JDBC Driver](https://github.com/bytehouse-cloud/driver-java-http/releases/)

3. A ByteHouse account.


<span id="34eb8555"></span>
## Configure the driver

We need to use the **driver management** function to upload custom JDBC drivers. FineBI inactivates uploading customer drivers, but we can activate this feature in two ways.

<span id="756b1777"></span>
### Activate the driver management function

<span id="d0de9424"></span>
#### Activate according to the official manual

Please refer to the [Driver Management - FineBI Help Documentation](https://help.fanruan.com/finebi/doc-view-1540.html) to complete the configuration.

<span id="652221be"></span>
#### Activate by modifying scripts

The following steps are executed on Mac, and you need to change some steps in your system.


1. Found the script file `db.` `Script` file, located under the FineBI installation path.

   ```SQL
   find ./ -name "db.script"
   ```
   


For example, on Mac systems, the path example is `/Applications/FineBI6.0/webapps/webroot/WEB-INF/embed/finedb/db.script`.


2. Open the file and change the following SQL statement.

   ```SQL
   INSERT INTO FINE_CONF_ENTITY VALUES('SystemConfig.driverUpload','false')
   // Change the `false` in the above statement to `true`, and after the modification, it will be as shown in the following line. 
   INSERT INTO FINE_CONF_ENTITY VALUES('SystemConfig.driverUpload','true')
   ```
   

3. Launch again the FineBI app.


<span id="0b3ef04c"></span>
### Import driver

You can select one of the drivers below to import according to your usage habits.


* MySQL JDBC Driver5 (no need to import)

* MySQL JDBC Driver8

* ClickHouse JDBC Driver

* ByteHouse JDBC Driver

* ByteHouse HTTP JDBC Driver

1. Administrator logs into the FineBI system, clicks "Management\> Data Connection Management\> Driver Management".

2. Click "New Driver", and enter a name to differentiate it from other drivers later on. Examples: "mysql8", "clickhouse", "bytehouse", "bytehouseHttp", and others.

3. Click "Upload Driver" to upload the database driver.

4. Click the "Driver" dropdown button, select a recently uploaded driver, and click "Save".

   For instance, after installing all four drivers, it appears as shown in the image below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3f9e12391154589829b9d039eacec91~tplv-goo7wpa0wc-image.image) </span>
