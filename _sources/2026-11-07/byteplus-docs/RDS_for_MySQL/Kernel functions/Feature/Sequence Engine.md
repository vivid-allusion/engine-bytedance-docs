---
title: "Sequence Engine"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Sequence_Engine"
---

This topic describes the Sequence Engine provided by RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

RDS for MySQL provides Sequence Engine to obtain unique and auto\-incrementing sequence values. Sequence Engine is a logical engine that still uses the InnoDB storage engine for data persistence and is compatible with existing data backup and recovery tools. Through encapsulation, the upper layer realizes the functions of sequence value generation, caching, and so on.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20241215 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250215 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5Yib5bu6LXNlcXVlbmNl"></span>
## Creating a Sequence

Use the `CREATE SEQUENCE` statement to create a Sequence.

```sql
CREATE SEQUENCE [IF NOT EXISTS] <数据库名>.<Sequence名称>
    [START WITH <constant>]
    [MINVALUE <constant>]
    [MAXVALUE <constant>]
    [INCREMENT BY <constant>]
    [CACHE <constant> | NOCACHE]
    [CYCLE | NOCYCLE]
;
```


The parameters in the statement are described as follows:


|Parameter |Description |Default value |
|---|---|---|
|START WITH |The starting value of the sequence.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">`START WITH` must be greater than or equal to `MINVALUE` and less than `MAXVALUE`.</div><br> |1 |
|MINVALUE |The minimum value of the Sequence.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">MINVALUE must be less than or equal to MAXVALUE.</div><br> |1 |
|MAXVALUE |The maximum value of the Sequence.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">MAXVALUE must be greater than or equal to MINVALUE.</div><br> |9223372036854775807 |
|INCREMENT BY |The increment value (compensation) for the sequence.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">`INCREMENT BY` must be greater than or equal to 1.</div><br> |1 |
|CACHE \| NOCACHE |The size of the Sequence cache. It improves performance by avoiding disk data updates every time nextval is obtained. Data in the cache is lost after a restart, and `nextval` jumps to the value of the next cache. |10000 |
|CYCLE \| NOCYCLE |Specifies whether the sequence can restart from `MINVALUE` after reaching its limit. |0 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The preceding parameters cannot be negative.</div>


&nbsp;

For compatibility with the MySQL Dump backup method, you can also create a Sequence by using `Engine=Sequence`. Specify the Sequence parameters by inserting an initial data row. The parameters are based on the first record. Users can download, back up, and restore a Sequence created with `Engine=Sequence` using tools such as MySQL Dump. Example as follows:

```sql
CREATE TABLE <数据库名>.<Sequence名称> (
  `currval` bigint(21) NOT NULL COMMENT 'current value',
  `nextval` bigint(21) NOT NULL COMMENT 'next value',
  `minvalue` bigint(21) NOT NULL COMMENT 'min value',
  `maxvalue` bigint(21) NOT NULL COMMENT 'max value',
  `start` bigint(21) NOT NULL COMMENT 'start value',
  `increment` bigint(21) NOT NULL COMMENT 'increment value',
  `cache` bigint(21) NOT NULL COMMENT 'cache size',
  `cycle` bigint(21) NOT NULL COMMENT 'cycle state',
  `round` bigint(21) NOT NULL COMMENT 'already how many round'
) ENGINE=Sequence DEFAULT CHARSET=latin1;
INSERT INTO <数据库名>.<Sequence名称> VALUES(0, 0, 1, 9223372036854775807, 1, 1, 10000, 0, 0);
```


<span id=".5Yig6ZmkLXNlcXVlbmNl"></span>
## Deleting a Sequence

You can delete a Sequence using the `DROP SEQUENCE` and `DROP TABLE` statements.


* Using the `DROP SEQUENCE` statement

   ```sql
   DROP SEQUENCE <数据库名>.<Sequence名称>;
   ```
   

* Using the `DROP TABLE` statement

   ```sql
   DROP TABLE <数据库名>.<Sequence名称>;
   ```
   


&nbsp;

<span id=".6I635Y-WLW5leHR2YWw="></span>
## Obtaining nextval

You can obtain nextval by using the `nextval()` function or accessing the `nextval` column in the Sequence table.


* Using the `nextval()` function

   ```sql
   SELECT nextval(<数据库名>.<Sequence名称>);
   ```
   

* Accessing the `nextval` column in the Sequence table

   ```sql
   SELECT <数据库名>.<Sequence名称>.nextval from dual;
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>SELECT nextval from <Database name>.<Sequence name>;</code> queries records in the Sequence table instead of obtaining the next value of the Sequence.</div>


<span id=".6I635Y-WLWN1cnJ2YWw="></span>
## Obtaining currval

You can obtain currval (the value of the last nextval obtained in the current session) by using the currval() function or by accessing the currval column in the Sequence table.


* Using the currval() function

   ```sql
   SELECT currval(<数据库名>.<Sequence名称>);
   ```
   

* Accessing the currval column in the Sequence table

   ```sql
   SELECT <数据库名>.<Sequence名称>.currval from dual;
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><code>SELECT currval from <Database name>.<Sequence name>;</code> queries records in the Sequence table instead of obtaining the current value of the Sequence.</div>


* <div data-tips="true" data-tips-type="warning">For a newly created Sequence, you must call its NEXTVAL once before querying it. Otherwise, a `<code>Sequence 'xxx' is not yet defined in current session</code>` error occurs.</div>


* <div data-tips="true" data-tips-type="warning">If the connection pool mode for the proxy endpoint is a transaction\-level connection pool, the obtained currval value may be incorrect. To obtain an accurate currval value, use a proxy endpoint in direct connection mode or disable the database proxy for the instance.</div>



<span id=".5p-l55yLLXNlcXVlbmNl"></span>
## View Sequence

You can view the specific properties of a Sequence by using the `SHOW` statement.

```sql
SHOW CREATE SEQUENCE <数据库名>.<Sequence名称>
```


&nbsp;
