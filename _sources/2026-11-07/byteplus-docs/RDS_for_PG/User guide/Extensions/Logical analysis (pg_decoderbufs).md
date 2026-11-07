---
title: "Logical analysis (pg_decoderbufs)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/logical_analysis-pg_decoderbufs"
---

pg_decoderbufs is a logical decoding extension using the protocol buffer format.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions

pg_decoderbufs supports DML statements (Delete, Update, and Insert) only for logical decoding and the result is presented in the protocol buffer format.

<span id=".5o-S5Lu26YCJ6aG5"></span>
## Extension options


|Options name |debug\-mode |
|---|---|
|Description |After performing logical decoding, output the decoded result in character mode. |
|Examples |```shell```<br>```select * from pg_logical_slot_peek_changes('demo', null, null, 'debug-mode', '1');```<br>```select * from pg_logical_slot_get_changes('demo', null, null, 'debug-mode', '1');```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Refer to the following SQL query for definitions of <code>pg_logical_slot_peek_changes</code> and <code>pg_logical_slot_get_changes</code> functions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>select * from pg_proc where proname = 'pg_logical_slot_peek_changes';</code></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>select * from pg_proc where proname = 'pg_logical_slot_get_changes';</code></div><br> |


<span id=".5pig5bCE5YWz57O7"></span>
## Mapping relationship

The mapping information between PostgreSQL types and decoderbuf fields is as follows:


|**PostgreSQL Type OID** |**Decoderbuf Field** |
|---|---|
|BOOLOID |datum_boolean |
|INT2OID |datum_int32 |
|INT4OID |datum_int32 |
|INT8OID |datum_int64 |
|OIDOID |datum_int64 |
|FLOAT4OID |datum_float |
|FLOAT8OID |datum_double |
|NUMERICOID |datum_double |
|CHAROID |datum_string |
|VARCHAROID |datum_string |
|BPCHAROID |datum_string |
|TEXTOID |datum_string |
|JSONOID |datum_string |
|XMLOID |datum_string |
|UUIDOID |datum_string |
|TIMESTAMPOID |datum_string |
|TIMESTAMPTZOID |datum_string |
|BYTEAOID |datum_bytes |
|POINTOID |datum_point |
|PostGIS geometry |datum_point |
|PostGIS geography |datum_point |


<span id=".5o-S5Lu255qE5L2_55So"></span>
## Using extensions

<span id=".5YmN572u5p2h5Lu2"></span>
### Prerequisites


* `wal_level` is set to `logical`.

* The table for logical analysis has a unique index, primary key, or a specified [REPLICA IDENTITY](https://www.postgresql.org/docs/11/sql-altertable.html#SQL-CREATETABLE-REPLICA-IDENTITY).


<span id=".5L2_55So5o-S5Lu2"></span>
### Extension usage


1. Create release and specify logical parsing extension as `decoderbufs`.

   ```sql
   select pg_create_logical_replication_slot('demo', 'decoderbufs');
   ```
   

2. Enable read/write and view logical parsing in `debug-mode` mode.

   ```sql
   select * from pg_logical_slot_peek_changes('demo', null, null, 'debug-mode', '1');
   select * from pg_logical_slot_get_changes('demo', null, null, 'debug-mode', '1');
   select * from pg_replication_slots;
   ```
