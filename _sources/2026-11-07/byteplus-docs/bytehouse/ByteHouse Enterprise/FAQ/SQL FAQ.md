---
title: "SQL FAQ"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/sql-faq"
---

<span id="q1-bytehouse-企业版是否兼容-clickhouse-社区版？"></span>
## Q1: Is ByteHouse Enterprise compatible with ClickHouse Community Edition?

ByteHouse Enterprise is fully compatible with ClickHouse 23.3, and partially compatible with other versions.

For versions lower than or higher than ClickHouse 23.3, ByteHouse does not guarantee compatibility. The main risks stem from changes in default behaviors of configuration parameters, functions, and other elements during the evolution of ClickHouse Community Edition.

<span id="q2-bytehouse-企业版的表引擎和社区是否有差异？"></span>
## Q2: Are there any differences in table engines between ByteHouse Enterprise and the ClickHouse Community Edition?

Engines supported by ByteHouse can be found in the [official website documentation](https://docs.byteplus.com/en/docs/bytehouse/intro). Meanwhile, ByteHouse also supports all community engines, as detailed in the [community documentation](https://clickhouse.com/docs/en/engines/table-engines/).

Additionally, ByteHouse has developed three engines based on real\-world scenario demands. For details, refer to [HaMergeTree](https://docs.byteplus.com/docs/bytehouse/hamergetree), [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree), and [HaKafka](https://docs.byteplus.com/docs/bytehouse/hakafka).

<span id="q3-bytehouse-企业版支持哪些数据类型？"></span>
## Q3: What data types does ByteHouse Enterprise support?

ByteHouse supports all community data types, as detailed in the [Common data types](https://docs.byteplus.com/docs/bytehouse/common-data-types).

In addition, ByteHouse has also developed [MAP type](https://docs.byteplus.com/docs/bytehouse/map-type) and [BitEngine](https://docs.byteplus.com/docs/bytehouse/bitengine) types based on actual scene demands.

<span id="e0d3b1f9"></span>
## Q4: How should the ILLEGAL_COLUMN (Code: 44) error be handled?


* **Error message**:

   ```SQL
   Cannot create table with column 'xx' which type is 'Object('json')' because experimental Object type is not allowed. Set setting allow_experimental_object_type = 1 in order to allow it 
   ```
   

* **Reason**:

   This error occurs because ByteHouse does not allow the use of the experimental Object type by default.

* **Solution**:

   You can allow the use of the experimental Object type by setting the session\-level parameter `allow_experimental_object_type = 1`. The usage example is as follows:

   ```SQL
   SET allow_experimental_object_type = 1;
   ```
