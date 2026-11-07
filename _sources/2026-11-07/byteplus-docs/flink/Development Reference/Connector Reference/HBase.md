---
title: "HBase"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/HBase"
---

The HBase connector provides read and write capabilities for distributed HBase database tables, supporting them as source tables, result tables, and dimension tables.

<span id="1392188c"></span>
## Usage Restrictions

Flink currently offers HBase\-1.4 and HBase\-2.2 connectors. Please choose according to the actual situation:


* Only the HBase\-1.4 connector is supported in the **Flink 1.11\-byted** engine version.

* The **Flink 1.16\-byted** engine version supports both HBase\-1.4 and HBase\-2.2 connectors.


<span id="2b1c1762"></span>
## Precautions

When connecting to Byteplus HBase in a public network environment, you need to add the following two parameters:


* `'properties.zookeeper.znode.metaserver' = 'public-meta-region-server'`

* `'properties.zookeeper.znode.master' = 'public-master'`


<span id="3703286f"></span>
## DDL Definition

```SQL
CREATE TABLE hbase_source (
    rowkey INT,               --行键
    family1 ROW<q1 INT>,      --声明列族、列和列名
    family2 ROW<q2 STRING, q3 BIGINT>,
    family3 ROW<q4 DOUBLE, q5 BOOLEAN, q6 VARCHAR>,
    PRIMARY KEY (rowkey) NOT ENFORCED   --行键定义为主键
 ) WITH (
     'connector' = 'hbase-1.4',
     'table-name'='<yourTableName>',
     'zookeeper.quorum'='<yourZookeeperQuorum>'
 );
```


Introduction to DDL Statements:


* It is necessary to declare the HBase Row Key.

* The Row Key of HBase needs to be defined as the table's Primary Key, which by default, is also the Row Key if it's not specified.

* The Column Family of HBase must be declared as ROW type, with the family name serving as the field name for that ROW. For example, the definition declares three Column Families: family1, family2, and family3.

* In HBase, the Columns in a Column Family correspond to each nested field in the corresponding ROW, with the column name being the field name. For instance, in the column family family2, q2 and q3 represent the field names of two columns.

* Apart from the fields of ROW type, there can only be one primitive type field, which will be considered the HBase Row Key, like the rowkey defined in the definition.


<span id="c62cb296"></span>
## WITH Parameters

<span id="f81b81e0"></span>
### General Parameters


