---
title: "Advanced diagnosis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/advanced-diagnosis"
---

Advanced diagnosis is used to collect relevant metadata of tables in the cluster, including creation date, storage volume, and other information, to support refined governance of tables by the business. ByteHouse also provides a table index diagnosis feature. By diagnosing the metadata of table indexes from different dimensions, such as storage mode and index settings, this feature helps you achieve more efficient table governance and enhances the stability and query performance of the instance. This feature is applicable to daily table governance, query performance optimization, resource control, and many other scenarios. This tutorial introduces an overview of the advanced diagnosis feature and explains how to use advanced diagnosis.

<span id="db73ea9c"></span>
# Function overview

The advanced diagnosis feature collects statistics from information log tables such as `system.optimizer_statistics`, `system.optimizer_statistics_paritioned_ha`, `system.data_skipping_indices`, and `system.tables` to gather relevant metadata about data tables in the cluster. This information is used to diagnose table quantity distribution, storage usage, table structure validity, and index effectiveness, and supports displaying the following diagnostic items:


|Diagnosis items |Description |Suggestion |
|---|---|---|
|Tables and Views per Database |It counts the number of tables and views by database. The table clearly displays the distribution of tables and views within the instance. |It can be used to identify databases with an excessive number of tables, prevent metadata overload in a single database, and optimize the database split strategy. |
|Partition tables and storage |It counts the total number of partition tables and the total storage they occupy. |This can be used to identify partition tables with high storage usage and, based on business scenarios, clean up historical partitions to reduce invalid storage usage. |
|Non\-partitioned tables and storage |It calculates the total number of all non\-partition tables and the total storage occupied by non\-partition tables. |It can be used to identify non\-partitioned tables with high storage usage, assess whether conversion to partitioned tables (such as partitioning by time) is needed, and improve data filtering efficiency during queries. |
|Empty tables |It counts tables with zero data storage (these may be newly created empty tables or tables where data has been cleared due to expiration). |It can be used to clean up invalid empty tables, reduce metadata redundancy, and ease the metadata management pressure on the instance. |
|Tables over 300 columns |It counts wide tables with more than 300 columns. |It can be used to identify wide tables. Wide tables can lead to unnecessary field scans during queries. By identifying wide tables and splitting such tables, query performance can be improved. |
|Order key tables over 3 columns |It counts tables where the number of `ORDER BY` fields exceeds 3 columns (`ORDER BY` fields affect the partition merging and query sorting efficiency of MergeTree tables). |It can be used to identify tables with too many `ORDER BY` columns. Having too many `ORDER BY` columns can reduce merge speed and increase memory consumption. Such tables can be optimized by identifying them, retaining primary sort fields, and adjusting the table structure configuration. |
|Shard key tables over 3 columns |It counts distributed tables with more than three `Shard Key` fields. |It can be used to identify tables with too many `Shard Key` columns. Having too many `Shard Key` columns increases the complexity of data sharding calculations and may lead to uneven data distribution. By identifying such tables and reducing the number of `Shard Key` columns to 1 or 2 core fields, you can optimize the table structure configuration. |
|Table data TTL less than 7 days |It counts the tables whose data expiration time (TTL) is less than 7 days. |It can be used to identify tables with short data expiration times, helping to avoid frequent cleanup that affects query stability or premature data loss caused by a short TTL. |
|Table skipping index |It collects statistics on the types of skipping indexes (such as MinMax, Set, Bloom Filter, and more), associated fields, and enables status for all tables. |It can be used to view existing skipping indexes in the table, determine whether there are any invalid indexes (such as index fields not used for query filtering) or "missing key indexes" (such as high\-frequency filtering fields without indexes), and optimize index configuration to reduce the amount of data scanned. |


<span id="50229094"></span>
# Use advanced diagnoses


1. Log in to the ByteHouse Enterprise console, click the top **Diagnostic** tab, click **Advanced diagnostics**, to access the feature page.

2. Select a cluster from the dropdown list, click **Diagnosis**, and the system will automatically analyze and display the metadata of tables in the current cluster.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79b9e07db043488cb96b1a1044aa9401~tplv-goo7wpa0wc-image.image) </span>

   ByteHouse supports a variety of diagnostic items that can assist in identifying irregularities in table metadata within the cluster. By considering your business issues together with diagnostic items, you can analyze the root causes and take appropriate optimization measures for efficient table governance. Please refer to [Function overview](https://docs.byteplus.com/docs/bytehouse/73580#db73ea9c) on how to use various diagnosis items.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab1854282bc044898d3af1fd8f31d850~tplv-goo7wpa0wc-image.image) </span>
