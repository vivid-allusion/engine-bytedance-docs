---
title: "merges"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/merges"
---

The system table `merges` contains information about ongoing merges and part mutations, and applies to tables in the MergeTree series.

<span id="3bf323b2"></span>
## Column name


|**Name** |**Data type** |**Field meanings** |
|---|---|---|
|database |String |Name of the database where the table resides. |
|table |String |Table name. |
|elapsed |Float64 |Elapsed time since merge start (unit: seconds). |
|progress |Float64 |The percentage of completed work, ranging from 0 to 1. |
|num_parts |UInt64 |Quantity of parts to be merged. |
|source_part_names |Array(String) |The name of the part to be merged. |
|result_part_name |String |Name of the part formed after merging. |
|source_part_paths |Array(String) |Path of the part to be merged. |
|result_part_path |String |Path of the part formed after the merge. |
|partition |String |Partition key. |
|partition_id |String |ID of the partition into which the data part is inserted. If partitioning is based on `tuple()`, then the value of this column is `all`. |
|is_mutation |UInt8 |If this process is a part mutation operation, then it is 1. |
|total_size_bytes_compressed |UInt64 |Total size of compressed data in the merged part. |
|total_size_marks |UInt64 |The total number of marks in the merged parts. |
|bytes_read_uncompressed |UInt64 |Number of uncompressed bytes read. |
|rows_read |UInt64 |Number of rows read. |
|bytes_written_uncompressed |UInt64 |Number of uncompressed bytes written. |
|rows_written |UInt64 |Number of rows written. |
|columns_written |UInt64 |Number of columns written. |
|memory_usage |UInt64 |Memory consumption of the merge process. |
|thread_id |UInt64 |The thread ID of the merge process. |
|merge_type |String |The current merge type. If it is a mutation, this field is empty. |
|merge_algorithm |String |The algorithm used in the current merge. If it is a mutation, the field is empty. |


<span id="65a13e4a"></span>
## Example


* Search for current merge tasks:

   ```SQL
   select 
       database,
       table,
       round(elapsed, 0) as elapsed_,
       round(progress, 2) as progress,
       num_parts as n_parts,
       result_part_name,
       total_size_marks as marks,
       columns_written as col_written,
       formatReadableSize(total_size_bytes_compressed) as total_size,
       thread_id,
       formatReadableSize(memory_usage) as memory
   from
       system.merges
   order by
       (database, table, elapsed)
   DESC;
   ```
   

   Examples of output results are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d7518c3578441249eb4141c0e5c267e~tplv-goo7wpa0wc-image.image) </span>
