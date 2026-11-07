---
title: "Manually deploying high-performance databases: selection and performance test"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-high-performance-database-instance-type-selection-and-performance-tests"
---

This topic describes how to select ECS instances to manually deploy various high\-performance databases.

<span id=".5LiA44CB5Zy65pmv5o-P6L-w"></span>
## Scene description

Databases have been a core component in building modern applications, since almost all applications start from and end with data. As the data\-driven era comes, data is everywhere and further serves as a cornerstone for future innovation.

With the growing trends toward microservice\-oriented applications and data diversification, one type of database can no longer meet the needs of modern applications. As a result, various purpose\-built databases appear, including relational databases, key\-value databases, document databases, in\-memory databases, graph databases, time\-series databases, wide\-column databases, and ledger databases.

As the data mesh concept is introduced, data management platforms are shifting from centralized models to customization based on business lines (LOBs)​. Businesses customize solutions based on their needs to build a data management platform with high availability, high performance, and rich features. This type of platform has higher infrastructure requirements.

<span id=".5LqM44CB5pWw5o2u5bqT6YCJ5Z6L"></span>
## Select a database

The following table shows the features and corresponding products of different database types. Select an appropriate database product based on your actual business needs.


|Database type |Feature |Application |Database product​s |
|---|---|---|---|
|Relational database |High data accuracy, high continuity​, support for transactions, and unlimited indexes. |Traditional applications, ERP, CRM, transaction systems, data warehouses |PostgreSQL, MySQL, MariaDB, Oracle Database, SQL Server |
|Key\-value database |High\-concurrency read/write capabilities and flexible data structures. |High\-traffic web applications, e\-commerce shopping carts, games, live streaming, real\-time bidding, product catalogs, customer preference storage |Redis, TiKV |
|In\-memory database |Sub\-millisecond latency, millions of operations per second, support for multiple programming languages, and compatibility with various databases. |Caching, session management, game leaderboards, geolocation information, real\-time analytics |Redis, Memcached |
|Document database |Flexible structure, support for semi\-structured data, hierarchization, fast querying, and powerful indexing capabilities. |Content management, customer profiles, user configuration files, personalization, mobile applications |MongoDB, Couchbase |
|Wide\-column database |Flexible structure, high scalability, and support for larger single\-row data. |Large\-scale industrial applications for equipment maintenance, queue management, and route optimization, real\-time data analytics |Cassandra |
|Graph database |Optimized for strongly relational data, with efficient query and traversal capabilities. |Fraud detection, social networks, recommendation engines, data lineage, knowledge graphs |Neo4j, dgraph |
|Time\-series database |High scalability, suitable for rapidly growing data, and capable of monitoring data changes. |IoT applications, industrial telemetry, DevOps, application monitoring |influxDB, QuestDB, TimescaleDB |
|Ledger database |High accuracy, transparency, immutability, auditability, and high scalability. |System records, supply chains, registrations, banking transactions, HR and payroll systems, retail, insurance, manufacturing |Amazon QLDB, Alicloud LedgerDB |


<span id=".5LiJ44CB5oCn6IO95rWL6K-V"></span>
## Run a performance test

After determining the database type, you can run a performance test to confirm the database configuration.

<span id=".54Gr5bGx5byV5pOO5Z-656GA546v5aKD5p6E5bu6"></span>
### Build a basic environment

Follow [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create ECS instances. In the example provided in this topic, the configurations of created instances are as follows:


* Basic configuration:

   * Instance type: ecs.r3il.xlarge

   * Image: Windows Server

   * Storage: System volume capacity \> 100 GiB

* Network configuration: Select "Assign Elastic IP (EIP)".

* Quantity: 2.

* Instance name: HammerDB\-01 and HammerDB\-02, respectively.


<span id=".6YOo572y5rWL6K-V5bel5YW3SGFtbWVyREI="></span>
### Deploy a HammerDB test tool

Deploy HammerDB on the instance named HammerDB\-01.


1. Log in to the instance HammerDB\-01 via VNC. For detailed steps, refer to [Logging in to a Windows instance through ECS console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

3. Press Ctrl + Alt + Del at the same time. Or, as shown in the picture below, click the icons in the labeled order. Then, the interface with a password text box appears. Enter the password to remotely log in to the instance.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d9b4516e6550f36941cc312a6b23502a) </span>

4. Open the IE browser and, in the address bar, manually input https://www.hammerdb.com/download.html to download and install HammerDB test software.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d89820b55aa199dfdfb28948f07de9f8) </span>

5. After the download, double\-click the software installation package to install HammerDB. Then, follow the guidance of the installation wizard to complete the installation.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_abe5c5563cf6e00b8794d8a574b199e5) </span>

   If the following output is displayed, the installation is completed.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3d279c578a967242fb909f1467e3142e) </span>

6. Open a new page in the IE browser and, in the address bar, input https://go.microsoft.com/fwlink/?linkid=2168524 to download SQL Server ODBC Driver 17. Then, follow the guidance of the installation wizard to complete the installation.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5731f0421cfd8acccb26e1f0674dc904) </span>


<span id=".6YOo572y5pWw5o2u5bqT"></span>
### Deploy a database

Deploy SQL Server 2019 on the instance HammerDB\-02.


