---
title: "Best practice for creating tables in ByteHouse"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bytehouse-table-creation-best-practice"
---

<span id="6e430471"></span>
# Caution

When creating tables in ByteHouse, most configuration fields cannot be modified after creation, so please read this guide carefully before creating tables to plan accordingly.

<span id="建表参数指南"></span>
# Table creation parameter guide

<span id="_1-排序键-（必填）order-by"></span>
## 1. Sort Key (REQUIRED) Order By


* **Definition and Principle**: To enhance query performance, data is stored according to the order of sorting indexes. (Sorting indexes are not equivalent to MySQL's primary keys as values can be duplicated; nor are they equivalent to MySQL's indexes, which cannot be modified after table creation.)

* **Field Restrictions**: Cannot be Nullable, and supports setting 1 to 5 fields.

* **Configuration Suggestion**: Select 1 to 3 fields frequently used as filters for sorting indexes to improve the performance of related queries. The search speed based on the first sorting index is the fastest, with the subsequent two indexes decreasing in speed respectively.

* After the table is created, sorting indexes do not support modifying type, adding columns, or removing columns (to modify, the table must be deleted and data must be backtracked).


<span id="_2-分区键-粒度-（必填）-partition-by"></span>
## 2. Partition Key/Granularity (Optional) Partition By


* **Definition and Principles**: Partitions are logical data sets within a table divided according to specified rules, which can be carried out daily, monthly, or annually. To reduce the amount of data that needs to be handled, each partition is stored in separate files. When accessing data, ByteHouse strives to use the smallest subset of these partitions to boost performance.

* **Field Restrictions**: Partition fields do not support Nullable and can be configured with 1\-5 fields.

* **Partition Granularity**: When the column type is `Date`, it supports day and month\-level aggregation partitioning; when the column type is `Datetime`, it supports minute, hour, day, and month\-level aggregation partitioning.

* **Configuration Recommendations**:

   * It is advised to ensure as much as possible that the field type/content is time\-related, as other non\-time\-related contents will cause an excessive number of partition files, severely impacting import effects and query speeds.

   * Ideally, set the partition field as a frequently filtered date field, such as order time.

   * If the daily data volume exceeds 10 billion, consider hourly partitioning; otherwise, it is recommended to default to daily partitioning.

* After creating a table, partition fields do not support type modification, column addition, or column removal.


<span id="_3-分桶键（可选）-cluster-by"></span>
## 3. Bucketing Key (Optional): Cluster By


* **Definition and Principles**: When partitions cannot resolve even data distribution, further utilization of bucketing fields ensures an even distribution of data across each cluster node, maximizing cluster performance for queries. Proper bucketing field settings also help address data skewness, ensuring more uniform data distribution.

* **Field Restrictions**: Bucketing fields cannot support Nullable.

* **Configuration Recommendation**: It is generally advisable to select fields that often appear in Group by.

* After creating a table, bucketing fields do not support type modification or field alteration.


<span id="_4-数据保留时间-ttl-（可选）"></span>
## 4. Data Retention Time TTL (Optional)


* **Definition and Principles**: Set the data's life cycle in day units. Data retention time is calculated based on “partition fields”.

* **Field restriction**: ≥0. Entering "0" means not setting a TTL for the table, i.e., data is retained forever.

* Data retention time can be modified after table creation. Once the time limit exceeds the retention period, it will be automatically deleted.


<span id="_5-采样键-（可选）-sample-key"></span>
## 5. Sample Key (optional)


* **Definition and principle**: Used for sampling queries. This type of query is performed only on specific parts of data (samples). Highly suitable for sacrificing accuracy to gain performance, or for queries where the result is inherently an approximation.

* **Field restriction**:

   * Sample fields only support UInt8, UInt16, UInt32, UInt64.

   * No default settings, to execute a sample key, it must be included at table creation.

* **Configuration Suggestion**: If there is a need for sampling queries across the full table and certain fields have uniform data distribution (such as time\-related fields), consider setting them as sampling fields.

* After table creation, modifications are not supported.


<span id="_6-唯一键-（可选）-unique-key"></span>
## 6. Unique Key (Optional)


* **Definition and principles**: The unique key is a capability independently developed by the ByteHouse team, which maintains high query performance and supports unique key updates. This feature primarily addresses the pain point that open\-source ClickHouse cannot efficiently support update operations, helping businesses more easily develop real\-time analysis applications. Users can implement upsert write semantics by specifying a unique key (UNIQUE KEY), and queries will automatically return the latest value for each unique key.

* **Field restrictions**: It is recommended that the number of Unique Key fields does not exceed five; if multiple fields combine to form a unique key, you can use their `toString(sipHash128())` hash as the unique key. It currently supports three levels of granularity: table\-level, partition\-level, and bucket\-level unique keys.

* For more best practices and query examples related to unique keys, see [Best practice for ByteHouse Unique Key tables](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables).

* After table creation, modifications are not supported.


<span id="9e855c57"></span>
## 7. Primary Key (Optional)


* **Definition & Principle**: The primary key serves as a logical index for data sorting and query acceleration, rather than a traditional constraint identifier that enforces uniqueness.

* **Configuration Recommendations**: By default, there is no need to explicitly specify a primary key. ByteHouse will use the sort key as the primary key. In special scenarios where the primary key differs from the sort key, the primary key must be the leftmost prefix of the sort key. For example, if the sort key is `(OrderID, Date)`, the primary key must be `OrderID` and cannot be `Date`.
