---
title: "Overview"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Formats_Overview"
---

Flink provides a set of table formats to be used with table connectors. A table format is a storage format that defines how to map binary data to the columns of a table.

<span id="4448e1b9"></span>
## Flink Supported Formats

<span id="47511795"></span>
## Overview


|**Formats** |**Supported Connectors** |Flink Version Support |
|---|---|---|
|[CSV](https://docs.byteplus.com/docs/flink/CSV) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.11, 1.16 |
|[JSON](https://docs.byteplus.com/docs/flink/JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem)[Elasticsearch](https://docs.byteplus.com/docs/flink/Elasticsearch)[Redis](https://docs.byteplus.com/docs/flink/Redis)[Pulsar](https://docs.byteplus.com/docs/flink/Pulsar) |1.11, 1.16 |
|[Debezium-JSON](https://docs.byteplus.com/docs/flink/Debezium-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.11, 1.16 |
|[Canal-JSON](https://docs.byteplus.com/docs/flink/Canal-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.11, 1.16 |
|[Maxwell-JSON](https://docs.byteplus.com/docs/flink/Maxwell-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.16 |
|[Ogg-JSON](https://docs.byteplus.com/docs/flink/Ogg-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.16 |
|[Avro](https://docs.byteplus.com/docs/flink/Avro) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem)[Pulsar](https://docs.byteplus.com/docs/flink/Pulsar) |1.16 |
| |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.16 |
|[Protobuf](https://docs.byteplus.com/docs/flink/Protobuf) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Redis](https://docs.byteplus.com/docs/flink/Redis) |1.16 |
|[Parquet](https://docs.byteplus.com/docs/flink/Parquet) |[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.11, 1.16 |
|[ORC](https://docs.byteplus.com/docs/flink/ORC) |[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.11, 1.16 |
|[Raw](https://docs.byteplus.com/docs/flink/Raw) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |1.16 |


<span id="f931cb64"></span>
## Version Details

<span id="5c82c058"></span>
### Flink 1.16 Supported Formats


|**Formats** |**Supported Connectors** |
|---|---|
|[CSV](https://docs.byteplus.com/docs/flink/CSV) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[JSON](https://docs.byteplus.com/docs/flink/JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem)[Elasticsearch](https://docs.byteplus.com/docs/flink/Elasticsearch)[Redis](https://docs.byteplus.com/docs/flink/Redis)[Pulsar](https://docs.byteplus.com/docs/flink/Pulsar) |
|[Debezium-JSON](https://docs.byteplus.com/docs/flink/Debezium-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Canal-JSON](https://docs.byteplus.com/docs/flink/Canal-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Maxwell-JSON](https://docs.byteplus.com/docs/flink/Maxwell-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Ogg-JSON](https://docs.byteplus.com/docs/flink/Ogg-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Avro](https://docs.byteplus.com/docs/flink/Avro) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem)[Pulsar](https://docs.byteplus.com/docs/flink/Pulsar) |
| |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Protobuf](https://docs.byteplus.com/docs/flink/Protobuf) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Redis](https://docs.byteplus.com/docs/flink/Redis) |
|[Parquet](https://docs.byteplus.com/docs/flink/Parquet) |[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[ORC](https://docs.byteplus.com/docs/flink/ORC) |[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Raw](https://docs.byteplus.com/docs/flink/Raw) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Upsert Kafka](https://docs.byteplus.com/docs/flink/Upsert_Kafka)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |


<span id="2b324b56"></span>
### Flink 1.11 Supported Formats


|**Formats** |**Supported Connectors** |
|---|---|
|[CSV](https://docs.byteplus.com/docs/flink/CSV) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[JSON](https://docs.byteplus.com/docs/flink/JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem)[Elasticsearch](https://docs.byteplus.com/docs/flink/Elasticsearch) |
|[Debezium-JSON](https://docs.byteplus.com/docs/flink/Debezium-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Canal-JSON](https://docs.byteplus.com/docs/flink/Canal-JSON) |[Kafka/BMQ](https://docs.byteplus.com/docs/flink/Kafka_BMQ)[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[Parquet](https://docs.byteplus.com/docs/flink/Parquet) |[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
|[ORC](https://docs.byteplus.com/docs/flink/ORC) |[Filesystem](https://docs.byteplus.com/docs/flink/Filesystem) |
