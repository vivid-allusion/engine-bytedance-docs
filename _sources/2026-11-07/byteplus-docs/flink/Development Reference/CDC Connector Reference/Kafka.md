---
title: "Kafka"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Kafka"
---

The Kafka Pipeline connector can be used as a Data Sink in the Pipeline, writing data to [Kafka](https://www.volcengine.com/docs/6439). This document explains how to set up the Kafka Pipeline connector.

<span id="f2cfb2f6"></span>
## Usage Restrictions


* The Kafka Pipeline connector is currently only supported on engine versions **Flink 1.16\-volcano** and above.


<span id="57a1f1cc"></span>
## **Connector Features**


* Auto Table Creation

* Table Structure Change Synchronization

* Real\-time Data Synchronization


<span id="73aee974"></span>
## **How to Create a Pipeline**

A pipeline that reads data from MySQL and synchronizes it to Kafka can be defined as follows:

```YAML
source:
  type: mysql
  name: MySQL Source
  hostname: 127.0.0.1
  port: 3306
  username: admin
  password: pass
  tables: adb.\., bdb.user_table_[0-9]+, [app|web].order_\.
  server-id: 5401-5404

sink:
  type: kafka
  name: Kafka Sink
  properties.bootstrap.servers: PLAINTEXT://localhost:62510

pipeline:
  name: MySQL to Kafka Pipeline
  parallelism: 2
```


<span id="face13ac"></span>
## **Pipeline connector configuration**


|**Option** |**Required** |**Default** |**Type** |**Description** |
|---|---|---|---|---|
|type |required |(none) |String |Specify the connector to be used, which should be set to 'kafka'. |
|name |optional |(none) |String |The name of the sink. |
|value.format |optional |(none) |String |Data format used for serializing the value part of Kafka messages. Optional values include [debezium-json](https://debezium.io/documentation/reference/stable/integrations/serdes.html) and [canal-json](https://github.com/alibaba/canal/wiki), default value is `debezium-json`, and custom output formats are currently not supported. |
|properties.bootstrap.servers |required |(none) |String |List of host/port pairs used for initial connection with the Kafka cluster. |
|topic |optional |(none) |String |If this parameter is configured, all messages will be sent to this topic. |
|sink.add\-tableId\-to\-header\-enabled |optional |(none) |Boolean |If this parameter is configured, all messages will include headers with keys `namespace`, `schemaName`, `tableName`, and values corresponding to the strings in the event TableId. |
|properties.\* |optional |(none) |String |Pass the Kafka\-supported parameters to the pipeline, see [Kafka consume options](https://kafka.apache.org/28/documentation.html#consumerconfigs). |
|sink.custom\-header |optional |(none) |String |Kafka records custom Headers. Each Header is separated by ',', and key\-value pairs separated by ':'. For example, you can use this format 'key1:value1,key2:value2'. |


<span id="48551a38"></span>
## **Usage Instructions**


* The default topic written to Kafka will correspond to the string of the upstream table `namespace.schemaName.tableName`, but can be modified through the pipeline's route function.

* If a `topic` parameter is configured, all messages will be sent to this one topic.

* If the topic written to Kafka does not exist, it will be created by default.


<span id="6d37b970"></span>
### **Output Format**

The output format varies with different built\-in `value.format` options:

<span id="9b70bd6c"></span>
#### **debezium\-json**

Refer to [Debezium docs](https://debezium.io/documentation/reference/1.9/connectors/mysql.html); the debezium\-json format includes elements such as `before`,`after`,`op`, and `source`, but the `ts_ms` field is not included in the `source` element.

An example of output is:

```JSON
{
  "before": null,
  "after": {
    "col1": "1",
    "col2": "1"
  },
  "op": "c",
  "source": {
    "db": "default_namespace",
    "table": "table1"
  }
}
```


<span id="71422d1e"></span>
#### **canal\-json**

Refer to [Canal | Apache Flink](https://nightlies.apache.org/flink/flink-docs-master/docs/connectors/table/formats/canal/#available-metadata), the canal\-json format includes elements such as `old`, `data`, `type`, `database`, `table`, `pkNames`, but `ts` is not included.

An example of output is:

```JSON
{
    "old": null,
    "data": [
        {
            "col1": "1",
            "col2": "1"
        }
    ],
    "type": "INSERT",
    "database": "default_schema",
    "table": "table1",
    "pkNames": [
        "col1"
    ]
}
```


<span id="59fb83ba"></span>
## **Data Type Mapping**


|**CDC type** |**JSON type** |
|---|---|
|TINYINT |TINYINT |
|SMALLINT |SMALLINT |
|INT |INT |
|BIGINT |BIGINT |
|FLOAT |FLOAT |
|DOUBLE |DOUBLE |
|DECIMAL(p, s) |DECIMAL(p, s) |
|BOOLEAN |BOOLEAN |
|DATE |DATE |
|TIMESTAMP |DATETIME |
|TIMESTAMP_LTZ |TIMESTAMP_LTZ |
|CHAR(n) |CHAR(n) |
|VARCHAR(n) |VARCHAR(n) |
