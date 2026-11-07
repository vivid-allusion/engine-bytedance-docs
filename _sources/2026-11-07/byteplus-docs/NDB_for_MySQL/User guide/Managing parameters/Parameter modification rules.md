---
title: "Parameter modification rules"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_modification_rules"
---

This article describes the modification rules for some special parameters.

<span id="参数的值必须设定为-block-size-的倍数"></span>
## The value of the parameter must be set to a multiple of block_size

When some system variables are set to values ​​that are not an integer multiple of the specified block size (block_size), they are rounded down to the next smaller multiple of the block size before being stored by the server, that is, [FLOOR(value)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_floor)  **\* block_size**. For example, suppose the block size of a given variable is 4096, and you set the value of that variable to 100000 (assuming the maximum value of the variable is greater than that number). Since 100000 / 4096 = 24.4140625, the server automatically reduces the value to 98304 (24 \* 4096) before storing it.

In some cases, the specified maximum value for a variable is the maximum value allowed by the MySQL parser, but is not an exact multiple of the block size. In this case, the effective maximum is the next smaller multiple of the block size. For example, the maximum value of a system variable is displayed as 4294967295, and its block size is 1024, 4294967295 / 1024 = 4194303.9990234375. Therefore, if this variable is set to its specified maximum value, the actual value stored is 4194303 \* 1024 = 4294966272.

For more details about `block_size`, see [MySQL server system variables](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html).


|block_size |Parameter name |Instance version |Parameter default value |Value range |Need to restart |
|---|---|---|---|---|---|
|**1024** |transaction_alloc_block_size |* MySQL 8.0<br><br>* MySQL 5.7 |8192 |[1024\-131072] |No |
||thread_stack |MySQL 8.0 |1048576 |[131072\-1073741824] |Yes |
|||MySQL 5.7 |262144 |||
||innodb_buffer_pool_size |* MySQL 8.0<br><br>* MySQL 5.7 | |[{DBNodeClassMemory\*1/16}\-{DBNodeClassMemory\*4/5}] |No |
||transaction_prealloc_size |* MySQL 8.0<br><br>* MySQL 5.7 |4096 |[1024\-131072] |No |
||max_allowed_packet |* MySQL 8.0<br><br>* MySQL 5.7 |67108864 |[1024\-1073741824] |No |
||query_alloc_block_size |MySQL 8.0 |8192 |[1024\-4294966272] |No |
|||MySQL 5.7 ||[1024\-4294967295] ||
||max_heap_table_size |MySQL 8.0 |16777216 |[16384\-18446744073709550592] |No |
|||MySQL 5.7 ||[16384\-18446744073709551615] ||
||net_buffer_length |* MySQL 8.0<br><br>* MySQL 5.7 |16384 |[1024\-1048576] |No |
||query_prealloc_size |MySQL 8.0 |8192 |[8192\-18446744073709550592] |No |
|||MySQL 5.7 ||[8192\-18446744073709551615] ||
||range_alloc_block_size |MySQL 8.0 |4096 |[4096\-4294966272] |No |
|||MySQL 5.7 ||[4096\-4294967295] ||
||query_cache_size |MySQL 8.0 |0 |[0\-18446744073709550592] |No |
|||MySQL 5.7 ||[0\-18446744073709551615] ||
|**128** |join_buffer_size |* MySQL 5.7<br><br>* MySQL 8.0 | |[128\-67108864] |No |
|**100** |key_cache_age_threshold |* MySQL 5.7<br><br>* MySQL 8.0 |300 |[100\-18446744073709551600] |No |
|**512** |key_cache_block_size |* MySQL 5.7<br><br>* MySQL 8.0 |1024 |[512\-16384] |No |
|**4096** |binlog_cache_size |MySQL 8.0 |1048576 |[4096\-18446744073709547520] |No |
|||MySQL 5.7 ||[4096\-18446744073709551615] ||
||binlog_stmt_cache_size |MySQL 8.0 |32768 |[4096\-18446744073709547520] |No |
|||MySQL 5.7 ||[4096\-18446744073709551615] ||
||max_binlog_stmt_cache_size |MySQL 8.0 |18446744073709547520 |[4096\-18446744073709547520] |No |
|||MySQL 5.7 ||[4096\-18446744073709551615] ||


<span id="关联参数配置规则"></span>
## Association parameter configuration rules

There are specific relationships between some parameters, as detailed below:


|Parameter |**Instance version** |Verification rules |**Need to restart** |
|---|---|---|---|
|**innodb_io_capacity**<br><br>**innodb_io_capacity_max** |* MySQL 5.7<br><br>* MySQL 8.0 |`innodb_io_capacity` cannot be greater than `innodb_io_capacity_max`. |No |
|**collation_server**<br><br>**character_set_server** |* MySQL 5.7<br><br>* MySQL 8.0 |`collation_server` must be a collation that matches `character_set_server`. The value of `collation_server` must be selected from the collation corresponding to `character_set_server`. For example, if the value of `character_set_server` is `utf8mb4`, the value of `collation_server` must be a collation that is applicable to the `utf8mb4` character set, such as `utf8mb4_general_ci`. |Yes |
