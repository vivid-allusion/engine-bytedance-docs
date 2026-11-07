---
title: "mysql"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mysql-function"
---

Allows `SELECT` and `INSERT` queries on data stored on remote MySQL servers.
**Syntax**
```SQL
mysql('host:port', 'database', 'table', 'user', 'password'[, replace_query, 'on_duplicate_clause']);
```

**Parameter**

* `host:port` — Address of the MySQL server.
* `database` — Name of the remote database.
* `table` — Name of the remote table.
* `user` — MySQL user.
* `password` — User password.
* `replace_query` — Convert `INSERT INTO` queries to `REPLACE INTO` flags.
   * `0` - The query is executed as `INSERT INTO`.
   * `1` - The query is executed as `REPLACE INTO`.
* `on_duplicate_clause` — Add `ON DUPLICATE KEY on_duplicate_clause` expression to `INSERT` query. When using this, you need to set `replace_query = 0`. If you set `replace_query = 1` and `on_duplicate_clause` at the same time, ClickHouse / ByteHouse will produce an exception.

Simple `WHERE` clauses such as `=, !=, >, >=,<, <=` will be executed immediately on the MySQL server. The remaining conditions and `LIMIT` constraints will only be performed in ClickHouse / ByteHouse after the query to MySQL is complete.
Supports concurrent multi-copy queries using `|`, examples are as follows:
```SQL
SELECT name FROM mysql(`mysql{1|2|3}:3306`, 'mysql_database', 'mysql_table', 'user', 'password');
```

or
```SQL
SELECT name FROM mysql(`mysql1:3306|mysql2:3306|mysql3:3306`, 'mysql_database', 'mysql_table', 'user', 'password');
```

**Return value**
A table object with the same columns as the original MySQL table.
:::tip
In the `INSERT` query, to distinguish between `mysql(...)` and the table function with a list of column names, you must use the keyword `FUNCTION` or `TABLE FUNCTION`. View the following example.
:::
<span id="52630a9c"></span>
## Usage example
Tables in MySQL:
```Plain
mysql> CREATE TABLE `test`.`test` (
    ->   `int_id` INT NOT NULL AUTO_INCREMENT,
    ->   `float` FLOAT NOT NULL,
    ->   PRIMARY KEY (`int_id`));

mysql> INSERT INTO test (`int_id`, `float`) VALUES (1,2);

mysql> SELECT * FROM test;
+--------+-------+
| int_id | float |
+--------+-------+
|      1 |     2 |
+--------+-------+
```

Query data from ClickHouse:
```SQL
SELECT * FROM mysql('localhost:3306', 'test', 'test', 'bayonet', '123')
```

```Plain
┌─int_id─┬─float─┐
│      1 │     2 │
└────────┴───────┘
```

Replacement and insertion:
```SQL
INSERT INTO FUNCTION mysql('localhost:3306', 'test', 'test', 'bayonet', '123', 1) (int_id, float) VALUES (1, 3);
INSERT INTO TABLE FUNCTION mysql('localhost:3306', 'test', 'test', 'bayonet', '123', 0, 'UPDATE int_id = int_id + 1') (int_id, float) VALUES (1, 4);
SELECT * FROM mysql('localhost:3306', 'test', 'test', 'bayonet', '123');
```

```Plain
┌─int_id─┬─float─┐
│      1 │     3 │
│      2 │     4 │
└────────┴───────┘
```
