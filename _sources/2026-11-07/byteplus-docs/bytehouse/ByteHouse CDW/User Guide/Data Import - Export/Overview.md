---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-data-loading-feature-overview"
---

You can load existing external data into ByteHouse tables. Data import in ByteHouse is referred to as **Data Loading** **Task**. You can create import missions in the frontend console and trigger them through the frontend or API.

<span id="57756697"></span>
## 1 Supported datasources

ByteHouse currently supports the following datasources:


* BytePlus Object Storage TOS

* AWS Object Storage S3

* Apache Kafka / Confluent Cloud (0.10+)

* Local files


<span id="c2615092"></span>
## 2 Offline Import

Offline import is suitable for scenarios where data is prepared in advance and loaded into ByteHouse in one go, depending on whether the target table is partitioned, ByteHouse offers different loading modes. For details, refer to [Offline loading](https://docs.byteplus.com/docs/bytehouse/docs-batch-loading).

<span id="af006665"></span>
### 2.1 Total load

Total loading will replace all data in the table with the latest data.

<span id="127511d9"></span>
### 2.2 Incremental load

Incremental loading will add new data to the existing target table according to its partition. ByteHouse will replace existing partitions instead of merging them.

<span id="4fb24245"></span>
## 3. Supported file type

ByteHouse's offline import supports the following file formats:


* Delimited files (CSV, TSV, etc.)

* Json (multiline)

* Avro

* Parquet

* Excel (xls)


<span id="b2b22958"></span>
## 4. Real\-time import

ByteHouse can connect to Kafka and continuously transmit data to the target table. Unlike Offline imports, Kafka missions, once launched, will continue to run. ByteHouse's Kafka import mission can provide exactly\-once semantics. You can cancel/restore the consumption mission, and ByteHouse will record the offset information to ensure that no data is lost. For details, refer to [Streaming loading](https://docs.byteplus.com/docs/bytehouse/docs-kafka-stream-data-import-practice-parsing-nested-json).
