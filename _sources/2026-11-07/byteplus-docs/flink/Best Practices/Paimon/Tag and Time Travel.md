---
title: "Tag and Time Travel"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Tag_and_Time_Travel"
---

<span id="4bc11b22"></span>
## 1. Overview of Tag Features

Paimon's Tag feature allows users to create tags based on snapshots to preserve historical data. Since Paimon tables will automatically expire old snapshots based on configuration, it makes historical data unqueryable. Through the Tag feature, users can create tags for specific snapshots, thus preserving the data files and metadata corresponding to that snapshot for subsequent historical data queries. The Tag feature is particularly suitable for scenarios that require historical data to be preserved daily or hourly.

<span id="0eb6226a"></span>
## 2. Basic Operations of Tag

Before using, be aware that the Flink version requirements are:


* The Flink version must be \>= 1.17 to support syntax such as stored procedures.


<span id="bab2ad56"></span>
### 2.1 Creating a Tag

Users can create a Tag for a specified snapshot. The Tag will retain all the data files and metadata of the snapshot, ensuring historical data is queryable.

**Syntax example:** 

```SQL
CALL sys.create_tag('default.T', 'my_tag', 10, '1 d')
```


Parameter description:


* identifier (identifier): The identifier for the target table, which cannot be empty. In the format of `dbName.tableName`.

* tagName (tag name): The name of the new tag.

* snapshotId (long integer): The ID of the snapshot on which the new tag is based. null means creating from the latest snapshot.

* time_retained (retention time): The maximum duration for which the newly created tag is retained.


<span id="d66cb392"></span>
### Delete Tag

Users can delete tags that are no longer needed. Deleting a tag does not affect other snapshots or data files.

**Syntax Example:** 

```SQL
CALL sys.delete_tag('default.T', 'my_tag')
```


Parameter Description:


* identifier: The identifier of the target table, which cannot be empty. Formatted as `dbName.tableName`.

* tagName: The name of the new tag.


<span id="b15cbe5a"></span>
### Rollback to Tag

Users can rollback the table to a snapshot state corresponding to a specific tag. The rollback operation will delete all snapshots and Tags after the specified Tag, and clean up the corresponding data files.

**Syntax example:** 

```SQL
CALL sys.rollback_to('default.T', 'my_tag')
```


Parameter explanation:


* identifier (identifier): The identifier of the target table, which cannot be empty. In the format of `dbName.tableName`.

* tagName (tag name): The name of the new tag.


<span id="44869abc"></span>
## 3. Time travel operation

Paimon supports the Time Travel feature, allowing users to query historical snapshots or data corresponding to Tags.

<span id="ab1386b9"></span>
### 3.1 Batch query

When we choose the batch job development mode, the following methods are used to query specified snapshots.

<span id="8e8a9440"></span>
#### Query the latest snapshot data

Querying the latest snapshots is done using the classic Select statement to read data from the table, without specifying a Tag or Snapshot ID, and that defaults to querying the latest snapshot:

```SQL
SELECT * FROM t;
```


<span id="206938af"></span>
#### Batch Time Travel Query

Paimon's batch reading function with time travel can specify a snapshot or a tag, and read the corresponding data:

```SQL
-- Read snapshot with ID = 1
SELECT * FROM t /*+ OPTIONS('scan.snapshot-id' = '1') */;

-- Read snapshot from a specific Unix millisecond timestamp
SELECT * FROM t /*+ OPTIONS('scan.timestamp-millis' = '1678883047356') */;

-- Read snapshot from a specific timestamp string; it will be automatically converted to Unix milliseconds
-- Supported formats include: yyyy-MM-dd, yyyy-MM-dd HH:mm:ss, yyyy-MM-dd HH:mm:ss.SSS; local time zone is used by default
SELECT * FROM t /*+ OPTIONS('scan.timestamp' = '2023-12-09 23:09:12') */;

-- Read snapshot using a watermark; it will match the first snapshot after the specified watermark
SELECT * FROM t /*+ OPTIONS('scan.watermark' = '1678883047356') */;
```


