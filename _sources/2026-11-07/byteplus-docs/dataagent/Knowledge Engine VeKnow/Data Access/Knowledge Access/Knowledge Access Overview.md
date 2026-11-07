---
title: "Knowledge Access Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Knowledge_Access_Overview"
---

The system provides 40 + data connection methods, making it convenient for enterprises to integrate data into the enterprise knowledge engine system. This article describes the types and operations of data access.

<span id="84d21c2b"></span>
# Product Overview

The system provides 40 + data connection methods, including but not limited to relational databases (e.g. MySQL, Oracle, SQL Server, DB2, etc.), big data platforms (e.g. Hive, Impala, Clickhouse, etc.), MPP databases (Postgre, etc.), streaming databases (Kafka, etc.), text data (Excel, CSV), API interfaces, etc. It can not only connect with the customer data and business data access of various business companies within the customer (such as membership system, member mid\-platform system, etc.), but also connect with the official website, APP, official account, Mini Program, service number and other data sources.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aca84c8816d2eea0c950e9985983c2ac.png) </span>

In order to access as much user\-related data as possible and build a more accurate and complete data portrait, the system supports enterprises to access tripartite data. The data of the three parties may come from different platforms and channels. At this time, the ability of system text data access and API data access can be exerted. Through the text data import function, Excel and CSV data can be directly imported through the interface, and this part of the data can be stored in the platform. Users can customize the lifecycle and update cycle of imported data. At the same time, the system also provides Ocean Engine, A thousand rivers in great quantity, content platform and other data access capabilities to further enrich enterprise data.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efeac4e2db34463f88b3ade6aca4f1c5~tplv-goo7wpa0wc-image.image" width="300px" /></div>


<span id="e39c66d3"></span>
# Usage restrictions

**data management** module for the corresponding user in the **project center** **permission management** of the enterprise knowledge engine

<span id="ade4e36b"></span>
# Operation steps

Taking MySQL data connection as an example, the steps are as follows:


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Add Data Connection page, select and click **MySQL** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/652b94a3f3524c3ba53381c433450da2~tplv-goo7wpa0wc-image.image) </span>

3. On the Add MySQL Data Source page, configure the corresponding parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0826ea3b3314a4c98c7d022074b7575~tplv-goo7wpa0wc-image.image) </span>

   
   |name |describe |sample value |
   |---|---|---|
   |data connection name |The display name of the data source configuration list. |Demo data source |
   |server |Fill in the Internet Protocol Address. |10.225.34.22 |
   |Port |Fill in the correct port number. |3306 |
   |user name |The user name corresponding to the database. |cdp_admin |
   |password |The database corresponds to the password. |cdp_password123 |
   |connection method |optional<br><br>IP/Port means connecting to the database through the server IP + port.<br><br>JDBC connection string Need to fill in the corresponding JDBC format connection string |IP/Port |
   |permission mode |optional<br><br>Read, indicating that this connection can only query database data and cannot be modified.<br><br>Write, indicating that operations such as inserting, updating, and deleting data can be performed. |read |
   

4. Click **Test Connection** to test the data source connectivity.

5. After the test is successful, click **OK** .

6. Create a successful data connection page to view its **basic information** and **lineage view**.


&nbsp;
