---
title: "Handle invisible primary key errors"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Handle_invisible_primary_key_errors"
---

<span id="背景"></span>
## Background

In RDS for MySQL with Kernel minor versions of 20240615 and later, MySQL 8.0 has the invisible primary key (Generated Invisible Primary Keys, GIPK) feature Enabled by Default. After this feature is Enabled, if a Primary Key is not identified in a User's `create table` statement, an invisible primary key `my_row_id` will be added for the User. After an invisible primary key is added, if the User wants to Customize a new primary key by using DDL, they may encounter the following Error:


* You may encounter the following Error when defining a new primary key in an ALTER TABLE statement:

   
   |Error Message |description |
   |---|---|
   |`Error 1068: Multiple primary key defined.` |The custom primary key conflicts with the hidden primary key. |
   |`Error 1075: Incorrect table definition; there can be only one auto column and it must be defined as a key.` |The new auto\-increment column conflicts with the hidden primary key. |
   

* When defining a new primary key in a CREATE TABLE statement, you may encounter the following Error:

   
   |Error Message |description |
   |---|---|
   |`Error 4109: Failed to generate invisible primary key. Auto-increment column already exists.` |When GIPK is enabled, the auto\-increment column is not defined as a primary key index. |
   


<span id="查看-gipk"></span>
## View GIPK

Because GIPK has a "hidden column" attribute, the User cannot directly View GIPK by using `show create table`. They need to View GIPK by using the following method.


