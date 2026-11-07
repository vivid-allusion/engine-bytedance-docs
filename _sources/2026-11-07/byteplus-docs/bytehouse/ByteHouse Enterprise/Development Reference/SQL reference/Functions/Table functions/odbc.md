---
title: "odbc"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/odbc-function"
---

Retrieve tables through [ODBC](https://en.wikipedia.org/wiki/Open_Database_Connectivity) connection.
```sql
odbc(connection_settings, external_database, external_table)
```

Parameters:
`Connection settings` — name of the settings section in `odbc.ini` file.
`External database` — database name of external DBMS.
`External table` — table name in the `external database`.
To securely implement ODBC connections, ClickHouse uses a separate program `clickhouse-odbc-bridge`. If the ODBC driver is loaded directly from `clickhouse-server`, driver problems may cause ClickHouse server to crash. When needed, ClickHouse automatically starts `clickhouse-odbc-bridge`. The ODBC bridge program is installed from the same package as `clickhouse-server`.
Values containing `NULL` in the external table fields will be converted to the default values for their data types. For example, if a field in a remote MySQL table contains the `INT NULL` type, it will be converted to 0 (the default value for the ClickHouse `Int32` data type).
<span id="用法示例 {#usage-example}"></span>
## Usage example
**Retrieving data from a locally installed MySQL via ODBC**
This example reviews Ubuntu Linux 18.04 and MySQL Server 5.7.
Ensure unixODBC and MySQL Connector are installed.
By default (if installed from packages), ClickHouse launches as user `clickhouse`. Therefore, you need to create and configure this user in the MySQL server.
```bash
$ sudo mysql
```

```sql
mysql> CREATE USER 'clickhouse'@'localhost' IDENTIFIED BY 'clickhouse';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'clickhouse'@'clickhouse' WITH GRANT OPTION;
```

Then, configure the connection in `/etc/odbc.ini`.
```bash
$ cat /etc/odbc.ini
[mysqlconn]
DRIVER = /usr/local/lib/libmyodbc5w.so
SERVER = 127.0.0.1
PORT = 3306
DATABASE = test
USERNAME = clickhouse
PASSWORD = clickhouse
```

You can use the `isql` utility installed with unixODBC to check the connection.
```bash
$ isql -v mysqlconn
+-------------------------+
| Connected!                            |
|                                       |
...
```

Tables in MySQL:
```text
mysql> CREATE TABLE `test`.`test` (
    ->   `int_id` INT NOT NULL AUTO_INCREMENT,
    ->   `int_nullable` INT NULL DEFAULT NULL,
    ->   `float` FLOAT NOT NULL,
    ->   `float_nullable` FLOAT NULL DEFAULT NULL,
    ->   PRIMARY KEY (`int_id`));
Query OK, 0 rows affected (0,09 sec)

mysql> insert into test (`int_id`, `float`) VALUES (1,2);
Query OK, 1 row affected (0,00 sec)

mysql> select * from test;
+------+----------+-----+----------+
| int_id | int_nullable | float | float_nullable |
+------+----------+-----+----------+
|      1 |         NULL |     2 |           NULL |
+------+----------+-----+----------+
1 row in set (0,00 sec)
```

Retrieving data from MySQL tables in ClickHouse:
```sql
SELECT * FROM odbc('DSN=mysqlconn', 'test', 'test')
```

```text
┌─int_id─┬─int_nullable─┬─float─┬─float_nullable─┐
│      1 │            0 │     2 │              0 │
└────────┴──────────────┴───────┴────────────────┘
```
