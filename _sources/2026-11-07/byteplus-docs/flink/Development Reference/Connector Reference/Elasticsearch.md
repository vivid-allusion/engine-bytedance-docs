---
title: "Elasticsearch"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Elasticsearch"
---

The Elasticsearch connector provides writing capabilities to the Elasticsearch data analytics engine, supporting only data result tables. BytePlus Flink supports both Elasticsearch\-6 and Elasticsearch\-7 versions, with some configuration differences, please be aware of these distinctions.

<span id="e9828686"></span>
## DDL Definitions

```sql
CREATE TABLE elasticsearch_sink (
  user_id STRING,
  user_name STRING,
  uv BIGINT,
  pv BIGINT,
  PRIMARY KEY (user_id) NOT ENFORCED  
)  WITH (
  'connector' = 'elasticsearch-6',
  'hosts' = '<yourHosts>',
  'index' = '<yourIndex>',
  'document-type' = '<yourDocumentType>',
  'username' ='<yourUsername>',
  'password' ='<yourPassword>'
);
```


<span id="6662b9cb"></span>
## WITH Parameters


|**Parameters** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specify the connector to use, either Elasticsearch\-6 or Elasticsearch\-7 connector.<br><br>The connector version must be consistent with the cluster version to avoid compatibility issues. |
|hosts |Yes |(none) |String |Elasticsearch host address, **supports HTTP and HTTPS protocols.**  |
|index |Yes |(none) |String |Index directory. Supports both static and dynamic indexing methods.<br><br><br>* Static index: The static index value must be a pure string, such as `myIndex`, with all data written to the myIndex index.<br><br>* Dynamic index: Use `{field_name}` to reference field values in the record to dynamically generate the target index.<br><br><br>You can also use \*\*{field_name<br><br>For example, if set to \*\*{log_ts |
|document\-type |Mandatory in Elasticsearch\-6. |(none) |String |Document type.<br><br>Not supported in Elasticsearch\-7. |
|document\-id.key\-delimiter |No |_ |String |Document ID delimiter, default is `_`.<br><br>If a primary key is set, it is the delimiter for the primary key. For example, the final _id written to Elasticsearch would be "1_2_3". |
|failure\-handler |No |fail |String |Error handling strategy when Elasticsearch requests fail. The values are as follows:<br><br><br>* fail: Default value, the job fails if the request fails.<br><br>* ignore: Ignore the failure and delete the request.<br><br>* retry\-rejected: Rewrite the record.<br><br>* custom class name: Used to handle failures using a subclass of ActionRequestFailureHandler. |
|sink.flush\-on\-checkpoint |No |true |Boolean |Whether to perform Flush at Checkpoints.<br><br>If this feature is disabled, the connector will not wait for all requests to complete during Checkpoint. |
|sink.bulk\-flush.max\-actions |No |1000 |Integer |The maximum number of batch writes. When set to `0`, it means the batch write function is disabled. |
|sink.bulk\-flush.max\-size |No |2mb |MemorySize |The maximum cache size for batch writes, measured in MB. Setting `0` disables the batch writing feature. |
|sink.bulk\-flush.interval |No |1s |Duration |The refresh interval for batch writes. |
|sink.bulk\-flush.backoff.strategy |No |DISABLED |String |If the Flush operation fails due to temporary request errors, a retry strategy can be specified. The options are as follows:<br><br><br>* DISABLED (default): No retries are performed, and the state remains unchanged after a Flush operation failure.<br><br>* CONSTANT: Retry after waiting for the time set in **sink.bulk\-flush.backoff.delay**.<br><br>* EXPONENTIAL: Exponential backoff, where the waiting time increases exponentially with each backoff. |
|sink.bulk\-flush.backoff.max\-retries |No |8 |Integer |Bulk write failed, maximum retry count. |
|sink.bulk\-flush.backoff.delay |No |50ms |Duration |Bulk write failed, retry interval (for **CONSTANT** retry strategy); also can be understood as the base interval time for retries (for **EXPONENTIAL** retry strategy). |
|connection.max\-retry\-timeout |No |(none) |Duration |Maximum timeout duration for retry requests. |
|connection.path\-prefix |No |(none) |String |Prefix string added to each REST request, generally not set. |
|format |No |json |String |Specify the output format, default is the built\-in `JSON` format. |


<span id="8692f902"></span>
## Sample Code


* Elasticsearch\-6 Result Table

   ```SQL
   create table orders (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time as localtimestamp
     )
   WITH
     (
       'connector' = 'datagen',
       'rows-per-second' = '100',
       'fields.order_status.length' = '3',
       'fields.order_id.min' = '1',
       'fields.order_id.max' = '10000',
       'fields.order_product_id.min' = '1',
       'fields.order_product_id.max' = '100',
       'fields.order_customer_id.min' = '1',
       'fields.order_customer_id.max' = '1000'
     );
   
   
   create table es_sink (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp
     )
   WITH
     (
       'connector' = 'elasticsearch-6',
       'hosts' = 'https://elasticsearch-wu****l8e.escloud.byteplus.com:9200',
       'index' = 'test_orders',
       'document-type' = 'doc',
       'username' = 'admin', 
       'password' = 'cd****456' 
     );
   
   insert into es_sink
   select * from orders;
   ```
   

* Elasticsearch\-7 Result Table

   ```sql
   create table orders (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time as localtimestamp
     )
   WITH
     (
       'connector' = 'datagen',
       'rows-per-second' = '1',
       'fields.order_status.length' = '3',
       'fields.order_id.min' = '1',
       'fields.order_id.max' = '10000',
       'fields.order_product_id.min' = '1',
       'fields.order_product_id.max' = '100',
       'fields.order_customer_id.min' = '1',
       'fields.order_customer_id.max' = '1000'
     );
   
   
   create table es_sink (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp
     )
   WITH
     (
       'connector' = 'elasticsearch-7',
       'hosts' = 'https://elasticsearch-wu****l8e.escloud.byteplus.com:9200',
       'index' = 'test_orders',
       'username' = 'admin', 
       'password' = 'cd****456' 
     );
   
   insert into es_sink
   select * from orders;
   ```