The most common is to read data from a specific Tag:

```SQL
-- Read snapshot associated with tag 'my-tag'
SELECT * FROM t /*+ OPTIONS('scan.tag-name' = 'my-tag') */;
```


<span id="356d28ae"></span>
#### Query incremental data between two Tags

Read the incremental changes between the starting snapshot (not included) and the ending snapshot. For example:


* **Snapshot**: '5,10' indicates the changes between snapshot 5 and snapshot 10.

* **Tag**: 'TAG1,TAG3' indicates the changes between TAG1 and TAG3.


```SQL
-- Incremental changes between snapshot tags 'tag1' and 'tag3'
SELECT * FROM t /*+ OPTIONS('incremental-between' = 'tag1,tag3') */;

-- Incremental changes between two snapshot timestamps (in milliseconds)
SELECT * FROM t /*+ OPTIONS('incremental-between-timestamp' = '1692169000000,1692169900000') */;
```


By default, the change log files of tables generating change logs are scanned. Otherwise, scan the newly changed files. You can also force specify `incremental-between-scan-mode`. In batch SQL, DELETE records are not allowed to return, so \-D records will be discarded. If you want to view DELETE records, you can use the audit_log table:

```SQL
SELECT * FROM t$audit_log /*+ OPTIONS('incremental-between' = '12,20') */;
```


<span id="2189ef55"></span>
### 3.2 Stream Query

When we choose the stream job development mode, the following methods are methods of inquiry

<span id="95eb4340"></span>
#### 3.2.1 Stream Consumption Paimon Table

By default, streaming read first generates a snapshot for the current Paimon table, and after completion, it continuously reads the latest change data. The Paimon source in Paimon stream mode is unbounded, like an endless queue.

```SQL
-- First consume the snapshot: read the snapshot completely, then consume new changes
SELECT * FROM t;

-- Start consuming from the latest data only (skip historical snapshot)
SELECT * FROM t /*+ OPTIONS('scan.mode' = 'latest') */;
```


<span id="de72a175"></span>
#### 3.2.2 Stream Query Time Travel

If the current Paimon table is a partitioned table and you only want to process data from today and onwards, you can use a partition filter:

```SQL
SELECT * FROM t WHERE dt > '2023-06-26';
```


If it is not a partitioned table or you cannot filter by partition, you can use the time travel stream read.

```SQL
-- Read changes starting from snapshot ID 1L
SELECT * FROM t /*+ OPTIONS('scan.snapshot-id' = '1') */;

-- Read changes starting from a specific timestamp (in milliseconds)
SELECT * FROM t /*+ OPTIONS('scan.timestamp-millis' = '1678883047356') */;

-- On first startup, read the full snapshot at ID 1L, then continue reading incremental changes
SELECT * FROM t /*+ OPTIONS('scan.mode' = 'from-snapshot-full', 'scan.snapshot-id' = '1') */;
```


Time travel stream reads rely on snapshots, but by default, snapshots only retain data within 1 hour, which may prevent you from reading earlier incremental data. Therefore, Paimon also provides another streaming read mode `scan.file-creation-time-millis`, which offers a rough filter to retain files created after timeMillis.

```SQL
SELECT * FROM t /*+ OPTIONS('scan.file-creation-time-millis' = '1678883047356') */;
```


<span id="93b9b6c4"></span>
## 4. Auto\-create Tag feature

Paimon supports automatically creating Tags in writing tasks, allowing users to configure periodic automatic Tag generation.

<span id="bad6e548"></span>
### 4.1 Configuring Auto\-create Tag

<span id="fb0a682a"></span>
#### 4.1.1 Configuring Tag Automatic Creation Mode

Set the creation mode of a Tag through the table option `tag.automatic-creation`, supporting the following modes:


* `Process-time`: Create a tag based on machine time.

* `Watermark`: Create a tag based on the Watermark input by Sink.

* `Batch`: In batch processing scenarios, generate a tag after completion of tasks.


