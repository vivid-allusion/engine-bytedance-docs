---
title: "Invisible Index"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/invisible_index"
---

This topic describes the invisible index feature that RDS for MySQL provides for MySQL 5.7 instances.

<span id="3f1MMiwM"></span>
## Background

After an index is made invisible, if an application or user is actually using it, they will receive errors or experience performance problems. This method allows you to assess the impact of deleting an index before it is deleted, so you can confirm whether it can be safely deleted. RDS for MySQL ports this feature from MySQL 8.0 to MySQL 5.7, making the feature available in MySQL 5.7 as well.

<span id="pUTjYVmw"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20250615 and above.

* MySQL 8.0 version, all kernel minor versions are supported.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<span id="Lljea7Iu"></span>
## Use cases

This feature allows you to set an index to invisible before deleting it, to determine if the index is still in use by checking for errors or performance problems. It is suitable for business scenarios that require high security.

<span id="j0h1Pu8j"></span>
## Precautions


* Using force index on an invisible index causes an error:

   ```SQL
   CREATE TABLE `test2` (
     `i` int DEFAULT NULL,
     `j` int DEFAULT NULL,
     `k` int DEFAULT NULL,
     KEY `idx_i` (`i`),
     KEY `idx_j` (`j`) INVISIBLE,
     KEY `idx_k` (`k`) INVISIBLE 
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   
    
   mysql> EXPLAIN SELECT  i, j FROM test2  FORCE INDEX (idx_j)  WHERE j >= 2\G;
   ERROR 1176 (42000): Key 'idx_j' doesn't exist in table 'test2'
   ```
   

* Invisible index is a new syntax that RDS for MySQL adds for MySQL 5.7. After using this syntax, note the downstream binlog consumption.


<span id="JWzq46wS"></span>
## Instructions


* Use the following statements to create an invisible index or change an index to an invisible index:

   ```SQL
   CREATE TABLE test2 (
     i INT,
     j INT,
     k INT,
     INDEX idx_i (i) INVISIBLE
   ) ENGINE = InnoDB;
   CREATE INDEX idx_j ON test2 (j) INVISIBLE;
   ALTER TABLE test2 ADD INDEX idx_k (k) INVISIBLE;
   ```
   

* Use the following statement to change it to a visible index:

   ```SQL
   ALTER TABLE test2 ALTER INDEX idx_i INVISIBLE;
   ALTER TABLE test2 ALTER INDEX idx_i VISIBLE;
   ```
