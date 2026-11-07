---
title: "Data Connection Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Connection_Overview"
---

Data connection, also known as data source access, is the first step to complete the docking with the database. After completion, a dataset can be created as an input for data lake visualization query analysis; it can also be used as an input for data lake visualization modeling.

# Prerequisite

The Intelligent Analytics Agent product allows users to make private deployments or use the Volcano Engine SaaS version directly. For the SaaS version, users need to set the IP of the relevant server to a whitelist, as follows:

* Beijing: 180.184.64.81 , 180.184.87.232 , 180.184.102.141

* Shanghai: 14.103.128.84

After the above Internet Protocol Address is successfully set, you can access the data in the SaaS environment.

# List of supported databases

The data source types supported by the data agent include not only local file uploads, but also online forms, application data sources, APIs, OLAP, relational databases, column databases, data warehouses, document databases, Volcano Engine matrices, Web connectors, Douyin ecosystem data, WeChat ecosystem data, public data, and advertising data.

* See the difference between connection methods directly [Supported connection methods](https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview#a7cf7826).

* Some databases have version distinctions. The version numbers supported by the product are listed below.

* Quick understanding of the access method of the database can be viewed [Quick Start](https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview#59851b5e).

* Supported direct connection data source types: ClickHouse, ByteHouse, Doris, StarRocks, PostgreSQL, Hologres, OpenGuass, MySQL, OceanBase Oracle. For detailed information, see the table below.

**The following table provides a quick preview of the database\-based data sources:**

|Data source name |Support connection method |Supported database version |Does it support creation?<br><br>[Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL_) |Access method |
|---|---|---|---|---|
|Excel/CSV file |Upload |\-\- |Not supported |[Local Excel/CSV File](https://docs.byteplus.com/docs/dataagent/Local_Excel_CSV_File) |
|Access |Offline extraction |\-\- |Not supported |[Access](https://docs.byteplus.com/docs/dataagent/Access_) |
|Lark spreadsheet |Offline extraction |\-\- |Not supported |[Lark SpreadSheet](https://docs.byteplus.com/docs/dataagent/Lark_SpreadSheet__) |
|Lark Base table |Offline extraction |\-\- |Not supported |[Lark Base Table](https://docs.byteplus.com/docs/dataagent/Lark_Base_Table__) |
|REST API 2.0 |Offline extraction |\-\- |Not supported |[REST API 2.0](https://docs.byteplus.com/docs/dataagent/REST_API_2_0__) |
|AnalyticDB for MySQL 2.0 |Offline extraction |\-\- |Support |[AnalyticDB for MySQL 2.0](https://docs.byteplus.com/docs/dataagent/AnalyticDB_for_MySQL_2_0__) |
|AnalyticDB for MySQL 3.0 |Offline extraction |\-\- |Support |[AnalyticDB for MySQL 3.0](https://docs.byteplus.com/docs/dataagent/AnalyticDB_for_MySQL_3_0__) |
|GreenPlum |Offline extraction |6.8.0 |Support |[GreenPlum](https://docs.byteplus.com/docs/dataagent/GreenPlum__) |
|SAP HANA |Offline extraction |2.x |Support |[SAP HANA](https://docs.byteplus.com/docs/dataagent/SAP_HANA__) |
|Impala |Offline extraction |2.12.0\-cdh5.15.1<br><br>3.x<br><br>4.x |Support |[Impala](https://docs.byteplus.com/docs/dataagent/Impala__) |
|ClickHouse Community Edition |Offline extraction, direct connection |19<br><br>20<br><br>21<br><br>22 |Support |[ClickHouse](https://docs.byteplus.com/docs/dataagent/ClickHouse__) |
|HBase Phoenix |Offline extraction |Phoenix 4.14 / Hbase 1.3 |Support |[Hbase Phoenix](https://docs.byteplus.com/docs/dataagent/Hbase_Phoenix__) |
|Vertica |Offline extraction |7.1.1\-0 |Not supported |[Vertica](https://docs.byteplus.com/docs/dataagent/Vertica__) |
|Amazon Athena |Offline extraction |\-\- |Support |[Amazon Athena](https://docs.byteplus.com/docs/dataagent/Amazon_Athena__) |
|Amazon Redshift |Offline extraction |8.0.2 |Support |[Amazon Redshift](https://docs.byteplus.com/docs/dataagent/Amazon_Redshift__) |
|ByteHouse CE |Offline extraction, direct connection |2.1 |Support |[ByteHouse CE](https://docs.byteplus.com/docs/dataagent/ByteHouseCE__) |
|ByteHouse CDW |Offline extraction, direct connection |\-\- |Support |[ByteHouse CDW](https://docs.byteplus.com/docs/dataagent/ByteHouseCDW) |
|Presto |Offline extraction |\-\- |Support |[Presto](https://docs.byteplus.com/docs/dataagent/Presto__) |
|Databricks |Offline extraction |2.48 |Support |[Databricks](https://docs.byteplus.com/docs/dataagent/Databricks__) |
|Transwarp ArgoDB |Offline extraction |5.2 |Not supported |[Transwarp ArgoDB](https://docs.byteplus.com/docs/dataagent/TranswarpArgoDB) |
|Hologres |Offline extraction, direct connection |\-\- |Support |[Hologres](https://docs.byteplus.com/docs/dataagent/Hologres__) |
|Hetu |Offline extraction |3.3 |Not supported |[Hetu](https://docs.byteplus.com/docs/dataagent/Hetu__) |
|MySQL |Offline extraction, direct connection |5.5<br><br>5.6<br><br>5.7<br><br>8.0 |Support |[MySQL](https://docs.byteplus.com/docs/dataagent/MySQL__) |
|IBM DB2 |Offline extraction |11.5.4.0 |Support |[IBM DB2](https://docs.byteplus.com/docs/dataagent/IBMDB2) |
|Oracle |Offline extraction |11g Enterprise Edition Release<br><br>11.2.0.1.0<br><br>12<br><br>18<br><br>19 |Support |[Oracle](https://docs.byteplus.com/docs/dataagent/Oracle__) |
|PostgreSQL |Offline extraction, direct connection |8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14<br><br>15 |Support |[PostgreSQL](https://docs.byteplus.com/docs/dataagent/PostgreSQL__) |
|OpenGauss |Offline extraction, direct connection |\-\- |Support |[OpenGauss](https://docs.byteplus.com/docs/dataagent/OpenGauss__) |
|SQL Server |Offline extraction |2012<br><br>2014<br><br>2016<br><br>2017<br><br>2019 |Support |[SQL Server](https://docs.byteplus.com/docs/dataagent/SQL_Server__) |
|Teradata |Offline extraction |\-\- |Support |[Teradata](https://docs.byteplus.com/docs/dataagent/Teradata__) |
|Doris |Offline extraction, direct connection |\-\- |Support |[Doris](https://docs.byteplus.com/docs/dataagent/Doris__) |
|VastBase |Offline extraction |G100 2.2.10<br><br>G100 2.2.15 |Not supported |[VastBase](https://docs.byteplus.com/docs/dataagent/VastBase__) |
|Damon |Offline extraction |\-\- |Support |[Damon](https://docs.byteplus.com/docs/dataagent/Damon__) |
|TiDB |Offline extraction |\-\- |Support |[TiDB](https://docs.byteplus.com/docs/dataagent/TiDB__) |
|GoldenDB |Offline extraction |\-\- |Support |[GoldenDB](https://docs.byteplus.com/docs/dataagent/GoldenDB__) |
|OceanBase MySQL |Offline extraction |\-\- |Support |[OceanBase MySQL](https://docs.byteplus.com/docs/dataagent/OceanBase_MySQL__) |
|OceanBase Oracle |Offline extraction, direct connection |\-\- |Support |[OceanBase Oracle](https://docs.byteplus.com/docs/dataagent/OceanBase_Oracle__) |
|HBase |Offline extraction |1.x<br><br>2.x |Not supported |[HBase](https://docs.byteplus.com/docs/dataagent/HBase__) |
|Hive |Offline extraction |1.x<br><br>2.x<br><br>3.x<br><br>2.1.1\-cdh6.3.2 |Support |[Hive](https://docs.byteplus.com/docs/dataagent/Hive__) |
|MaxCompute |Offline extraction |1.0<br><br>2.0 |Support |[MaxCompute](https://docs.byteplus.com/docs/dataagent/MaxCompute__) |
|LAS (Public Cloud Edition) |Offline extraction |\-\- |Support |[LAS](https://docs.byteplus.com/docs/dataagent/LAS___) |
|StarRocks |Offline extraction, direct connection |\-\- |Support |[StarRocks](https://docs.byteplus.com/docs/dataagent/StarRocks__) |
|Tencent Cloud DLC |Offline extraction |\-\- |Support |[Tencent Cloud DLC](https://docs.byteplus.com/docs/dataagent/Tencent_Cloud_DLC__) |
|MongoDB |Offline extraction |4.4.4<br><br>5.0.9 |Support |[MongoDB](https://docs.byteplus.com/docs/dataagent/MongoDB__) |
|Intelligent outbound call |Offline extraction |Smart outbound calls require versions from December 2022 and later |\-\- | |
|Tencent Cloud COS |Offline extraction |\-\- |Not supported |[Tencent Cloud COS](https://docs.byteplus.com/docs/dataagent/Tencent_Cloud_COS__) |
|Alibaba Cloud OSS |Offline extraction |\-\- |Not supported |[Alibaba Cloud OSS](https://docs.byteplus.com/docs/dataagent/Alibaba_Cloud_OSS__) |
|Volcanic Cloud TOS |Offline extraction |\-\- |Not supported |[Volcanic Cloud TOS](https://docs.byteplus.com/docs/dataagent/Volcanic_Cloud_TOS__) |
|Ocean Engine/A thousand rivers in great quantity |Offline extraction |\-\- |Not supported | |
|WeChat official account |Offline extraction |\-\- |Not supported | |

# Supported connection methods

## Offline extraction

Data is extracted offline into DataAgent's built\-in high\-performance storage computing engine. Most currently supported databases support offline extraction by default.

**Application scenario**

* Coverage of a wide range of data sources: The extraction mode supports all of the above data source types.

* Strong modeling ability: support multi\-table join and multi\-table merge across data sources.

* Query performance is fast: It supports multi\-dimensional queries for large amounts of data, and the built\-in computing engine has good performance, enabling fast analysis of large amounts of data.

**Usage restrictions**

* Lack of real\-time data: A synchronization period needs to be set, and the data is synchronized within the user\-selected synchronization node.

## Real\-time extraction

Extract data to the engine in real time and store it. Only Kafka, Pulsar data sources are supported.

## Direct connection

Connect directly to the database to take advantage of its performance.

**Application scenario**

* It supports real\-time data functions and can directly connect to the user's database without the need for data updates, meeting the user's requirements for real\-time data.

* Supported direct connection data source types: ClickHouse, ByteHouse, Doris, StarRocks, PostgreSQL, Hologres, OpenGuass, MySQL, OceanBase Oracle.

**Usage restrictions**

* Query performance is highly influenced by database performance: Due to the direct connection to the user database, query performance may be affected due to data connection and database engine performance limitations.

* Except for the finder data connection, which only supports a single table, other directly connected data sources can support multi\-table Union, Join, and custom SQL. Multi\-tables cannot be used across data sources and cross\-data connections, such as table A from the A data connection and table B from the B data connection. Union/join cannot be performed, or the operation of tables A and B simultaneously exists in the custom SQL.

# Quick Start

1. Enter the Intelligent Analysis Agent product, click to enter a specific item, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image)

2. Select the type of data source to connect to.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb99406285c345df866fc162d0afb6f1~tplv-goo7wpa0wc-image.image)

3. To configure the corresponding parameters, you can refer to the following MySQL DEMO library information.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c8d919832574d6aa687ff81ed6e77cd~tplv-goo7wpa0wc-image.image)

   The relevant parameter configuration instructions are as follows:

   |name |describe |sample value |
   |---|---|---|
   |data connection name |The display name of the data source configuration list. |Demo data source |
   |server |Fill in the IP address. |10.225.34.22 |
   |Port |Fill in the correct port number. |3306 |
   |user name |The user name corresponding to the database. |DataAgent_admin |
   |password |Database corresponding password. |DataAgent_password123 |
   |permission mode |It supports both reading and writing. |read |
   |vpcMode |To obtain the VPC ID, please refer to [2.2 to obtain the database LAN IP and VPC ID ](https://www.volcengine.com/docs/4726/1418732#de8ed400). |No |

   > **说明**

   > The example values given are for reference only and are not valid connections that can be filled in directly.

4. Click Connection Test to perform the data source connectivity test. After the test is successful, confirm and save it.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/885b3b29e55b4083ab4643aeefa75538~tplv-goo7wpa0wc-image.image)

5. Locate the data connection that has been created.

   In the data connection directory (list on the left), you can filter and search by the permissions you have.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8bb9d95ef8548a595aea95cea33947e~tplv-goo7wpa0wc-image.image)
