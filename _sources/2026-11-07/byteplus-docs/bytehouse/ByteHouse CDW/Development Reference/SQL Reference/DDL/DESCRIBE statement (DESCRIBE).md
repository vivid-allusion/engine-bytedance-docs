---
title: "DESCRIBE statement (DESCRIBE)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/describe-statement"
---

DESCRIBE returns the column definitions of the table.

**Syntax**

```SQL
DESC|DESCRIBE TABLE [db.]table [INTO OUTFILE filename] [FORMAT format]
```


The DESCRIBE statement returns a line for each table column, containing the following string values:


* Name — Column name.

* Type — Column type.

* default_type — The clause used in the column's default expression: Default, MATERIALIZED, or ALIAS. If there is no default expression, an empty string is returned.

* default_expression — The expression specified after the DEFAULT clause.

* comment — Column comments.

* codec_expression — Encoding applied to this column.

* ttl_expression — TTL expression.

* is_subcolumn — For internal subcolumns, the value is 1. Only when subcolumn descriptions are activated through the settings of describe_include_subcolumns is this flag included in the results.


**Example**

```SQL
-- Create a table
CREATE TABLE describe_example (
    id UInt64, text String DEFAULT 'unknown' CODEC(ZSTD),
    user Tuple (name String, age UInt8)
) ENGINE = CnchMergeTree() ORDER BY id;

--Return the definition of the columns in the table
DESCRIBE TABLE describe_example;
┌─name─┬─type──────────────────────────┬─default_type─┬─default_expression─┬─comment─┬─codec_expression─┬─ttl_expression─┐
│ id   │ UInt64                        │              │                    │         │                  │                │
│ text │ String                        │ DEFAULT      │ 'unknown'          │         │ ZSTD(1)          │                │
│ user │ Tuple(name String, age UInt8) │              │                    │         │                  │                │
└──────┴───────────────────────────────┴──────────────┴────────────────────┴─────────┴──────────────────┴────────────────┘
```
