---
title: "Paged query performance optimization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Paged_query_performance_optimization"
---

This topic describes the paged query performance optimization feature of RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In the community edition of MySQL, limit and offset are processed at the SQL layer. For the following query, the storage engine returns at least 10,000,010 rows, and then the SQL layer returns rows from 10,000,001 to 10,000,010 as the result.

```sql
SELECT * FROM sbtest1 LIMIT 10000000, 10;
```


Limit and offset are typically used together in pagination scenarios. In pagination scenarios, especially for deep pagination where the number of rows skipped by offset is much larger than the number of rows retained by limit, the speed of filtering the skipped rows has a significant impact on overall query performance.

RDS for MySQL optimizes this scenario by pushing limit and offset directly to the storage engine. This approach significantly reduces interactions between the storage engine and the SQL layer. Furthermore, if the storage engine scans data through a secondary index, pushing down limit and offset can also greatly reduce the number of table lookups.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20250615 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250415 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If your instance's kernel minor version is not supported, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">manually upgrade the instance kernel version</a>.</div>


<span id=".5L2_55So6K-05piO"></span>
## Instructions

Modify the runtime value of the loose_limit_offset_pushdown_threshold parameter to a value other than \-1 to enable the paged query performance optimization feature.


|Parameter name |Default value |Does it need instance restart to take effect? |Value range |Scope |Parameter description |
|---|---|---|---|---|---|
|loose_limit_offset_pushdown_threshold |\-1 |No |[\-1, 9223372036854775807] |Global, Session |Specifies the minimum number of offset rows required to enable the paginated query performance optimization feature. Set to \-1 to always disable the paginated query performance optimization feature. |


<span id=".5L2_55So56S65L6L"></span>
## Examples


* Example 1: A simple limit + offset query.

   ```sql
   SELECT * FROM sbtest1 LIMIT 10000000, 10;
   ```
   

* Example 2: A limit + offset query with a where clause that can be fully pushed down.

   ```sql
   SELECT * FROM sbtest1 WHERE id > 10 AND id < 60000000 LIMIT 10000000, 10;
   ```
   

* Example 3: A limit + offset query with an order by clause, requiring an index on the ordered column that is used in the query plan.

   ```sql
   -- A secondary index exists on k
   SELECT * FROM sbtest1 ORDER BY k LIMIT 10000000, 10;
   ```
   

* You can use the EXPLAIN statement to check whether a SQL statement will be optimized for paged query performance.

   ```sql
   EXPLAIN SELECT c_int FROM lop_test ORDER BY c_int LIMIT 5, 5;
   ```
   

   The preceding statement can be optimized, and the output is as follows (`Using pushed limit offset` indicates that the pagination query performance is optimized):

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b5ea7439fdea0507383f500e9138e6d.png) </span>


&nbsp;

<span id=".5oCn6IO95rWL6K-V"></span>
## Performance test

The test environment is a 4\-core, 16 GB Exclusive type MySQL 8.0 instance. A sysbench table with 20,000,000 rows is created. The elapsed times for executing examples 1 to 3 before and after this feature is enabled are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f2d0ae8aaa2be00d48a79d8662216f8.png) </span>
