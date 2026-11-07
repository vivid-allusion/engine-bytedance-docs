---
title: "Redis"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Redis"
---

Redis Connector offers the capability to write to Redis cache databases, supporting both result tables and dimension tables.

Using Redis Connector for result tables and dimension tables provides various scalability advantages:


|**Type** |**Advantages** |
|---|---|
|Result table |* String data type supports serialization writing in specified formats.<br><br>* Writing supports setting data expiration time.<br><br>* Supports batch writing. |
|Dimension table |* String type data supports deserialization reading in the specified format.<br><br>* Supports enabling cache.<br><br>* Supports delayed join. |


<span id="6ee86c67"></span>
## DDL Definition

```SQL
CREATE TABLE redis_sink (
  key VARCHAR PRIMARY KEY NOT ENFORCED,
  val VARCHAR
) WITH (
  'connector' = 'redis',
  'redis-mode' = 'single-node',
  'host' = '172.0.0.1',
  'port' = '6379',
  'value-type' = 'string'
);
```


<span id="00811ca4"></span>
## **WITH Parameters**

<span id="7f3bbac5"></span>
### General Parameters


|**Parameter** |**Mandatory** |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|connector |Is |(none) |String |Specify the connector to use; this is the Redis connector. |
|value\-type |No |string |Enum |Data types supported by the Redis database. The values are as follows:<br><br><br>* String: Basic string type.<br><br>   * The result table supports `set`, `setex`, `incrby`, and `incrbyfloat` commands.<br><br>   * The dimension table supports the `get` command.<br><br>* Hash: Hash type.<br><br>   * The result table supports `hmset`, `hincrby`, and `hincrbyfloat` commands.<br><br>   * The dimension table supports the `hmget` command.<br><br>* List: List type.<br><br>   * The result table supports the `lpush` command.<br><br>   * The dimension table supports the `lrange` command.<br><br>* Set: Collection type.<br><br>   * The result table supports the `sadd` command.<br><br>   * The dimension table supports the `smembers` command.<br><br>* zset: Sorted Set type.<br><br>   * The result table supports the `zadd` command.<br><br>   * The dimension table supports the `zrange` command. |
|format |no |(none) |String |When the data type is String, the format for serialization and deserialization includes: json, pb, etc.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If 'format' is configured, 'value\-type' does not need to be configured.</div><br> |
|redis\-mode |Yes |single\-node |Enum |Mode for connecting to the Redis database, options include:<br><br><br>* single\-node (single\-node mode)<br><br>* cluster (cluster mode)<br><br>* sentinel (sentinel high availability mode) |
|host |(Mandatory in single\-point mode) |172.0.0.1 |String |Address of Redis Server in single\-point mode, such as `172.0.0.1`. |
|port |(Mandatory in single\-point mode) |6379 |String |Connection port of Redis Server in single\-point mode, default value is 6379. |
|cluster.nodes |(required for cluster mode) |(none) |String |List of hosts in cluster mode, separated by semicolons; host and IP are divided by a semicolon (;). For example: "127.0. *.* :6379;10.133. *.* :6379;10.248. *.* :6379" |
|master.name |(required for sentinel mode) |(none) |String |The name of the master in sentinel mode. |
|sentinels.info |(Required for sentinel mode) |(none) |String |Information of sentinels in sentinel mode, list separated by semicolons. |
|db |No |0 |Integer |Connected Redis database. |
|password |No |(none) |String |Password for Redis database login. The default value is empty, indicating that no authorization is required.<br><br>If the Redis cluster requires authentication, a password needs to be filled out. |
|connection.timeout |No |2 seconds |Duration |Connection timeout duration. |
|connection.socket.timeout |No |2 seconds |Duration |Socket timeout duration. |
|connection.max\-retries |No |5 |Integer |Maximum number of retry attempts for failed connections. |
|connection.max\-total\-num |No |5 |Integer |Maximum number of connections. |
|connection.max\-idle\-num |No |5 |Integer |Maximum idle connections. |
|connection.min\-idle\-num |No |5 |Integer |Minimum idle connections. |
|rate\-limit\-num |No |(none) |Integer |Configuration for the job’s rate limiting.<br><br>For example, if this parameter is set to 1000000, it means the total OPS for the operator does not exceed 1 million.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Throttling is distributed evenly among all subtasks considering data balance and software quota calculations; hence, set the throttling limit not too low.</div><br> |


