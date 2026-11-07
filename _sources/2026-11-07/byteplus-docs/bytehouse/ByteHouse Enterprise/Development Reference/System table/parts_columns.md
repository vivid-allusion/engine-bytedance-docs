---
title: "parts_columns"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/parts_columns"
---

`parts_columns` contains information about the parts and columns of the [MergeTree](https://docs.byteplus.com/en/docs/bytehouse/merge-tree) table. Each line describes a data part.

<span id="ef409ab8"></span>
## Column name


|**Field name** |**Data types** |**Field definitions** |
|---|---|---|
|partition |String |Partition names For the definition of partition, see the description in [Partition Actions](https://docs.byteplus.com/docs/bytehouse/ce-alter-statement#5bd45761).<br><br>Format:<br><br><br>* `YYYYMM` is used for automatic monthly partitioning.<br><br>* `any_string` is used for manual partitioning. |
|name |String |The name of the data part. |
|uuid |UUID |The UUID of the data part. |
|part_type |String |The storage format of the data part. Supported values are as follows:<br><br><br>* `Wide` — Each column is stored in a separate file in the file system.<br><br>* `Compact` — All columns are stored in a single file in the file system.<br><br><br>The data storage format is controlled by the [MergeTree](https://docs.byteplus.com/en/docs/bytehouse/merge-tree) table's `min_bytes_for_wide_part` and `min_rows_for_wide_part` settings. |
|active |UInt8 |Flag that indicates whether the data part is active. If a data part is active, it's used in a table. Otherwise, it's deleted. Inactive data parts remain after merging. |
|marks |UInt64 |Sparse index count. To obtain the approximate number of rows in a data part, multiply `marks` by the index granularity (typically 8192) (this note does not apply to adaptive granularity). |
|rows |UInt64 |Number of rows. |
|bytes_on_disk |UInt64 |Total size of data part file (in bytes). |
|data_compressed_bytes |UInt64 |Total size of compressed data in the data part. All auxiliary files (for example, sparse index files) are not included. |
|data_uncompressed_bytes |UInt64 |Total size of uncompressed data in the data part. All auxiliary files (for example, sparse index files) are not included. |
|marks_bytes |UInt64 |The size of files that contain sparse indexes. |
|modification_time |DateTime |Modify the time of the data part directory. This usually corresponds to the time when the data part is created. |
|remove_time |DateTime |The time when the data part becomes inactive. |
|refcount |UInt32 |Number of places where the data part is used. If the value is greater than 2, it indicates that the data part is used during queries or merges. |
|min_date |Date |The minimum value of the date key in the data part. |
|max_date |Date |The maximum value of the date key in the data part. |
|min_time |DateTime |The minimum value of the time key in the data part. |
|max_time |DateTime |The maximum value of the time key in the data part. |
|partition_id |String |Partition ID. |
|min_block_number |UInt64 |The minimum number of data parts that constitute the current part after merging. |
|max_block_number |UInt64 |The maximum number of data parts constituting the current part after merging. |
|level |UInt32 |The depth of the merge tree. Zero indicates that the current part was created by insertion rather than by merging other parts. |
|data_version |UInt64 |Number that is used to determine which mutations should be applied to the data part (mutations with a version higher than `data_version`). |
|primary_key_bytes_in_memory |UInt64 |Amount of memory used by the primary key value (unit: bytes). |
|primary_key_bytes_in_memory_allocated |UInt64 |Amount of memory reserved for primary key values (unit: bytes). |
|database |String |Database name. |
|table |String |Table name. |
|engine |String |Table engine name (without parameters). |
|disk_name |String |Name of the disk for the storage data part. |
|path |String |Absolute path of the data part folder. |
|delete_rows |UInt64 |The number of rows already deleted in a data part, commonly found in parts stored by the HaUniqueMergeTree engine. |
|delete_version |UInt64 |The latest version of the delete bitmap in this part |
|unique_index_size |UInt64 |The number of elements in the memory unique index. |
|unique_index_bytes_in_memeory |UInt64 |The memory used by a memory unique index. If the index is a disk unique index, this value is 0. |
|has_disk_unique_index |UInt8 |This value indicates whether the unique index type is a disk unique index. A value of false represents a memory unique index, while true represents a disk unique index. |
|unique_part_format_version |Int8 |None. |
|column |String |Column name. |
|type |String |Column types. |
|column_position |UInt64 |Ordinal position of a column in a table starting with 1. |
|default_kind |String |Expression type for the default value (`DEFAULT`, `MATERIALIZED`, `ALIAS`), if not defined, it is an empty string. |
|default_expression |String |Expression for the default value; if not defined, it is an empty string. |
|column_bytes_on_disk |UInt64 |Total size of the column (in bytes). |
|column_data_compressed_bytes |UInt64 |Total size of compressed data in the column (in bytes). |
|column_data_uncompressed_bytes |UInt64 |Total size of uncompressed data in the column (in bytes). |
|column_marks_bytes |UInt64 |Size of columns with sparse indexes (in bytes). |
|bucket_id |Int32 |Bucket ID. |
|serialization_kind |String |Types of serialization (Default/Sparse). |
|subcolumns.names |Array(String) |The name of a subcolumn of nested type. |
|subcolumns.types |Array(String) |Type of a subcolumn in a nested type. |
|subcolumns.serializations |Array(String) |The serialization method for subcolumns of nested types. |
|subcolumns.bytes_on_disk |Array(UInt64) |File size of nested type subcolumns under this part (in bytes). |
|subcolumns.data_compressed_bytes |Array(UInt64) |The total size of compressed data for nested\-type subcolumns under this part. All auxiliary files, for example, sparse index files, are not included. |
|subcolumns.data_uncompressed_bytes |Array(UInt64) |The total size of uncompressed data for nested type subcolumns under this part. All auxiliary files, for example, sparse index files, are not included. |
|subcolumns.marks_bytes |Array(UInt64) |The file size of the sparse index for the nested type subcolumn under this part. |
|bytes |UInt64 |An alias for `bytes_on_disk`. |
|marks_size |UInt64 |An alias for `marks_bytes`. |


<span id="8e4abca7"></span>
## **Example**

```SQL
SELECT * FROM system.parts_columns LIMIT 1 FORMAT Vertical;
```


```SQL
Row 1:
──────
partition:                             tuple()
name:                                  all_1_2_1
part_type:                             Wide
active:                                1
marks:                                 2
rows:                                  2
bytes_on_disk:                         155
data_compressed_bytes:                 56
data_uncompressed_bytes:               4
marks_bytes:                           96
modification_time:                     2020-09-23 10:13:36
remove_time:                           2106-02-07 06:28:15
refcount:                              1
min_date:                              1970-01-01
max_date:                              1970-01-01
partition_id:                          all
min_block_number:                      1
max_block_number:                      2
level:                                 1
data_version:                          1
primary_key_bytes_in_memory:           2
primary_key_bytes_in_memory_allocated: 64
database:                              default
table:                                 53r93yleapyears
engine:                                MergeTree
disk_name:                             default
path:                                  /var/lib/clickhouse/data/default/53r93yleapyears/all_1_2_1/
delete_rows:                           0
delete_versions:                       0
unique_index_size:                     0
unique_index_bytes_in_memory:          0
has_dish_unique_index:                 0
unique_part_format_version:            0
column:                                id
type:                                  Int8
column_position:                       1
default_kind:
default_expression:
column_bytes_on_disk:                  76
column_data_compressed_bytes:          28
column_data_uncompressed_bytes:        2
column_marks_bytes:                    48
bucket_id:                             -1
serialization_kind:                    default
subcolumns.names:                      []
subcolumns.types:                      []
subcolumns.serialization:              []
subcolumns.bytes_on_disk:              []
subcolumns.data_compressed_bytes:      []
subcolumns.data_uncompressed_bytes:    []
subcolumns.marks_bytes:                []
```
