---
title: "RocketMQ"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/RocketMQ"
---

RocketMQ Connector provides the capability to consume and write data from and to RocketMQ Topics, supporting use as both source and sink tables. You can create a source stream to retrieve data from RocketMQ Topics as input for the job; you can also use the RocketMQ sink table to write job output data back into RocketMQ Topics.

<span id="60216699"></span>
## Precautions


* The RocketMQ Connector is currently only supported in **Flink 1.16\-volcano** and higher engine versions.

* Current support for `MessageQueue` auto\-discovery is not available. If RocketMQ is scaled up, please stop the job after scaling up and restart it, choosing to resume from the last state (restarting from the next successful checkpoint can reduce duplicates).

* Please note to enable checkpointing; otherwise, data consumption cannot be ensured to be neither lost nor duplicated.


<span id="fbbf884b"></span>
## DDL Definitions

<span id="9b322888"></span>
### Used as a Data Source (Source)

```SQL
create table rmq_src (
    `id` BIGINT,
    `name` VARCHAR
) with (
    -- connector name, fixed as rocketmq
    'connector' = 'rocketmq',  
    -- Enter the access address from the RMQ product page
    'endPoint' = 'http://rocketmq-cnng535a1c59df3d.rocketmq.ivolces.com:9876',
    -- Enter the topic you're accessing
    'topic' = 'flink-rmq-test-topic',
    -- Enter the group ID, registerable on the RMQ product page
    'group' = 'GID-flink_rmq_connector_test_group',
    -- Enter the AK/SK with read permissions, available in the secret management section of the RMQ product page
    'accessId' = 'xxx',
    'accessKey' = 'xxx',
    -- Enter the format built into Flink
    'format' = 'json',
    -- When there is no data upstream for consumption, the source sleeps
    'pullIntervalMs' = '500'
);

create table print_sink (
    `id` BIGINT,
    `name` VARCHAR
) with (
    'connector' = 'print'
);

insert into print_sink
select * from rmq_src;
```


<span id="d1485470"></span>
### Used as a Data Destination (Sink)

```SQL
create table src (
    `id` BIGINT,
    `name` VARCHAR,
    proc_time as proctime()
) with (
    'connector' = 'datagen',
    'rows-per-second' = '3',
    'fields.id.min' = '1',
    'fields.id.max' = '20',
    'fields.name.length' = '3'
);

create table rmq_sink (
    `id` BIGINT,
    `name` VARCHAR
) with (
    -- Connector name, fixed as rocketmq
    'connector' = 'rocketmq',  
    -- Enter the access address of the RMQ product page
    'endPoint' = 'http://rocketmq-cnng535a1c59df3d.rocketmq.ivolces.com:9876',
    -- Enter the topic to access
    'topic' = 'flink-rmq-test-topic',
    -- Enter the group id, which can be registered on the RMQ product page
    'group' = 'GID-flink_rmq_connector_test_group',
    -- Enter the AK SK with read permissions, available in the key management section of the RMQ product page
    'accessId' = 'xxx',
    'accessKey' = 'xxx',
    -- Retry count for write failures defaults to 10
    'retryTimes' = '10',
    -- Retry interval for write failures defaults to 5s
    'sleepTimeMs' = '5000',
    -- Write format: json
    'format' = 'json'
);

insert into rmq_sink
select id, name from src;
```


<span id="38b6f1af"></span>
## With parameters

<span id="41388a89"></span>
### Universal


|**Parameters** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |None |String |Specifies the connector to use, in this case the rocketmq connector. |
|endPoint |Yes |No |String |The URL of the RocketMQ version product page for the message queue, such as http://rocketmq\-xxx.rocketmq.ivolces.com:9876 |
|topic |Yes |No |String |The name of the topic being accessed |
|group |Yes |None |String |Group name of Consumer or Producer. |
|accessId |Yes |None |String |Enter the AK with read permissions, which can be viewed in the Key Management on the RocketMQ version product page. |
|accessKey |yes |none |String |Enter the SK with read permission, which can be found in the key management section of the RocketMQ message queue product page |
|format |yes |none |String |Specify the Flink format to use |


<span id="549b4928"></span>
### Unique to the source table


|**parameter** |**Is Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|pullIntervalMs |Yes |None |Int |Sleep time of the source when there is no data available upstream. Unit in milliseconds. Currently, there is no throttling mechanism to set the rate of reading from RocketMQ. |


<span id="c23b107b"></span>
### Unique to the result table


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|retryTimes |No |10 |Int |The number of write retries. |
|sleepTimeMs |No |5000 |Long |Retry interval time. |