|**Parameter** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specifies the connector to be used.<br><br><br>* In the **Flink 1.11\-byted** engine version, only the HBase\-1.4 connector is supported.<br><br>* In the **Flink 1.16\-byted** engine version, both HBase\-1.4 and HBase\-2.2 connectors are supported. |
|table\-name |yes |(none) |String |Specify the HBase table name to read data from. |
|zookeeper.quorum |yes |(none) |String |The zookeeper address of HBase. |
|zookeeper.znode.parent |No |/hbase |String |The root directory of HBase in zookeeper. |
|null\-string\-literal |No |null |String |When the HBase field type is a string, if the Flink field data is null, assign that field to `null-string-literal` and write it to HBase. |
|properties.\* |No |(none) |String |Configuration parameters passed to HBase. For specific parameters, see [HBase Default Configuration](https://hbase.apache.org/2.3/book.html#hbase_default_configurations).<br><br>Flink will remove `properties.` and pass the remaining configurations to the underlying HBase client.<br><br>Example: 'properties.hbase.security.authentication' = 'kerberos' configures Kerberos authentication. |


<span id="8bca4450"></span>
### Result Table Parameters


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|sink.buffer\-flush.max\-size |No |2mb |MemorySize |The amount of data cached in memory before being written to HBase. Increasing this value can improve the write performance of HBase, but it can also increase write latency and memory usage.<br><br>The default value is 2MB, supporting byte units B, KB, MB, and GB, case\-insensitive. Setting it to 0 means no caching will be performed. |
|sink.buffer\-flush.max\-rows |No |1000 |Integer |Before writing to HBase, the number of data items cached in memory. Increasing this value can enhance the write performance of HBase, but it will increase the write latency and memory usage.<br><br>The default value is 1000, setting it to 0 means no caching will be performed. |
|sink.buffer\-flush.interval |No |1s |Duration |The interval for writing cached data into HBase controls the write latency to HBase.<br><br>The default value is 1 second, supports time units ms, s, min, h, and d. Setting to 0 turns off periodic writes. |
|sink.parallelism |No |(none) |Integer |Define the parallelism for the HBase sink.<br><br>By default, the parallelism is determined by the framework, consistent with the parallelism of upstream and downstream operators. |


<span id="5a5560ff"></span>
## Dimension Table Parameters


|**Parameter** |**Required?**  |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|lookup.cache |No |NONE |Enum |Cache strategy for dimension tables.<br><br><br>* NONE: No cache.<br><br>* PARTIAL: Cache partial data in the dimension table. Each entry in the source table triggers the system to first search in the Cache; if not found, it then searches in the physical dimension table. |
|lookup.partial\-cache.max\-rows |No |(none) |Long |Maximum rows to cache; exceeding this limit, the oldest rows will expire.<br><br>This option can only be used when set to PARTIAL cache strategy. |
|lookup.partial\-cache.expire\-after\-write |No |(none) |Duration |After writing to the cache, the maximum lifetime of each row in the cache.<br><br>This option can only be used when set to PARTIAL cache strategy. |
|lookup.partial\-cache.expire\-after\-access |No |(none) |Duration |After accessing the cache, the maximum lifetime of each row in the cache.<br><br>This option can only be used when set to the PARTIAL cache strategy. |
|lookup.partial\-cache.cache\-missing\-key |No |true |Boolean |If the primary key does not match any row in the table, whether to continue caching the non\-existent key.<br><br>This option can only be used when set to the PARTIAL cache strategy. |
|lookup.max\-retries |No |3 |Integer |Maximum retries when database search fails. |


<span id="c103291c"></span>
## Data Type Mapping

The HBase connector uses the utility class provided by `org.apache.hadoop.hbase.util.Bytes` to convert Flink data types into byte arrays, which are then stored in HBase. When reading, convert the byte arrays into specific type objects.

The conversion method is as follows:


|Flink field type |HBase conversion |
|---|---|
|CHAR / VARCHAR / STRING |byte[] toBytes(String s)<br><br>String toString(byte[] b) |
|BOOLEAN |byte[] toBytes(boolean b)<br><br>boolean toBoolean(byte[] b) |
|BINARY / VARBINARY |byte[] |
|DECIMAL |byte[] toBytes(BigDecimal v)<br><br>BigDecimal toBigDecimal(byte[] b) |
|TINYINT |new byte[] { val }<br><br>bytes[0] |
|SMALLINT |byte[] toBytes(short val)<br><br>short toShort(byte[] bytes) |
|INT |byte[] toBytes(int val)<br><br>int toInt(byte[] bytes) |
|BIGINT |byte[] toBytes(long val)<br><br>long toLong(byte[] bytes) |
|FLOAT |byte[] toBytes(float val)<br><br>float toFloat(byte[] bytes) |
|DOUBLE |byte[] toBytes(double val)<br><br>double toDouble(byte[] bytes) |
|DATE |Convert the date to the number of days since January 1, 1970, represented as int, and convert it to a byte array using byte[] toBytes(int val). |
|TIME |Convert time to the number of milliseconds since 00:00:00, represented as int, and convert it to a byte array using byte[] toBytes(int val). |
|TIMESTAMP |Convert the timestamp into the number of milliseconds since January 1, 1970, represented by long, and convert it into a byte array using byte[] toBytes(long val). |
|ARRAY |Not supported. |
|MAP / MULTISET |Not supported. |
|ROW |Not supported. |


<span id="265f296e"></span>
## Sample Code


* Result Table

   ```SQL
   CREATE TABLE datagen_source (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_status varchar,
        order_update_time as localtimestamp
       )
   WITH (
       'connector' = 'datagen',
       'rows-per-second' = '1',
       'fields.order_status.length' = '3',
       'fields.order_id.min' = '1',
       'fields.order_id.max' = '1000',
       'fields.order_product_id.min' = '1',
       'fields.order_product_id.max' = '100',
       'fields.order_customer_id.min' = '1',
       'fields.order_customer_id.max' = '1000'        
   );
   
   CREATE TABLE hbase_sink (
       order_id bigint,
       order_info ROW (
         order_product_id bigint,
         order_customer_id bigint,
         order_status varchar,
         order_update_time TIMESTAMP(0)
           )
       )
   WITH (
     'connector' = 'hbase-1.4',
     'table-name' = 'orders',
     'zookeeper.quorum' = 'hb-a***929-zk.config.byteplus.com:2181'
   );
   
   insert into hbase_sink
   select
     order_id,
     ROW (
       order_product_id,
       order_customer_id,
       order_status,
       order_update_time
     ) as order_info
   from
     datagen_source;
   ```
   

* Dimension Table

   ```SQL
   CREATE TABLE orders (
       rowkey bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time as localtimestamp,
       proc_time as PROCTIME ()
     )
   WITH
     (
       'connector' = 'datagen',
       'rows-per-second' = '1',
       'fields.order_status.length' = '3',
       'fields.order_product_id.min' = '1',
       'fields.order_product_id.max' = '100',
       'fields.order_customer_id.min' = '1',
       'fields.order_customer_id.max' = '1000'
     );
   
   
   CREATE TABLE hbase_sink (
       rowkey bigint,
       cf1 ROW (
         order_product_id1 bigint,
         order_customer_id1 bigint,
         order_status1 varchar,
         order_update_time1 TIMESTAMP(0)
       )
     )
   WITH
     (
       'connector' = 'hbase-1.4',
       'table-name' = 'orders',
       'zookeeper.quorum' = 'hb-a***929-zk.config.byteplus.com:2181'
     );
   
   
   create table print_sink (
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_product_id1 bigint,
       order_customer_id1 bigint,
       order_status1 varchar
     )
   with
     ('connector' = 'print');
   
   
   insert into print_sink
   SELECT
     orders.order_product_id,
     orders.order_customer_id,
     orders.order_status,
     hbase_sink.order_product_id1,
     hbase_sink.order_customer_id1,
     hbase_sink.order_status1
   FROM
     orders
     LEFT JOIN hbase_sink FOR SYSTEM_TIME AS OF orders.proc_time ON orders.rowkey = hbase_sink.rowkey;
   ```