If the `watermark` mode is selected, and the Watermark is not in UTC time, configure `sink.watermark-time-zone`. This parameter represents the time zone for interpreting the watermark value as a TIMESTAMP. The default value is 'UTC', implying that the watermark is defined on the TIMESTAMP column, or not defined at all. If the watermark is defined on the TIMESTAMP_LTZ column, the watermark’s time zone will be the user\-configured local time zone. Option values can be full names, such as 'America/Los_Angeles', or custom time zone IDs, like 'GMT\-08:00'.

<span id="4782d0f9"></span>
#### 4.1.2 Configure Tag Creation Period

Set the frequency of tag creation through `tag.creation-period`, supporting the following options:


* `Daily`: Create one Tag every day.

* `Hourly`: Create one Tag every hour.

* `Two-hours`: Create one Tag every two hours.


If you need to wait for late\-arriving data, you can configure a delay time `tag.creation-delay`.

<span id="acc0df08"></span>
#### Configure Automatic Deletion of Tags

Set the number of Tags to retain through `tag.num-retained-max`. Excess old Tags will be automatically deleted.

<span id="bbb89e4a"></span>
#### Configure Tag Formatting

You can set the format for automatically created Tags through `tag.period-formatter`, supporting the following two formats:


* `With_dashes`: Default value, timestamps are connected with dashes, e.g., 'yyyy\-MM\-dd HH'

* `Without_dashes`: Timestamps are not connected with dashes, e.g., 'yyyyMMdd HH'


<span id="61c49002"></span>
### Configuring Tag Success Signature File

Often, Flink real\-time writes into Paimon tables need to be coordinated with downstream batch processing schedules. A Tag will be automatically created once the data freshness meets the requirements. After successful tag creation, the following file is generated:

```Bash
# The data table is paimon_tag.paimon_tag.tag_table
# Tag format is "tag-2025-02-20 15"
tos://<bucket>/paimon_tag/paimon_tag.db/tag_table/tag/tag-2025-02-20 15
```


During downstream batch job scheduling, check for the creation of this file to schedule dependent downstream batch tasks.

<span id="156c2211"></span>
### Example Configuration

<span id="46d3abf2"></span>
#### Create Tags Based on Processing Time

The following example configuration automatically creates a Tag at 0:10 daily and retains the Tags for the most recent 90 days:

```SQL
CREATE TABLE IF NOT EXISTS paimon_tag.paimon_tag.tag_table (
    user_id STRING PRIMARY KEY NOT ENFORCED,
    ts TIMESTAMP(3),
    url STRING
) WITH (
    'tag.automatic-creation' = 'process-time',
    'tag.creation-period' = 'daily',
    'tag.creation-delay' = '10 m',
    'tag.num-retained-max' = '90',
    'tag.create-success-file' = 'true' -- Create a success file when the tag is generated
);
```


<span id="11c4e276"></span>
#### Create Tags Based on Event Time Watermark Values

The following example configuration creates a Tag automatically each hour when the event time reaches 00:00, allowing a 1\-minute delay for the Tag:

```SQL
-- Tags are generally more commonly used in primary key table scenarios. We'll use a primary key table as an example
CREATE TABLE IF NOT EXISTS paimon_tag.paimon_tag.tag_table_watermark082 (
    user_id STRING,
    ts TIMESTAMP(3),
    url STRING,
    PRIMARY KEY (`user_id`) NOT ENFORCED
) WITH (
    'tag.automatic-creation' = 'watermark',
    'tag.creation-period' = 'hourly',
    'tag.num-retained-max' = '30'
);

-- Simulated data source, with watermark set to allow 1-minute late data
CREATE TABLE IF NOT EXISTS datasource (
    user_id STRING,
    ts TIMESTAMP(3),
    url STRING,
    WATERMARK FOR ts AS ts - INTERVAL '1' MINUTE
) WITH (
    'connector' = 'datagen'
);

INSERT INTO paimon_tag.paimon_tag.tag_table_watermark082
SELECT * FROM datasource;
```


With the features above, Paimon offers robust historical data management and query capabilities, suitable for scenarios that require retaining and querying historical data.
