---
title: "Connection Configuration"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/fine-bi-connection-config"
---

This article explains how to install different ByteHouse drivers on Fine BI and complete the connection configuration.

<span id="08c24c10"></span>
# Background information

ByteHouse allows you to connect to it via FineBI using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="27408a72"></span>
# Prerequisites

Install FineBI according to [Environment preparation](https://docs.byteplus.com/docs/bytehouse/fine-bi-env-preparation) and datasource configuration is complete.

<span id="ef1b5125"></span>
# Connection Information

<span id="b06dd6aa"></span>
## Use IAM user


| |Driver class |Connection string |Port |Other configurations |
|---|---|---|---|---|
|MySQL JDBC Driver5 |System default driver |Automatic Generation |3306 |Your_Database?enabledTLSProtocols=TLSv1.2,TLSv1.3 |
|MySQL JDBC Driver8 |`com.mysql.jdbc.Driver` |Automatically generated |3306 | |
|ClickHouse JDBC Driver |`com.clickhouse.jdbc.ClickHouseDriver` |jdbc:clickhouse://<host\>:8123/<database_name\>?user=bytehouse&password=<API_Key\>&ssl=true&compress=0&server_version=54021&server_time_zone=Asia/Shanghai |8123 | |
|ByteHouse JDBC Driver |`com.bytedance.bytehouse.jdbc.ByteHouseDriver` |jdbc:bytehouse://<host\>:19000/<database_name\>?user=bytehouse&password=<API_Key\>&secure=true&compress=true |19000 | |
|ByteHouse HTTP JDBC Driver |`com.bytedance.jdbc.ByteHouseDriver` |jdbc:clickhouse://<host\>:8123/<database_name\>?user=bytehouse&password=<API_Key\>&ssl=true&compress=false&server_version=54021&server_time_zone=Asia/Shanghai |8123 | |


Parameter description:

When connecting with an IAM account, the general parameter configuration details are as follows. For more information, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889).


* `<user>`: Set as `bytehouse`.

* `<password>`: Use the API Key of ByteHouse, which can be obtained in **ByteHouse Console** \> **Tenant management** \> **Connection information**. For details, refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).

* `<Host>`: Configure as the public network connection domain name of ByteHouse, which can be viewed in **ByteHouse Console** \> **Tenant management** \> **Basic information** \> **Network information**. For details, refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

* **SSL Tunnel**: Set it as true.


<span id="62858d81"></span>
## Use database use


| |Driver class |Connection string |Port |Other configurations |
|---|---|---|---|---|
|MySQL JDBC Driver5 |System default driver |Automatic Generation |3306 |Your_Database?enabledTLSProtocols=TLSv1.2,TLSv1.3 |
|MySQL JDBC Driver8 |`com.mysql.jdbc.Driver` |Automatically generated |3306 | |
|ClickHouse JDBC Driver |`com.clickhouse.jdbc.ClickHouseDriver` |jdbc:clickhouse://<host\>:8123/<database_name\>?user={accountID_or_accountName}::{username}[::{envID}]&password=&ssl=true&compress=0&server_version=54021&server_time_zone=Asia/Shanghai |8123 |无 |
|ByteHouse JDBC Driver |`com.bytedance.bytehouse.jdbc.ByteHouseDriver` |jdbc:bytehouse://<host\>:19000/<database_name\>?user={accountID_or_accountName}::{username}[::{envID}]&password=&secure=true&compress=true |19000 |无 |
|ByteHouse HTTP JDBC Driver |`com.bytedance.jdbc.ByteHouseDriver` |jdbc:clickhouse://<host\>:8123/<database_name\>?user={accountID_or_accountName}::{username}[::{envID}]&password=&ssl=true&compress=false&server_version=54021&server_time_zone=Asia/Shanghai |8123 |无 |


Parameter description:

When connecting with a database account, the general parameter configuration details are as follows:


* `<user>`: Composed of `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889):

   * `{accountID_or_accountName}`: Refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.

   * `{username}`: The username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.

   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.

      Examples:

      * Default env: `30xxxxxxxx::demouser`

      * Other env: `30xxxxxxxx::demouser::demoenv`

* `<password>`: The password for the database account, which is custom\-configured by the administrator when creating the database account. Contact your administrator to obtain the password. If the password is lost or forgotten, contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043).

* `<Host>`: Configure as the public network connection domain name of ByteHouse. You can view the corresponding information in **ByteHouse Console** \> **Tenant Management** \> **Basic Information** \> **Network Information**. For details, refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

* **SSL Tunnel**: Set it as true.


<span id="5ff40dc9"></span>
# Configure data connection

<span id="1e82c1bc"></span>
## Connect via MySQL JDBC Driver5


1. Log in to the Fine BI Console, click "manage System\>Data Connection\>Data Connection Management \> Create New Data Connection" to create a new data connection, select the built\-in MySQL driver.

2. According to the **configuration information** provided, enter the corresponding database information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e2f997f16cd4b269a3b4efcdcc56c9b~tplv-goo7wpa0wc-image.image) </span>


<span id="d866f996"></span>
## Connect via MySQL JDBC Driver8


1. Log in to the Fine BI Console, click "manage System\>Data Connection\>Data Connection Management \> Create New Data Connection" to create a new data connection, choose the previously defined database type "MySQL".

2. According to the **configuration information** provided, enter the corresponding database information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8fe5c78e0a74763bd22bb7d0cabd740~tplv-goo7wpa0wc-image.image) </span>


<span id="32584eda"></span>
## Connect via ClickHouse JDBC Driver


1. Log in to the Fine BI Console, click "manage System\>Data Connection\>Data Connection Management \> Create New Data Connection" to create a new data connection, select the previously defined database type "ClickHouse".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4a92b9281024997a906bb02861c0b19~tplv-goo7wpa0wc-image.image) </span>

2. According to the **configuration information** provided, enter the corresponding database information.


<span id="abcb81c9"></span>
## Connect via ByteHouse TCP JDBC Driver


1. Log in to Fine BI Console, click "System Management\>Data Connection\>Data Connection Management \> New Data Connection" to create a new data connection, select the previously defined database type "ByteHouse".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ba3de8759184846a5c459a50bebf9fe~tplv-goo7wpa0wc-image.image) </span>

2. According to **connection information**, input the corresponding information for the database.


<span id="74cac48d"></span>
## Connect through ByteHouse HTTP JDBC Driver


1. Log in to Fine BI Console, click "System Management\>Data Connection\>Data Connection Management \> New Data Connection" to create a new data connection, select the previously defined database type "ByteHouseHTTP".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33b4878276b14802b50d3529f5c3d301~tplv-goo7wpa0wc-image.image) </span>

2. According to **connection information**, input the corresponding information for the database.
