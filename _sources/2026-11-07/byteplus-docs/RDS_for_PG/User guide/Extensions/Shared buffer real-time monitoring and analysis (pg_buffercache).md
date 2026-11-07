---
title: "Shared buffer real-time monitoring and analysis (pg_buffercache)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pg_buffercache"
---

<span id="S7p8XECq"></span>
## Introduction and applicable scenarios

pg_buffercache is an official standard extension (contrib module) that provides developers and DBAs with a real\-time window into the internal state of the PostgreSQL shared buffer. Through it, we can precisely understand the distribution, usage frequency, and state of data blocks in memory, making it a key tool for performance analysis and optimization.

Typical applicable scenarios include:


* **Identifying hot data**: quickly locate which tables and indexes in the current database are frequently accessed and whose data pages occupy the highest proportion in memory.

* **Assessing cache utilization**: analyze the usage of `shared_buffers` to determine whether its size is appropriate and whether there is a large amount of free or inefficiently used cache space.

* **Monitoring dirty and pinned pages**: monitor the proportion of dirty pages to understand checkpoint pressure. Simultaneously, observe pinned buffers to detect potential long\-running queries or connection issues.

* **Assisting SQL and index tuning**: combined with tools like `pg_stat_statements`, analyze whether the data accessed by high\-cost SQL statements efficiently utilizes the cache.


<span id="yBosa8Vx"></span>
## Precautions

Queries on pg_buffercache require reading the shared buffer. Frequent execution may cause a slight performance impact on the system. It is recommended to analyze in a test environment or a maintenance window.

<span id="1Xn3lLYM"></span>
## Create and delete extension

<span id="aZImaIyp"></span>
### Create extension

Execute the following command in the database that requires analysis to enable pg_buffercache.

```SQL
CREATE EXTENSION IF NOT EXISTS pg_buffercache;
```


<span id="onoQCpUX"></span>
### Delete extension

If this feature is no longer needed, execute the following command to uninstall it. After uninstallation, related views and functions will be removed.

```SQL
DDROP EXTENSION pg_buffercache;
```


<span id="E4ICZwlx"></span>
## Extension usage

<span id="W7EV36SV"></span>
### View the quantity of buffers occupied by each object

The following query counts the tables and indexes that occupy the most memory buffers in the current database, which is the most direct method to identify "hotspot objects".

```SQL
regression=> SELECT n.nspname, c.relname, count(*) AS buffers
             FROM pg_buffercache b JOIN pg_class c
             ON b.relfilenode = pg_relation_filenode(c.oid) AND
                b.reldatabase IN (0, (SELECT oid FROM pg_database
                                      WHERE datname = current_database()))
             JOIN pg_namespace n ON n.oid = c.relnamespace
             GROUP BY n.nspname, c.relname
             ORDER BY 3 DESC
             LIMIT 10;
 
   nspname   |        relname         | buffers
------------+------------------------+---------
 public     | delete_test_table      |     593
 public     | delete_test_table_pkey |     494
 pg_catalog | pg_attribute           |     472
 public     | quad_poly_tbl          |     353
 public     | tenk2                  |     349
 public     | tenk1                  |     349
 public     | gin_test_idx           |     306
 pg_catalog | pg_largeobject         |     206
 public     | gin_test_tbl           |     188
 public     | spgist_text_tbl        |     182
(10 rows)
```


Application scenario: identify objects with excessively high memory usage, determine whether indexes are fully cached, and verify if hot data effectively resides in memory.

<span id="eA5xBbm2"></span>
### View overall buffer status

This function provides a quick, low\-cost snapshot of the global state of the shared buffer

```SQL
regression=> SELECT * FROM pg_buffercache_summary();
 buffers_used | buffers_unused | buffers_dirty | buffers_pinned | usagecount_avg 
--------------+----------------+---------------+----------------+----------------
          128 |              0 |            11 |              0 |      1.3984375
(1 row)
```


Application scenario: quickly assess the overall pressure of the buffer to determine whether there is a buffer shortage or a dirty page backlog issue.

<span id="jwfl0xBF"></span>
### View the distribution of buffer usage counts

This function counts the buffer distribution by usage_count. PostgreSQL manages buffers using a clock scanning algorithm with a count range of 0 to 5, where higher values indicate more frequent page access.

```SQL
regression=> SELECT * FROM pg_buffercache_usage_counts();
 usage_count | buffers | dirty | pinned 
-------------+---------+-------+--------
           0 |      52 |     8 |      0
           1 |      35 |     0 |      1
           2 |      30 |     6 |      0
           3 |       4 |     1 |      0
           4 |       5 |     0 |      0
           5 |       2 |     0 |      0
(6 rows)
```


Application scenarios:


* There are many buffers with a usage count of 0 to 1, indicating frequent buffer eviction and possible memory pressure.

* Buffers with a usage count of 4 to 5 represent the real hot data and should have priority to remain resident in memory.

* Dirty pages concentrate in buffers with high usage counts, indicating frequent updates to hot data.
