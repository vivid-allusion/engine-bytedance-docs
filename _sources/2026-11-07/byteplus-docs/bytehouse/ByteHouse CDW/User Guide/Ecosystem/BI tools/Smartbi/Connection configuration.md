---
title: "Connection configuration"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/smartbi-connection-configuration"
---

This tutorial introduces how to install different ByteHouse drivers on Smartbi and complete connection configuration.

<span id="6940f8e4"></span>
# Background information

ByteHouse allows you to connect to it via Smartbi using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="ff68dbe1"></span>
# Prerequisites


1. Make sure that Smartbi is installed and data has been imported into ByteHouse.

2. Obtain the driver for connecting to ByteHouse by choosing one of the following:

   1. [MySQL JDBC Driver](https://mvnrepository.com/artifact/mysql/mysql-connector-java) (included with Smartbi)

   2. [ClickHouse JDBC Driver](https://github.com/ClickHouse/clickhouse-java/releases/download/v0.4.6/clickhouse-jdbc-0.4.6.jar)

   3. [ByteHouse JDBC Driver](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/): Use the latest version.

   4. ClickHouse Data Source


<span id="c14e6171"></span>
# Configure drivers


1. Prepare one of the following drivers as needed:

   1. ClickHouse JDBC Driver: Create a ClickHouse folder and copy the corresponding JDBC Driver jar file into the directory.

   2. ByteHouse JDBC Driver: Create a ByteHouse folder and copy the corresponding JDBC Driver jar file into the directory.

2. Copy the required driver folders into the following directories:

   * `{Smartbi}/Tomcat/{user}/dynamicLibraryPath`

   * `{Smartbi}/smartbiOLAP/dynamicLibraryPath`


<span id="45703123"></span>
# Connection information

<span id="e19141c7"></span>
## Connect to ByteHouse using an IAM user


| |Driver class |Connection string |Driver directory |
|---|---|---|---|
|MySQL JDBC Driver |`com.mysql.jdbc.Driver` |jdbc:mysql://<HOST\>:3306/<database_name\>?useOldAliasMetadataBehavior=true&useUnicode=true&characterEncoding=UTF8&zeroDateTimeBehavior=convertToNull&useCursorFetch=true&defaultFetchSize=\-2147483648 |Bundled |
|ClickHouse JDBC Driver |`com.clickhouse.jdbc.ClickHouseDriver` |jdbc:clickhouse://<host\>:8123/<database_name\>?user=bytehouse&password=<API_Key\>&ssl=true&compress=0&server_version=54021&server_time_zone=Asia/Shanghai |ClickHouse |
|ByteHouse JDBC Driver |`com.bytedance.bytehouse.jdbc.ByteHouseDriver` |jdbc:bytehouse://<host\>:19000/<database_name\>?user=bytehouse&password=<API_Key\>&secure=true&compress=true |ByteHouse |
|ClickHouse |`ru.yandex.clickhouse.ClickHouseDriver` |jdbc:clickhouse://:8123/<database_name\>?socket_timeout=1000000&ssl=true&compress=0 |None |


**Parameter description:** 

When connecting with an IAM account, the common parameter configuration is as follows. For details, please see [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889).


* `<user>` : Set it as `bytehouse`.

* `<password>`: It refers to the API Key of ByteHouse, which can be obtained from **ByteHouse Console** \> **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).

* `<Host>` is configured as ByteHouse’s network domain name; you can check the information in ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

* SSL Tunnel: enabled.


<span id="e5c6d0d8"></span>
## Connect to ByteHouse using a database user


| |Driver class |Connection string |Driver storage directory |
|---|---|---|---|
|MySQL JDBC Driver |`com.mysql.jdbc.Driver` |jdbc:mysql://<HOST\>:3306/<database_name\>?useOldAliasMetadataBehavior=true&useUnicode=true&characterEncoding=UTF8&zeroDateTimeBehavior=convertToNull&useCursorFetch=true&defaultFetchSize=\-2147483648 |Built\-in |
|ClickHouse JDBC Driver |`com.clickhouse.jdbc.ClickHouseDriver` |jdbc:clickhouse://<host\>:8123/<database_name\>?user={accountID_or_accountName}::{username}[::{envID}]&password=&ssl=true&compress=0&server_version=54021&server_time_zone=Asia/Shanghai |ClickHouse |
|ByteHouse JDBC Driver |`com.bytedance.bytehouse.jdbc.ByteHouseDriver` |jdbc:bytehouse://<host\>:19000/<database_name\>?user={accountID_or_accountName}::{username}[::{envID}]&password=&secure=true&compress=true |ByteHouse |
|ClickHouse |`ru.yandex.clickhouse.ClickHouseDriver` |jdbc:clickhouse://:8123/<database_name\>?socket_timeout=1000000&ssl=true&compress=0 |None |


**Parameter description:** 

When connecting with a database account, general parameter configuration details are as follows.


* `<user>` consists of `{accountID_or_accountName}::{username}[::{envID}]`. For details, see [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889):

   * `{accountID_or_accountName}`: refers to the user account or name, which can be viewed and copied by logging into the ByteHouse console and clicking the personal center at the top right to find the account ID or name.

   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.

   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.

      Examples:

      * Default env: `30xxxxxxxx::demouser`

      * Other env: `30xxxxxxxx::demouser::demoenv`

* `<password>` is the password for the database account, set by the administrator when creating the account. You may contact the administrator to obtain the password. If the password is lost or forgotten, contact the administrator to reset it. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043).

