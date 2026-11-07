---
title: "RETURNING syntax usage"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/RETURNING_syntax_usage"
---

The RETURNING syntax enables you to retrieve the rows affected by an insert, update, or delete operation after executing a DML operation without requiring additional queries. This article introduces the basic usage of RETURNING syntax.

<span id=".5Yqf6IO96K-05piO"></span>
## Function description

The RETURNING syntax supports directly returning the affected row data (the returned result can be any column, expression, or subquery) when executing DML statements such as INSERT, REPLACE, UPDATE, and DELETE, without the need for additional SELECT queries to obtain result information. Through the RETURNING syntax, users can intuitively view the results of database operations, simplify the database operation process, reduce the interaction between the Client and MySQL Server, and improve the efficiency and performance of database operations.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

Version restrictions: The instance compatible version is MySQL 8.0, and the kernel version is greater than or equal to 3.0.5.2. For details on the version, please refer to [Version management](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Version_number_management).

<span id=".6K-t5rOV6K-05piO"></span>
## Syntax


* **Syntax definition**

   
   |DML |Syntax |
   |---|---|
   |**INSERT ... RETURNING** |```SQL```<br>```INSERT[LOW_PRIORITY```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    [(col_name [, col_name] ...)]```<br>```    { {VALUES```<br>```    [AS row_alias[(col_alias [, col_alias] ...)]]```<br>```    [ON DUPLICATE KEY UPDATE assignment_list]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br>``````<br>```INSERT[LOW_PRIORITY```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    SET assignment_list```<br>```    [AS row_alias[(col_alias [, col_alias] ...)]]```<br>```    [ON DUPLICATE KEY UPDATE assignment_list]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br> |
   |**REPLACE ... RETURNING** |```sql```<br>```REPLACE [LOW_PRIORITY```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    [(col_name [, col_name] ...)]```<br>```    { {VALUES```<br>``````<br>```      VALUES row_constructor_list```<br>```    }```<br>```    [RETURNING select_expr [, select_expr] ...]```<br>``````<br>``` REPLACE [LOW_PRIORITY```<br>```    [INTO] tbl_name```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    SET assignment_list```<br>```    [RETURNING select_expr [, select_expr] ...]```<br> |
   |**DELETE ... RETURNING** |```SQL```<br>```DELETE[LOW_PRIORITY] [QUICK] [IGNORE] FROM tbl_name [[AS] tbl_alias]```<br>```    [PARTITION (partition_name [, partition_name] ...)]```<br>```    [WHERE where_condition]```<br>```    [ORDER BY ...]```<br>```    [LIMIT row_count]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br> |
   |**UPDATE ... RETURNING** |```sql```<br>```UPDATE [LOW_PRIORITY] [IGNORE] table_reference```<br>```    SET assignment_list```<br>```    [WHERE where_condition]```<br>```    [ORDER BY ...]```<br>```    [LIMIT row_count]```<br>```    [RETURNING select_expr [, select_expr] ...]```<br> |
   

* **Parameter description**

   NDB for MySQL extends the MySQL INSERT, REPLACE, UPDATE, and DELETE syntax to support the use of a `RETURNING select_expr` list based on the original syntax. The select_expr can be the following:

   * Column name

   * Expression.

   * `*`: Indicates expansion to all columns.

   * A subquery can only return one row of results.

   * Function, Aggregate Function is not supported.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Does not support <code>INSERT...</code> <code>SELECT ...</code>、<code>REPLACE ...</code> <code>SELECT ...</code> , <code>Multiple-Table delete</code>, <code>Multiple-Table update</code>, etc. syntax.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In any syntax, aliases cannot use <code>RETURNING</code>.   </div>
   


<span id=".56S65L6L"></span>
## example


* INSRET RETURNING

   ```sql
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
   

* DELETE RETURNING

   ```sql
   MySQL [test]> delete from t1 where name = 'Jackie Chan' returning *;
   +----+-------------+
   | id | name        |
   +----+-------------+
   |  1 | Jackie Chan |
   +----+-------------+
   1 row in set (0.01 sec)
   ```
   

* REPLACE RETURNING

   ```sql
   MySQL [test]> insert into t1(name) values('Jackie Chan') returning *;
   +----+-------------+
   | id | name        |
   +----+-------------+
   |  3 | Jackie Chan |
   +----+-------------+
   1 row in set (0.00 sec)
   
   MySQL [test]> replace into t1(id,name) values(3, 'lisi') returning *;
   +----+------+
   | id | name |
   +----+------+
   |  3 | lisi |
   +----+------+
   1 row in set (0.01 sec)
   ```
   

* UPDATE RETURNING

   ```sql
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
