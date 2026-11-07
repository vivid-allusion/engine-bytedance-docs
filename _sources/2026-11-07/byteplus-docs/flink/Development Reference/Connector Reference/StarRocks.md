---
title: "StarRocks"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Connector_StarRocks"
---

StarRocks connector provides both read and write capabilities for the StarRocks data warehouse, supporting its use as a source table, result table, and dimension table.

<span id="a22c9f86"></span>
## Usage Restrictions


* StarRocks connector is currently only supported in **Flink 1.16\-byted** engine version.

* **It is suggested to replace StarRocks dimension table scenarios with JDBC dimension tables, as the effect is the same. Additionally, JDBC is more widely used and more stable. Refer to** [JDBC](https://docs.byteplus.com/docs/flink/JDBC) **.** 


<span id="f2e92002"></span>
## DDL Definitions

```SQL
CREATE TABLE starrocks_table(
 name VARCHAR,
 score BIGINT
 ) WITH (
 'connector' = 'starrocks',
 'jdbc-url'='jdbc:mysql://fe1_ip:query_port,fe2_ip:query_port,fe3_ip:query_port',
 'load-url'='fe1_ip:http_port;fe2_ip:http_port;fe3_ip:http_port',
 'database-name' = 'doc_db',
 'table-name' = 'table1',
 'username' = 'flinkuser',
 'password' = 'flinkpw'
 );
```


<span id="74daf90f"></span>
## WITH Parameters

<span id="57bc5504"></span>
## General Parameters


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specify the connector to be used, here it is the StarRocks connector. |
|jdbc\-url |is |(none) |String |IP and query port information of FE nodes, separated by commas (,) if multiple.<br><br>Format is `jdbc:mysql://fe_ip1:query_port,fe_ip2:query_port..`. |
|database\-name |is |(none) |String |StarRocks database name. |
|table\-name |Yes |(none) |String |StarRocks table name. |
|username |Yes |(none) |String |StarRocks User Name. |
|password |Yes |(none) |String |StarRocks User Password. |


<span id="63e158bb"></span>
### Source Table Parameters


|**Parameter** |**Required** |**Default** |**Data Type** |**Description** |
|---|---|---|---|---|
|scan\-url |Yes |(none) |String |FE node's IP and http port information, if multiple, should be separated by commas (,).<br><br>Format as `fe_ip1:http_port,fe_ip2:http_port..`. |
|scan.connect.timeout\-ms |No |1000 |String |Timeout duration for connecting to the StarRocks Data Warehouse, in milliseconds. |
|scan.params.keep\-alive\-min |No |10 |String |Keep alive duration for read tasks, in minutes. |
|scan.params.query\-timeout\-s |No |600 |String |The maximum timeout duration for reading tasks, in seconds. |
|scan.params.mem\-limit\-byte |No |1073741824 |String |The memory limit for a single query in BE nodes, measured in bytes. The default value is 1073741824, which is equivalent to 1GB. |
|scan.max\-retries |No |1 |String |Maximum retries after failing to read task |


<span id="6c9eb334"></span>
### Result Table Parameters


|**Parameter** |**Required** |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|load\-url |Is |(none) |String |FE node's IP and http port information, if there are multiple, they should be separated by commas (,).<br><br>The format is `fe_ip1:http_port,fe_ip2:http_port..`. |
|sink.semantic |No |at\-least\-once |String |Data write semantics.<br><br><br>* at\-least\-once: Default value, write at least once.<br><br>* exactly\-once: Write only once, no duplicates.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When configured for <code>exactly-once</code> write semantics, data is only written during checkpoints. Note that at this time, the <code>sink.buffer-flush.*</code> parameters are ineffective.</div><br> |
|sink.version |No |AUTO |String |The interface used during data loading.<br><br><br>* V1: Data loaded using the Stream Load interface.<br><br>* V2: Use the Transaction Stream Load interface to load data, requiring StarRocks to be at least version 2.4.<br><br>* AUTO: Determine if StarRocks supports the Transaction Stream Load interface, then select the version. If supported, select V2; if not, select V1. |
|sink.buffer\-flush.max\-bytes |No |94371840 |String |Before data is written to StarRocks, the maximum amount of data the Buffer can hold, ranging from [64MB, 10GB].<br><br>The default value is 94371840, equivalent to 90MB. |
|sink.buffer\-flush.max\-rows |No |500000 |String |Maximum number of data rows that the buffer can accommodate before writing to StarRocks. |
|sink.buffer\-flush.interval\-ms |No |300000 |String |Buffer flush interval, in milliseconds, with a range of [64,000 to 5,000,000]. |
|sink.max\-retries |No |3 |String |The maximum number of retries for the write task is between 0 and 10. |
|sink.connect.timeout\-ms |No |1000 |String |The timeout duration for connecting to the StarRocks Data Warehouse is in milliseconds, ranging from 100 to 60000. |
|sink.parallelism |No |NULL |String |Specify parallelism.<br><br>If parallelism is not specified, global parallelism is used. |
|sink.properties.\* |No |(none) |String |Result table properties.<br><br>Here are three parameters listed. For more information, please refer to [STREAM LOAD](https://docs.starrocks.io/docs/introduction/StarRocks_intro/).<br><br><br>* sink.properties.format: The data format written into StarRocks, supports CSV and JSON, with the default value being `csv`.<br><br>   * **It is recommended to set it to JSON format, which can avoid data conflicts caused by the CSV delimiter in the CSV format.** <br><br>* sink.properties.column_separator: Used to specify the column separator for CSV format, with the default value being `\t`.<br><br>* sink.properties.row_delimiter: Used to specify the row delimiter for CSV format, with the default value being `\n`. |


<span id="2af76136"></span>
### Dimension Table Parameters


|**Parameter** |**Is it Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|lookup.cache.ttl\-ms |No |5000 |Long |Cache timeout for dimension table queries. |


**Note: For StarRocks dimension table scenarios, it is recommended to replace with JDBC dimension tables, which yield the same results. Moreover, JDBC is more widely used and stable,**  **refer to ** [JDBC Connector](https://arcosite.bytedance.net/sites/1669282940762/63c669547df7d2021de60214/editor/67c5cadf142fe20524761ea7/?docLang=en&bv=655468147c29cc0301edef19) **.** 

<span id="71d82bd4"></span>
## Data Type Mapping


* Source Table

   
   |**StarRocks field type** |**Flink field type** |
   |---|---|
   |NULL |NULL |
   |BOOLEAN |BOOLEAN |
   |TINYINT |TINYINT |
   |SMALLINT |SMALLINT |
   |INT |INT |
   |BIGINT |BIGINT |
   |LARGEINT |STRING |
   |FLOAT |FLOAT |
   |DOUBLE |DOUBLE |
   |DATE |DATE |
   |DATETIME |TIMESTAMP |
   |DECIMAL |DECIMAL |
   |DECIMALV2 |DECIMAL |
   |DECIMAL32 |DECIMAL |
   |DECIMAL64 |DECIMAL |
   |DECIMAL128 |DECIMAL |
   |CHAR |CHAR |
   |VARCHAR |STRING |
   

* Result Table

   
   |**Flink Field Types** |**StarRocks Field Types** |
   |---|---|
   |BOOLEAN |BOOLEAN |
   |TINYINT |TINYINT |
   |SMALLINT |SMALLINT |
   |INTEGER |INTEGER |
   |BIGINT |BIGINT |
   |FLOAT |FLOAT |
   |DOUBLE |DOUBLE |
   |DECIMAL |DECIMAL |
   |BINARY |INT |
   |CHAR |STRING |
   |VARCHAR |STRING |
   |STRING |STRING |
   |DATE |DATE |
   |TIMESTAMP_WITHOUT_TIME_ZONE(N) |DATETIME |
   |TIMESTAMP_WITH_LOCAL_TIME_ZONE(N) |DATETIME |
   |ARRAY |ARRAY |
   |MAP<KT,VT\> |JSON STRING |
   |ROW |JSON STRING |
   


<span id="e88fee11"></span>
## Sample Code


* Source Table

   ```SQL
   CREATE TABLE starrocks_source (
       id INTEGER,
       name STRING,
       score INTEGER,
       PRIMARY KEY (id) NOT ENFORCED
   ) WITH (
     'connector' = 'starrocks',
     'jdbc-url' = 'jdbc:mysql://172.28.*.*:9030', 
     'scan-url' = '172.28.*.*:8030', 
     'database-name' = 'doc_db',
     'table-name' = 'table1',
     'username' = 'docuser',
     'password' = 'docpw'
   );
   
   CREATE TABLE print_sink (
       id INTEGER,
       name STRING,
       score INTEGER
   ) WITH (
     'connector' = 'print'
   );
   
   INSERT INTO print_sink
   SELECT * FROM starrocks_source;
   ```
   

* Result Table

   ```SQL
   CREATE TABLE datagen_source(
     id INTEGER,
     name STRING,
     score INTEGER
   ) WITH (
     'connector' = 'datagen',
     'rows-per-second' = '1',
     'fields.name.length' = '9',
     'fields.id.min' = '1',
     'fields.id.max' = '1000',
     'fields.score.min' = '1',
     'fields.score.max' = '1000'
   );
   
   CREATE TABLE starrocks_sink(
     id INTEGER,
     name STRING,
     score INTEGER,
     PRIMARY KEY (id) NOT ENFORCED
   ) WITH (
     'connector' = 'starrocks',
     'jdbc-url' = 'jdbc:mysql://172.28.*.*:9030', 
     'load-url' = '172.28.*.*:8030', 
     'database-name' = 'doc_db',
     'table-name' = 'table1',
     'username' = 'docuser',
     'password' = 'docpw',
     'sink.parallelism' = '1'
   );
   
   
   INSERT INTO starrocks_sink
   SELECT * FROM datagen_source;
   ```
   

* **Dimension Table (using JDBC dimension tables to read the SR table)** 

   ```SQL
   CREATE TABLE datagen_source (
       id1 INTEGER,
       name1 STRING,
       score1 INTEGER,
       proc_time as PROCTIME ()
     )
   WITH
     (
       'connector' = 'datagen',
       'rows-per-second' = '1',
       'fields.name1.length' = '9',
       'fields.id1.min' = '1',
       'fields.id1.max' = '1000',
       'fields.score1.min' = '1',
       'fields.score1.max' = '1000'
     );
   
   
   CREATE TABLE starrocks_lookup (
       id INTEGER,
       name STRING,
       score INTEGER,
       PRIMARY KEY (id) NOT ENFORCED
     )
   WITH
     (
       'connector' = 'jdbc',
       'url' = 'jdbc:mysql://192.*.*.*:3306/doc_db',     
       'table-name' = '<yourtablename>',
       'username' = 'admin',          
       'password' = 'MyPa$$w0rd',      
       'lookup.cache.max-rows' = '100',
       'lookup.max-retries' = '3'
     );
   
   
   CREATE TABLE print_sink (
       id1 INTEGER,
       name1 STRING,
       score1 INTEGER,
       id INTEGER,
       name STRING,
       score INTEGER
     )
   WITH
     ('connector' = 'print');
   
   
   INSERT INTO
     print_sink
   SELECT
     datagen_source.id1,
     datagen_source.name1,
     datagen_source.score1,
     starrocks_lookup.id,
     starrocks_lookup.name,
     starrocks_lookup.score
   FROM
     datagen_source
     LEFT JOIN starrocks_lookup FOR SYSTEM_TIME AS OF proc_time ON datagen_source.id1 = starrocks_lookup.id;
   ```
   


<span id="696a2542"></span>
## FAQ

<span id="685e3404"></span>
### CSV Format Delimiter Issue

In CSV format, if the data contains CSV delimiters, it will cause StarRocks to decode the data incorrectly, splitting the columns incorrectly. This results in a different count of output columns compared to the actual number, generating the following error:

> errorLog: Error: Target column count: 17 doesn't match source value column count: 12


It is recommended to switch to JSON format to avoid the above issues.

<span id="a3827c59"></span>
### Multi\-Warehouse Writing in StarRocks

Multi\-warehouse is a resource isolation mechanism in StarRocks, where each warehouse can bind a separate group of BE nodes to isolate resources.

Steps for writing into StarRocks multi\-warehouse with Flink are as follows:


1. Use version 1.2.10 of the community Connector and rely on this file in the Flink job. Connector Jar download link is as follows: (Note: The current platform has integrated version 1.2.9, and after integrating 1.2.10, dependency on the Jar file will no longer be necessary)


https://github.com/StarRocks/starrocks\-connector\-for\-apache\-flink/releases/download/v1.2.10/flink\-connector\-starrocks\-1.2.10_flink\-1.16.jar


2. Add the following parameters in the option of StarRocks DDL:


```SQL
'sink.version'='V1',
'sink.semantic'='at-least-once',
'sink.properties.strip_outer_array'='true'
```


The last parameter is to ensure compatibility with the V1 version of the Sink, which does not support certain import forms; primarily, the first two parameters play a role.
