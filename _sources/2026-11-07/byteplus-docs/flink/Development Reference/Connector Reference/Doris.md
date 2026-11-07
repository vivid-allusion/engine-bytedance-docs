---
title: "Doris"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Connector_Doris"
---

The Doris connector provides read and write capabilities for the Doris database, supporting both source tables and result tables. You can create a source stream to fetch data from a Doris Table as input data for the job; you can also write the job's output data to a Doris Table through a Doris result table.

<span id="8d93d4f2"></span>
## DDL Definition

<span id="cdcfb15e"></span>
### Used as a source (Source)

```SQL
CREATE TABLE doris_source (
   name   STRING,
   score   INT
)  WITH (
   'connector' = 'doris',
   'fenodes' = 'FE_IP:FE_HTTP_PORT',     
   'table.identifier' = 'test.sales_order',  
   'username' = 'root',                     
   'password' = 'password'                          
 );
```


<span id="219bf83c"></span>
### Used as a data destination (Sink)

```SQL
CREATE TABLE doris_sink (
   name   STRING,
   score   INT
)  WITH (
   'connector' = 'doris',
   'fenodes' = 'FE_IP:FE_HTTP_PORT',     
   'table.identifier' = 'test.sales_order',  
   'username' = 'root',                     
   'password' = 'password',                 
   'sink.batch.size' = '500',                
   'sink.batch.interval' = '1s'              
 );
```


<span id="e83ec798"></span>
## WITH parameters


|**Parameters** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specifies the connector to use, here is the Doris connector. |
|fenodes |Yes |(none) |String |The HTTP address of Doris FE is formatted as `FE_IP:FE_HTTP_PORT`, where the PORT is fixed at 8030 and the FE_IP can be any Node IP where Doris is deployed. |
|table.identifier |Yes |(none) |String |The table name is formatted as `db.table`. |
|username |Yes |(none) |String |Username for logging into the Doris database. |
|password |Yes |(none) |String |Password for logging into the Doris database. |
|doris.request.retries |No |3 |Integer |Number of retries for sending requests to Doris. |
|doris.request.connect.timeout.ms |No |30000 |Duration |Connection timeout duration for sending requests to Doris. |
|doris.request.read.timeout.ms |No |30000 |Duration |Read timeout for sending requests to Doris. |
|doris.request.query.timeout.s |No |3600 |Duration |Timeout for querying Doris. Setting to `-1` indicates no timeout limit. |
|doris.request.tablet.size |No |Integer. MAX_VALUE |Integer |The number of Doris Tablets corresponding to a partition.<br><br>The smaller the value, the more partitions, which can improve the parallelism of Flink jobs. |
|doris.batch.size |No |1024 |Integer |Maximum number of rows read from BE in a single fetch.<br><br>Increasing this value can reduce the number of connections between Flink and Doris, thereby lowering network latency. |
|doris.exec.mem.limit |No |2147483648 |Long |Memory limit for a single query. Default is 2GB, measured in bytes. |
|doris.deserialize.arrow.async |No |false |Boolean |Supports asynchronous conversion.<br><br><br>* True: supported.<br><br>* False: not supported. |
|doris.deserialize.queue.size |No |64 |Integer |Asynchronously converts the internal processing queue to Arrow format. |
|doris.read.field |No |(none) |String |Read column names from a Doris table, separated by commas. |
|doris.filter.query |No |(none) |String |Expression for filtering reading data. |
|sink.batch.size |No |1000 |Integer |Maximum number of rows in a single BE write. |
|sink.max\-retries |No |1 |Integer |Maximum number of retries after a BE write failure. |
|sink.batch.interval |No |1s |Duration |Flush interval time, after which the asynchronous thread writes cached data to BE if the time is exceeded.<br><br>The default value is 1 second, supported time units are ms, s, min, h, and d. When set to `0`, it means to turn off regular writing. |


<span id="36718248"></span>
## Sample code


* Result table

   ```SQL
   CREATE TABLE datagen_source (
        siteid INT,
        citycode SMALLINT,
        username STRING,
        pv BIGINT
        )
   WITH (
       'connector' = 'datagen',
       'rows-per-second'='1',    
       'fields.username.length' = '3',
       'fields.siteid.min' = '6',                   
       'fields.siteid.max' = '1000',  
       'fields.citycode.min' = '1',
       'fields.citycode.max' = '100',
       'fields.pv.min' = '1',
       'fields.pv.max' = '1000'
   );
   CREATE TABLE doris_sink (
       siteid INT,
       citycode SMALLINT,
       username STRING,
       pv BIGINT
       ) 
       WITH (
           'connector' = 'doris',
           'fenodes' = 'FE_IP:FE_HTTP_PORT',     
           'table.identifier' = 'DOC.table2',  
           'username' = 'root',                     
           'password' = 'password'                            
   );
   insert into doris_sink
   select * from datagen_source;
   ```
