---
title: "External Table - S3"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-s3-external-table"
---

The engine integrates with object storage, allowing the management of data on S3 through ByteHouse.

<span id="903206a7"></span>
### Usage \- Table Engine

```SQL
-- Create a single-file table
CREATE TABLE s3_engine_table (name String, value UInt32) ENGINE=CnchS3('http://....' or 'https://' or 's3://', '[format]', '[compression]', '[ak_id, ak_secret]') 

-- Create a multi-file table using wildcards
CREATE TABLE s3_engine_table_glob_uri (name String, value UInt32) ENGINE=CnchS3('http://....' or 'https://' or 's3://', '[format]', '[compression]', '[ak_id, ak_secret]') 

-- Query
select * from s3_engine_table
select * from s3_engine_table_glob_uri where _file = 'fileSimple*.csv'

-- Insert
insert into s3_engine_table values ('one', 1), ('two', 2), ('three', 3)
```


Query supports pruning through `_path` and `_file` columns.

<span id="675e1178"></span>
#### CnchS3 Engine Parameters


* s3_path:

   * s3://bucket/file_path will use the S3 storage configured by default in the Bytehouse cluster

   * http[s]://s3_endpoints/bucket/prefix/\*.csv will access the object storage specified by the path

* Compression: Supports gzip/zstd/lz4/snappy/bzip2/xz/brotli. When unspecified, it is inferred from the file extension

* Access ID, access key: The user has the key to access object storage. When not specified, use the default key configured by Bytehouse or specify through settings s3_access_key_id = xx, s3_access_key_secret = xxx

* Format: The following file formats are supported.

   
   |File Format |Read |Write |
   |---|---|---|
   |[TabSeparated](https://clickhouse.com/docs/en/sql-reference/formats#tabseparated) |✅ |✅ |
   |[TabSeparatedRaw](https://clickhouse.com/docs/en/sql-reference/formats#tabseparatedraw) |✅ |❌ |
   |[TabSeparatedWithNames](https://clickhouse.com/docs/en/sql-reference/formats#tabseparatedwithnames) |✅ |✅ |
   |[TabSeparatedWithNamesAndTypes](https://clickhouse.com/docs/en/sql-reference/formats#tabseparatedwithnamesandtypes) |✅ |❌ |
   |[CSV](https://clickhouse.com/docs/en/sql-reference/formats#csv) |✅ |✅ |
   |[CSVWithNames](https://clickhouse.com/docs/en/sql-reference/formats#csvwithnames) |✅ |✅ |
   |[CustomSeparated](https://clickhouse.com/docs/sql-reference/formats#format-customseparated) |✅ |❌ |
   |[JSON](https://clickhouse.com/docs/en/sql-reference/formats#json) |❌ |✅ |
   |[JSONCompact](https://clickhouse.com/docs/en/sql-reference/formats#jsoncompact) |❌ |✅ |
   |[JSONEachRow](https://clickhouse.com/docs/en/sql-reference/formats#jsoneachrow) |✅ |✅ |
   |[JSONObjectEachRow](https://clickhouse.com/docs/en/sql-reference/formats#jsonobjecteachrow) |❌ |✅ |
   |[TSKV](https://clickhouse.com/docs/en/sql-reference/formats#tskv) |✅ |✅ |
   |[Pretty](https://clickhouse.com/docs/en/sql-reference/formats#pretty) |❌ |✅ |
   |[PrettyCompact](https://clickhouse.com/docs/en/sql-reference/formats#prettycompact) |❌ |✅ |
   |[PrettyCompactNoEscapes](https://clickhouse.com/docs/en/sql-reference/formats#prettycompactnoescapes) |❌ |✅ |
   |[PrettyCompactMonoBlock](https://clickhouse.com/docs/en/sql-reference/formats#prettycompactmonoblock) |❌ |✅ |
   |[PrettySpace](https://clickhouse.com/docs/en/sql-reference/formats#prettyspace) |❌ |✅ |
   |[PrettySpaceNoEscapes](https://clickhouse.com/docs/en/sql-reference/formats#prettyspacenoescapes) |❌ |✅ |
   |[Protobuf](https://clickhouse.com/docs/en/sql-reference/formats#protobuf) |✅ |✅ |
   |[Parquet](https://clickhouse.com/docs/en/sql-reference/formats#data-format-parquet) |✅ |✅ |
   |[RowBinary](https://clickhouse.com/docs/en/sql-reference/formats#rowbinary) |✅ |✅ |
   |[RowBinaryWithNamesAndTypes](https://clickhouse.com/docs/en/sql-reference/formats#rowbinarywithnamesandtypes) |✅ |✅ |
   |[Native](https://clickhouse.com/docs/en/sql-reference/formats#native) |✅ |✅ |
   |[XML](https://clickhouse.com/docs/en/sql-reference/formats#xml) |❌ |✅ |
   |[CapnProto](https://clickhouse.com/docs/en/sql-reference/formats#capnproto) |✅ |❌ |
   


<span id="0fcf508f"></span>
### Usage \- table function

```JavaScript
# Query
select * from CnchS3('http://s3.region.amazonaws.com.cn/bucket/normal.csv', 'name String, id String')
select * from CnchS3('http://s3.region.amazonaws.com.cn/bucket/*.csv', 'name String, id String') where _path like '%test%'


# Insert
insert into function  CnchS3('http://s3.region.amazonaws.com.cn/bucket/normal_write.csv', 'name String, id String') values ('one', '1'), ('two', '2'), ('three', '3')

# Insert by partition
# Ensure that the '{_partition_id}' field is included in the path
insert into function
    CnchS3('http://s3.region.amazonaws.com.cn/bucket/{_partition_id}_partition_write.csv', 'name String, id String')
    partition by name
values ('one', '1'),('one', '2'),('two', '1'),('two', '2');

select * from jiashuo_db.s3_glob where _file like '%partition_write%' 
```


Format and Compression are optional parameters. The schema of the data needs to be specified.
