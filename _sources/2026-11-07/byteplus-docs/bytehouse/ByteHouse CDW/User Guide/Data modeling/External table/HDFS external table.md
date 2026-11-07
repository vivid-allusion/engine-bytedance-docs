---
title: "HDFS external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hdfs-external-table"
---

This engine provides integration with the [Apache Hadoop](https://en.wikipedia.org/wiki/Apache_Hadoop) ecosystem, allowing data on [HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html) to be managed through ByteHouse.

<span id="9dd9eb58"></span>
### Usage \- Table Engine

```JavaScript
# Create a single-file table
CREATE TABLE hdfs_engine_table (name String, value UInt32) ENGINE=CnchHDFS('hdfs//ip:port/prefix/file.csv', 'CSV', '[compression]') settings key=value

# Create a multi-file table using wildcards
CREATE TABLE hdfs_engine_table_glob_uri (name String, value UInt32) ENGINE=CnchHDFS('hdfs//ip:port/prefix/test/file*.csv', 'CSV'，'[compression]') settings key=value

# Query
select * from hdfs_engine_table
select * from hdfs_engine_table_glob_uri where _file = 'fileSimple*.csv'

# Insert
insert into hdfs_engine_table values ('one', 1), ('two', 2), ('three', 3)
```


The query supports pruning via the `_path` and `_file` columns.

<span id="0cc7ded6"></span>
#### CnchHDFS Engine Parameters


* hdfs_path: Specific to a certain path or use a wildcard character to select multiple files

* Format: For file format, refer to [CNCH S3/HDFS External Table Usage](https://bytedance.larkoffice.com/docx/Gi2pdCk7roemkWxDtL7cEWV6nkd).

   * CSV

   * JSON

   * JSONEachRow

   * Parquet

   * ORC

* Compression: Supports gzip/zstd/lz4/snappy/bzip2/xz/brotli. If not specified, guess from file suffix


<span id="4a26b838"></span>
### Usage \- table function

```JavaScript
# Query
select * from CnchHDFS('hdfs//ip:port/prefix/test/file.csv', 'city String, name String', '[format]', '[compression]')
select * from CnchHDFS('hdfs//ip:port/prefix/test/file*.csv', 'city String, name String', '[format]', '[compression]') where _path like '%test%'


# Insert
insert into function CnchHDFS('hdfs//ip:port/prefix/test/file.csv', 'city String, name String', '[format]', '[compression]') values ('one', '1'), ('two', '2'), ('three', '3')

# Insert by partition
# Ensure that the '{_partition_id}' field is included in the path
insert into function CnchHDFS('hdfs//ip:port/prefix/test/{_partition_id}_file.csv', 'city String, name String', '[format]', '[compression]') partition by city values ('one', '1'), ('two', '2'), ('three', '3')
```


Format and Compression are optional parameters. The schema of the data must be specified.
