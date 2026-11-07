---
title: "Overview of Data Connection"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Overview_of_Data_Connection"
---

Data connection, also referred to as data source integration, is the first step in connecting to a database. After completing this step, you can create datasets to use as input for data visualization query analysis, or as input for data visualization modeling.

# Prerequisites

The Intelligent Analytics Agent product supports users in deploying privately or directly using the BytePlus SaaS version. For the SaaS version, users need to add the relevant server IP addresses to the allowlist, as follows:

* Beijing: 180.184.64.81, 180.184.87.232, 180.184.102.141

* Shanghai: 14.103.128.84

Once the above IP addresses are successfully added, you can connect data in the SaaS environment.

# List of supported databases

The Intelligent Data Agent supports integration with various types of data sources, including local file uploads, online spreadsheets, application data sources, APIs, OLAP, relational databases, columnar databases, data warehouses, document databases, BytePlus Matrix, web connectors, Douyin ecosystem data, WeChat ecosystem data, public data, and advertising data, among others.

* For differences in connection methods, see [Supported connection methods](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection#b2925a8e)

* Some databases have version distinctions. The supported version numbers are listed below.

* For a quick overview of database integration methods, see [Quick start](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection#b14f5b3e).

* Supported direct connection data source types: ClickHouse, ByteHouse, Doris, StarRocks, PostgreSQL, Hologres, OpenGuass, MySQL, OceanBase Oracle. For detailed information, see the table below.

**The table below lists database\-centric data sources for your quick preview:**

|Data source name |Supported connection methods |Supported database versions |Creation supported<br><br>[Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL) |Integration method |
|---|---|---|---|---|
|Excel/CSV file |Upload |\-\- |Not supported |[Local Excel/CSV Files](https://docs.byteplus.com/docs/dataagent/Local_Excel_CSV_files) |
|Access |Offline extraction |\-\- |Not supported |[Access](https://docs.byteplus.com/docs/dataagent/Access) |
|Lark spreadsheet |Offline extraction |\-\- |Not supported |[Lark Sheets](https://docs.byteplus.com/docs/dataagent/Lark_Sheets) |
|Lark Base Table |Offline extraction |\-\- |Not supported |[Lark Base Tables](https://docs.byteplus.com/docs/dataagent/Lark_Base_Tables) |
|REST API 2.0 |Offline extraction |\-\- |Not supported |[REST API 2.0](https://docs.byteplus.com/docs/dataagent/REST_API_2_0) |
|AnalyticDB for MySQL 2.0 |Offline extraction |\-\- |Supported |[AnalyticDB for MySQL 2.0](https://docs.byteplus.com/docs/dataagent/AnalyticDB_for_MySQL_2_0) |
|AnalyticDB for MySQL 3.0 |Offline extraction |\-\- |Supported |[AnalyticDB for MySQL 3.0](https://docs.byteplus.com/docs/dataagent/AnalyticDB_for_MySQL_3_0) |
|GreenPlum |Offline extraction |6.8.0 |Supported |[GreenPlum](https://docs.byteplus.com/docs/dataagent/GreenPlum) |
|SAP HANA |Offline extraction |2.x |Supported |[SAP HANA](https://docs.byteplus.com/docs/dataagent/SAP_HANA) |
|Impala |Offline extraction |2.12.0\-cdh5.15.1<br><br>3.x<br><br>4.x |Supported |[Impala](https://docs.byteplus.com/docs/dataagent/Impala) |
|ClickHouse Community Edition |Offline extraction, direct connection |19<br><br>20<br><br>21<br><br>22 |Supported |[ClickHouse](https://docs.byteplus.com/docs/dataagent/ClickHouse) |
|HBase Phoenix |Offline extraction |Phoenix 4.14 / Hbase 1.3 |Supported |[Hbase Phoenix](https://docs.byteplus.com/docs/dataagent/Hbase_Phoenix) |
|Vertica |Offline extraction |7.1.1\-0 |Not supported |[Vertica](https://docs.byteplus.com/docs/dataagent/Vertica) |
|Amazon Athena |Offline extraction |\-\- |Supported |[Amazon Athena](https://docs.byteplus.com/docs/dataagent/Amazon_Athena) |
|Amazon Redshift |Offline extraction |8.0.2 |Supported |[Amazon Redshift](https://docs.byteplus.com/docs/dataagent/Amazon_Redshift) |
|ByteHouse CE |Offline extraction, direct connection |2.1 |Supported |[ByteHouse CE](https://docs.byteplus.com/docs/dataagent/ByteHouse_CE) |
|ByteHouse CDW |Offline extraction, direct connection |\-\- |Supported |[ByteHouse CDW](https://docs.byteplus.com/docs/dataagent/ByteHouse_CDW) |
|Presto |Offline extraction |\-\- |Supported |[Presto](https://docs.byteplus.com/docs/dataagent/Presto) |
|Databricks |Offline extraction |2.48 |Supported |[Databricks](https://docs.byteplus.com/docs/dataagent/Databricks) |
|Transwarp ArgoDB |Offline extraction |5.2 |Not supported |[Transwarp ArgoDB](https://docs.byteplus.com/docs/dataagent/Transwarp_ArgoDB) |
|Hologres |Offline extraction, direct connection |\-\- |Supported |[Hologres](https://docs.byteplus.com/docs/dataagent/Hologres) |
|Hetu |Offline extraction |3.3 |Not supported |[Hetu](https://docs.byteplus.com/docs/dataagent/Hetu) |
|MySQL |Offline extraction, direct connection |5.5<br><br>5.6<br><br>5.7<br><br>8.0 |Supported |[MySQL](https://docs.byteplus.com/docs/dataagent/MySQL) |
|IBM DB2 |Offline extraction |11.5.4.0 |Supported |[IBM DB2](https://docs.byteplus.com/docs/dataagent/IBM_DB2) |
|Oracle |Offline extraction |11g Enterprise Edition Release<br><br>11.2.0.1.0<br><br>12<br><br>18<br><br>19 |Supported |[Oracle](https://docs.byteplus.com/docs/dataagent/Oracle) |
|PostgreSQL |Offline extraction, direct connection |8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14<br><br>15 |Supported |[PostgreSQL](https://docs.byteplus.com/docs/dataagent/PostgreSQL) |
|OpenGauss |Offline extraction, direct connection |\-\- |Supported |[OpenGauss](https://docs.byteplus.com/docs/dataagent/OpenGauss) |
|SQL Server |Offline extraction |2012<br><br>2014<br><br>2016<br><br>2017<br><br>2019 |Supported |[SQL Server](https://docs.byteplus.com/docs/dataagent/SQL_Server) |
|Teradata |Offline extraction |\-\- |Supported |[Teradata](https://docs.byteplus.com/docs/dataagent/Teradata) |
|Doris |Offline extraction, direct connection |\-\- |Supported |[Doris](https://docs.byteplus.com/docs/dataagent/Doris) |
|VastBase |Offline extraction |G100 2.2.10<br><br>G100 2.2.15 |Not supported |[VastBase](https://docs.byteplus.com/docs/dataagent/VastBase) |
|Dameng |Offline extraction |\-\- |Supported |[Damon](https://docs.byteplus.com/docs/dataagent/Damon) |
|TiDB |Offline extraction |\-\- |Supported |[TiDB](https://docs.byteplus.com/docs/dataagent/TiDB) |
|GoldenDB |Offline extraction |\-\- |Supported |[GoldenDB](https://docs.byteplus.com/docs/dataagent/GoldenDB) |
|OceanBase MySQL |Offline extraction |\-\- |Supported |[OceanBase MySQL](https://docs.byteplus.com/docs/dataagent/OceanBase_MySQL) |
|OceanBase Oracle |Offline extraction, direct connection |\-\- |Supported |[OceanBase Oracle](https://docs.byteplus.com/docs/dataagent/OceanBase_Oracle) |
|HBase |Offline extraction |1.x<br><br>2.x |Not supported |[HBase](https://docs.byteplus.com/docs/dataagent/HBase) |
|Hive |Offline extraction |1.x<br><br>2.x<br><br>3.x<br><br>2.1.1\-cdh6.3.2 |Supported |[Hive](https://docs.byteplus.com/docs/dataagent/Hive) |
|MaxCompute |Offline extraction |1.0<br><br>2.0 |Supported |[MaxCompute](https://docs.byteplus.com/docs/dataagent/MaxCompute) |
|LAS (public cloud version) |Offline extraction |\-\- |Supported |[LAS](https://docs.byteplus.com/docs/dataagent/LAS) |
|StarRocks |Offline extraction, direct connection |\-\- |Supported |[StarRocks](https://docs.byteplus.com/docs/dataagent/StarRocks) |
|Tencent Cloud DLC |Offline extraction |\-\- |Supported |[Tencent Cloud DLC](https://docs.byteplus.com/docs/dataagent/Tencent_Cloud_DLC) |
|MongoDB |Offline extraction |4.4.4<br><br>5.0.9 |Supported |[MongoDB](https://docs.byteplus.com/docs/dataagent/MongoDB) |
|Intelligent outbound call |Offline extraction |Intelligent outbound call requires version from December 2022 or later |\-\- | |
|Tencent Cloud COS |Offline extraction |\-\- |Not supported |[Tencent Cloud COS](https://docs.byteplus.com/docs/dataagent/Tencent_Cloud_COS) |
|Alibaba Cloud OSS |Offline extraction |\-\- |Not supported |[Alibaba Cloud OSS](https://docs.byteplus.com/docs/dataagent/Alibaba_Cloud_OSS) |
|BytePlus TOS |Offline extraction |\-\- |Not supported |[Volcano Engine TOS](https://docs.byteplus.com/docs/dataagent/Volcano_Engine_TOS) |
|Ocean Engine/Juliang Qianchuan |Offline extraction |\-\- |Not supported | |
|WeChat Official Account |Offline extraction |\-\- |Not supported | |

# Supported connection methods

## Offline extraction

Data can be extracted offline into the DataAgent's built\-in high\-performance storage and computing engine. Most supported databases currently default to offline extraction.

**Application scenarios**

* Wide coverage of data sources: The extraction mode supports all of the above data source types.

* Strong modeling capabilities: Supports multi\-table join and multi\-table merge across data sources.

* Fast query performance: Supports multi\-dimensional queries on large volumes of data. The built\-in computing engine delivers high performance and enables rapid analysis of large datasets.

**Usage limitations**

* Lack of real\-time data: You need to set a synchronization cycle, and data will be synchronized at the user\-selected synchronization nodes.

## Real\-time extraction

Extract data in real time and store it in the engine. Only Kafka, Pulsar, and similar data sources are supported.

## Direct connection

Connect directly to the database to leverage the database's performance.

**Application scenarios**

* Supports real\-time data functionality, allowing direct connection to the user's database without requiring data updates, meeting the user's requirements for data timeliness.

* Supported direct connection data source types: ClickHouse, ByteHouse, Doris, StarRocks, PostgreSQL, Hologres, OpenGuass, MySQL, OceanBase Oracle.

**Usage limitations**

* Query performance is significantly affected by database performance: Because the user's database is connected directly, query performance may be impacted by data connection and database engine performance limitations.

* Except for finder data connections, which only support single tables, other direct connection data sources support multi\-table Union, Join, and custom SQL. Multi\-table operations cannot be performed across data sources or data connections. For example, Table A from data connection A and Table B from data connection B cannot be used for union/join, nor can operations involving both Table A and Table B be included in custom SQL.

# Quick start

1. Enter the Intelligent Analysis Agent product, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image)

2. Select the type of data source to connect.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1d086ec19494982811166d167852b83~tplv-goo7wpa0wc-image.image)

3. Configure the corresponding parameters. You can refer to the following DEMO database information for MySQL.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90a505ae3e614174af485bdbc0d47f69~tplv-goo7wpa0wc-image.image)

   The configuration instructions for related parameters are as follows:

   |Name |Description |Example value |
   |---|---|---|
   |Data connection name |The display name in the data source configuration list. |Demo data source |
   |Server |Enter the IP address. |10.225.34.22 |
   |Port |Enter the correct port number. |3306 |
   |Username |The username corresponding to the database. |DataAgent_admin |
   |Password |The password corresponding to the database. |DataAgent_password123 |
   |Permission mode |Supports both reading and writing. |Read |
   |vpcMode |To obtain the VPC ID, see [2.2 Obtain the database LAN IP and VPC ID](https://www.volcengine.com/docs/4726/1418732#de8ed400). |No |

   > **说明**

   > The example values provided are for reference only and are not valid connections that can be used directly.

4. Click Connection Test to test the connectivity of the data source. After a successful test, confirm and save.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d241ca558acc4d45a9351e61bad235da~tplv-goo7wpa0wc-image.image)

5. Find the created data connections.

   In the data connection directory (left\-side list), you can filter and search according to your permissions.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d31eadb71765417cada6ed96c45ddb3c~tplv-goo7wpa0wc-image.image)
