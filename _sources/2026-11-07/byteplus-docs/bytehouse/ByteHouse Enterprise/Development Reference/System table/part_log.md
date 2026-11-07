---
title: "part_log"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/part_log"
---

`system.part_log` table is only created when the part_log server setting is specified. This table contains information about events related to data parts that occur in MergeTree family tables, such as adding or merging data. After data is inserted into the `MergeTree` table for the first time, the `system.part_log` table is created.

<span id="21424d69"></span>
## Column name


|**Field name** |**Data types** |**Field definitions** |
|---|---|---|
|query_id |String |The identifier for the `INSERT` query for this data part. |
|event_type |Enum8 |Types of events that occur with the data part. It can be one of the following values:<br><br><br>* `NewPart` — Insert a new data part.<br><br>* `MergePartsStart` — The merging of the data part has started.<br><br>* `MergeParts` — The merging of the data part has been completed.<br><br>* `DownloadPart` — Downloading part of the data.<br><br>* `RemovePart` — Use [DETACH PARTITION<br><br>* `MutatePartStart` — The change to the data part has started.<br><br>* `MutatePart` — The change to the data part has been completed.<br><br>* `MovePart` — Move a data part from one disk to another disk. |
|event_date |Date |Event date. |
|event_time |DateTime |Event time. |
|event_time_microseconds |DateTime64 |Event time, accurate to the microsecond. |
|duration_ms |UInt64 |Duration. |
|database |String |Name of the database the data part is in. |
|table |String |Name of the table the data part is in. |
|part_name |String |The name of the data part. |
|partition_id |String |The ID of the partition into which the data part was inserted. If partitioning is based on `tuple()`, the value of this column is `all`. |
|bucket_id |String |Bucket ID used by the data part. |
|partition |String |Partition key. |
|path_on_disk |String |Absolute path of the folder containing the data part file. |
|rows |UInt64 |Number of rows in data part. |
|size_in_bytes |UInt64 |Data part size (in bytes). |
|merged_from |Array(String) |Array of names of the parts that make up the current part (after merging). |
|bytes_uncompressed |UInt64 |The uncompressed byte size. |
|read_rows |UInt64 |The number of rows read during the merge process. |
|read_bytes |UInt64 |The number of bytes read during merging. |
|peak_memory_usage |Int64 |The main difference in allocating and freeing memory in this thread context. |
|error |UInt16 |The code number of the occurred error. |
|exception |String |Text message of the occurred error. |


<span id="ae5d1b4e"></span>
## **Example**

```SQL
SELECT * FROM system.part_log LIMIT 1 FORMAT Vertical;
```


```SQL
Row 1:
──────
query_id:                      983ad9c7-28d5-4ae1-844e-603116b7de31
event_type:                    NewPart
event_date:                    2021-02-02
event_time:                    2021-02-02 11:14:28
event_time_microseconds:       2021-02-02 11:14:28.861919
duration_ms:                   35
database:                      default
table:                         log_mt_2
part_name:                     all_1_1_0
partition_id:                  all
bucket_id:                     -1
partition:                     tuple()
path_on_disk:                  db/data/default/log_mt_2/all_1_1_0/
rows:                          115418
size_in_bytes:                 1074311
merged_from:                   []
bytes_uncompressed:            0
read_rows:                     0
read_bytes:                    0
peak_memory_usage:             0
error:                         0
exception:                     ""
```
