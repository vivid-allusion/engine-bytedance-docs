---
title: "RETURNING"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/RETURNING"
---

This topic describes the RETURNING syntax provided by RDS for MySQL.

<span id="FEEfjAhW"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20251015 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.43_20251015 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<span id="e1sSTSZb"></span>
## Background

In some business scenarios, after executing DML statements such as INSERT, REPLACE, UPDATE, and DELETE, an additional query is required to retrieve the specific records of the operation. This increases the number of interactions between the client and the MySQL Server, resulting in additional performance overhead and latency.

To simplify the operation flow and reduce communication between clients and the server, RDS for MySQL provides the RETURNING syntax, which allows the server to return the result set directly when executing DML statements.

<span id="oqfiY6iv"></span>
## Feature description

When executing DML statements such as INSERT, REPLACE, UPDATE, and DELETE, the RETURNING syntax directly returns a result set (Resultset) packet. This packet contains the affected row data (the returned result can be any column, expression, or subquery) and eliminates the need for an additional SELECT query to obtain result information.

Typical applicable scenarios include:


* After an insert operation is completed, return the AUTO_INCREMENT primary key and the values of other columns for subsequent related operations.

* When executing an update operation, return the latest column values or the result of an expression to continue processing business logic.

* When executing a delete operation, return a snapshot of the fields before deletion for auditing or compensation records.


<span id="bAIwrKT6"></span>
## Instructions

<span id="tSoEd1zg"></span>
### Syntax description

The `RETURNING select_expr` clause can be appended to the original syntax of a single\-table DML statement. `select_expr` can be the following:


* Column name

* Expression

* \*: Expands to all columns

* Subquery. It must be a subquery that returns a single row.

* Function. Aggregate functions are not supported.



|**DML** |**Syntax** |
|---|---|
|**INSERT ... RETURNING** |```SQL```<br>```INSERT [LOW_PRIORITY \| DELAYED \| HIGH_PRIORITY] [IGNORE]```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    [(col_name [, col_name] ...)]```<br>```    { {VALUES \| VALUE} (value_list) [, (value_list)] ... }```<br>```    [AS row_alias[(col_alias [, col_alias] ...)]]```<br>```    [ON DUPLICATE KEY UPDATE assignment_list]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br>``````<br>```INSERT [LOW_PRIORITY \| DELAYED \| HIGH_PRIORITY] [IGNORE]```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    SET assignment_list```<br>```    [AS row_alias[(col_alias [, col_alias] ...)]]```<br>```    [ON DUPLICATE KEY UPDATE assignment_list]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br> |
|**REPLACE ... RETURNING** |```SQL```<br>```REPLACE [LOW_PRIORITY \| DELAYED]```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    [(col_name [, col_name] ...)]```<br>```    { {VALUES \| VALUE} (value_list) [, (value_list)] ...```<br>```      \|```<br>```      VALUES row_constructor_list```<br>```    }```<br>```    [RETURNING select_expr [, select_expr] ...]```<br>```    ```<br>``` REPLACE [LOW_PRIORITY \| DELAYED]```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    SET assignment_list[RETURNING select_expr [, select_expr] ...]```<br> |
|**DELETE ... RETURNING** |```SQL```<br>```DELETE [LOW_PRIORITY] [QUICK] [IGNORE] FROM tbl_name [[AS] tbl_alias]```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    [WHERE where_condition]```<br>```    [ORDER BY ...]```<br>```    [LIMIT row_count]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br> |
|**UPDATE ... RETURNING** |```SQL```<br>```UPDATE [LOW_PRIORITY] [IGNORE] table_reference```<br>```    SET assignment_list```<br>```    [WHERE where_condition]```<br>```    [ORDER BY ...]```<br>```    [LIMIT row_count]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br> |


<span id="rCN6ewrK"></span>
### Examples


* **INSERT ... RETURNING**


```SQL
MySQL [test]> create table t1 (id bigint auto_increment, name varchar(64), primary key (id));
Query OK, 0 rows affected (0.06 sec)
MySQL [test]> insert into t1(name) values('Jackie Chan'),('Bruce Lee') returning *;
+----+-------------+
| id | name        |
+----+-------------+
|  1 | Jackie Chan |
|  2 | Bruce Lee   |
+----+-------------+
2 rows in set (0.01 sec)
```



* **REPLACE ... RETURNING**


```SQL
MySQL [test]> insert into t1(name) values('Jackie Chan') returning *;
+----+-------------+
| id | name        |
+----+-------------+
|  3 | Jackie Chan |
+----+-------------+
1 row in set (0.00 sec)
MySQL [test]> replace into t1(id,name) values(3, 'lisi') returning id*2, name;
+------+------+
| id*2 | name |
+------+------+
|    6 | lisi |
+------+------+
1 row in set (0.00 sec)
```



* **DELETE ... RETURNING**


```SQL
mysql> delete from t1 where name = 'Jackie Chan' returning id, LENGTH(name);
+----+--------------+
| id | LENGTH(name) |
+----+--------------+
|  1 |           11 |
+----+--------------+
1 row in set (0.01 sec)    
```



* **UPDATE ... RETURNING**


```SQL
MySQL [test]> create table t2 (id bigint primary key, cnt bigint);
Query OK, 0 rows affected (0.03 sec)
MySQL [test]> insert into t2 values(1,0),(2,0);
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0
MySQL [test]> update t2 set cnt = cnt + 1 returning *;
+----+------+
| id | cnt  |
+----+------+
|  1 |    1 |
|  2 |    1 |
+----+------+
2 rows in set (0.00 sec)
MySQL [test]> update t2 set cnt = cnt + 1 returning *;
+----+------+
| id | cnt  |
+----+------+
|  1 |    2 |
|  2 |    2 |
+----+------+
2 rows in set (0.00 sec)
```


<span id="gVNu2wbi"></span>
### Precautions


* The RETURNING clause is not supported for the following syntaxes:

   * INSERT ... SELECT ...

   * REPLACE ... SELECT ...

   * Multiple\-Table DELETE

   * Multiple\-Table UPDATE

* Table aliases cannot be used with RETURNING in DELETE statements.

* INSERT/REPLACE/UPDATE ... RETURNING returns the post\-update image; DELETE ... RETURNING returns the pre\-delete image.
