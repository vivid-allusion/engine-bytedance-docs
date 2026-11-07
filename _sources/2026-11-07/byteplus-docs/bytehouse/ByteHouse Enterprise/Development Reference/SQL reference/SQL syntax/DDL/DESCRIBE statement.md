---
title: "DESCRIBE statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-describe-statement"
---

`DESCRIBE` statement can be used to return the column definitions of a table.

<span id="36089b70"></span>
## **Grammar**

```SQL
DESC|DESCRIBE TABLE [db.]table [INTO OUTFILE filename] [FORMAT format]
```


<span id="19128135"></span>
## Parameter description


|Parameters |Required field |Note |
|---|---|---|
|INTO OUTFILE filename |Optional |Export the results to a file (an absolute path is required, for example, `/data/dict_list.csv`). |
|FORMAT format |Optional |Specify the format of the returned results (such as `JSON`, `CSV`, and more). |


<span id="c26b18a7"></span>
### Output column descriptions


|Column name |Note |Example value |
|---|---|---|
|`name` |Column name |`user_id` |
|`type` |Column data types |`Nullable(String)` |
|`default_type` |Clauses used in column default expressions:<br><br>• `DEFAULT`<br><br>• `MATERIALIZED`<br><br>• `ALIAS`<br><br>If there is no default expression, an empty string is returned. |`DEFAULT` |
|`default_expression` |The expression specified after the DEFAULT clause |`toUUID('00000000-0000-0000-0000-000000000000')` |
|`comment` |Column annotations |`Unique user identifier` |
|`codec_expression` |Data compression encoding for the column |`CODEC(ZSTD(5))` |
|`ttl_expression` |TTL (time to live) expression |`created_at + INTERVAL 1 YEAR` |
|`is_subcolumn` |Subcolumn identifier<br><br>• `1`: Internal sublist<br><br>• `0`: Standard column<br><br>This flag is included in the result only when subcolumn description is enabled via `describe_include_subcolumns`. |Settings that need to be enabled:<br><br>`SET describe_include_subcolumns=1` |


<span id="cb2829aa"></span>
## **Example**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a table
DROP TABLE IF EXISTS sample_db.describe_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.describe_table ON CLUSTER sample_cluster (
    id UInt64, 
    text String DEFAULT 'unknown' CODEC(ZSTD),
    user Tuple (name String, age UInt8)
) ENGINE = MergeTree() 
ORDER BY id;

-- 3. Return the definitions of the columns in the table
DESCRIBE TABLE sample_db.describe_table;

-- Example output is as follows:
┌─name─┬─type───────────────┬─default_type─┬─default_expression─┬─comment─┬─codec_expression─┬─ttl_expression─┐
│ id    │ UInt64                        │               │                     │           │                   │                 │
│ text  │ String                        │ DEFAULT       │ 'unknown'           │           │ ZSTD(1)           │                 │
│ user  │ Tuple(name String, age UInt8) │               │                     │           │                   │                 │
└────┴───────────────────┴─────────┴────────────┴───────┴───────────┴──────────┘
```
