---
title: "postgresql"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/postgresql-function"
---

Allows `SELECT` and `INSERT` queries on data stored on a remote PostgreSQL server.
**Syntax**
```sql
postgresql('host:port', 'database', 'table', 'user', 'password'[, `schema`])
```

**Parameter**
`host:port` — Address of the PostgreSQL server.
`database` — Name of the remote database.
`table` — Name of the remote table.
`user` — PostgreSQL user.
`password` — User password.
`schema` — Non-default table structure. Optional.
**Return value**
A table object with the same number of columns as the original PostgreSQL table.
:::tip
In an `INSERT` query, to distinguish the table function `postgresql(..)` from the table name and the list of column names, you must use the keyword `FUNCTION` or `TABLE FUNCTION`. See the example below.
:::
<span id="实施细节 {#implementation-details}"></span>
## Implementation details
`SELECT` queries run in a read-only PostgreSQL transaction using `COPY (SELECT ...) TO STDOUT`, with a commit after each `SELECT` query.
Simple `WHERE` clause such as `=` and `!` `=`, `>`, `>=`, `<`, `<=` and `IN` are executed on the PostgreSQL server.
All connections, aggregates, sorting, `IN [ array ]` conditions, and `LIMIT` sampling restraints are only executed in ClickHouse after the PostgreSQL query ends.
`INSERT` queries on PostgreSQL run in PostgreSQL transactions using the method `COPY "table_name" (field1, field2, ... fieldN) FROM STDIN`, with automatic `commit` after each INSERT statement.
PostgreSQL array types are converted to ClickHouse arrays.
!!! info "Note"
Take care, in PostgreSQL, columns of array data types like Integer[] can contain arrays of different dimensions in different rows, but in ClickHouse, only arrays of the same dimensions are allowed in all rows.
Support for setting priority for Replicas in the PostgreSQL Dictionary sources is provided. The larger the number in the map, the lower the priority. `0` represents the highest priority.
**Example**
Tables in PostgreSQL:
```text
postgres=# CREATE TABLE "public"."test" (
"int_id" SERIAL,
"int_nullable" INT NULL DEFAULT NULL,
"float" FLOAT NOT NULL,
"str" VARCHAR(100) NOT NULL DEFAULT '',
"float_nullable" FLOAT NULL DEFAULT NULL,
PRIMARY KEY (int_id));

CREATE TABLE

postgres=# INSERT INTO test (int_id, str, "float") VALUES (1,'test',2);
INSERT 0 1

postgresql> SELECT * FROM test;
  int_id | int_nullable | float | str  | float_nullable
 --------+--------------+-------+------+----------------
       1 |              |     2 | test |
(1 row)
```

Retrieving data from ClickHouse:
```sql
SELECT * FROM postgresql('localhost:5432', 'test', 'test', 'postgresql_user', 'password') WHERE str IN ('test');
```

```text
┌─int_id─┬─int_nullable─┬─float─┬─str──┬─float_nullable─┐
│      1 │         ᴺᵁᴸᴸ │     2 │ test │           ᴺᵁᴸᴸ │
└────────┴──────────────┴───────┴──────┴────────────────┘
```

Inserting data:
```sql
INSERT INTO TABLE FUNCTION postgresql('localhost:5432', 'test', 'test', 'postgrsql_user', 'password') (int_id, float) VALUES (2, 3);
SELECT * FROM postgresql('localhost:5432', 'test', 'test', 'postgresql_user', 'password');
```

```text
┌─int_id─┬─int_nullable─┬─float─┬─str──┬─float_nullable─┐
│      1 │         ᴺᵁᴸᴸ │     2 │ test │           ᴺᵁᴸᴸ │
│      2 │         ᴺᵁᴸᴸ │     3 │      │           ᴺᵁᴸᴸ │
└────────┴──────────────┴───────┴──────┴────────────────┘
```

Using a non-default table structure:
```text
postgres=# CREATE SCHEMA "nice.schema";

postgres=# CREATE TABLE "nice.schema"."nice.table" (a integer);

postgres=# INSERT INTO "nice.schema"."nice.table" SELECT i FROM generate_series(0, 99) as t(i)
```

```sql
CREATE TABLE pg_table_schema_with_dots (a UInt32)
        ENGINE PostgreSQL('localhost:5432', 'clickhouse', 'nice.table', 'postgrsql_user', 'password', 'nice.schema');
```
