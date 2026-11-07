---
title: "use DTS to synchronize MariaDB data to Volcano Engine RDS for MySQL"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/synchronize-mariadb-data-to-volcano-engine-mysql-using-dts"
---

In scenarios of database cloud migration or switching database platforms, you may need to synchronize local IDC, competitor cloud, or self\-built MariaDB data on other servers to a BytePlus RDS for MySQL instance. This topic introduces how to synchronize MariaDB data to an RDS for MySQL instance using the Database Transmission Service (DTS).

## Prerequisites

* A self\-built MariaDB instance accessible over the public network is deployed, and a database account with synchronization permissions is created.

* A BytePlus RDS for MySQL instance and database are created. For details, refer to [Creating an instance (RDS for MySQL)](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database).

* If access restrictions are enabled on the source MariaDB, add the IP address range of the DTS server to the allowlist or security group of the source database. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* The source MariaDB has enabled binlog, with `binlog_format` set to `ROW`, `binlog_row_image` set to `FULL`, and `server_id` greater than `0`. Otherwise, the pre\-check will report an error and incremental synchronization cannot start.

* Bandwidth requirements: adequate egress bandwidth is required on the source server and the destination server. Failure to meet this prerequisite will lead to suboptimal synchronization performance.

* Compatibility evaluation is completed, and incompatible objects have been modified. For details, refer to [compatibility evaluation and modification](https://docs.byteplus.com/en/docs/DTS/synchronize-mariadb-data-to-volcano-engine-mysql-using-dts?lang=en#YVpriz21).

## Precautions

* Currently only supported synchronizing MariaDB 10 data. To synchronize MariaDB 11 or MariaDB 12 data, submit tickets.

* The source end Binlog must be retained for at least 24 hours, preferably for more than 7 days, to avoid task interruption or failure due to log expiration during retries.

* DTS supports automatic synchronization of regular table structures. However, MariaDB\-specific objects, data types, functions, and syntax require modification before synchronization or manual creation on the target database to prevent schema initialization failure or incremental task errors.

* MariaDB GTID is incompatible with MySQL. DTS does not use GTID positions. When performing incremental synchronization only, the task initially locates the start position based on the timestamp. Breakpoint resume after task start is handled by physical positions. Avoid switching the source primary and secondary servers during the entire synchronization window, as it may cause errors due to invalid positions.

* Synchronizing built\-in system accounts such as `mysql`, `mariadb.sys`, and `healthcheck` is not supported yet. If these accounts are required by your business, create and authorize them on the target end before synchronization.

* The target database generates a large number of Binlog files during full initialization, which may cause the target database's disk usage to be much higher than the source instance. It is recommended to adjust the retention policy of the target database Binlog before full initialization.

* When switching business after completing data synchronization, conduct the operation after stopping writes on the source end and pausing related business, or schedule it during off\-peak hours to avoid impacting normal business operations.

* The general constraints and limitations of synchronization tasks are consistent with those for public network MySQL synchronization. For details, refer to [synchronizing from public network MySQL to Volcengine MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_RDS_for_MySQL?lang=en).

## Database account minimum permission policy

The account used for synchronization must have the following minimum permissions:

|**Database** |**Schema initialization** |**Full initialization** |**Incremental synchronization** |
|---|---|---|---|
|Source end MariaDB |SELECT permission |SELECT permission |REPLICATION SLAVE, REPLICATION CLIENT, and SELECT permissions |
|Target end MySQL |CREATE, DROP, ALTER, INDEX, REFERENCES permissions |SELECT, INSERT, UPDATE, DELETE permissions |SELECT, INSERT, UPDATE, DELETE, CREATE, ALTER, DROP, INDEX, REFERENCES permissions |

## Procedure

### Step 1: Compatibility evaluation and modification

MariaDB shares its origin with MySQL, but both have some proprietary objects and syntax that are mutually incompatible. Before synchronizing data, you must perform a compatibility evaluation on the source database. Use the database structure export tool or manual inspection to confirm whether the following MariaDB proprietary features exist. If incompatible items are found, business modifications must be completed before synchronization.

1. Compatibility evaluation: Export the table structure and object definitions of the source MariaDB, and inspect each item against the following incompatible contents including `SEQUENCE`, `INET6`, `INVISIBLE`, Aria engine, vector type, proprietary functions, etc.

   |**incompatible item** |**Impact** |**Suggestion** |
   |---|---|---|
   |`SEQUENCE` objects and related statements |MySQL natively does not support the `SEQUENCE` object; related DDL cannot be executed on the target, and functions such as `NEXTVAL()`, `SETVAL()` are unavailable. |Rewrite on the source end before synchronization: change sequence primary key columns to `AUTO_INCREMENT` auto\-increment columns; if the sequence logic must be preserved, simulate it with a single table at the business side. |
   |`INET6` data type |MySQL does not support the INET6 type; create table statements using this type will fail to execute on the target. |Before synchronization, convert the column type at the source end to a compatible type, such as `VARCHAR(46)` or `VARBINARY(16)`. |
   |`INVISIBLE` hidden column |Versions of MySQL before 8.0.23 do not support hidden columns, and related DDL statements will fail on the destination database. |If the target MySQL version does not support hidden columns, run `ALTER TABLE ...` before synchronization `MODIFY COLUMN ...` Redefine the complete column definition and remove the `INVISIBLE` attribute.<br><br>Test in the testing environment before executing to avoid changes in column type, default value, character set, or comments. |
   |`ENGINE=Aria` storage engine |MySQL does not support the Aria storage engine; create table statements will fail to execute on the target. |Before synchronization, convert all Aria engine tables on the source end to MySQL\-compatible engines, recommended using `ALTER TABLE ...` `ENGINE=InnoDB`。 |
   |Vector data type and function |MySQL lacks native vector type and corresponding function operations; related table structure and business SQL cannot synchronize. |When the target MySQL does not support the corresponding vector type or function, related objects cannot be directly synchronized. Remove or modify the related columns and SQL before synchronization. If business requires retaining vector search capability, separate evaluation of storage and retrieval solutions is needed. |
   |Proprietary system functions (such as `DECODE_ORACLE`, dynamic column functions) |MySQL does not support special functions such as `DECODE_ORACLE`, `COLUMN_CREATE()`, `COLUMN_GET()`, and `COLUMN_ADD()`; views, stored procedures, or business SQL that rely on them will report errors during execution. |Locate and evaluate the call chain on the source end before synchronization, and rewrite views, stored procedures, and business SQL using MySQL compatible syntax (such as `CASE WHEN`). |
   |JSON data type and syntax differences |MariaDB and MySQL differ in JSON underlying implementation, function, and operator support scope.<br><br>MariaDB’s JSON is usually implemented as `LONGTEXT` with verification constraints; different MariaDB versions vary in support for operators like `->` and `->>`.<br><br>Before synchronization, check JSON types, functions, and path expressions according to the source end version, and rewrite using syntax supported by the target MySQL. |It is recommended to select according to business requirements and complete the corresponding syntax adaptation at the source end:<br><br><br>1. Type selection: The target end can choose to use MySQL native JSON type or compatible TEXT type based on query and index needs.<br><br>2. Syntax rewriting: MariaDB's JSON extractors (such as `->`, `->>`) are incompatible with MySQL. Before migration, replace them at the source end with MySQL standard functions (e.g., replace `->` with `JSON_EXTRACT()`, `->>` with `JSON_UNQUOTE()`).<br><br>3. Data verification: If the target end selects the native JSON type, pre\-verify that existing data are valid JSON format to avoid migration or query errors. |
   |function expression in column default value |Different MySQL versions support function expressions in column default values (such as `default (UUID()`) differently, which may cause table creation to fail on the target side. |Remove column\-level function expression default values on the source end before synchronization. Instead, generate default values on the business application side or handle them in business layer triggers or stored procedures. |

2. Examples of modifying incompatible items: Use the following examples to complete the modifications on both the source and target ends. Objects that cannot be synchronized automatically by DTS must be manually created in the MySQL target end.

   ### Example 1: Transforming MariaDB independent SEQUENCE sequence into MySQL AUTO_INCREMENT auto\-increment column

   * **Description**

   MariaDB supports using independent `SEQUENCE` sequence objects with the `NEXT VALUE FOR` function to generate auto\-increment primary keys. MySQL does not support independent `SEQUENCE` sequence objects and requires the standard `AUTO_INCREMENT` attribute to implement column\-level auto\-increment.

   * **modification steps**

      1. Add the `AUTO_INCREMENT` attribute to the auto\-increment primary key column when creating a new table in MySQL.

      1. Remove the `CREATE SEQUENCE` statement for creating the `SEQUENCE` object in MariaDB, as well as the `DEFAULT NEXT VALUE FOR ...` default value declaration in the original primary key column. the default value declaration.

   * **Code transformation comparison**

      * before modification: using the `SEQUENCE` object in MariaDB:

      ```SQL
      CREATE SEQUENCE s1;
      
      CREATE TABLE t1 (
        id BIGINT NOT NULL DEFAULT NEXT VALUE FOR s1,
        name VARCHAR(50),
        PRIMARY KEY (id)
      );
      ```

      * after modification: using `AUTO_INCREMENT` in MySQL:

      ```SQL
      CREATE TABLE t1 (
        id BIGINT NOT NULL AUTO_INCREMENT,
        name VARCHAR(50),
        PRIMARY KEY (id)
      );
      ```

   ### Example 2: Convert the INET6 type to VARCHAR(64)

   * **Description**

   MariaDB natively supports the INET6 data type for storing IPv6 addresses, but MySQL 5.7 and earlier 8.0 versions do not support this type. It must be converted to the most compatible string type before synchronization.

   * **modification suggestions**

   Based on the business storage format, convert INET6 to VARCHAR(64) or use VARBINARY(16) together with `INET6_ATON()` and `INET6_NTOA()` for access. Using VARCHAR(64) can reserve space for different IPv6 text representations.

   * **Code transformation comparison**

      * Before transformation: MariaDB environment

      ```SQL
      -- MariaDB uses native INET6 type
      CREATE TABLE user_network_info (
          id INT PRIMARY KEY,
          user_ip INET6 NOT NULL COMMENT '用户IPv6地址'
      );
      ```

      * After transformation: MySQL environment

      ```SQL
      -- MySQL uses VARCHAR(64) compatibility
      CREATE TABLE user_network_info (
          id INT PRIMARY KEY,
          user_ip VARCHAR(64) NOT NULL COMMENT '用户IPv6地址'
      );
      ```

   ### example three: modifying the Aria engine to InnoDB

   * **Description**

   Aria is a unique storage engine in MariaDB, usually used for internal temporary tables or specific scenarios, which MySQL does not support at all. If the `ENGINE=Aria` is included in the table structure, executing the create table statement on the MySQL side will report an error.

   * **modification suggestions**

   InnoDB is MySQL's default and most recommended storage engine, supporting transactions, row\-level locking, and foreign keys. It is recommended to convert all non\-InnoDB engines (such as Aria, MyISAM) to InnoDB before synchronization.

   * **Code transformation comparison**

   You can perform the conversion in the MariaDB source database in advance or modify the engine definition when creating the table in the MySQL target database.

      1. Confirm the current table’s engine.

      ```SQL
      SHOW CREATE TABLE orders;
      ```

      The output result may contain `ENGINE=Aria ...`.

      2. Execute the engine conversion command.

      ```SQL
      ALTER TABLE orders ENGINE = InnoDB;
      ```

      3. Execute the command again to confirm the current table’s engine.

      ```SQL
      SHOW CREATE TABLE orders;
      ```

      The output result should be: `ENGINE=InnoDB ...`.

### Step 2: create data synchronization task and data verification task

The operation steps for synchronization tasks are consistent with MySQL synchronization over a public network. For details, refer to [synchronizing from public network MySQL to BytePlus Edition MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_RDS_for_MySQL?lang=en).

* When configuring the source database, select MySQL as the instance type and public network MySQL as the access method. Then enter MariaDB’s public network address, port, database account number, and password.

* To prevent business abnormalities after switching, it is recommended to create a bidirectional synchronization task.

### Step 3: data verification and business switch

After stopping business writes on the source end MariaDB, confirm no active write transactions exist in the source database and continuously monitor the DTS incremental synchronization delay. Only after the incremental delay drops to 0 (or stabilizes at an acceptable low level) and the full data verification results are consistent can the final business cutover be executed.

1. Wait for synchronization to complete: wait for schema initialization and full initialization to finish, then the task enters the incremental synchronization phase while monitoring incremental delay.

2. Source database silent check: after data verification results are consistent and incremental delay drops close to 0, log in to the source end MariaDB database and execute the following command to view current session status, ensuring no new sessions perform write operations.

```SQL
SHOW FULL PROCESSLIST;
```

3. Execute business cutover: confirm no writes on the source database and no synchronization delay, then switch the business connection address to the target MySQL instance (BytePlus cloud database MySQL version).

### Step 4: Pause the forward migration task and start the reverse migration task;

1. Pause the forward migration task.Task; For detailed operations, refer to Pausing a synchronization task.

When the forward synchronization task is paused, do not start the task arbitrarily, as this may cause data inconsistency.

2. Configure the reverse synchronization task and start it. For the configuration method, refer to [Configuring reverse synchronization](https://docs.byteplus.com/en/docs/DTS/Configuring_reverse_synchronization?lang=en).

3. Start writing cloud business.

4. Test business functions.

### Step 5: (optional) Service rollback

1. If an exception occurs in the cloud service after switching business, immediately stop writing cloud business.

2. Switch business to the source end.

   * Establish a reverse synchronization chain: wait for the reverse synchronization delay to drop to 0 and confirm that newly added cloud data has synchronized to the source end MariaDB, then switch the business connection address back to the source end.

   * If the reverse synchronization chain is not established: do not switch directly back to the source end. Evaluate and migrate newly added cloud data first to avoid data loss.

3. Resume writing business data.
