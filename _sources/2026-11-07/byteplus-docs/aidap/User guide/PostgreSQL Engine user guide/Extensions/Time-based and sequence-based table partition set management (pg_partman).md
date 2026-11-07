---
title: "Time-based and sequence-based table partition set management (pg_partman)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_partman"
---

pg_partman is an extension for creating and managing time\-based and sequence\-based table partition sets, designed to simplify the management of table partitions based on time or numbers/IDs.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Create and delete extension


* Create extension

   ```sql
   CREATE EXTENSION pg_partman;
   ```
   

* Delete extension

   ```sql
   DROP EXTENSION pg_partman;
   ```
   


<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage

<span id=".5Z-65LqO5pe26Ze05YiG5Yy6"></span>
### Time\-based partitioning

The following is an example of time\-based partitioning, which can help quickly understand the extension capabilities.


1. Create partitioned table

   ```sql
   -- create partition table first
   CREATE TABLE test_schema.time_partition_table(
       col1 int,
       col2 text default 'stuff',
       col3 timestamptz NOT NULL DEFAULT now()
   )PARTITION BY RANGE (col3);
   -- create non-unique index
   CREATE INDEX ON test_schema.time_partition_table(col3);
   ```
   

   ```sql
   test_db=> -- view table structure
   test_db=> \d+ test_schema.time_partition_table
                                         Partitioned table "test_schema.time_partition_table"
    Column |           Type           | Collation | Nullable |    Default    | Storage  | Compression | Stats target | Description
   --------+--------------------------+-----------+----------+---------------+----------+-------------+--------------+-------------
    col1   | integer                  |           |          |               | plain    |             |              |
    col2   | text                     |           |          | 'stuff'::text | extended |             |              |
    col3   | timestamp with time zone |           | not null | now()         | plain    |             |              |
   Partition key: RANGE (col3)
   Indexes:
       "time_partition_table_col3_idx" btree (col3)
   Number of partitions: 0
   ```
   

2. Create template table

   ```sql
   -- create template table for properties inheritance
   CREATE TABLE test_schema.time_partition_table_template (LIKE test_schema.time_partition_table);
   -- create primary key for template for subsequent properties inheritance
   ALTER TABLE test_schema.time_partition_table_template ADD PRIMARY KEY (col1);
   ```
   

   ```sql
   test_db=> \d+ test_schema.time_partition_table_template
                                       Table "test_schema.time_partition_table_template"
    Column |           Type           | Collation | Nullable | Default | Storage  | Compression | Stats target | Description
   --------+--------------------------+-----------+----------+---------+----------+-------------+--------------+-------------
    col1   | integer                  |           | not null |         | plain    |             |              |
    col2   | text                     |           |          |         | extended |             |              |
    col3   | timestamp with time zone |           | not null |         | plain    |             |              |
   Indexes:
       "time_partition_table_template_pkey" PRIMARY KEY, btree (col1)
   Access method: heap
   ```
   