<span id="378a029e"></span>
### Result Table Parameters


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|sink.mode |No |insert |Enum |Data Write Mode. The values are as follows:<br><br><br>* Insert (default)<br><br>* Incr (incremental write mode)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Incr mode for incremental writing supports scenarios using String and Hash's incrby; for other scenarios, please use the default value.</div><br> |
|sink.record.ttl |No |(none) |Duration |The data written will be kept permanently by default.<br><br>When setting, you can specify the following units:<br><br><br>* DAYS: such as `1 d` or `1 day`.<br><br>* HOURS: such as `1 h` or `1 hour`.<br><br>* MINUTES: such as `1 min` or `1 minute`.<br><br>* SECONDS: such as `1 s`, `1 sec` or `1 second`.<br><br>* MILLISECONDS: Such as `1 ms`, `1 milli` or `1 millisecond`.<br><br>* MICROSECONDS: Such as `1 µs`, `1 micro` or `1 microsecond`.<br><br>* NANOSECONDS: Such as `1 ns`, `1 nano` or `1 nanosecond`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no unit is specified during setup, the default is milliseconds; the unit is case\-insensitive, and spaces between numbers and units can be omitted.</div><br> |
|sink.max\-retries |No |5 |Integer |Maximum number of retries on write failure. |
|value.format.skip\-key |No |true |Boolean |When serializing, does the value include the primary key?<br><br><br>* true: Indicates that it does not include the primary key.<br><br>* false: Includes the primary key. |
|sink.ignore\-delete |No |true |Boolean |Does it filter out upstream retract messages? |
|sink.ignore\-null |No |false |Boolean |Whether to filter out null values before writing. |
|sink.buffer\-flush.max\-rows |No |50 |Integer |Batch write count: Determines the maximum number of records to accumulate before writing to Redis. When the number of records exceeds this configured value, data will be written to Redis. Can be set to 0 to disable this batch writing feature. |
|sink.buffer\-flush.interval |No |2s |Duration |Batch write interval: Used to determine the time interval for asynchronous threads writing data to Redis. When this interval is reached, the data will be written to Redis. Can be set to 0 to disable this timed writing feature. |


<span id="54eda91f"></span>
### Dimension Table Parameters


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|lookup.cache.max\-rows |No |(none) |Integer |Maximum number of data entries for dimension table cache.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Caching is disabled by default. To enable it, both <code>lookup.cache.max-rows</code> and <code>lookup.cache.ttl</code> parameters must be configured.</div><br> |
|lookup.cache.ttl |No |(none) |Duration |Expiration time of the dimension table cache.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Caching is disabled by default. To enable it, both <code>lookup.cache.max-rows</code> and <code>lookup.cache.ttl</code> parameters must be configured.</div><br> |
|lookup.max\-retries |No |3 |Integer |Maximum number of retries for failed dimension table queries. |
|lookup.cache\-null\-value |No |true |Boolean |Whether to cache null data, effective only when caching is enabled. |
|lookup.later\-join\-retry\-times |No |0 |Duration |Interval time for delayed Join. |
|lookup.later\-join\-latency |No |1 |Integer |Number of retries for delayed Join. |
|lookup.enable\-input\-keyby |No |false |Boolean |Whether upstream data is hashed according to the Join key and distributed to the Join operator. |


<span id="f3213970"></span>
## Sample Code

<span id="fc0ecff7"></span>
### Single\-node Mode

