---
title: "projection_parts_columns"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/projection_parts_columns"
---

You can obtain metadata information for each column in the projection data parts of all [MergeTree](https://docs.byteplus.com/en/docs/bytehouse/merge-tree) tables from the system table `projection_parts_columns`.

<span id="18604901"></span>
## Column name


|**Field name** |**Data types** |**Field definitions** |
|---|---|---|
|partition |String |Partition name. For the definition of partition, refer to the description of [ALTER statement](https://docs.byteplus.com/docs/bytehouse/ce-alter-statement).<br><br>Format:<br><br><br>* `YYYYMM` is used for automatic monthly partitioning.<br><br>* `any_string` is used for manual partitioning. |
|name |String |The name of the projection part. |
|part_type |String |The storage format of the projection part.<br><br>Supported values:<br><br><br>* `Wide` — Each column is stored in a separate file in the file system.<br><br>* `Compact` — All columns are stored in a single file in the file system.<br><br><br>The data storage format is controlled by the [MergeTree](https://docs.byteplus.com/en/docs/bytehouse/merge-tree) table's `min_bytes_for_wide_part` and `min_rows_for_wide_part` settings. |
|parent_name |String |The name of the original data part that the projection depends on. |
|parent_uuid |UUID |Projection\-dependent raw data part UUID. |
|parent_part_type |String |Storage format of the projection\-dependent raw data part. |
|active |UInt8 |A flag indicating whether the projection part is active. If the projection part is active, use it in the table. Otherwise, it will be deleted. The inactive projection part still exists after the merge. |
|marks |UInt64 |Mark count. To estimate the number of rows in the projection part, multiply `marks` by the index granularity (usually 8192). This note does not apply to adaptive granularity. |
|rows |UInt64 |Number of rows. |
|bytes_on_disk |UInt64 |Total size of all projection part files (in bytes). |
|data_compressed_bytes |UInt64 |The total size of compressed data in the projection part. All auxiliary files (for example, markup files) are not included. |
|data_uncompressed_bytes |UInt64 |The total size of uncompressed data in the projection part. All auxiliary files (for example, markup files) are not included. |
|marks_bytes |UInt64 |Size of mark files. |
|parent_marks |UInt64 |Number of tags in the original table that the projection depends on. To obtain an approximate number of rows in the projection part, multiply `marks` by the index granularity (usually 8192). Note: This tip does not apply when adaptive granularity is used. |
|parent_rows |UInt64 |Number of rows in the projection\-dependent raw data part. |
|parent_bytes_on_disk |UInt64 |Total size (in bytes) of projection\-dependent original data part files. |
|parent_data_compressed_bytes |UInt64 |The total size of compressed data in the projection\-dependent raw data part. All auxiliary files (for example, files with tags) are not included. |
|parent_data_uncompressed_bytes |UInt64 |Total size of uncompressed data in the projection\-dependent raw data part. All auxiliary files (for example, tagged files) are not included. |
|parent_marks_bytes |UInt64 |The size of files with markers contained in the projection\-dependent original data part. |
|modification_time |DateTime |Modify the time of the projection part directory. This usually corresponds to the time when the projection part is created. |
|remove_time |DateTime |The time when the projection part becomes inactive. |
|refcount |UInt32 |Number of times the projection part is used. If the value is greater than 2, it means that the projection part is used in querying or merging. |
|min_date |Date |The minimum value of the date key in the projection part. |
|max_date |Date |The maximum value of the date key in the projection part. |
|min_time |DateTime |The minimum value of the time key in the projection part. |
|max_time |DateTime |The maximum value of the time key in the projection part. |
|partition_id |String |The partition ID. |
|min_block_number |Int64 |The minimum number of parts that constitute the current projection after merging. |
|max_block_number |Int64 |The maximum number of parts that constitute the current projection after merging. |
|level |UInt32 |The depth of the merge tree. A value of zero indicates that the current projection part was created by insertion rather than by merging other projections. |
|data_version |UInt64 |Number that is used to determine which mutations should be applied to the data part (mutations with a version higher than data_version). |
|primary_key_bytes_in_memory |UInt64 |The amount of memory used by the primary key value (in bytes). |
|primary_key_bytes_in_memory_allocated |UInt64 |The amount of memory reserved for primary key values (in bytes). |
|database |String |Database name. |
|table |String |Table name. |
|engine |String |Table engine name (without parameters). |
|disk_name |String |The name of the disk which stores the projection part. |
|path |String |The absolute path of the projection part folder. |
|column |String |Column name. |
|type |String |Column types. |
|column_position |UInt64 |Column numbers in the table and the number starts from 1. |
|default_kind |String |Expression type of the default value (`DEFAULT`, `MATERIALIZED`, `ALIAS`). If not defined, it is an empty string. |
|default_expression |String |Expression for the default value; if not defined, it is an empty string. |
|column_bytes_on_disk |UInt64 |Total size of the column (in bytes). |
|column_data_compressed_bytes |UInt64 |Total size of compressed data in the column (in bytes). |
|column_data_uncompressed_bytes |UInt64 |Total size of uncompressed data in the column (in bytes). |
|column_marks_bytes |UInt64 |Size of the column containing a marker (in bytes). |
|bytes |UInt64 |An alias for `bytes_on_disk`. |
|marks_size |UInt64 |An alias for `marks_bytes`. |


<span id="5108bf79"></span>
## Example

```SQL
SELECT * FROM system.projection_parts_columns; 
```