3. Create child table

   ```sql
   -- create subtables for partitioned table
   SELECT test_schema.create_parent(
       p_parent_table := 'test_schema.time_partition_table',
       p_control := 'col3',
       p_interval := '1 day',
       p_template_table := 'test_schema.time_partition_table_template'
   );
   \d+ test_schema.time_partition_table
   ```
   

   ```sql
   test_db=> \d+ test_schema.time_partition_table
                                         Partitioned table "test_schema.time_partition_table"
    Column |           Type           | Collation | Nullable |    Default    | Storage  | Compression | Stats target | Description
   --------+--------------------------+-----------+----------+---------------+----------+-------------+--------------+-------------
    col1   | integer                  |           |          |               | plain    |             |              |
    col2   | text                     |           |          | 'stuff'::text | extended |             |              |
    col3   | timestamp with time zone |           | not null | now()         | plain    |             |              |
   Partition key: RANGE (col3)
   Indexes:
       "time_partition_table_col3_idx" btree (col3)
   Partitions: test_schema.time_partition_table_p20250413 FOR VALUES FROM ('2025-04-13 00:00:00+08') TO ('2025-04-14 00:00:00+08'),
               test_schema.time_partition_table_p20250414 FOR VALUES FROM ('2025-04-14 00:00:00+08') TO ('2025-04-15 00:00:00+08'),
               test_schema.time_partition_table_p20250415 FOR VALUES FROM ('2025-04-15 00:00:00+08') TO ('2025-04-16 00:00:00+08'),
               test_schema.time_partition_table_p20250416 FOR VALUES FROM ('2025-04-16 00:00:00+08') TO ('2025-04-17 00:00:00+08'),
               test_schema.time_partition_table_p20250417 FOR VALUES FROM ('2025-04-17 00:00:00+08') TO ('2025-04-18 00:00:00+08'),
               test_schema.time_partition_table_p20250418 FOR VALUES FROM ('2025-04-18 00:00:00+08') TO ('2025-04-19 00:00:00+08'),
               test_schema.time_partition_table_p20250419 FOR VALUES FROM ('2025-04-19 00:00:00+08') TO ('2025-04-20 00:00:00+08'),
               test_schema.time_partition_table_p20250420 FOR VALUES FROM ('2025-04-20 00:00:00+08') TO ('2025-04-21 00:00:00+08'),
               test_schema.time_partition_table_p20250421 FOR VALUES FROM ('2025-04-21 00:00:00+08') TO ('2025-04-22 00:00:00+08'),
               test_schema.time_partition_table_default DEFAULT
   ```
   

   ```json
   test_db=> -- 查看子表，父表和模板表的索引都在子表中成功创建
   test_db=> \d+ test_schema.time_partition_table_p20250419
                                          Table "test_schema.time_partition_table_p20250419"
    Column |           Type           | Collation | Nullable |    Default    | Storage  | Compression | Stats target | Description
   --------+--------------------------+-----------+----------+---------------+----------+-------------+--------------+-------------
    col1   | integer                  |           | not null |               | plain    |             |              |
    col2   | text                     |           |          | 'stuff'::text | extended |             |              |
    col3   | timestamp with time zone |           | not null | now()         | plain    |             |              |
   Partition of: test_schema.time_partition_table FOR VALUES FROM ('2025-04-19 00:00:00+08') TO ('2025-04-20 00:00:00+08')
   Partition constraint: ((col3 IS NOT NULL) AND (col3 >= '2025-04-19 00:00:00+08'::timestamp with time zone) AND (col3 < '2025-04-20 00:00:00+08'::timestamp with time zone))
   Indexes:
       "time_partition_table_p20250419_pkey" PRIMARY KEY, btree (col1)
       "time_partition_table_p20250419_col3_idx" btree (col3)
   Access method: heap
   ```
   


<span id="wYttbbQy"></span>
### Convert non\-partitioned table to partitioned table

The following is an example of converting a non\-partitioned table to a partitioned table offline.


1. Construct test data

   ```sql
   -- create a normal table for subsequent testing
   CREATE TABLE test_schema.original_table(
       col1 bigint not null,
       col2 text not null,
       col3 timestamptz DEFAULT now(),
       col4 text
   );
   CREATE INDEX ON test_schema.original_table(col1);
   -- construct partial data
   INSERT INTO test_schema.original_table (col1, col2, col3, col4) VALUES (generate_series(1,100000), 'stuff'||generate_series(1,100000), now(), 'stuff');
   ```
   

2. Data migration

   ```sql
   -- begin migration with the following steps
   -- 1. rename the table to be migrated
   ALTER TABLE test_schema.original_table RENAME to old_nonpartitioned_table;
   
   -- 2. create a new partition table with the same name as the original, then create subtables
   CREATE TABLE test_schema.original_table(
       col1 bigint not null,
       col2 text not null,
       col3 timestamptz DEFAULT now(),
       col4 text
   ) PARTITION BY RANGE (col1);
   CREATE INDEX ON test_schema.original_table (col1);
   SELECT test_schema.create_parent(
       p_parent_table := 'test_schema.original_table',
       p_control := 'col1',
       p_interval := '10000'
   );
   \d+ test_schema.original_table
   
   -- 3. call the function partition_data_proc to migrate data
   CALL test_schema.partition_data_proc(
       p_parent_table := 'test_schema.original_table',
       p_loop_count := 200,
       p_interval := '1000',
       p_source_table := 'test_schema.old_nonpartitioned_table'
   );
   ```
   

