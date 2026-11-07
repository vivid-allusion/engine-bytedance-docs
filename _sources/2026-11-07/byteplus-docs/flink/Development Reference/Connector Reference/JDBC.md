---
title: "JDBC"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/JDBC"
---

The JDBC connector provides read and write capabilities for common relational databases such as MySQL and PostgreSQL, and supports data source tables, result tables, and dimension tables.

<span id="86dfedd9"></span>
## Precautions

If you need to connect to the cloud database veDB MySQL edition using the JDBC connector, please configure your connection terminal according to the following requirements; otherwise, task failures may occur due to custom connection terminal restrictions.

For a detailed understanding of each parameter, please refer to [edit connection terminal](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints).


* Read/Write Mode: Set to **read/write**.

* Consistency Level: Set to **eventual consistency**.

* Master Node Accepts Reads: **Disable** this option.

* Transaction Splitting: **Enable** this option.

* Based on compliance requirements, if you need to use JDBC MySQL related features, users must upload the MySQL Driver themselves. Please go to the [MySQL official website](https://downloads.mysql.com/archives/c-j/) to download version 8.0.27 and upload it to the project development dependencies. For specific operations, please refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources).


<span id="11f91f06"></span>
## DDL Definition

<span id="e4ef5294"></span>
### Used as Data Source

```sql
CREATE TABLE jdbc_source (
    name String,
    score INT
 ) WITH (
    'connector' = 'jdbc',
    'url' = 'jdbc:mysql://192.*.*.*:3306/doc_db',  
    'table-name' = '<yourtablename>',
    'username' = 'admin',          
    'password' = 'Passord',      
    'scan.partition.column' = 'score',       
    'scan.partition.num' = '2',           
    'scan.partition.lower-bound' = '0',     
    'scan.partition.upper-bound' = '100',     
    'scan.fetch-size' = '1' 
);
```


<span id="1e7acb43"></span>
### Used as Data Sink

```SQL
CREATE TABLE jdbc_sink (
    name String,
    score INT
 ) WITH (
    'connector' = 'jdbc',
    'url' = 'jdbc:mysql://192.*.*.*:3306/doc_db',     
    'table-name' = '<yourtablename>',
    'username' = 'admin',          
    'password' = 'Pa$$w0rd',      
    'sink.buffer-flush.max-rows' = '100'
);
```


<span id="9ae98869"></span>
### Used as Data Lookup Table

```SQL
CREATE TABLE jdbc_lookup (
    name String,
    score INT
 ) WITH (
    'connector' = 'jdbc',
    'url' = 'jdbc:mysql://192.*.*.*:3306/doc_db',     
    'table-name' = '<yourtablename>',
    'username' = 'admin',          
    'password' = 'MyPa$$w0rd',      
    'lookup.cache.max-rows' = '100',
    'lookup.max-retries' = '3'
);
```


<span id="efd698b1"></span>
## WITH Parameters


|**Parameters** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specifies the connector to be used, which is the JDBC connector in this case. |
|url |Yes |(none) |String |The connection address of the JDBC database. |
|table\-name |Yes |(none) |String |Table name. |
|driver |No |(none) |String |Class name of the JDBC Driver. If not set, it is automatically extracted from the URL parameter value. |
|username |No |(none) |String |Database login username and password. When used, both must be used together. |
|password |No |(none) |String |Database login username and password. When in use, both must be used together. |
|scan.partition.column |No |(none) |String |Specifies the column name for a partitioned scan, which must be of a numeric type, date type, timestamp type, etc. |
|scan.partition.num |No |(none) |Integer |After enabling partition scan, specify the number of partitions. |
|scan.partition.lower\-bound |No |(none) |Integer |After enabling partition scan, specify the minimum value for the first partition. |
|scan.partition.upper\-bound |No |(none) |Integer |After enabling partition scanning, specify the maximum value for the last partition. |
|scan.fetch\-size |No |0 |Integer |When reading data, the number of rows read in batches.<br><br>Default is 0, which means reading one row at a time, and is less efficient (low throughput). |
|sink.buffer\-flush.max\-rows |No |100 |Integer |During batch output, how much data can be cached at most in the cache. If set to 0, output caching is disabled. |
|sink.buffer\-flush.interval |No |1s |Duration |During batch output, the maximum interval per batch, in milliseconds.<br><br>**If static output caching is set, but the batch output interval is greater than 0s, it indicates that pure asynchronous output functionality is enabled, i.e., data is output to the operator and finally written to the database from the operator.**  |
|sink.max\-retries |No |3 |Integer |Maximum number of retries when data writing fails. |
|lookup.cache.max\-rows |No |(none) |Integer |Maximum number of data rows stored in the Lookup Cache. Must be used in conjunction with lookup.cache.ttl. |
|lookup.cache.ttl |No |(none) |Duration |The maximum caching time for each record in the query cache. Must be used in conjunction with lookup.cache.max\-rows. |
|lookup.max\-retries |No |3 |Integer |Maximum number of retries when database query fails. |
|lookup.cache |Yes |NONE |String |Available cache strategies for dimension tables:<br><br><br>* FULL: Full table caching, suitable for small tables<br><br>* PARTIAL: Partial caching<br><br>* NONE: No caching |
|lookup.full\-cache.reload\-strategy |No |PERIODIC |String |Define the strategy to reload the Full Cache:<br><br><br>* Periodic: The cache is reloaded at fixed time intervals with no initial delay.<br><br>* Timed: The cache is reloaded at specified times at fixed intervals, which are multiples of a day. |
|lookup.full\-cache.periodic\-reload.interval |No |(none) |Duration |Reinitialization interval for Full Cache under the PERIODIC loading strategy. |
|lookup.full\-cache.periodic\-reload.schedule\-mode |No |FIXED_DELAY |String |Scheduling mode definition under the PERIODIC loading strategy:<br><br>FIXED_DELAY\*:\* The reinitialization interval is the time between the end of the last reload and the start of the next reload.<br><br>FIXED_RATE\*:\* The reinitialization interval is the time between the start of the last reload and the start of the next reload. |
|lookup.full\-cache.timed\-reload.iso\-time |No |(none) |String |Full Cache loading time under TIMED loading strategy, time is in ISO\-8601 format.<br><br>It is useful when a dimension table updates every few days at a specified time. You can specify a time with or without a timezone (the target JVM's local timezone will be used). For example, "10:15" = local TZ, "10:15Z" = UTC TZ, "10:15+07:00" = UTC +7 TZ. |
|lookup.full\-cache.timed\-reload.interval\-in\-days |No |1 |Integer |Under the TIMED loading strategy, the Full Cache loading interval is a multiple of one day. Setting it to 1 means loading once a day, and setting it to 2 means loading once every two days. |


<span id="06fb69fb"></span>
## Example Code


* Result Table.

   ```SQL
   CREATE TABLE datagen_source (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_update_time as localtimestamp
       )
   WITH (
        'connector' = 'datagen',
        'rows-per-second' = '5'            
   );
   
   
   CREATE TABLE jdbc_sink (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_update_time timestamp,
        PRIMARY KEY (order_id) NOT ENFORCED
    ) WITH (
       'connector' = 'jdbc',
       'url' = 'jdbc:mysql://mysq**3fb.rds.byteplus.com:3306/doc_db', 
       'username' = 'admin',      
       'password' = '***',  
       'table-name' = 'orders'
   );
   
   
   insert into jdbc_sink
   select * from datagen_source; 
   ```
   

* Source Table.

   ```sql
   CREATE TABLE jdbc_source (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_status varchar,
        order_update_time timestamp,
        PRIMARY KEY (order_id) NOT ENFORCED
    ) WITH (
       'connector' = 'jdbc',
       'url' = 'jdbc:mysql://mysq**3fb.rds.byteplus.com:3306/doc_db', 
       'username' = 'admin',      
       'password' = 'Passord',  
       'table-name' = 'source_table'
   );
   
    CREATE TABLE print_sink (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_status varchar,
        order_update_time timestamp
       )
   WITH (
        'connector' = 'print'           
   );
   
   insert into print_sink
   select * from jdbc_source; 
   ```
   


<span id="cac6fab5"></span>
## FAQ

<span id="7dae309a"></span>
### Partial Update

JDBC Sink supports partial updates; the columns to be updated can be specified during DDL definition.

For instance, if a table has four columns: id, a, b, c, and only column a is subjected to a partial update, then the DDL only needs to define the id and a fields.

```SQL
CREATE TABLE jdbc_sink ( 
     `id` bigint, 
     a string
     PRIMARY KEY (`id`) NOT ENFORCED 
 ) WITH ( 
    'connector' = 'jdbc', 
    'url' = 'jdbc:mysql://mysq**3fb.rds.byteplus.com:3306/doc_db',  
    'username' = 'admin',       
    'password' = '***',   
    'table-name' = 'test' 
);
```