```SQL
create table datagen_source (
    key varchar,
    val varchar
) with (
    'connector' = 'datagen',
    'rows-per-second' = '5',
    'fields.key.length' = '2',
    'fields.val.length' = '5'
 );
 
 create table redis_sink (
     key varchar PRIMARY KEY NOT ENFORCED,
     val varchar
 ) with (
     'connector' = 'redis',
     'redis-mode' = 'single-node',
     'host' = '172.0.0.1',
     'port' = '6379',
     'password' = 'Pw**5',
     'value-type' = 'string'
);

insert into redis_sink
select * from datagen_source;
```


<span id="d3f25fb5"></span>
### Cluster mode

```SQL
create table datagen_source (
    key varchar,
    val varchar
) with (
    'connector' = 'datagen',
    'rows-per-second' = '5',
    'fields.key.length' = '2',
    'fields.val.length' = '5'
 );
 
 create table redis_sink (
     key varchar PRIMARY KEY NOT ENFORCED,
     val varchar
 ) with (
     'connector' = 'redis',
     'redis-mode' = 'cluster',
     'cluster.nodes' = 'redis-cnl**ymz.redis.ivolces.com:6379',
     'password' = 'Pw**5',
     'value-type' = 'string'
);

insert into redis_sink
select * from datagen_source;
```


<span id="8115a541"></span>
### String data type


* Specify format

   ```SQL
   create table redis_tb (
     id int primary key not enforced,
     name varchar,
     age int,
     gender boolean,
     description varchar
   ) with (
     'connector' = 'redis',
     'redis-mode' = 'single-node',
     'host' = '172.0.0.1',
     'port' = '6379',
     'password' = 'Pw**5',
     'format' = 'json'
   )
   ```
   

* Incremental writing

   ```SQL
   create table redis_tb (
     id int primary key not enforced,
     val long
   ) with (
     'connector' = 'redis',
     'redis-mode' = 'single-node',
     'host' = '172.0.0.1',
     'port' = '6379',
     'password' = 'Pw**5',
     'value-type' = 'string',
     'sink.mode' = 'incr'
   )
   ```
   


<span id="a8b88d99"></span>
### Hash data type


* Normal read and write

   ```SQL
   create table redis_tb (
     key int primary key not enforced,
     field1 varchar,
     field2 int,
     field3 boolean
   ) with (
     'connector' = 'redis',
     'redis-mode' = 'single-node',
     'host' = '172.0.0.1',
     'port' = '6379',
     'password' = 'Pw**5',
     'value-type' = 'hash'
   )
   ```
   

* Incremental writing

   ```SQL
   create table redis_tb (
     key int primary key not enforced,
     field1 varchar,
     val long,
   ) with (
     'connector' = 'redis',
     'redis-mode' = 'single-node',
     'host' = '172.0.0.1',
     'port' = '6379',
     'password' = 'Pw**5',
     'value-type' = 'hash',
     'sink.mode' = 'incr'
   )
   ```
   


<span id="4bf224e3"></span>
### List and Set data types

Normal read and write


* The item field is used for writing.

* The vals field is used for dimension table reads.


```SQL
create table redis_tb (
  key int primary key not enforced,
  item varchar,
  vals array<varchar>
) with (
  'connector' = 'redis',
  'redis-mode' = 'single-node',
  'host' = '172.0.0.1',
  'port' = '6379',
  'password' = 'Pw**5',
  'value-type' = 'list'
)
```


<span id="430c75ba"></span>
### ZSet data type

Ordinary read and write


* The score and item fields are used for writing.

* The vals field is used for dimension table reads.


```SQL
create table redis_tb (
  key int primary key not enforced,
  score double,
  item varchar,
  vals array<varchar>
) with (
  'connector' = 'redis',
  'redis-mode' = 'single-node',
  'host' = '172.0.0.1',
  'port' = '6379',
  'password' = 'Pw**5',
  'value-type' = 'zset'
)
```
