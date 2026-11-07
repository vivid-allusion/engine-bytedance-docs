---
title: "distribution_queue"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/distribution_queue"
---

The system table distribution_queue contains information about local files that are queued for delivery to shards. These local files contain new parts files that are created when new data is inserted into a distributed table using asynchronous mode.

<span id="791791f3"></span>
## Column name


|**Field name** |**Data types** |**Description of field meanings** |
|---|---|---|
|database |String |The database name |
|table |String |Table name |
|data_path |String |Folder path containing local files |
|is_blocked |UInt8 |Indicates whether sending local files to the server is blocked |
|error_count |UInt64 |Error count |
|data_files |UInt64 |Number of local files in the folder |
|data_compressed_bytes |UInt64 |The size of the compressed data in the local file (unit: bytes) |
|broken_data_files |UInt64 |Number of files marked as damaged due to errors |
|broken_data_compressed_bytes |UInt64 |Size of compressed data in the damaged file, unit: bytes |
|last_exception |Sring |The text message for the most recent error, if any. |
|last_exception_time |DateTime |The time of the latest error |


<span id="9b7cdaa0"></span>
## Example

```SQL
SELECT * FROM system.distribution_queue LIMIT 1 FORMAT Vertical;
```


```SQL
Row 1:
──────
database:                     db_dorado_01
table:                        tb_dorado_01
data_path:                    /data00/clickhouse/data/store/416/416bcf77-931e-4e34-92de-496c90fc3938/shard2_all_replicas/
is_blocked:                   0
error_count:                  0
data_files:                   0
data_compressed_bytes:        0
broken_data_files:            0
broken_data_compressed_bytes: 0
last_exception:               
last_exception_time:          1970-01-01 00:00:00
```
