---
title: "Power BI (ODBC)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-power-bi"
---

Power BI is a powerful business intelligence tool developed by Microsoft. It enables users to visualize and analyze data to make informed business decisions. Users can create interactive and customizable dashboards, reports, and visualizations.

<span id="4bd57b28"></span>
## Prerequisites


1. Operating System and Environment Requirements:

   1. Supports only the 64\-bit (x64) platforms of Windows 11, Windows 10, Windows Server 2012 R2, Windows Server 2012, Windows 8, Windows 8.1, Windows Server 2016, Window Server 2019.

   2. The system uses Internet Explorer 10 or higher versions.

2. Install ClickHouse ODBC Driver version 1.2.1.20220905, you can obtain the installer [here](https://github.com/ClickHouse/clickhouse-odbc/releases/tag/v1.2.1.20220905).

3. Install Power BI Gateway. Refer to the [official document](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-install#download-and-install-a-standard-gateway) for installation.

4. Install the ClickHouse community's power\-bi\-clickhouse Connector for data analysis. Refer to the [official document](https://github.com/ClickHouse/power-bi-clickhouse?tab=readme-ov-file#installation) for installing ClickHouse ODBC Driver and power\-bi\-clickhouse.

5. Have a ByteHouse account.


<span id="19223be2"></span>
## Configuration and Usage


1. Activate Custom connector. In PowerBI Cloud, activate power\-bi\-clickhouse; custom connector needs to be enabled. The folder for Custom Connectors needs remote access permission; the default granted object is *NT SERVICE\PBIEgwService*.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0539258de98a4ce381fdc98b341cf74c~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad303f31c7854de290de1fdd4a6ff9fe~tplv-goo7wpa0wc-image.image) </span>

2. Verify whether the Custom Connector was successful. If this information does not appear in Connectors, try to restart the Gateway.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6b89d5221b5433aad8eaf984af4fc74~tplv-goo7wpa0wc-image.image) </span>

3. PowerBI adds a datasource.

   After entering PowerBI, access Get data \-\> More \-\> Search ClickHouse, and you can see the ClickHouse(Beta)(Custom) datasource.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef25ee9d62ec4f87abc82e47c10da9d0~tplv-goo7wpa0wc-image.image) </span>

4. Fill in the connection information for Bytehouse.

   1. Server: Please refer to [Supported cloud providers and regions](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers) to get the HOST address.

   2. Port: Default is `8123`.

   3. Database: Fill in the database name for the connection.

   4. Options: Fill in `SSLMode=require`.

   5. Check the `DirectQuery` option.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38e382ce641a4ce3a3a01a294d87f239~tplv-goo7wpa0wc-image.image) </span>

5. Fill in the authentication information for Bytehouse.

   1. UserName: Default is bytehouse.

   2. Password: API key. Refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d27e296c51342dabad36b1e497b94b3~tplv-goo7wpa0wc-image.image) </span>

6. After the connection is successful, load the corresponding database table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c13d45de93b640e6a65aef8fcc9e2ec1~tplv-goo7wpa0wc-image.image) </span>


<span id="d3bd6ba6"></span>
## Test data set demo

<span id="44d382f4"></span>
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


<span id="24b615e8"></span>
### DQL

When adding data via ODBC, write it into the SQL statement.

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
