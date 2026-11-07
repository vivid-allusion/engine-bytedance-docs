---
title: "Using StarRocks partitioned tables"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Using_StarRocks_partitioned_tables"
---

Partitioned tables in the StarRocks database are a table structure used for storing and managing large\-scale data. They split a large table into multiple smaller partitions, with each partition containing a portion of the table's data. These partitions can be divided according to specific rules, such as time, geographic location, business domain, and more.

The advantages of partitioned tables include:


1. Improved query performance: By splitting a large table into multiple partitions, the amount of data scanned during queries can be reduced, thereby improving query performance. Queries can scan only the relevant partitions instead of scanning the entire table.

2. More flexible data management: Different partitions can be managed independently, such as backup, restore, index maintenance, and more. This allows for more granular control over the data lifecycle and maintenance processes.

3. Better scalability: As the volume of data increases, the table's storage capacity can be horizontally expanded by adding more partitions, without needing to restructure the entire table.

4. Improved data locality: Partitioned tables can distribute data across different physical storage based on data characteristics, enhancing data locality and reducing I/O overhead.


<span id="创建分区表"></span>
## Create partitioned tables

StarRocks partitions support three partitioning methods, [Using StarRocks partitioned tables](https://docs.byteplus.com/docs/E-MapReduce/109506) (recommended), [Range 分区](https://docs.byteplus.com/docs/E-MapReduce/109506#range-%E5%88%86%E5%8C%BA), and [Using StarRocks partitioned tables](https://docs.byteplus.com/docs/E-MapReduce/109506).

<span id="表达式分区"></span>
### Expression partitioning

StarRocks supports expression partitioning, allowing you to set partition expressions (time function expressions or list expressions) when creating tables. When importing data, StarRocks automatically creates partitions based on the data and the rules defined by the partition expression. You do not need to manually or batch\-create a large number of partitions in advance when creating tables, nor configure dynamic partition attributes.

<span id="创建语法："></span>
#### Creation syntax:

```sql
PARTITION BY expression
...
PROPERTIES( 'partition_live_number' = 'xxx' ) ]
```


<span id="参数说明："></span>
#### Parameter note:

Currently, expression only supports the date_trunc and time_slice functions.

<span id="样例："></span>
#### Example:

```sql
CREATE TABLE tb_expression_partition (
    event_day DATETIME NOT NULL,
    id INT,
    name VARCHAR(32)
)
DUPLICATE KEY(event_day, id, name)
PARTITION BY date_trunc('day', event_day)
DISTRIBUTED BY HASH(event_day, id);
```


```sql
-- Insert data
INSERT INTO tb_expression_partition 
    VALUES ("2020-05-01 20:12:04",1,"name1");
```


<span id="range分区"></span>
### Range partitioning

Range partitioning is suitable for simple and continuous data, such as time series data (date or timestamp) or continuous numerical data. Data is often queried and managed based on continuous date or numerical ranges.


* **Static partition**


<span id="创建语法："></span>
##### Creation syntax:

```sql
PARTITION BY RANGE (partition_columns)（ PARTITION <partition_name> 
VALUES LESS THAN ("yyyy-hh-dd") | VALUES [('startValue'), ('endValue')) 
, [, ...] )
```


<span id="样例："></span>
##### Example:

```sql
CREATE TABLE tb_static_partition(
    part DATE,
    id INT DEFAULT '10',
    name VARCHAR(100)
)
UNIQUE KEY(part, id)
PARTITION BY RANGE(part)(
    PARTITION p2020 VALUES [('2020-01-01'), ('2021-01-01'))
)
DISTRIBUTED BY HASH(id);
```



* **Dynamic partition**


Dynamic partitions support automatic creation and deletion of partitions based on the current time. This eliminates the need to manually create and delete partitions.

<span id="创建语法："></span>
##### Creation syntax:

When creating a dynamic partition, specify the following properties in PROPERTIES:

```sql
PROPERTIES(
    "dynamic_partition.enable" = "true",
    "dynamic_partition.time_unit" = "xxx",
    "dynamic_partition.start" = "xxx",
    "dynamic_partition.end" = "xxx",
    "dynamic_partition.prefix" = "xxx",
    "dynamic_partition.history_partition_num" = "xxx"
);
```


<span id="参数说明："></span>
##### Parameter description:


|Parameter |Required |Note |
|---|---|---|
|dynamic_partition.enable |No |Enable the dynamic partition feature. The value can be true (default) or false. |
|dynamic_partition.time_unit |Yes |The time granularity for dynamic partitions. The value can be HOUR, DAY, WEEK, MONTH, or YEAR. The time granularity determines the suffix format of dynamically created partition names.<br><br>When the value is HOUR, only the Datetime type is supported. The suffix format of dynamically created partition names is yyyyMMddHH, for example, 2020032101.<br><br>When the value is DAY, the suffix format of dynamically created partition names is yyyyMMdd, for example, 20200321.<br><br>When the value is WEEK, the suffix format of dynamically created partition names is yyyy_ww, for example, 2020_13 represents the 13th week of 2020.<br><br>When the value is MONTH, the suffix format of dynamically created partition names is yyyyMM, for example, 202003.<br><br>When the value is YEAR, the suffix format of dynamically created partition names is yyyy, for example, 2020. |
|dynamic_partition.time_zone |No |The time zone for dynamic partitions. The default is consistent with the system time zone. |
|dynamic_partition.start |No |The starting offset for retained dynamic partitions. The value must be a negative integer. Depending on the dynamic_partition.time_unit property, partitions before this offset based on the current day (week/month) will be deleted. For example, if set to \-3 and dynamic_partition.time_unit is day, partitions from three days ago will be deleted.<br><br>If not specified, the default is Integer.MIN_VALUE, that is, \-2147483648, which means historical partitions are not deleted. |
|dynamic_partition.end |Yes |The number of partitions to be created in advance. The value must be a positive integer. Depending on the dynamic_partition.time_unit property, partitions within the corresponding range are created in advance based on the current day (week/month). |
|dynamic_partition.prefix |No |The prefix name for dynamic partitions. The default value is p. |
|dynamic_partition.buckets |No |The number of buckets for dynamic partitions. The default is consistent with the number of buckets specified by the BUCKETS reserved keyword or the number of buckets automatically set by StarRocks. |
|dynamic_partition.history_partition_num |No |The number of historical partitions created for dynamic partitions. The default value is 0. When the value is greater than 0, historical partitions will be created in advance. Since version 2.5.2, StarRocks supports configuring this parameter. |
|dynamic_partition.start_day_of_week |No |When dynamic_partition.time_unit is WEEK, this parameter specifies the first day of each week. Valid values are 1 to 7. 1 indicates Monday, and 7 indicates Sunday. The default value is 1, which means each week starts from Monday. |
|dynamic_partition.start_day_of_month |No |When dynamic_partition.time_unit is MONTH, this parameter specifies the first day of each month. Valid values are 1 to 28. 1 indicates the first day of the month, and 28 indicates the 28th day of the month. The default value is 1, which means each month starts from the first day. The first day of the month cannot be set to the 29th, 30th, or 31st. |
|dynamic_partition.replication_num |No |The number of tablet replicas in dynamically created partitions. The default value is the same as the number of replicas configured when creating the table. |


<span id="样例："></span>
##### Example:

```sql
CREATE TABLE tb_dynamic_partition(
    part DATE,
    id INT DEFAULT '10',
    name VARCHAR(100)
)
UNIQUE KEY(part, id)
PARTITION BY RANGE(part)(
    PARTITION p2020 VALUES [('2020-01-01'), ('2021-01-01'))
)
DISTRIBUTED BY HASH(id)
PROPERTIES(
    "dynamic_partition.enable" = "true",
    "dynamic_partition.time_unit" = "DAY",
    "dynamic_partition.start" = "-10",
    "dynamic_partition.end" = "3",
    "dynamic_partition.prefix" = "p",
    "dynamic_partition.history_partition_num" = "10"
);
```


<span id="动态修改动态分区属性："></span>
##### Dynamically modify dynamic partition properties:

```sql
ALTER TABLE tb_demo SET("dynamic_partition.history_partition_num"="100");
```


<span id="list分区"></span>
### List partition

List partitions are suitable for storing data with columns that have a small number of enumerated values, and for scenarios where data is frequently queried and managed based on the enumerated values of columns. For example, columns representing geographic location, status, or category. Each value in the column represents a distinct category. Partitioning data by the enumerated values of a column can improve query performance and facilitate data management.

<span id="创建语法："></span>
#### Creation syntax:

```sql
PARTITION BY LIST (partition_columns)（ PARTITION <partition_name> VALUES IN (value_list) [, ...] )
```


<span id="样例："></span>
#### Example:

Set the city column values Beijing and Tianjin as the northern partition, and Guangzhou and Shenzhen as the southern partition.

```sql
CREATE TABLE tb_list_partition (
    city bigint,
    id bigint,
    name varchar(20) not null
)
DUPLICATE KEY(id)
PARTITION BY LIST (part) (
   PARTITION pNorth VALUES IN ("Beijing","Tianjin"), 
   PARTITION pSouth VALUES IN ("Shenzhen","Guangzhou")
)
DISTRIBUTED BY HASH(`id`);
```


<span id="使用限制："></span>
#### Limits:


* Dynamic and batch creation of List partitions is not supported.

* StarRocks compute\-storage separation mode supports this feature starting from version 3.1.1.

* When using `ALTER TABLE <table_name> DROP PARTITION <partition_name>;`, the partition is deleted directly and cannot be recovered.

* List partitions currently do not support backup and restore.

* Asynchronous materialized views do not currently support creation based on base tables that use List partitions.
