---
title: "Power BI (MySQL)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/power-bi-mysql"
---

Power BI is a powerful business intelligence tool developed by Microsoft. It allows users to visualize and analyze data to make informed business decisions. Users can create interactive and customizable dashboards, reports, and visualizations.

<span id="79bed01e"></span>
## Background information

ByteHouse allows you to connect to it via Power BI using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="1e0e20d9"></span>
## Prerequisites


1. Operating System and Environment Requirements:

   1. Only supports the 64\-bit (x64) platform of Windows 11, Windows 10, Windows Server 2012 R2, Windows Server 2012, Windows 8, Windows 8.1, Windows Server 2016, Windows Server 2019;

   2. The system uses Internet Explorer 10 or higher versions.

2. Install Power BI Gateway. Please refer to the [official document](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-install#download-and-install-a-standard-gateway) for installation.

3. A ByteHouse account.


<span id="75d0ae04"></span>
## Configure and use ByteHouse and PowerBI


1. After entering Power BI, access Get data \> more \> Search MySQL, and you can see the MySQL database Datasource.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/069bb7c5d611487fa482875b9d06faf0~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the connection information for ByteHouse.

   1. Server: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.

   2. Database: Fill in the connected Database name.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccd25b90b3ae43d09ebbbaf537ddf744~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the authentication information for ByteHouse. Please refer to [Retrieve API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d9bd3430) to get the API key.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14b9c921d8f342cdab480294d6b696fa~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |UserName |It is recommended to create a new API Key for connection. You can go to **ByteHouse Console** \> **Tenant management** \> **Connection information** to create a new API Key. For details, refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br>The User Name is the first part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `xxxx`. |UserName combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br><br>* `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>* `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Permission Management** \> **Users**.<br><br>* `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>   Examples:<br><br>   * Default env: `30xxxxxxxx::demouser`<br><br>   * Other env: `30xxxxxxxx::demouser::demoenv` |
   |Password |The Password is the second part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `yyyy`. |You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

4. After a successful connection, load the corresponding database tables.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02c84498ad9544ec87355e732d73dfe0~tplv-goo7wpa0wc-image.image) </span>


<span id="6033757c"></span>
## Test dataset Demo

<span id="d5d0a650"></span>
### DDL

```SQL
CREATE database IF NOT EXISTS hamster_odbc;
DROP table IF EXISTS hamster_odbc.all_types;
CREATE table IF NOT EXISTS hamster_odbc.all_types (
    c1 Int8,
    c2 Int16,
    c3 Int32,
    c4 Int64,
    c5 Float32,
    c6 Float64,
    c7 String,
    c8 Nullable(String),
    c9 Date,
    c10 DateTime,
    c11 UUID,
    c12 Array(Int8),
    c13 Enum8('v1'=1, 'v2'=2),
    c14 Enum16('v3'=1, 'v4'=2),
    c15 Decimal(2, 2),
    c16 FixedString(2),
    c17 Tuple(s String, i Int64),
    c18 Map(String, String)
) ENGINE = CnchMergeTree ORDER BY c1;

INSERT INTO hamster_odbc.all_types
(c1,c2,c3,c4,c5,c6,c7,c8,c9,c10,c11,c12,c13,c14,c15,c16,
--c17,
c18)
VALUES (
    127,
    32767,
    2147483647,
    9223372036854775807,
    100000.1,
    14000000000.1,
    'OK',
    NULL,
    '2022-12-30',
    '2022-12-30 13:44:17',
    417ddc5d-e556-4d27-95dd-a34d84e46a50,
    [1,2,3,4],
    'v1',
    'v3',
    4.20,
    'b\0',
--    ('a', 1),
    {'key1': 'value1', 'key2': 'value2'}
), (
    100,
    3200,
    2147483647,
    9223372036854775807,
    100000.1,
    14000000000.1,
    'OK',
    NULL,
    '2022-12-31',
    '2022-12-30 13:44:17',
    417ddc5d-e556-4d27-95dd-a34d84e46a50,
    [1,2,3,4],
    'v1',
    'v3',
    4.20,
    'b\0',
--    ('a', 1),
    {'key1': 'value1', 'key2': 'value2'}
), (
    100,
    3200,
    2147483647,
    9223372036854775807,
    100000.1,
    14000000000.1,
    'OK',
    NULL,
    '2022-12-29',
    '2022-12-30 13:44:17',
    417ddc5d-e556-4d27-95dd-a34d84e46a50,
    [1,2,3,4],
    'v1',
    'v3',
    4.20,
    'b\0',
--    ('a', 1),
    {'key1': 'value1', 'key2': 'value2'}
);
DROP TABLE IF EXISTS hamster_odbc.range_key_dictionary_source_table;
CREATE TABLE IF NOT EXISTS hamster_odbc.range_key_dictionary_source_table ( `key` UInt64, `value` String, `value_nullable` Nullable(String) ) ENGINE=CnchMergeTree() PRIMARY KEY tuple() ORDER BY tuple();
INSERT INTO hamster_odbc.`range_key_dictionary_source_table` VALUES (1, 'OK', NULL), (2, 'OK', 'OK');
DROP DICTIONARY IF EXISTS hamster_odbc.range_key_dictionary;
CREATE DICTIONARY hamster_odbc.range_key_dictionary (
  `key` UInt64,
  `value` String,
  `value_nullable` Nullable(String)
) PRIMARY KEY `key` SOURCE(
  CLICKHOUSE(USER 'default' TABLE 'range_key_dictionary_source_table' PASSWORD '' DB 'hamster_odbc')
) LIFETIME(MIN 10 MAX 20) LAYOUT(FLAT());
```


<span id="789bda5f"></span>
### DQL

When adding data through ODBC, write the SQL statement.

```SQL
select 
ifNull(c7, 'was_null'),
ifNull(c8, 'OK'),
JSONExtractString('{"a": "OK", "b": [-100, 200.0, 300]}', 'a'),
multiIf(c7='OK', c7, 'a'='a', 'issue', 'issue'),
multiIf('a'='c', 'issue', c8 IS NULL, 'OK', 'issue'),
multiIf('a'='c', 'issue', c8='OK', 'issue', 'OK'),
if(c10=toDateTime('2022-12-30 13:44:17'), 'OK', 'issue'),
if(c10=toDateTime(1672407857, 'UTC'), 'OK', 'issue'),
if(date_trunc('hour', c10)=toDateTime('2022-12-30 13:00:00'), 'OK', 'issue'),
if(date_trunc('month', c10)=toDateTime('2022-12-01 00:00:00'), 'OK', 'issue'),
if(year(c10)=2022, 'OK', 'issue'),
if(month(c10)=12, 'OK', 'issue'),
if(date(c10)=toDateTime('2022-12-30 00:00:00'), 'OK', 'issue'),
case when 'a'='a' then 'OK' else 'issue' end,
case when 'a'='b' then 'issue' else 'OK' end,
if((SELECT argMin(c2, c1) FROM hamster_odbc.all_types)=3200, 'OK', 'issue'),
if((select uniqExactIf(number, number % 2 = 0) from numbers(100))=50, 'OK', 'issue'),
if((select max(c1) from hamster_odbc.all_types)=127, 'OK', 'issue'),
if(leftPad(c7, 5)='   OK', 'OK', 'issue'),
dictGetOrDefault('hamster_odbc.range_key_dictionary', 'value', toUInt64(1), 'issue') as dict_1,
dictGetOrDefault('hamster_odbc.range_key_dictionary', 'value', toUInt64(3), 'OK') as dict_2
from hamster_odbc.all_types limit 1;

select 
c1, c9,
leadInFrame(c9) OVER (PARTITION BY c1 ORDER BY c9 ASC ROWS
                 BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
from hamster_odbc.all_types;
```


The output of DQL is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c81e64301c0499abf33f1c165b0d2ea~tplv-goo7wpa0wc-image.image) </span>