* `<Host>` should be configured as the network domain name of ByteHouse, which you can find in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, please refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

* SSL Tunnel: enabled.


<span id="10c10129"></span>
# Configure data connection

<span id="3aff4284"></span>
## Connect using MySQL JDBC Driver


1. Log in to the Smartbi Enterprise Platform, select **Data Connection \> Relational Database**, then click the **MySQL** icon to enter the database connection interface. As shown below:

2. Enter the database information according to the configuration details provided in [Connection Information](https://docs.byteplus.com/docs/bytehouse/smartbi-connection-configuration#45703123).


<span id="1e9b6191"></span>
## Connect using ClickHouse JDBC Driver


1. Log in to the Smartbi Enterprise Platform, select **Data Connection \> All Databases**, then click the ByteHouse icon to enter the database connection interface.

2. Enter the corresponding database information based on the configuration provided in [Connection Information](https://docs.byteplus.com/docs/bytehouse/smartbi-connection-configuration#45703123). Select Clickhouse for "Choose driver type \- Custom".


<span id="f11cb601"></span>
## Connected via ByteHouse TCP JDBC Driver


1. Log in to the Smartbi Enterprise Platform, select **Data Connection** \> **All Databases**, and click the ByteHouse icon to enter the database connection interface.

2. Enter the corresponding database information based on the configuration provided in [Connection Information](https://docs.byteplus.com/docs/bytehouse/smartbi-connection-configuration#45703123). Select Bytehouse for "Choose driver type \- Custom".


<span id="0394ad21"></span>
## Connect directly using ClickHouse data source


1. Log in to the Smartbi Enterprise Platform, select **Data Connection \> All Databases**, and click the ClickHouse icon to enter the database connection interface.

2. Enter the corresponding database information based on the configuration provided in [Connection Information](https://docs.byteplus.com/docs/bytehouse/smartbi-connection-configuration#45703123). Select "Built\-in product" for the "Choose driver" option. As shown below:


<span id="afae0cdd"></span>
# **Test connection**


1. After entering the information correctly, click **Test Connection**. If the **Test Passed** popup appears as shown below, it means the database connection is successful. As shown below:

2. After a successful test connection, click the **Save** button in the lower right corner, choose the location to save the data source, and once saved, the data connection is added successfully.

3. After the database connection is successful, you can refer to Smartbi official [Getting Started](https://wiki.smartbi.com.cn/pages/viewpage.action?pageId=111897106) for data querying and management.


&nbsp;
