---
title: "MySQL external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mysql-external-table"
---

The MySQL engine can perform `SELECT` queries on data stored on a remote MySQL server.
Invocation Format:
```Plain
MySQL('host:port', 'database', 'table', 'user', 'password'[, replace_query, 'on_duplicate_clause']);
```

**Invocation parameters**

* `host:port` — MySQL server address.
* `database` — Name of the database.
* `table` — Table name.
* `user` — Database user.
* `password` — User password.
* `replace_query` — A flag that converts `INSERT INTO` queries into `REPLACE INTO`.
   * `0` - The query was run as `INSERT INTO`.
   * `1` - The query was run as `REPLACE INTO`.
* `on_duplicate_clause` — Add the `ON DUPLICATE KEY on_duplicate_clause` expression to the `INSERT` query. When using this setting, you need to set `replace_query = 0`. If you set both `replace_query = 1` and `on_duplicate_clause` simultaneously, ClickHouse / ByteHouse will produce an abnormality.

At that point, simple `WHERE` clauses (such as `=, !=, >, >=,<, <=`) are executed on the MySQL server.
The remaining conditions and `LIMIT` sampling constraint statements are only executed in ClickHouse / ByteHouse after the MySQL query is complete.
The `MySQL` engine does not support nullable data types. Therefore, when reading data from MySQL tables, `NULL` is converted to the default value of the specified column type (usually 0 or an empty string).