3. Data verification

   ```sql
   test_db=> -- check data
   test_db=> SELECT count(*) FROM test_schema.old_nonpartitioned_table;
    count
   -------
        0
   (1 row)
   
   test_db=> SELECT count(*) FROM test_schema.original_table;
    count
   --------
    100000
   (1 row)
   
   test_db=> \d+ test_schema.original_table
                                         Partitioned table "test_schema.original_table"
    Column |           Type           | Collation | Nullable | Default | Storage  | Compression | Stats target | Description
   --------+--------------------------+-----------+----------+---------+----------+-------------+--------------+-------------
    col1   | bigint                   |           | not null |         | plain    |             |              |
    col2   | text                     |           | not null |         | extended |             |              |
    col3   | timestamp with time zone |           |          | now()   | plain    |             |              |
    col4   | text                     |           |          |         | extended |             |              |
   Partition key: RANGE (col1)
   Indexes:
       "original_table_col1_idx1" btree (col1)
   Partitions: test_schema.original_table_p0 FOR VALUES FROM ('0') TO ('10000'),
               test_schema.original_table_p10000 FOR VALUES FROM ('10000') TO ('20000'),
               test_schema.original_table_p100000 FOR VALUES FROM ('100000') TO ('110000'),
               test_schema.original_table_p20000 FOR VALUES FROM ('20000') TO ('30000'),
               test_schema.original_table_p30000 FOR VALUES FROM ('30000') TO ('40000'),
               test_schema.original_table_p40000 FOR VALUES FROM ('40000') TO ('50000'),
               test_schema.original_table_p50000 FOR VALUES FROM ('50000') TO ('60000'),
               test_schema.original_table_p60000 FOR VALUES FROM ('60000') TO ('70000'),
               test_schema.original_table_p70000 FOR VALUES FROM ('70000') TO ('80000'),
               test_schema.original_table_p80000 FOR VALUES FROM ('80000') TO ('90000'),
               test_schema.original_table_p90000 FOR VALUES FROM ('90000') TO ('100000'),
               test_schema.original_table_default DEFAULT
   
   test_db=> SELECT count(*) FROM test_schema.original_table_p10000;
    count
   -------
    10000
   (1 row)
   ```
   


<span id="c6vQfZos"></span>
### pg_partman_bgw background worker process

pg_partman_bgw is a background worker process that automatically executes `run_maintenance()` regularly, iterating over all partitioned tables in the part_config table that require maintenance, creating future partitions as needed or cleaning expired partitions as needed, without manual intervention or external scheduling tasks.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">pg_partman_bgw needs to be loaded in shared_preload_libraries (<strong>default configured</strong>).</div>


<span id="AG4Cv0ln"></span>
#### pg_partman_bgw key parameters


|Parameter name |Required |Instructions |
|---|---|---|
|pg_partman_bgw.dbname |Yes |The target Database to which the background process connects. Multiple databases can be set, separated by commas. |
|pg_partman_bgw.role |Yes |The role name used by the background process to connect to the target Database. |
|pg_partman_bgw.interval |recommend |Execution interval of the background process (second), default 3600 (1 Hour). |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/aidap/ModifyComputeParameters">ModifyComputeParameters</a> API to change the running value of these three parameters.</div>


<span id="tyUT7AKm"></span>
#### Verify normal operation of pg_partman_bgw

```SQL
-- Check the preload shared library to confirm whether it includes pg_partman_bgw
SHOW shared_preload_libraries;

-- Check All configuration items related to pg_partman_bgw
SELECT name, setting, source
FROM pg_settings
WHERE name LIKE 'pg_partman_bgw%'
ORDER BY name;

-- Check the running Status of partman background worker process
SELECT pid, backend_type, state, query
FROM pg_stat_activity
WHERE backend_type LIKE '%partman%';
```