1. Log in to the instance HammerDB\-02 via VNC. For detailed steps, refer to [Logging in to a Windows instance through ECS console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Follow Step 3 in the "Deploy a HammerDB test tool" section, and log in to the instance HammerDB\-02.

3. Open the IE browser and, in the address bar, manually input https://www.microsoft.com/zh\-cn/sql\-server/sql\-server\-downloads to download SQL Server 2019.

4. Select the installation type of "Basic".

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_7b676540a08d004f94ee144079f3d525) </span>

   Click "Accept" to continue the installation until it is completed.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8350ec9414f1be929d3e7cb8a2477ca2) </span>

5. On the SQL Server 2019 download page in IE browser, scroll down to the "SQL tools and drivers" section, and click "Download now" in the "SQL Server Management Studio" section.

6. The page will then redirect to the download page. Click as shown in the picture below to download SQL Server Management Studio (SSMS) 18.10.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d42b0f4ceb0b765a9c8eb0f2eab2d7a9) </span>

7. Install SSMS as guided by interface prompts. After SSMS is installed, restart the instance.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ef8710c96e06064c87390ba5180c5831) </span>

8. Configure SQL Server.

   1. Click as shown in the picture below to open SQL Server Configuration Manager.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a05a733fdf51775bdaa4a193ffc66cd0) </span>

   2. In the "Sql Server Configuration Manager" window, under the "Status" column, right\-click "Disabled" of "Named Pipes" and "TCP/IP" respectively, to change statuses to "Enabled". After this, Named Pipes and TCP/IP protocols are enabled.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_417141749334f61f6f83683cb35d421b) </span>

9. Click as shown in the picture below to use SSMS to access the database.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e6ee5e9ad326e468753b1998f04a8182) </span>

10. Click "Connect" to connect to the database.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ab5db1648d7d8a804bec9989b65fea53) </span>

11. Right\-click the database name, and click "Properties" to set properties.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ec576ef7039686267cca37a7cd1bf676) </span>

12. Click "Security" to enter the "Security" page, select "SQL Server and Windows Authentication mode", and then click "OK". In the dialog box that pops up, click "OK".

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_7a179df0c54304ea99becf405f18a9bf) </span>

13. Right\-click "Database \> New Database" to create a new database.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_71ca917a1401a13cae3d3a0c98ee659e) </span>

14. Operate as shown in the picture below to create a database named "tpcc". After the database is created, click "OK".

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_435264c3f55d326b70dd76a05d599ed3) </span>

15. Under the "Security" directory, right\-click "Logins \> New Login".

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c66b7379d9b1528885d221cc493637c2) </span>

16. Operate as shown in the picture below to create the user "tpcc\-test". At this time, do not click "OK".

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f6fe913fd4c93ba6c9f41be8a5f71bb5) </span>

17. Click "User Mapping", check "tpcc", and click "OK".

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c9c3855e386e0e8e5f3f11073affe71e) </span>


<span id=".55Sf5oiQ5rWL6K-V5pWw5o2u"></span>
### Generate the test data

Use the HammerDB tool to generate the test data.


1. Remotely connect to the instance HammerDB\-01 with HammerDB installed, and then open HammerDB.

2. Double\-click "SQL Server", select "TPCC\-C", and then click "OK".

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ee1484000fe9403aa2c30664ac237de1) </span>

3. Double\-click "TPROC\-C", double\-click "Schema Build" in the displayed directory, and then double\-click "Options" in the expanded directory.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3a88915419f2ebc5571fab01c84d0b00) </span>

4. In the "Microsoft SQL Server TPROC\-C Build Options" box, enter the private IP address of instance HammerDB\-02 (where SQL Server is installed), along with the account and password of the tpcc\-test database. Set a desired number of Warehouses (determines the size of test data generated in the database) and the number of virtual accounts for parallel insertion. After configuration, click "OK."


> You can obtain the private IP address of the instance on the Instances page in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/dashboard).



<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f7fcaffbc7534af56e379c17fe0f9e2a) </span>

5. Double\-click "Build", and in the pop\-up dialog box, click "Yes".

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_869818d4fc23776e5970bc51acb67bdf) </span>

6. The test data insertion starts. This process may take several hours.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_59c351fa15c20cc196d8a147202365af) </span>

   If the following output is displayed, the data insertion process is complete.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b3c4420a8fe177403807d99cc53f5d32) </span>

7. Click the red square to destroy the virtual client.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_aa9e08339f31f59470babc5393a33f99) </span>


<span id=".5byA5aeL5rWL6K-V"></span>
### Start the test


1. As shown below, click "Load" to load the test script.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_aa9284a43a84e53da566586b83786ae2) </span>

2. As shown below, click "Options" under "Virtural User". In the pop\-up dialog box, set the number of clients to test for the "Virtual Users" parameter (the larger the number, the higher the concurrency). Then, configure the action intervals in "User Delay", along with "Repeat Delay" (the smaller the values, the more frequent the operations), and click "OK".

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_83e7e80842d54b2bed505805f70b4df7) </span>

3. Double\-click "Create" to create a virtual client.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_159bda3cd463ccb7133adec33dfaa5c2) </span>

4. Double\-click "Run" to start the test.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_abab988dcb5376ec353492bcf51e59ed) </span>

5. Click to open "Transaction Counter" to view TPM.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c654ed7a1b16fb16894505fabada064e) </span>


<span id=".5rWL6K-V5oC757uT"></span>
### Summarize the test

We can obtain performance test results as accurate as possible by averaging the results of multiple tests on the same instance type. By thoroughly testing the performance of cloud services across instances of different types, you can apply the most cost\-effective solution to deploy different databases.
