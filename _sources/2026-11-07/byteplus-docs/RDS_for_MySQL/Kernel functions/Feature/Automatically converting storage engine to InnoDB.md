---
title: "Automatically converting storage engine to InnoDB"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Automatically_converts_storage_engine_to_InnoDB"
---

This topic describes the feature in RDS for MySQL that automatically converts MyISAM, Memory, and Archive storage engines to the InnoDB storage engine.

<span id="C9411Tv8"></span>
## Background

RDS for MySQL supports the InnoDB storage engine by default but does not support the MyISAM, Memory, or Archive storage engines. To facilitate database migration or upgrades, you can automatically convert MyISAM, Memory, and Archive storage engines to the InnoDB storage engine.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20250415 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250415 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5L2_55So6K-05piO"></span>
## Instructions


* When a user creates a table and specifies the storage engine as MyISAM, Memory, or Archive, the storage engine is automatically converted to InnoDB.

   ```sql
   mysql> create table t(a int) engine = myisam;
   Query OK, 0 rows affected, 2 warnings (0.14 sec)
   
   mysql> show create table t\G
   *************************** 1. row ***************************
          Table: t
   Create Table: CREATE TABLE `t` (
     `a` int(11) DEFAULT NULL
   ) ENGINE=InnoDB DEFAULT CHARSET=latin1
   1 row in set (0.00 sec)
   ```
   

* If a user creates a table without specifying a storage engine but sets the default engine to MyISAM, Memory, or Archive (for example, `default_storage_engine = 'myisam'`), the storage engine is also automatically converted to InnoDB.

   ```sql
   mysql> set global default_storage_engine = 'myisam';
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> create table t(a int);
   Query OK, 0 rows affected (0.12 sec)
   
   mysql> show create table t\G
   *************************** 1. row ***************************
          Table: t
   Create Table: CREATE TABLE `t` (
     `a` int(11) DEFAULT NULL
   ) ENGINE=InnoDB DEFAULT CHARSET=latin1
   1 row in set (0.00 sec)
   ```
   

* To disable the automatic conversion feature, set the value of the `loose_convert_disabled_engines_to_innodb` parameter to `off`. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).


<span id=".6ZmQ5Yi25Zy65pmv"></span>
## Limitations

The MyISAM engine supports composite primary keys that include auto\-increment columns, while the InnoDB engine does not. Therefore, an error is reported when creating a table after it has been converted from MyISAM to InnoDB. The error message is as follows:

```sql
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
```


We recommend that you create an index for the auto\-increment column to use composite primary keys that include an auto\-increment column in the InnoDB engine. Example as follows:

```sql
mysql> create table t_multikey (
    ->   id int AUTO_INCREMENT,
    ->   name varchar(20),
    ->   address varchar(20),
    ->   primary key (name,id)
    -> ) ENGINE=MyISAM;
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
```


The modification is as follows. The table is created successfully with the InnoDB storage engine:

```sql
mysql> create table t_multikey (
    ->   id int AUTO_INCREMENT,
    ->   name varchar(20),
    ->   address varchar(20),
    ->   primary key (name,id),
    ->   key idx_id(id)
    -> ) ENGINE=MyISAM;
Query OK, 0 rows affected, 2 warnings (0.11 sec)

mysql> show warnings;
+---------+------+-------------------------------------------------------------------+
| Level   | Code | Message                                                           |
+---------+------+-------------------------------------------------------------------+
| Warning | 3161 | Storage engine MyISAM is disabled (Table creation is disallowed). |
| Warning | 1266 | Using storage engine InnoDB for table 't_multikey'                |
+---------+------+-------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show create table t_multikey\G
*************************** 1. row ***************************
       Table: t_multikey
Create Table: CREATE TABLE `t_multikey` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  `address` varchar(20) DEFAULT NULL,
  PRIMARY KEY (`name`,`id`),
  KEY `idx_id` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1
1 row in set (0.00 sec)
```
