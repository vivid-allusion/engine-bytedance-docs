---
title: "Hint syntax usage instructions"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Hint_syntax_usage_instructions"
---

This article introduces how to use Hint syntax in NDB for MySQL, as well as related precautions.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

Only read\-write terminal (automatic read\-write separation) addresses support Hint syntax. Read\-only terminal addresses and master node terminal addresses do not support Hint syntax. Even if Hint syntax is added to the SQL statement, it will not take effect. For more information about connecting end points, see [About connection endpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/About_connection_endpoint).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Hint has the highest routing priority and is not subject to functions such as connection binding, consistency level, and transaction splitting caused by transactions. Please evaluate whether it can be used for business before using it.

* The MySQL command line will filter comments in SQL statements by default. Therefore, when using the MySQL command line to execute Hint statements, you need to add the `-c` option when connecting to the database. For example, `mysql -h<connection address> -P<port> -u<user name> -p -c`. Otherwise, Hint will be filtered and become invalid. For more information, see the [MySQL documentation](https://dev.mysql.com/doc/refman/5.6/en/mysql-command-options.html#option_mysql_comments).

* Do not include statements that change environment variables in the Hint statement, such as `/*FORCE_SLAVE*/ set names utf8;`, as such statements may cause subsequent business errors. Also, do not set user variables through Hint, because after Hint is specified, the variables will only be set for the specified node, and will not be set for other nodes. If used improperly, it will cause inconsistency in the connection variables of different backend nodes of the same frontend connection.


<span id=".5L2_55So6K-05piO"></span>
## Instructions

NDB for MySQL supports the following three Hints:


* Add `/* FORCE_MASTER */` to the SQL statement to force the SQL to execute on the primary node.

   For example, `select * from test;` will normally be routed to the read\-only node. If you add Hint syntax to the statement and change it to `/*FORCE_MASTER*/ select * from test`, the statement will be forced to be routed to the primary node.

* Add `/*FORCE_SLAVE*/` to the SQL statement to force the specified SQL to be executed on the read\-only node.

   When specified by `/* FORCE_SLAVE */`, if there are multiple read\-only nodes at the read\-write endpoint, SQL will be sent to one of the read\-only nodes for execution according to the load balancing policy.

* Add `/*force_node=<node ID>*/` to the SQL statement to force the specified SQL to be executed on a certain node.

   For example, `/* force_ node=vedbm-255rdo****-0*/show processlist`, the `show processlist` command is executed only on `vedbm-255rdo **** -0` nodes. If the node fails or the specified node does not exist, an error `ERROR 15202 (HY000): No available conn for query is returned`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hint statements are not case sensitive and can only be used at the <strong>beginning</strong> of an SQL statement.</div>


* <div data-tips="true" data-tips-type="tip">If several hints are used in a SQL statement at the same time, only the last hint will take effect. For example, <code>/*FORCE_MASTER*//*FORCE_SLAVE*//*force_node=vedbm-255rdo****-0*/</code>, then <code>/*force_node=vedbm-255rdo****-0*/</code> will take effect.</div>


* <div data-tips="true" data-tips-type="tip">If you use <code>/*FORCE_SLAVE*/</code> or <code>/*force_node=<node ID>*/</code> to force a read\-only node to perform write operations or DDL operations, such as insert, update, and alter table, an error message will be returned: <code>The MySQL server is running with the --replica-mode option so it cannot execute this statement</code>.</div>



<span id=".56S65L6L"></span>
## example


* If Hint is used to specify a node to execute PREPARE, EXECUTE can only be executed on the corresponding node.

   ```sql
   MySQL [test]> /*FORCE_MASTER*/ PREPARE selecttest from 'select * from test where id=?';
   Query OK, 0 rows affected (0.00 sec)
   Statement prepared
   
   MySQL [test]> set @a=555;
   Query OK, 0 rows affected (0.01 sec)
   
   # 指定在主节点执行命令或不指定节点，成功。
   MySQL [test]> execute selecttest using @a;
   +------+------+
   | id   | code |
   +------+------+
   |  555 | 05   |
   +------+------+
   1 row in set (0.01 sec)
   MySQL [test]> /*FORCE_MASTER*/ execute selecttest using @a;
   +------+------+
   | id   | code |
   +------+------+
   |  555 | 05   |
   +------+------+
   1 row in set (0.00 sec)
   
   # 指定在只读节点执行命令，失败。
   MySQL [test]> /* force_node=vedbm-apdm3ztf****-2 */ execute selecttest using @a;
   ERROR 1243 (HY000): Unknown prepared statement handler (selecttest) given to EXECUTE
   ```
   

* If you specify set to be executed on a specific node through Hint, the variable can only be used on the corresponding node.

   ```sql
   MySQL [test]> /* force_node=vedbm-apdm3ztf****-1 */ set @a=111;
   Query OK, 0 rows affected (0.01 sec)
   
   MySQL [test]> /* force_node=vedbm-apdm3ztf****-1 */ select @a;
   +------+
   | @a   |
   +------+
   |  111 |
   +------+
   1 row in set (0.00 sec)
   
   MySQL [test]> /*FORCE_MASTER*/ select @a;
   +------+
   | @a   |
   +------+
   | NULL |
   +------+
   1 row in set (0.00 sec)
   ```
   

* Hint has the highest priority in a transaction.

   ```sql
   MySQL [test]> begin;
   Query OK, 0 rows affected (0.01 sec)
   
   MySQL [test]> INSERT INTO `test` VALUES ('222', '02');
   Query OK, 1 row affected (0.01 sec)
   
   MySQL [test]> /*FORCE_SLAVE*/ select * from test;
   +------+------+
   | id   | code |
   +------+------+
   |  111 | 01   |
   +------+------+
   1 row in set (0.01 sec)
   
   MySQL [test]> /*FORCE_MASTER*/ select * from test;
   +------+------+
   | id   | code |
   +------+------+
   |  111 | 01   |
   |  222 | 02   |
   +------+------+
   2 rows in set (0.01 sec)
   
   MySQL [test]> INSERT INTO `test` VALUES ('333', '03');
   Query OK, 1 row affected (0.01 sec)
   
   MySQL [test]> /*FORCE_MASTER*/ select * from test;
   +------+------+
   | id   | code |
   +------+------+
   |  111 | 01   |
   |  222 | 02   |
   |  333 | 03   |
   +------+------+
   3 rows in set (0.01 sec)
   
   MySQL [test]> /*FORCE_SLAVE*/ select * from test;
   +------+------+
   | id   | code |
   +------+------+
   |  111 | 01   |
   +------+------+
   1 row in set (0.00 sec)
   
   MySQL [test]> commit;
   Query OK, 0 rows affected (0.01 sec)
   
   MySQL [test]> /*FORCE_SLAVE*/ select * from test;
   +------+------+
   | id   | code |
   +------+------+
   |  111 | 01   |
   |  222 | 02   |
   |  333 | 03   |
   +------+------+
   3 rows in set (0.01 sec)
   ```
