---
title: "Pulsar"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Pulsar"
---

Apache Pulsar is an open\-source distributed pub\-sub messaging system. Pulsar connectors provide the capability to consume and write data from and to Pulsar Topics, supporting data source tables and result tables.

<span id="ca3ecd94"></span>
## Considerations

Pulsar connectors currently only support use in the **Flink V1.11** engine version.

<span id="87bcea6d"></span>
## DDL Definition

<span id="c5f50bb1"></span>
### Used as a data source

```SQL
CREATE TABLE pulsar_source (
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar
 ) WITH (
     'connector' = 'pulsar',
     'topic' = 'persistent://public/default/topic82547611',
     'service-url' = 'pulsar://localhost:6650',
     'admin-url' = 'http://localhost:8080', 
     'auth-params' = 'token:{topic token}',
     'auth-plugin-classname'='org.apache.pulsar.client.impl.auth.AuthenticationToken',     
     'format' = 'json',
     'scan.startup.mode' = 'latest'
 );
```


<span id="9d4d994d"></span>
### Used as a data destination

```SQL
CREATE TABLE pulsar_sink (
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar
 ) WITH (
     'connector' = 'pulsar',
     'topic' = 'persistent://public/default/topic82547611',
     'service-url' = 'pulsar://localhost:6650',
     'admin-url' = 'http://localhost:8080', 
     'auth-params' = 'token:{topic token}',
     'auth-plugin-classname'='org.apache.pulsar.client.impl.auth.AuthenticationToken',     
     'format' = 'json',
     'scan.startup.mode' = 'latest'
 );
```


<span id="f58be566"></span>
## WITH Parameters


|**Parameter** |**Required** |**Default value** |**Description** |
|---|---|---|---|
|connector |Yes |(none) |Specify the connector to use, here it is the Pulsar connector. |
|service\-url |Yes |(none) |Address of the Pulsar broker service, such as `pulsar://localhost:6650`. |
|admin\-url |Yes |(none) |Address of the Pulsar Admin service, such as `http://localhost:8080`. |
|topic |No |(none) |Specify the name of the Topic from which the data is read. If data is read from multiple Topics, separate the Topics using commas (,).<br><br>This parameter is mutually exclusive with the `topic-pattern` parameter; only one of them should be used. |
|topic\-pattern |No |(none) |Use regular expressions to match the Topics from which the data is read.<br><br>This parameter is mutually exclusive with the `topic` parameter; only one of them should be used. |
|scan.startup.mode |No |latest |Startup mode of Source. Supports `earliest`, `latest`, `external-subscription`, and `specific-offsets` options. |
|scan.startup.specific\-offsets |No |(none) |Specify the message offset.<br><br>When choosing the `specific-offsets` startup mode, it is necessary to set the message offset. |
|scan.startup.sub\-name |No |(none) |When choosing the `external-subscription` startup mode, it is necessary to set this parameter. |
|discovery topic interval |No |(none) |Partition discovery interval, in milliseconds. |
|properties |No |empty |Pulsar optional configuration set in the format `properties.key='value'`. For supported configuration parameters, please refer to the **optional configuration parameter set** in this article. |
|key.format |No |(none) |The serialization format of keys in Pulsar messages. Supports formats such as `raw`, `avro`, `json`. |
|key.fields |No |(none) |The SQL\-defined fields needed when serializing keys. If multiple fields are required, use a comma (,) to connect them. |
|key.fields\-prefix |No |(none) |Define a custom prefix for all fields in the key format to avoid conflicts with fields in the value format.<br><br>By default, the prefix is empty. If a custom prefix is defined, both the Table mode and `'key.fields'` will use the prefixed names. When constructing data types in key format, the prefix will be removed, and non\-prefixed names will be used within the key format. |
|format or value.format |Yes |(none) |The serialization format of the Pulsar message body. Supports formats such as `json` and `avro`. |
|value.fields\-include |No |ALL |Pulsar message body includes field strategy. Supports the `ALL` and `EXCEPT_KEY` options. |
|sink.message\-router |No |key\-hash |Routing method to write messages to Pulsar partitions. Supports `key-hash`, `round-robin`, and reference paths to custom MessageRouter implementation classes. |
|sink.semantic |No |at\-least\-once |The guarantee level of message writing in Sink. Supports `at-least-once`, `exactly-once`, and `none` options. |


<span id="e0e2212f"></span>
## Optional Configuration Set


|**Parameter** |**Default value** |**Description** |
|---|---|---|
|topic |(none) |Pulsar Topic。 |
|topics |(none) |Multiple Pulsar Topics connected with English commas (,). |
|topicspattern |(none) |Use Java regular expressions to match multiple pulsar Topics. |
|partition.discovery.interval\-millis |\-1 |Automatic metadata acquisition interval for Topics. Setting it to \-1 disables this feature; settings greater than 0 enable this feature. |
|clientcachesize |100 |Cache amount for the Pulsar client. |
|auth\-plugin\-classname |(none) |Authentication class for the Pulsar client. |
|auth\-params |(none) |Authentication parameters for Pulsar clients. |
|polltimeoutms |120000 |Timeout for waiting to fetch the next message, in milliseconds. |
|pulsar.reader.fail\-on\-data\-loss |true |Whether to fail upon data loss. |
|pulsar.reader.use\-earliest\-when\-data\-loss |false |When data is lost, reset the offset using earliest. |
|commitmaxretries |3 |Maximum retry attempts when offsetting messages in Pulsar. |
|scan.startup.mode |latest |Start\-up mode for the Source. Supports options `earliest`, `latest`, `external-subscription`, and `specific-offsets`. |
|enable\-key\-hash\-range |false |Enable Pulsar Key\-Shared subscription mode. |
|pulsar.reader.\* | |Details of the Pulsar reader configuration. |
|pulsar.reader.subscriptionRolePrefix |flink\-pulsar\- |When no subscriber is specified, automatically create a prefix for the subscriber name. |
|pulsar.reader.receiverQueueSize |1000 |Receiver queue size. |
|flushoncheckpoint |true |Write messages to Pulsar Topic during Flink snapshotState. |
|failonwrite |false |Continue to acknowledge messages when there is an error in the Sink. |
|send\-delay\-millisecond |0 |Delay message sending, measured in milliseconds. |
|pulsar.producer.sendTimeoutMs |30000 |Timeout period for sending messages, measured in milliseconds. |
|pulsar.producer.blockIfQueueFull |false |When the Producer's message queue is full, it supports blocking methods instead of throwing exceptions. |


<span id="c3d5a38c"></span>
## Sample code

```SQL
create table pulsar_table (
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/topic82547611',
  'service-url' = 'pulsar://localhost:6650',
  'admin-url' = 'http://localhost:8080', 
  'auth-params' = 'token:{topic token}',
  'auth-plugin-classname'='org.apache.pulsar.client.impl.auth.AuthenticationToken',    
  'format' = 'json',
  'scan.startup.mode' = 'latest'
);

create table print_sink (
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar
) WITH (
  'connector' = 'print',
  'print-sample-ratio' = '1'
);

insert into print_sink
select * from pulsar_table;
```
