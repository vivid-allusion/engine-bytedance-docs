---
title: "Flashback queries"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Flashback_queries"
---

The flashback query function enables you to quickly query data information at a certain point in the past, which helps with data recovery or troubleshooting. This article describes how to use the flashback query feature.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance with a compatible version of MySQL 8.0 has been created. For action steps, see [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The `innodb_flashback_query` parameter is enabled in instance parameter management and is turned off by default. For operation steps, see [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Version restrictions: The instance compatible version is MySQL 8.0, and the kernel version is greater than or equal to 3.0.5.2. For details on the version, please refer to [Version management](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Version_number_management).

* Only innoDB tables are supported, and view and other engines (such as HTAP engines) are not supported.

* Supported only in read\-only statements (insert ... select ... statements are supported in read committed isolation level).

* Only flashback queries within seconds are supported, and the time accuracy is not guaranteed. If there are multiple changes within one second, any one of them may be queried.

* After executing DDL (which will generate DDL to rebuild table, such as truncate table), the previous data flashback query results may not meet expectations.

* After PITR, the flashback query function of the instance fails because the undo log is lost (error `DB_MISSING_HISTORY`).

* Enabling flashback query will delay undo log cleanup and increase memory usage. Therefore, it is not recommended to set `innodb_flashback_query_window` too large. It is recommended to set it between 900 and 1800.

* It is recommended to use flashback query in single\-table scenarios, and it is not recommended to use Flashback Query in complex query scenarios (such as JOIN and subqueries).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

Control the flashback query function with the following parameters.


|Parameter |Default value |Description |Need restart? |
|---|---|---|---|
|**innodb_flashback_query** |OFF |Turn the flashback query function on or off. Value range:<br><br><br>* `ON`: Open.<br><br>* `OFF`: Off (default). |No |
|**innodb_flashback_query_window** |900 |The time length supported by flashback query is in seconds and the value range is 0~604800 (7 days).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Enabling flashback query will delay undo log cleanup and increase memory usage. Therefore, it is not recommended to set <code>innodb_flashback_query_window</code> too large. It is recommended to set it between 900 and 1800.</div><br> |No |


<span id=".6K-t5rOV6K-05piO"></span>
## Syntax

Flashback queries are supported using the following syntax.

```sql
SELECT <column name> FROM <table name> AS OF TIMESTAMP <time> WHERE <condition>;
```


<span id=".56S65L6L"></span>
## example


1. Create a table at `2025-03-25 15:50:35` and insert the data.

   ```sql
   CREATE TABLE t1 (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255),
       create_time TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
   );
   
   INSERT INTO t1 (name) VALUES ('Bob'), ('Charlie'), ('David');
   ```
   

   ```sql
   select * FROM t1;
   +----+---------+---------------------+
   | id | name    | create_time         |
   +----+---------+---------+-----------+
   |  1 | Bob     | 2025-03-25 15:50:35 |
   |  2 | Charlie | 2025-03-25 15:50:35 |
   |  3 | David   | 2025-03-25 15:50:35 |
   +----+---------+---------------------+
   ```
   

2. At `2025-03-25 16:04:50`, change `Bob` to `Alice`.

   ```sql
   UPDATE t1 SET name = 'Alice', create_time = NOW() WHERE name = 'Bob';
   
   select * FROM t1 ;
   +----+---------+---------------------+
   | id | name    | create_time         |
   +----+---------+---------+-----------+
   |  1 | Alice   | 2025-03-25 16:04:50 |
   |  2 | Charlie | 2025-03-25 15:50:35 |
   |  3 | David   | 2025-03-25 15:50:35 |
   +----+---------+---------------------+
   ```
   

3. View the data in the `2025-03-25 16:00:00` time point table.

   ```sql
   SELECT * FROM t1 AS OF TIMESTAMP '2025-03-25 16:00:00' ;
   
   select * FROM t1 ;
   +----+---------+---------------------+
   | id | name    | create_time         |
   +----+---------+---------+-----------+
   |  1 | Bob     | 2025-03-25 15:50:35 |
   |  2 | Charlie | 2025-03-25 15:50:35 |
   |  3 | David   | 2025-03-25 15:50:35 |
   +----+---------+---------------------+
   ```
   

4. At `2025-03-25 16:10:00` delete the row data with `name='David'`.

   ```sql
   DELETE FROM t1 WHERE name = 'David';
   
   select * FROM t1 ;
   +----+---------+---------------------+
   | id | name    | create_time         |
   +----+---------+---------+-----------+
   |  1 | Alice   | 2025-03-25 16:04:50 |
   |  2 | Charlie | 2025-03-25 15:50:35 |
   +----+---------+---------------------+
   ```
   

5. Look at the data for `id=3` in the time point table `2025-03-25 16:05:00`.

   ```sql
   SELECT * FROM t1 AS OF TIMESTAMP '2025-03-25 16:05:00' where id = 3;
   +----+---------+---------------------+
   | id | name    | create_time         |
   +----+---------+---------+-----------+
   |  3 | David   | 2025-03-25 15:50:35 |
   +----+---------+---------------------+
   ```