1. Enable the `show_gipk_in_create_table_and_information_schema` Parameter, and then you can see the invisible primary key `my_row_id` in `show create table`.

   ```sql
   mysql> set show_gipk_in_create_table_and_information_schema=on;
   
   mysql> show variables like '%gipk%';
   +--------------------------------------------------+-------+
   | Variable_name                                    | Value |
   +--------------------------------------------------+-------+
   | show_gipk_in_create_table_and_information_schema | ON    |
   +--------------------------------------------------+-------+
   1 row in set (0.01 sec)
   
   mysql> show create table t00;
   +-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Table | Create Table                                                                                                                                                                                                                  |
   +-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | t00   | CREATE TABLE `t00` (
     `my_row_id` bigint unsigned NOT NULL AUTO_INCREMENT /*!80023 INVISIBLE */,
     `id` int DEFAULT NULL,
     `c` varchar(16) DEFAULT NULL,
     PRIMARY KEY (`my_row_id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
   +-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   1 row in set (0.01 sec)
   ```
   

2. You do not need to close GIPK when replacing the primary key; keep it enabled.

   ```sql
   mysql> select @@sql_generate_invisible_primary_key;
   +--------------------------------------+
   | @@sql_generate_invisible_primary_key |
   +--------------------------------------+
   |                                    1 |
   +--------------------------------------+
   1 row in set (0.00 sec)
   ```
   


<span id="将-gipk-替换为自定义主键"></span>
## Replace GIPK with a custom primary key

<span id="_1-将已有列升级为主键"></span>
### 1. Promote an existing column to a primary key

**Operation description:**  Set an existing field in the table as the primary key.

**Error** **SQL** **Example:** 

```sql
alter table table_name add primary key(id);
```


**Error details**: `Error 1068: Multiple primary key defined`

**Example of the table structure before the modification:**  The table contains a hidden primary key column `my_row_id`

```sql
mysql> show create table t00;
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                                  |
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| t00   | CREATE TABLE `t00` (
  `my_row_id` bigint unsigned NOT NULL AUTO_INCREMENT /*!80023 INVISIBLE */,
  `id` int DEFAULT NULL,
  `c` varchar(16) DEFAULT NULL,
  PRIMARY KEY (`my_row_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.01 sec)
```


**Modification SQL**:


* MySQL 8.0


```sql
alter table t00 drop column my_row_id, add primary key(id);
```



* MySQL 5.7 (instances with kernel minor version 20240615 and later)


```sql
alter table t00 drop column byte_rds_ai_uk_row_id, add primary key(id);
```


**Table structure after modification:**  the hidden primary key `my_row_id` is removed, and `id` is the new primary key.

```sql
mysql> show create table t00;
+-------+--------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                         |
+-------+--------------------------------------------------------------------------------------------------------------------------------------+
| t00   | CREATE TABLE `t00` (
  `id` int NOT NULL,
  `c` varchar(16) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+--------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```


<span id="_2-新加一个主键列"></span>
### 2. Add a new primary key column.

**Operation description**: add a column as the primary key.

**Related SQL error**:

```sql
alter table table_name 
            add column new_id bigint primary key;
```


**Related error**: `Error 1068: Multiple primary key defined`

**Example of table structure before modification**: contains the hidden primary key column `my_row_id`

```sql
mysql> show create table t01;
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                                  |
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| t01   | CREATE TABLE `t01` (
  `my_row_id` bigint unsigned NOT NULL AUTO_INCREMENT /*!80023 INVISIBLE */,
  `i` int DEFAULT NULL,
  `c` varchar(16) DEFAULT NULL,
  PRIMARY KEY (`my_row_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```


**Modification SQL**:

Add a column with no additional requirements to replace the GIPK, for example, a `new_id` column with the `BIGINT` attribute.


* MySQL 8.0


```sql
alter table table_name 
            drop column my_row_id, 
            add column new_id bigint primary key;
```



* MySQL 5.7 (instances with kernel minor version 20240615 and later)


```sql
alter table table_name 
            drop column byte_rds_ai_uk_row_id, 
            add column new_id bigint primary key;
```


**Table structure after modification**: the hidden primary key `my_row_id` is removed, and `new_id` is the new primary key.

```sql
mysql> show create table t01;
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                      |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| t01   | CREATE TABLE `t01` (
  `i` int DEFAULT NULL,
  `c` varchar(16) DEFAULT NULL,
  `new_id` bigint unsigned NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`new_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```



3. ### Add an auto\-increment column <span id="新增自增列"></span>


**Operation description**: the user adds an auto\-increment column

**SQL error example**:

```sql
alter table table_name 
            add column new_id bigint unsigned not null auto_increment key;
```


**Error details**: `Error 1075: Incorrect table definition; there can be only one auto column and it must be defined as a key`

**Pre\-modification table structure example**: contains a hidden primary key column `my_row_id`

```sql
mysql> show create table t01;
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                                  |
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| t01   | CREATE TABLE `t01` (
  `my_row_id` bigint unsigned NOT NULL AUTO_INCREMENT /*!80023 INVISIBLE */,
  `i` int DEFAULT NULL,
  `c` varchar(16) DEFAULT NULL,
  PRIMARY KEY (`my_row_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```


**Modification SQL**:

Add the auto\-increment column `new_id` and replace the GIPK.


* MySQL 8.0


```sql
alter table table_name 
            drop column my_row_id, 
            add column new_id bigint unsigned not null auto_increment key;
```



* MySQL 5.7 (Instances with kernel minor version 20240615 and newer)


```sql
alter table table_name 
            drop column byte_rds_ai_uk_row_id, 
            add column new_id bigint unsigned not null auto_increment key;
```


&nbsp;

**Table structure after modification:**  The hidden primary key `my_row_id` is removed, and `new_id` is the new primary key.

```sql
mysql> show create table t01;
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                      |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| t01   | CREATE TABLE `t01` (
  `i` int DEFAULT NULL,
  `c` varchar(16) DEFAULT NULL,
  `new_id` bigint unsigned NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`new_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```



4. ### Create a table with an auto\-increment column <span id="创建含有自增列的表"></span>


**Operation description:**  create a table with an auto\-increment column

**Error SQL example:** 

```sql
create table table_name (
             id bigint unsigned NOT NULL AUTO_INCREMENT [UNIQUE KEY],
             c varchar(16));
```


**Error details:**  `Error 4109: Failed to generate invisible primary key.` `Auto-increment column already exists.`

**Modification SQL:** 

Use the `PRIMARY KEY` or `KEY` keyword.

```sql
create table table_name  (
             id bigint unsigned NOT NULL AUTO_INCREMENT [PRIMARY] KEY,
             c varchar(16));
```


**Table structure after modification**: `new_id` is the new primary key

```sql
mysql> show create table t01;
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                      |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| t01   | CREATE TABLE `t01` (
  `new_id` bigint unsigned NOT NULL AUTO_INCREMENT,
  `c` varchar(16) DEFAULT NULL,
  PRIMARY KEY (`new_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```


<span id="_5-打开-gipk-创建分区表"></span>
### 5. Enable GIPK to create a partitioned table

**Operation description**: create a partitioned table with no primary key

**SQL error example**:

```sql
CREATE TABLE t1 (f1 INT, f2 DATE) PARTITION BY KEY(f2) PARTITIONS 2;
```


**Error details**: `Error 1235: This version of MySQL doesn't yet support 'generating invisible primary key for the partitioned tables`

**Modification operation**: submit a ticket to close GIPK.
