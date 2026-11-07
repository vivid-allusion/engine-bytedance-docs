---
title: "Case sensitivity"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-case-sensitivity"
---

Case sensitivity (Case sensitivity) refers to situations where using uppercase letters and lowercase letters yields different results.

For example, for the case\-sensitive (`String` `ByteHouse` and `bytehouse`) data entries String type, the values stored in the database are not equal then.

<span id="27a0477e"></span>
## Data Type

The case sensitivity of all supported data types in the ByteHouse Cloud Data Warehouse Edition is shown in the table below, with case_insensitive=0 indicating case sensitivity.


|Data Type |Case Sensitivity (case_sensitive) |
|---|---|
|AggregateFunction |0 |
|Array |0 |
|Base64ToBinary |1 |
|BIGINT |1 |
|BIGINT SIGNED |1 |
|BIGINT UNSIGNED |1 |
|BINARY |1 |
|BINARY LARGE OBJECT |1 |
|BINARY VARYING |1 |
|BitMap64 |0 |
|BLOB |1 |
|Bool |1 |
|bool |1 |
|boolean |1 |
|BYTE |1 |
|BYTEA |1 |
|CHAR |1 |
|CHAR LARGE OBJECT |1 |
|CHAR VARYING |1 |
|CHARACTER |1 |
|CHARACTER LARGE OBJECT |1 |
|CHARACTER VARYING |1 |
|CLOB |1 |
|Date |1 |
|Date32 |1 |
|DateTime |1 |
|DateTime32 |1 |
|DateTime64 |1 |
|DateTimeWithoutTz |1 |
|DEC |1 |
|Decimal |1 |
|Decimal128 |1 |
|Decimal256 |1 |
|Decimal32 |1 |
|Decimal64 |1 |
|DOUBLE |1 |
|DOUBLE PRECISION |1 |
|Enum |1 |
|ENUM |1 |
|Enum16 |0 |
|Enum8 |0 |
|FIXED |1 |
|FixedString |0 |
|FLOAT |1 |
|Float32 |0 |
|Float64 |0 |
|HllSketchBinary |1 |
|INET4 |1 |
|INET6 |1 |
|INT |1 |
|INT SIGNED |1 |
|INT UNSIGNED |1 |
|INT1 |1 |
|INT1 SIGNED |1 |
|INT1 UNSIGNED |1 |
|Int128 |0 |
|Int16 |0 |
|Int256 |0 |
|Int32 |0 |
|Int64 |0 |
|Int8 |0 |
|INTEGER |1 |
|INTEGER SIGNED |1 |
|INTEGER UNSIGNED |1 |
|IntervalDay |0 |
|IntervalHour |0 |
|IntervalMinute |0 |
|IntervalMonth |0 |
|IntervalQuarter |0 |
|IntervalSecond |0 |
|IntervalWeek |0 |
|IntervalYear |0 |
|IPv4 |0 |
|IPv6 |0 |
|LONGBLOB |1 |
|LONGTEXT |1 |
|LowCardinality |0 |
|Map |0 |
|MEDIUMBLOB |1 |
|MEDIUMINT |1 |
|MEDIUMINT SIGNED |1 |
|MEDIUMINT UNSIGNED |1 |
|MEDIUMTEXT |1 |
|MultiPolygon |0 |
|NATIONAL CHAR |1 |
|NATIONAL CHAR VARYING |1 |
|NATIONAL CHARACTER |1 |
|NATIONAL CHARACTER LARGE OBJECT |1 |
|NATIONAL CHARACTER VARYING |1 |
|NCHAR |1 |
|NCHAR LARGE OBJECT |1 |
|NCHAR VARYING |1 |
|Nested |0 |
|Nothing |0 |
|Nullable |0 |
|NUMERIC |1 |
|NVARCHAR |1 |
|Point |0 |
|Polygon |0 |
|REAL |1 |
|Ring |0 |
|Set |0 |
|SimpleAggregateFunction |0 |
|SINGLE |1 |
|SketchBinary |0 |
|SMALLINT |1 |
|SMALLINT SIGNED |1 |
|SMALLINT UNSIGNED |1 |
|String |0 |
|TEXT |1 |
|Time |1 |
|TIMESTAMP |1 |
|TINYBLOB |1 |
|TINYINT |1 |
|TINYINT SIGNED |1 |
|TINYINT UNSIGNED |1 |
|TINYTEXT |1 |
|Tuple |0 |
|UInt128 |0 |
|UInt16 |0 |
|UInt256 |0 |
|UInt32 |0 |
|UInt64 |0 |
|UInt8 |0 |
|UUID |0 |
|VARBINARY |1 |
|VARCHAR |1 |
|VARCHAR2 |1 |
