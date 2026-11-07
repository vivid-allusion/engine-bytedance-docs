---
title: "parts"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/parts"
---

The system table `parts` contains information about the parts of the MergeTree table.

<span id="06aa4652"></span>
## Column name


|**Field name** |**Data types** |**Field descriptions** |
|---|---|---|
|partition |String |The partition name. The format is as follows:<br><br><br>* `YYYYMM` is used for automatic partitioning by month.<br><br>* `any_string` is used for manual partitioning. |
|name |String |The name of the data part. The part naming structure can be used to determine many aspects related to data, ingestion, and merging patterns. The naming format for part is as follows:<br><br>```Plain```<br>```<partition_id>_<minimum_block_number>_<maximum_block_number>_<level>_<data_version>```<br><br><br><br>* `partition_id` \- It identifies the partition key.<br><br>* `minimum_block_number` \- It identifies the minimum block number in "part". ByteHouse always merges contiguous blocks.<br><br>* `maximum_block_number` \- It indicates the maximum block number in the part.<br><br>* `level` \- It increases by one with each additional merge. 0 indicates that this is a new part that has not yet been merged. All parts in ByteHouse are always immutable.<br><br>* `data_version` \- Optional value. It increases when parts change. Similarly, changed data is always written only to a new part, because a part is immutable. |
|uuid |UUID |The UUID of the data part. |
|part_type |String |The data part storage format.<br><br>Optional values:<br><br><br>* `Wide` — Each column is stored as a separate file in the file system.<br><br>* `Compact` — All columns are stored in a single file in the file system.<br><br><br>The data storage format is controlled by the MergeTree table's `min_bytes_for_wide_part` and `min_rows_for_wide_part` settings. |
|active |UInt8 |It is the flag indicating whether the data part is active. If the data part is active, use it in the table. Otherwise, it has been deleted. After the merge, the inactive data part still exists. |
|compact_map |UInt8 |Whether to enable the Compact Map feature. |
|marks |UInt64 |The quantity of marks. To estimate the number of rows in a data part, multiply `marks` by the index granularity (usually 8192). This tip does not apply when adaptive granularity is used. |
|rows |UInt64 |Number of rows. |
|bytes_on_disk |UInt64 |Total size of data part files (in bytes). |
|data_compressed_bytes |UInt64 |Total size of compressed data in the data part. All auxiliary files (for example, files with tags) are not included. |
|data_uncompressed_bytes |UInt64 |Total size of uncompressed data in the data part. All auxiliary files (for example, files with tags) are not included. |
|marks_bytes |UInt64 |The size of the file with markup. |
|modification_time |DateTime |The modification time of the data part directory. This usually corresponds to the time when the data part was created. |
|remove_time |DateTime |Time when the data part becomes inactive. |
|refcount |UInt32 |Number of places where the data part is used. A value greater than 2 indicates that the data part is used in queries or merges. |
|min_date |Date |The minimum value of the date key in the data part. |
|max_date |Date |The maximum value of the date key in the data part. |
|min_time |DateTime |The minimum value of the date and time keys in the data part. |
|max_time |DateTime |The maximum value of date and time keys in the data part. |
|partition_id |String |Partition ID. |
|min_block_number |Int64 |The minimum data block number that makes up the current part after merging. |
|max_block_number |Int64 |The largest data block number that makes up the current part after merging. |
|level |UInt32 |The depth of the merge tree. Zero indicates that the current part was created by insertion rather than by merging other parts. |
|data_version |UInt64 |Number that is used to determine which mutations should be applied to the data part (mutations with a version higher than `data_version`). |
|primary_key_bytes_in_memory |UInt64 |The amout of memory used by primary key values (unit: bytes). |
|primary_key_bytes_in_memory_allocated |UInt64 |The amount of memory reserved for primary key values (unit: bytes). |
|is_frozen |UInt8 |Flag indicating whether a partition data backup exists. Supports the following values:<br><br><br>* 1: A backup exists.<br><br>* 0: Backup does not exist. |
|database |String |Database name. |
|table |String |Table name. |
|engine |String |Table engine name without parameters. |
|disk_name |String |Name of a disk that stores the data part. |
|path |String |The absolute path to the folder with data part files. |
|has_bitmap_index |Map(String, UInt8) |Construction status of the bitmap index in this part. |
|total_index_cache_size |UInt64 |The amount of memory used by the index cache in this part, in bytes. |
|delete_rows |UInt64 |The number of rows that have been deleted in a data part, commonly found in parts stored by the HaUniqueMergeTree engine. |
|delete_version |UInt64 |The latest version of the delete bitmap in this part. |
|unique_index_size |UInt64 |Number of elements in the memory unique index. |
|unique_index_bytes_in_memory |UInt64 |The memory used by a memory unique index. If it is a disk unique index, this value is 0. |
|has_disk_unique_index |UInt8 |Whether the type of unique index is a disk unique index. False means a memory unique index, and true means a disk unique index. |
|unique_part_format_version |Int8 |None. |
|hash_of_all_files |String |The compressed file of [sipHash128](https://docs.byteplus.com/docs/bytehouse/hash-function#siphash128). |
|hash_of_uncompressed_files |String |The uncompressed files (files with tags, index files, and more) of [sipHash128](https://docs.byteplus.com/docs/bytehouse/hash-function#siphash128). |
|uncompressed_hash_of_compressed_files |String |The hash of data in the compressed file of [sipHash128](https://docs.byteplus.com/docs/bytehouse/hash-function#siphash128) as if they were uncompressed. |
|delete_ttl_info_min |DateTime |The minimum value of the date and time key for the [TTL DELETE rule](https://docs.byteplus.com/en/docs/bytehouse/ttl). |
|delete_ttl_info_max |DateTime |The maximum value of the date and time key of [TTL DELETE rule](https://docs.byteplus.com/en/docs/bytehouse/ttl). |
|move_ttl_info.expression |Array(String) |Expression arrays. Each expression defines an [TTL MOVE rule](https://docs.byteplus.com/en/docs/bytehouse/ttl).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>move_ttl_info.expression</code> array is primarily for backward compatibility. The simplest way to check <code>TTL MOVE</code> rules now is to use the <code>move_ttl_info.min</code> and <code>move_ttl_info.max</code> fields.</div><br> |
|move_ttl_info.min |Array(DateTime) |Array of date and time values. Each element describes the minimum key value for the [TTL MOVE rule](https://docs.byteplus.com/en/docs/bytehouse/ttl). |
|move_ttl_info.max |Array(DateTime) |Array of date and time values. Each element describes the maximum key value for the [TTL MOVE rule](https://docs.byteplus.com/en/docs/bytehouse/ttl). |
|num_columns_encrypted |UInt64 |Number of encrypted columns in a part. Effective after table encryption is enabled. |
|bucket_id |Int32 |Bucket ID. |
|bytes |UInt64 |An alias for `bytes_on_disk`. |
|marks_size |UInt64 |Alias of `marks_bytes`. |


<span id="1b2b2d68"></span>
## **Example**

```SQL
SELECT * FROM system.parts LIMIT 1 FORMAT Vertical; 
```


```SQL
Row 1:
──────
partition:                             tuple()
name:                                  all_1_4_1_6
uuid:                                  00000000-0000-0000-0000-000000000000
part_type:                             Compact
active:                                1
compact_map:                           0
marks:                                 2
rows:                                  6
bytes_on_disk:                         330
data_compressed_bytes:                 123
data_uncompressed_bytes:               19
marks_bytes:                           144
modification_time:                     2020-06-18 13:01:49
remove_time:                           1970-01-01 00:00:00
refcount:                              1
min_date:                              1970-01-01
max_date:                              1970-01-01
min_time:                              1970-01-01 00:00:00
max_time:                              1970-01-01 00:00:00
partition_id:                          202503
min_block_number:                      1
max_block_number:                      4
level:                                 1
data_version:                          6
primary_key_bytes_in_memory:           8
primary_key_bytes_in_memory_allocated: 64
is_frozen:                             0
database:                              default
table:                                 local_aggregated_data
engine:                                AggregatingMergeTree
disk_name:                             default
path:                                  /var/lib/clickhouse/data/default/months/all_1_4_1_6/
has_bitmap_index:                      {}
total_index_cache_size:                0
delete_rows:                           0
delete_version:                        0
unique_index_size:                     0
unique_index_bytes_in_memory:          0
has_disk_unique_index:                 0
unique_part_format_version:            0
hash_of_all_files:                     2d0657a16d9430824d35e327fcbd87bf
hash_of_uncompressed_files:            84950cc30ba867c77a408ae21332ba29
uncompressed_hash_of_compressed_files: 1ad78f1c6843bbfb99a2c931abe7df7d
delete_ttl_info_min:                   1970-01-01 00:00:00
delete_ttl_info_max:                   1970-01-01 00:00:00
move_ttl_info.expression:              []
move_ttl_info.min:                     []
move_ttl_info.max:                     []
default_compression_codec:             LZ4
recompression_ttl_info.expression:     []
recompression_ttl_info.min:            []
recompression_ttl_info.max:            []
group_by_ttl_info.expression:          []
group_by_ttl_info.min:                 []
group_by_ttl_info.max:                 []
rows_where_ttl_info.expression:        []
rows_where_ttl_info.min:               []
rows_where_ttl_info.max:               []
only_keep_projection_parts:            0
num_columns_encrypted:                 0
bucket_id:                             -1
```
