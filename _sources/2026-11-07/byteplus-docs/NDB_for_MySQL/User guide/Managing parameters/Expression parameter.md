---
title: "Expression parameter"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Expression_parameter"
---

Parameters of an instance allow its run value to be configured as an expression that is relevant to the instance specification. This article describes parameters that support configuration using expressions, as well as configuration rules for expressions.

## Applicable scenarios

When you modify an instance parameter and create a parameter template, you can configure the parameter run value as an expression. After being configured as an expression, the result is automatically evaluated according to the instance specification according to the expression, and the result is set to the actual running value of the parameter.

## Function description

Among the modifiable parameters of the instance, the values of some parameters are closely related to the specifications of the instance. After changing the instance configuration, in order to make the instance reach the optimal operating state, you need to re\-set the operating values ​​of these parameters according to the new specifications of the instance. In order to enhance the user experience and improve the work efficiency of the instance, these parameters are given the function of being configured as expressions.

The parameters that support expression configuration and the default expressions are shown in the following table:

|Parameter name |Default value |Value range |Need restart? |
|---|---|---|---|
|innodb_buffer_pool_size |`{DBNodeClassMemory*3/4}` |`[{DBNodeClassMemory*1/16}-{DBNodeClassMemory*4/5}]` |No |
|innodb_purge_threads |`{MIN(MAX(DBNodeClassCPU,4),32)}` |[1\-32] |Yes |
|table_open_cache_instances |`{MAX(DBNodeClassCPU,32)}` |[1\-64] |Yes |
|thread_pool_size |`{DBNodeClassCPU*4}` |`[{DBNodeClassCPU*1}-{DBNodeClassCPU*10}]` |No |
|table_open_cache |`{MAX(DBNodeClassMemory/1073741824*256,2048)}` |[1\-524288] |No |
|join_buffer_size |`{MIN(DBNodeClassMemory/1048576*128,262144)}` |[128\-67108864] |No |
|innodb_open_files<br><br> |`{MIN(MAX(DBNodeClassMemory/1048576,8192),1048576) }` |[10,2147483647]<br><br> |Yes |
|innodb_lru_scan_depth |`{MIN(DBInstanceClassMemory/1048576/8, 8192)}` |[100\-1099511627776]<br><br> |No |
|innodb_purge_batch_size |`MIN(MAX({DBNodeClassCPU * 100}, 300), 5000)` |[1\-5000] |No |
|performance_schema_max_metadata_locks |`{Min(DBNodeClassConnections*20,1048576)}` |[\-1\-1048576] |Yes |
|performance_schema_max_thread_instances |`{Min(DBNodeClassConnections,1048576)}` |[\-1\-1048576] |Yes |

## Limitations

* The parameter whose value range is an expression can be set to either an expression or a specific value when modifying it. For the value range, please refer to the [Function description](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Expression_parameter#.5Yqf6IO96K-05piO).

* After changing the instance configuration, the settings before the change are directly used.

* The values ​​of the following parameters should meet the corresponding rules when configuring. If the rules are not met, it will be rounded down according to the rules of the expression under the premise of satisfying the parameter value range. For details, see [Parameter modification rules](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_modification_rules).

   * The value of `join_buffer_size` should be an integer multiple of 128.

   * The value of `innodb_buffer_pool_size` should be an integer multiple of 1024 and 50% to 75% of the node memory size.

## Expression syntax

The variables and functions supported by parameter expressions are as follows:

* Variable

   * `DBNodeClassMemory`: Memory size of computing node specifications, integer type. The default unit is Byte.

   * `DBNodeClassCPU`: The number of CPU cores of the computing node specification, integer type.

* Operator

   * Expression syntax: Use`{}`package.

   * Division operator (`/`): Divides the dividend by the divisor and returns an integer quotient. If the quotient is a decimal, do not round it off and only take the integer part. Syntax: `dividend/divisor`.

   * Multiplication operator (`*`): Multiplies two multipliers and returns the integer product. If the product is a decimal, do not round it off and only take the integer part. Syntax: `expression*expression`.

   > **tip**

   > The dividend, divisor, and multiplier do not support decimal operations. For example `{DBNodeClassMemory*3/4}` is supported, but not `{DBNodeClassMemory*0.75/4}`.

* Function

   |Function |Function description |Examples |
   |---|---|---|
   |MIN(x, y) |Take the smaller value between x and y. |`{MIN(DBNodeClassMemory/1073741824*512,2048)}` |
   |MAX(x, y) |Take the maximum value between x and y. |`{MAX(DBNodeClassCPU,2)}` |
