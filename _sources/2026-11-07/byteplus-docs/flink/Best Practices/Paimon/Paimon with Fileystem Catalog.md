---
title: "Paimon with Fileystem Catalog"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Paimon_with_Fileystem_Catalog"
---

<span id="80b70675"></span>
## 1. Overview

Apache Paimon is a new type of streaming data lake storage technology that combines LSM\-Tree structure and lake format, offering high throughput, low latency data ingestion, complete streaming change subscriptions, and efficient OLAP query capabilities. This manual will guide you on how to use the Flink engine for Paimon's development tasks through a FileSystem\-based metadata scheme, covering the entire process from environment preparation to data writing and reading.

<span id="ae72594b"></span>
## 2. Environment Preparation

<span id="75c24a1a"></span>
### 2.1 Activate Serverless Flink

Ensure you have:


1. Activated the **BytePlus Flink** product and can create Flink SQL tasks in job development.

2. You have already purchased pay\-as\-you\-go or subscription\-based resource pools in the **Resource Management \- Resource Pool** feature module and can submit Flink tasks normally.


<span id="8b76f527"></span>
### 2.2 Flink Version Requirements


* Flink version must be \>= 1.16. It supports the following features:

   * Flink 1.16 includes Paimon version 0.6

   * Flink 1.17 includes enhanced features of Paimon version 0.8.2, supporting syntax such as stored procedures


<span id="20407800"></span>
### Create Flink SQL Task

**Operation path**: Job development \- Flink SQL job \- Create job

**Reference document** [Flink SQL tasks](https://docs.byteplus.com/docs/flink/Flink_SQL_tasks)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6ef0a4338b14357b6319ac950a439a9~tplv-goo7wpa0wc-image.image) </span>

<span id="dc5938b1"></span>
## Create Catalog

The first step in using Paimon in Flink is to create a Catalog. A Catalog in Paimon is used to manage the metadata storage for databases and tables. Before creating a Catalog, you need to create related TOS buckets and Catalog folders. For related documents, please see [Create Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) and [Create Folder](https://docs.byteplus.com/en/docs/tos/docs-creating-a-folder).

> **Note**: Please ensure that Flink and TOS are in the same Region, as Flink currently does not support cross\-Region access to TOS buckets.


```SQL
CREATE CATALOG ${catalog_name}
WITH
  (
    'type' = 'paimon',
    'warehouse' = 'tos://${bucket_name}/${catalog_name}'
  );
```



* `${catalog_name}`: The name of the Catalog, customizable.

* `${bucket_name}`: The name of the TOS (Object Storage) bucket storing Paimon data.


<span id="4180fc25"></span>
## Create Database & Table

<span id="c084b817"></span>
### Create Databases

Create a Database within a Catalog to organize and manage tables.

```SQL
CREATE DATABASE IF NOT EXISTS ${catalog_name}.${db_name};
```



* `${db_name}`: The name of the Database, customizable.


<span id="85564c2a"></span>
### Create Tables

Create tables within a Database, defining table structure and related configurations.

```SQL
CREATE TABLE IF NOT EXISTS `${catalog_name}`.`${db_name}`.`${table_name}` (
    word varchar,
    cnt bigint,
    PRIMARY KEY (word) NOT ENFORCED
) WITH (
    'bucket' = '4',
    'changelog-producer' = 'input'
);
```



* `${table_name}`: The name of the table, customizable.

* `bucket`: The number of buckets, recommended to store about 1GB of data per bucket.

* `changelog-producer`：

   * Set to `input`, indicates generating data based on upstream additions for downstream stream reading. Refer to [Paimon](https://docs.byteplus.com/docs/flink/CDC_Connector_Paimon) for detailed selection. If a changelog is not needed, use the `none` option to save storage and writing resources.


<span id="c3754736"></span>
## Data Writing Example

The following example demonstrates how to write data into Paimon tables using Flink SQL.

<span id="caf3021f"></span>
### Create Data Source Table

First, create a data source table to generate simulated data.

```SQL
CREATE TABLE doc_source (word varchar)
WITH
  (
    'connector' = 'datagen',
    'rows-per-second' = '5',
    'fields.word.length' = '30'
  );
```



* `Connector`: Use the `datagen` connector to generate simulated data.

* `Rows-per-second`: Number of rows generated per second.

* `Fields.word.length`: Generate the length of field `word`.


<span id="a24d7928"></span>
### 5.2 Write data to the Paimon table

Write data from the source table to the Paimon table.

```SQL
INSERT INTO `paimon_test`.`default`.`doc_result`
select
  t.word,
  count(1)
from
  doc_source t
GROUP BY
  t.word;
```



* `paimon_test`: Catalog name.

* `default`: Database name.

* `doc_result`: Target table name.


<span id="68505af8"></span>
### 5.3 Enable Checkpoint

Paimon's snapshot submission mechanism is closely related to BytePlus Flink's Checkpoint, so configuring Checkpoint parameters appropriately is crucial for ensuring that downstream streaming or batch tasks can promptly detect changes in upstream data. Taking Flink's default Checkpoint interval as an example, setting it to 5 minutes means that only after completing a Checkpoint every 5 minutes can downstream tasks observe the latest data insertions, updates, or deletions. Therefore, adjusting the Checkpoint interval according to business needs is key to optimizing data visibility and processing timeliness.

> **Note:**  The interval of the Checkpoint can be reduced or increased based on real\-time data requirements. It is generally recommended that the Checkpoint interval **be no less than 1 minute**. If data delay is severe, data updates frequent, or freshness requirements are not high, it is advisable to appropriately extend the Checkpoint time to 5 minutes or longer.


The Checkpoint is set up as shown below, in **Job Development \- Config Parameters \- Checkpoint Configuration \- Checkpoint Interval**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8af485b3a69440e4923c0c9b0429d877~tplv-goo7wpa0wc-image.image) </span>

<span id="50ca07d1"></span>
## Launch Tasks

<span id="5b81d399"></span>
### Task Launch

At this point, you can click the verification button in the toolbar to check some basic SQL syntax issues.

If there are no other errors in the SQL, you may opt to go live with the SQL task, using Toolbar \- Go Live, and select the appropriate resource pool for launching.

After going live, start the task on the task management page and check that the task is in a Running state.

<span id="8c2e9554"></span>
### 6.2 Confirm the task is executed successfully.

You can access the TOS bucket management interface (access rights are required) and see data files generated in the data table's TOS directory. This indicates the data has been written successfully.

<span id="9022c4c7"></span>
## 7. Data Retrieval Example

The following example demonstrates how to use Flink SQL to read data from the Paimon table in both streaming and batch modes.

<span id="3ec82e1c"></span>
### 7.1 Create a Print Table

Create a print table for outputting the read data.

```SQL
CREATE TABLE `print_table` (
    word varchar,
    cnt bigint
) WITH (
  'connector' = 'print'
);
```



* `Connector`: Use the `print` connector to print data to the console.


<span id="bb016077"></span>
### 7.2 Read Data from the Paimon Table

Read data from the Paimon table and write it to the print table.

```SQL
INSERT INTO `print_table`
SELECT * FROM `paimon_test`.`default`.`doc_result`;
```



* `paimon_test`: Catalog name.

* `default`: Database name.

* `doc_result`: Source table name.
