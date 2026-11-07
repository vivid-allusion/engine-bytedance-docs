---
title: "Test models"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/test_models"
---

This topic describes the models used to stress test RDS for MySQL.

<span id="test-models"></span>
## Test Models

<span id="table-schema"></span>
### **Table Schema**

```Plain Text
CREATE TABLE `sbtest` (
`id` INTEGER UNSIGNED NOT NULL AUTO_INCREMENT,
`k` INTEGER UNSIGNED DEFAULT '0' NOT NULL,
`c` CHAR(120) DEFAULT '' NOT NULL,
`pad` CHAR(60) DEFAULT '' NOT NULL,
PRIMARY KEY (`id`)
) ENGINE=InnoDB

```


<span id="read-write-ratio"></span>
### **Read\-Write Ratio**

Each transaction submitted by Sysbench contains 18 SQL statements by default. The specific statements and their quantity are as follows:


* 10 primary key SELECT statements:


```Plain Text
SELECT c FROM ${rand_table_name} where id=${rand_id};

```



* 4 scope SELECT statements:


```Plain Text
SELECT c FROM ${rand_table_name} WHERE id BETWEEN ${rand_id_start} AND ${rand_id_end};
SELECT SUM(K) FROM ${rand_table_name} WHERE id BETWEEN ${rand_id_start} AND ${rand_id_end};
SELECT c FROM ${rand_table_name} WHERE id BETWEEN ${rand_id_start} AND ${rand_id_end} ORDER BY c;
SELECT DISTINCT c FROM ${rand_table_name} WHERE id BETWEEN ${rand_id_start} AND ${rand_id_end} ORDER BY c;
```



* 2 UPDATE statements:


```Plain Text
UPDATE ${rand_table_name} SET k=k+1 WHERE id=${rand_id}
UPDATE ${rand_table_name} SET c=${rand_str} WHERE id=${rand_id}
```



* 1 DELETE statement:


```Plain Text
DELETE FROM ${rand_table_name} WHERE id=${rand_id}
```



* 1 INSERT statement:


```Plain Text
INSERT INTO ${rand_table_name} (id, k, c, pad) VALUES (${rand_id},${rand_k},${rand_str_c},${rand_str_pad})
```
