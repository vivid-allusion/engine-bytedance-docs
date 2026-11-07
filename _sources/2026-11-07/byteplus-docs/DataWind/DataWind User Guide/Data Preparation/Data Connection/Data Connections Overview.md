---
title: "Data Connections Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Connections_Overview"
---

Data connection, also referred to as data source integration, is the first step in connecting to a database. After completing this step, you can create datasets to use as inputs for data visualization queries and analysis, or as inputs for data visualization modeling.

<span id="f01c8555"></span>
# Feature overview

DataWind supports two main categories: **local file uploads** and **online/system data sources**, including FTP connections, online spreadsheets, streaming databases, OLAP databases, relational databases, other data warehouses, BytePlus Matrix data sources, Douyin ecosystem data, API connections, content management platforms, WeChat Official Accounts, astrology data, calendar data, and more.

For detailed information about data source integration, refer to the following guides:


* For the list of supported data sources, corresponding database version requirements, and environment differences between private deployment and SaaS versions, see [All supported data sources](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview#48e13267).

* For quick integration methods for database\-type data sources, see [Quickly connect to BytePlus databases and data warehouse data sources](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview#ac884d50).


<span id="0b15f366"></span>
## Connection methods

DataWind supports connecting to data sources via offline extraction, real\-time extraction, and direct connection:


|Connection methods |Offline extraction |Real\-time extraction |Direct connection |
|---|---|---|---|
|Definition |Extract data offline into the built\-in high\-performance storage and computing engine of DataWind. Most supported databases currently support offline extraction by default. |Extract data in real time into the engine for storage. Only data sources such as Kafka and Pulsar are supported. |Connect directly to the database to utilize the database's performance. |
|Application scenarios |* Wide coverage of data sources: The extraction mode supports all the above data source types.<br><br>* Strong modeling capabilities: Supports multi\-table join and multi\-table merge across data sources.<br><br>* Fast query performance: Supports multidimensional queries on massive data volumes. The built\-in computing engine delivers high performance and enables rapid analysis of large datasets. |Stream data processing: Adapts to the continuous data ingestion and analysis requirements of streaming data sources such as Kafka and Pulsar. |Supports real\-time data functionality. You can connect directly to the user's database without requiring data updates, meeting the user's requirements for data timeliness. |
|Usage limitations |Data is not real\-time: A synchronization interval must be set, and data will be synchronized within the synchronization node selected by the user. |Only Kafka, Pulsar, and similar data sources are supported. |* Query performance is heavily affected by database performance: Because the user database is connected directly, query performance may be impacted by data connection and database engine limitations.<br><br>* Only single\-table direct queries are supported prior to version V2.50.0.<br><br>* From version V2.50.0 and later, except for finder data connections which only support single tables, other direct data sources support multi\-table Union, Join, and custom SQL. Multi\-table operations cannot be performed across data sources or data connections. For example, Table A from data connection A and Table B from data connection B cannot be unioned or joined, nor can operations involving both Table A and Table B appear simultaneously in custom SQL. |


<span id="296d7ec1"></span>
# Prerequisites


* The DataWind product supports private deployment or direct use of the BytePlus SaaS version. For the SaaS version, before connecting to data sources, you need to add the relevant server IPs to the allowlist as follows:

   * Beijing: `180.184.64.81`, `180.184.87.232`, `180.184.102.141`

   * Shanghai: `14.103.128.84`, `100.67.0.0/16`, `100.68.0.0/16`

   * Johor: `101.47.44.45`

      After successfully adding the above IP addresses, you can connect to data sources in the SaaS environment.

* Before configuring a data source connection, ensure that the account being used has obtained read, write, and authentication permissions for the data source.


<span id="48e13267"></span>
# All supported data sources

The table below lists the database\-based data sources and their corresponding connection documentation for your quick reference:


|Data source name |Supported connection method |Supported database version |Supported environment |Supported environment version |Creation supported<br><br>[Custom SQL](https://docs.byteplus.com/docs/DataWind/110006) |Access method |
|---|---|---|---|---|---|---|
|Excel/CSV file |Offline extraction, direct connection |\-\- |SaaS, private deployment |\-\- |Not supported |[Local Excel/CSV Files](https://docs.byteplus.com/docs/DataWind/Local_Excel_CSV_Files) |
|Access |Offline extraction |\-\- |Private deployment |\-\- |Not supported |[Access](https://docs.byteplus.com/docs/DataWind/Access) |
|Kafka |Real\-time extraction |Version 0.8.x and above |Private deployment |\-\- |Not supported |[Kafka](https://docs.byteplus.com/docs/DataWind/Kafka) |
|Pulsar |Real\-time extraction |2.8.3<br><br>2.10.1 |Private deployment |\-\- |Not supported |[Pulsar](https://docs.byteplus.com/docs/DataWind/Pulsar) |
|GreenPlum |Offline extraction |6.8.0 |SaaS, private deployment |\-\- |Supported |[GreenPlum](https://docs.byteplus.com/docs/DataWind/GreenPlum) |
|SAP HANA |Offline extraction |2.x |SaaS, private deployment |\-\- |Supported |[SAP HANA](https://docs.byteplus.com/docs/DataWind/SAP_HANA) |
|Impala |Offline extraction, direct connection |2.12.0\-cdh5.15.1<br><br>3.x<br><br>4.x |SaaS, private deployment |\-\- |Supported |[Impala](https://docs.byteplus.com/docs/DataWind/Impala) |
|ClickHouse Community Edition |Offline extraction, direct connection |19<br><br>20<br><br>21<br><br>22 |SaaS, private deployment |\-\- |Supported |[ClickHouse](https://docs.byteplus.com/docs/DataWind/ClickHouse) |
|HBase Phoenix |Offline extraction |Phoenix 4.14 / Hbase 1.3 |SaaS, private deployment |\-\- |Supported |[Hbase Phoenix](https://docs.byteplus.com/docs/DataWind/Hbase_Phoenix) |
|Gauss DWS |Offline extraction, direct connection |\-\- |SaaS, private deployment |V2.68.0 |Supported |[Gauss DWS](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62a68) |
|HBase |Offline extraction |1.x<br><br>2.x |SaaS, private deployment |\-\- |Not supported |[HBase](https://docs.byteplus.com/docs/DataWind/HBase) |
|Vertica |Offline extraction |7.1.1\-0 |SaaS, private deployment |\-\- |Not supported |[Vertica](https://docs.byteplus.com/docs/DataWind/Vertica) |
|Amazon Athena |Offline extraction |\-\- |SaaS, private deployment |V2.44.0 |Supported |[Amazon Athena](https://docs.byteplus.com/docs/DataWind/Amazon_Athena) |
|Amazon Redshift |Offline extraction |8.0.2 |SaaS, private deployment |\-\- |Supported |[Amazon Redshift](https://docs.byteplus.com/docs/DataWind/Amazon_Redshift) |
|ByteHouse CDW |Offline extraction, direct connection |\-\- |SaaS, private deployment |V2.44.0 |Supported |[ByteHouse CDW](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW) |
|ByteHouse CE |Offline extraction, direct connection |2.1 |SaaS, private deployment |\-\- |Supported |[ByteHouse CE](https://docs.byteplus.com/docs/DataWind/ByteHouse_CE) |
|Presto |Offline extraction, direct connection (supported from version V2.50.0 and later) |\-\- |SaaS, private deployment |\-\- |Supported |[Presto](https://docs.byteplus.com/docs/DataWind/Presto) |
|Trino |Offline extraction, direct connection |\-\- |SaaS, private deployment |V2.64.0 |Supported |[Trino](https://docs.byteplus.com/docs/DataWind/Trino) |
|Databricks |Offline extraction, direct connection |2.48 |SaaS, private deployment |\-\- |Supported |[Databricks](https://docs.byteplus.com/docs/DataWind/Databricks) |
|AnalyticDB for MySQL 2.0 |Offline extraction |\-\- |SaaS, private deployment |\-\- |Supported |[AnalyticDB for MySQL 2.0](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f625ba) |
|AnalyticDB for MySQL 3.0 |Offline extraction |\-\- |SaaS, private deployment |\-\- |Supported |[AnalyticDB for MySQL 3.0](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f625bb) |
|Hologres |Offline extraction, direct connection |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[Hologres](https://docs.byteplus.com/docs/DataWind/Hologres) |
|MySQL |Offline extraction, direct connection |5.5<br><br>5.6<br><br>5.7<br><br>8.0 |SaaS, on\-premises deployment |\-\- |Supported |[MySQL](https://docs.byteplus.com/docs/DataWind/MySQL) |
|IBM DB2 |Offline extraction |11.5.4.0 |SaaS, on\-premises deployment |\-\- |Supported |[IBM DB2](https://docs.byteplus.com/docs/DataWind/IBM_DB2) |
|Oracle |Offline extraction |11g Enterprise Edition Release<br><br>11.2.0.1.0<br><br>12<br><br>18<br><br>19 |SaaS, on\-premises deployment |\-\- |Supported |[Oracle](https://docs.byteplus.com/docs/DataWind/Oracle) |
|PostgreSQL |Offline extraction, direct connection |8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14<br><br>15 |SaaS, on\-premises deployment |\-\- |Supported |[PostgreSQL](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62795) |
|OpenGauss |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[OpenGauss](https://docs.byteplus.com/docs/DataWind/OpenGauss) |
|SQL Server |Offline extraction |2012<br><br>2014<br><br>2016<br><br>2017<br><br>2019 |SaaS, on\-premises deployment |\-\- |Supported |[SQL Server](https://docs.byteplus.com/docs/DataWind/SQL_Server) |
|Teradata |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[Teradata](https://docs.byteplus.com/docs/DataWind/Teradata) |
|Doris |Offline extraction, direct connection |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[Doris](https://docs.byteplus.com/docs/DataWind/Doris) |
|Damon |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[Damon](https://docs.byteplus.com/docs/DataWind/Damon) |
|TiDB |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[TiDB](https://docs.byteplus.com/docs/DataWind/TiDB) |
|GoldenDB |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[GoldenDB](https://docs.byteplus.com/docs/DataWind/GoldenDB) |
|OceanBase MySQL |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[OceanBase MySQL](https://docs.byteplus.com/docs/DataWind/OceanBase_MySQL) |
|OceanBase Oracle |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[OceanBase Oracle](https://docs.byteplus.com/docs/DataWind/OceanBase_Oracle) |
|Hive |Offline extraction |1.x<br><br>2.x<br><br>3.x<br><br>2.1.1\-cdh6.3.2 |SaaS, on\-premises deployment |\-\- |Supported |[Hive](https://docs.byteplus.com/docs/DataWind/Hive) |
|MaxCompute |Offline extraction |1.0<br><br>2.0 |SaaS, on\-premises deployment |\-\- |Supported |[MaxCompute](https://docs.byteplus.com/docs/DataWind/MaxCompute) |
|Transwarp Inceptor |Offline extraction, direct connection |\-\- |SaaS, on\-premises deployment |\-\- |\-\- |[Transwarp Inceptor](https://docs.byteplus.com/docs/DataWind/Transwarp_Inceptor) |
|StarRocks |Offline extraction, direct connection |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[StarRocks](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f6258c) |
|Huawei FusionInsight |Offline extraction |\-\- |SaaS, on\-premises deployment |V2.56.1 |Supported |[Huawei FusionInsight](https://docs.byteplus.com/docs/DataWind/Huawei_FusionInsight) |
|Tencent Cloud DLC |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[腾讯云 DLC](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f625c2) |
|DataFinder |Direct connection |\-\- |SaaS, on\-premises deployment |**On\-premises deployment**:<br><br>Finder requires V4.3.0;<br><br>DataWind requires V2.50.0<br><br>**SaaS:** <br><br>Finder must be the cloud\-native version |Not supported |[DataFinder](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f627aa) |
|LAS (public cloud version) |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Supported |[LAS](https://docs.byteplus.com/docs/DataWind/LAS) |
|Intelligent outbound calling |Offline extraction |Intelligent outbound calling requires versions from December 2022 and later |SaaS, on\-premises deployment |Intelligent outbound calling: versions after December 2022;<br><br>DataWind: V2.54.0 version |\-\- |[Intelligent Outbound Calling](https://docs.byteplus.com/docs/DataWind/109753) |
|Ocean Engine/Qianchuan |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Not supported |[Juliang Engine/Juliang Qianchuan](https://docs.byteplus.com/docs/undefined/6a057f1efd1222050e7c4e74) |
|REST API |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Not supported |[REST API 2.0](https://docs.byteplus.com/docs/DataWind/REST_API_2_0) |
|Content platform |Offline extraction |\-\- |SaaS, on\-premises deployment |V2.44.0 |Not supported |[Content Management Platform（BytePlus没有上，不发布）](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62726) |
|MongoDB |Offline extraction |4.4.4<br><br>5.0.9 |SaaS, on\-premises deployment |\-\- |Supported |[MongoDB](https://docs.byteplus.com/docs/DataWind/MongoDB) |
|WeChat Official Account |Offline extraction |\-\- |SaaS, on\-premises deployment |SaaS cloud hosting: after 2024.4.11<br><br>On\-premises deployment: V2.68.0 |Not supported |[WeChat Official Account](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f6273f) |
|Constellation data |Direct connection |\-\- |SaaS, on\-premises deployment |SaaS cloud hosting: after 2024.4.11<br><br>On\-premises deployment: V2.68.0 |Not supported |[Constellation data](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f627a4) |
|Calendar data |Direct connection |\-\- |SaaS, on\-premises deployment |SaaS cloud hosting: after 2024.4.11<br><br>On\-premises deployment: V2.68.0 |Not supported |[Calendar data](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f627a6) |
|Feishu Sheets |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Not supported |[Lark Sheets](https://docs.byteplus.com/docs/DataWind/Lark_Sheets) |
|Feishu Bitable |Offline extraction |\-\- |SaaS, on\-premises deployment |\-\- |Not supported |[Lark Base Table](https://docs.byteplus.com/docs/DataWind/Lark_Base_Table) |
|Feishu Project Data (Meego) |Offline extraction |\-\- |SaaS, on\-premises deployment |V2.72.0 |Not supported |Feishu project (Meego) data |
|Alibaba Cloud OSS |Offline extraction |\-\- |SaaS, private deployment |V2.74.0 |Not supported |[Alibaba Cloud OSS](https://docs.byteplus.com/docs/DataWind/Alibaba_Cloud_OSS) |
|Tencent Cloud COS |Offline extraction |\-\- |SaaS, private deployment |V2.74.0 |Not supported |[Tencent Cloud COS](https://docs.byteplus.com/docs/DataWind/Tencent_Cloud_COS) |
|Volcengine TOS |Offline extraction |\-\- |SaaS, private deployment |V2.74.0 |Not supported |[Volcano Engine TOS](https://docs.byteplus.com/docs/DataWind/Volcano_Engine_TOS) |
|Transwarp ArgoDB |Offline extraction, direct connection |5.2 |SaaS, private deployment |V2.78.0 |Not supported |[Transwarp ArgoDB](https://docs.byteplus.com/docs/DataWind/Transwarp_ArgoDB) |
|VastBase |Offline extraction |G100 2.2.10<br><br>G100 2.2.15 |SaaS, private deployment |V2.78.0 |Not supported |[VastBase](https://docs.byteplus.com/docs/DataWind/VastBase) |
|Hetu |Offline extraction, direct connection |3.3 |SaaS, private deployment |V2.78.0 |Not supported |[Hetu](https://docs.byteplus.com/docs/DataWind/Hetu) |
|Gbase 8a jdbc |Offline extraction |\-\- |SaaS, private deployment |V2.83.0 |Supported |[Gbase 8a jdbc](https://docs.byteplus.com/docs/DataWind/Gbase_8a_jdbc) |
|KingbaseES |Offline extraction, direct connection |v9 General Market Edition \- MySQL compatible mode |SaaS, private deployment |V2.91.0 |Supported |[KingbaseES](https://docs.byteplus.com/docs/DataWind/KingbaseES) |


<span id="ac884d50"></span>
# Quickly connect to BytePlus databases and data warehouse data sources

This section describes the general configuration for quickly connecting to BytePlus database\-type and data warehouse\-type data sources. For guidance on connecting database\-type data sources and other types of data sources, see [All supported data sources](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview#48e13267).

**Operation steps**:


1. Go to BytePlus DataWind product. Click a specific project to enter it, click **Data Preparation**, and in the dropdown list, click **Data Connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select the type of data source to connect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1d086ec19494982811166d167852b83~tplv-goo7wpa0wc-image.image) </span>

3. Configure the connection information. The following example demonstrates connecting to a MySQL database. The sample values provided in the parameter descriptions are for reference only; please replace them with your actual parameter values when using.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90a505ae3e614174af485bdbc0d47f69~tplv-goo7wpa0wc-image.image) </span>

   The relevant parameter configuration instructions are as follows:

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Data connection name |The display name shown in the custom data source configuration list. |Demo data source |
   |Server |Enter the IP address. |10.225.34.22 |
   |Port |Enter the correct port number. |3306 |
   |Username |The username for the database. |DataWind_admin |
   |Password |The password for the database. |DataWind_password123 |
   |Permission mode |Supports both read and write modes. Please ensure that the permission mode you enter matches the actual permissions you have for the data source. |Read |
   |vpcMode |Whether to use VPC mode (private network mode). Usage scenarios are as follows:<br><br><br>* **Enable VPC mode**: For data sources that are **Volcengine databases or data warehouse products**, **it is recommended to use VPC mode**. Set vpcMode to **Yes**, and enter the VPC ID. For instructions on obtaining the VPC ID, refer to [Obtain the VPC ID](https://docs.byteplus.com/docs/DataWind/Access_Regions_and_BytePlus_Intranet_Connection#06269f9c).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use VPC mode for Volcengine products to ensure data security and avoid additional data transfer costs.   </div><br>   <br><br>* **Disable VPC mode**: If your data source has enabled public network access, there is no need to set vpcMode; you can set it to No. |No |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The example values provided are for reference only and cannot be used directly as valid connections.   </div>
   

4. Click **Connection Test** in the upper right corner to test the connectivity of the data source. After a successful test, click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d241ca558acc4d45a9351e61bad235da~tplv-goo7wpa0wc-image.image) </span>

5. Find the created data connection on the Data Preparation page.

   In the data connection directory in the left\-side list, you can filter and search according to your permissions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d31eadb71765417cada6ed96c45ddb3c~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature is supported in v2.54.0 and later versions.   </div>
   

&nbsp;
