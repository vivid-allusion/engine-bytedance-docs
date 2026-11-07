---
title: "projection_parts"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/projection_parts"
---

You can use the system table `projection_parts` to obtain information about the data parts that currently exist for the projections of all MergeTree tables in the cluster. The information about the data part corresponding to the source table is stored in columns prefixed with `parent_`.

<span id="f887d54a"></span>
## Column name


|**Field name** |**Data types** |**Field definitions** |
|---|---|---|
|partition |String |Partition name. Format as follows:<br><br><br>* `YYYYMM` is used for automatic partitioning by month.<br><br>* `any_string` is used for manual partitioning. |
|name |String |Name of the projection data part. The projection naming structure can be used to determine many aspects related to data, ingestion, and merging patterns. The projection naming format is as follows:<br><br>```Plain```<br>```<partition_id>_<minimum_block_number>_<maximum_block_number>_<level>_<data_version>```<br><br><br><br>* `partition_id` \- Partition key identifier<br><br>* `minimum_block_number` \- It identifies the minimum block number in the projection part. ByteHouse always merges contiguous blocks.<br><br>* `maximum_block_number` \- It identifies the largest block number in the projection part.<br><br>* `level` \- It increases by one with each additional merge. 0 indicates that this is a new projection that has not yet been merged. All projection parts in ByteHouse are always immutable.<br><br>* `data_version` \- Optional value. It increments when the projection changes. Similarly, changed data is always written only to the new projection part, because the projection part is immutable. |
|part_type |String |Storage formats for the projection part.<br><br>Supported values:<br><br><br>* `Wide` — Each column is stored in a separate file in the file system.<br><br>* `Compact` — All columns are stored in a single file in the file system.<br><br><br>The data storage format is controlled by the `min_bytes_for_wide_part` and `min_rows_for_wide_part` settings of the [MergeTree](https://docs.byteplus.com/en/docs/bytehouse/merge-tree) table. |
|parent_name |String |Projection\-dependent raw data part name. |
|parent_uuid |UUID |The UUID of the original data part that the projection depends on. |
|parent_part_type |String |Storage format of the raw data component associated with projection dependencies. |
|active |UInt8 |Indicator showing whether the projection part is active. If the projection part is active, use it in the table. Otherwise, it has been deleted. After the merge, the inactive projection part still exists. |
|marks |UInt64 |Number of marks. To obtain the approximate number of rows in the projection part, multiply `marks` by the index granularity (usually 8192). This tip does not apply when adaptive granularity is used. |
|rows |UInt64 |Number of rows. |
|bytes_on_disk |UInt64 |Total size of the projection part file (in bytes). |
|data_compressed_bytes |UInt64 |The total size of compressed data in the projection part. All auxiliary files (for example, files with tags) are not included. |
|data_uncompressed_bytes |UInt64 |The total size of uncompressed data in the projection part. All auxiliary files (for example, files with tags) are not included. |
|marks_bytes |UInt64 |Size of file containing marks. |
|parent_marks |UInt64 |Number of marks in the projection\-dependent raw data part. To obtain the approximate number of rows in the projection section, multiply `marks` by the index granularity (usually 8192). This tip does not work when adaptive granularity is used. |
|parent_rows |UInt64 |The number of rows in the projection\-dependent raw data part. |
|parent_bytes_on_disk |UInt64 |The total size of raw data part files required for projection dependencies (in bytes). |
|parent_data_compressed_bytes |UInt64 |The total size of compressed data in the projection\-dependent original data part. All auxiliary files (for example, files with tags) are not included. |
|parent_data_uncompressed_bytes |UInt64 |The total size of uncompressed data in the projection\-dependent raw data part. All auxiliary files (for example, files with tags) are not included. |
|parent_marks_bytes |UInt64 |The raw data part for projection dependencies contains the size of the marked files. |
|modification_time |DateTime |Modification time of the projection part directory. This usually corresponds to the time when the projection part is created. |
|remove_time |DateTime |Time when the projection part becomes inactive. |
|refcount |UInt32 |The number of places where the projection part is used. A value greater than 2 indicates that the projection part is used in queries or merges. |
|min_date |Date |The minimum value of the date key in the projection part. |
|max_date |Date |The maximum value of the date key in the projection part. |
|min_time |DateTime |The minimum value of the date and time keys in the projection part. |
|max_time |DateTime |The maximum value of the date and time keys in the projection part. |
|partition_id |String |The partition ID. |
|min_block_number |Int64 |The minimum data block number that makes up the current projection part after merging. |
|max_block_number |Int64 |The maximum data block number that makes up the current projection part after merging. |
|level |UInt32 |The depth of the merge tree. Zero indicates that the current projection part was created by insertion rather than by merging with other projection parts. |
|data_version |UInt64 |It is used to determine which versions of changes should be applied to the projection part (changes with versions higher than `data_version`). |
|primary_key_bytes_in_memory |UInt64 |Memory used by primary key values (in bytes). |
|primary_key_bytes_in_memory_allocated |UInt64 |Amount of memory reserved for primary key values (in bytes). |
|is_frozen |UInt8 |Flag indicating whether a data backup exists for the projection part. The following values are supported:<br><br><br>* 1: Bckup exists.<br><br>* 0: Backup does not exist. |
|database |String |The database name. |
|table |String |Table name. |
|engine |String |Table engine name without parameters. |
|disk_name |String |The disk name of the storage projection part. |
|path |String |The absolute path of the projection folder. |
|hash_of_all_files |String |The compressed file of [sipHash128](https://docs.byteplus.com/docs/bytehouse/hash-function#siphash128). |


<span id="43454551"></span>
## Example

```SQL
select partition, count() from system.projection_parts where table = 'xx' group by partition
```
