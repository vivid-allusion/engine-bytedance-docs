---
title: "Partition health diagnosis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/partition-health-diagnosis"
---

When creating a partition table, if the settings are not reasonable, it will affect query performance, deduplication efficiency, and cluster stability. ByteHouse's diagnostic analysis feature supports partition health monitoring and diagnosis, helping you visually inspect partition status, providing partition diagnostic information, and assisting in optimizing your partition tables.

<span id="f3c65a0d"></span>
# **Usage Restrictions**


* Before use, ensure your engine is version v2.3 or later. You can check your current engine version on the **Tenant management \> Basic Information** page in the ByteHouse console.

* This feature is in Beta. To enable it, please submit a ticket or contact the ByteHouse team to request allowlist access.


<span id="4cc6f52a"></span>
# Partition health diagnostic metrics

ByteHouse calculates partition fragmentation number and unique table row count based on metrics such as parts count, part sizes, total data volume (rows), and bucket count. It judges the partition health based on the calculation results. Specific metrics and methods are as follows:


|Diagnostic Items |Calculation Method |Potential Impact |Healthy |Unhealthy |Description |
|---|---|---|---|---|---|
|Number of Parts |Read the file blocks under the partition. |Too many parts can affect query performance. |`< 100,000` |`>= 100,000` |ByteHouse has now merged the metrics of "parts count" and "average parts size" to calculate the number of partition fragments, and to assess the health of the partition. Only when both metrics are within the unhealthy threshold range will the system declare it as unhealthy. |
|Average parts size |Parts size per number of parts |If the average size of parts is too small, it may indicate insufficient merging, which could lead to an excessive number of parts. |`>= 50 MB` |`< 50 MB` ||
|Unique table row count |* When there is no bucket number, unique table row count = total row count (estimated).<br><br>* When a bucket number exists, unique table row count = total row count (estimated) / Bucket number. |Having too many unique table rows will affect the deduplication efficiency. |`< 100,000,000` |`>= 100,000,000` |None |


<span id="132bd841"></span>
# View Partition Diagnostic Information


1. On the ByteHouse console, click **Diagnostic Analysis \> Partition Health** tab to enter the partition health page, click the **Check Details** button in the Actions column to view the partition health diagnosis details of a specific table.

2. On the diagnosis details page, you can view the basic information and diagnostic details of the table partition.

   * The basic information module displays the partition key, partition value, total count of rows, number of buckets, parts count, and total parts among other information.

   * The diagnosis details module provides the diagnosis results based on items such as part count, average part size, unique table row count, and their current values. You can adjust the partitions according to the diagnostic results to improve the health of the partitions.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eed79fa7afe4094bdf48e264e3959de~tplv-goo7wpa0wc-image.image) </span>
