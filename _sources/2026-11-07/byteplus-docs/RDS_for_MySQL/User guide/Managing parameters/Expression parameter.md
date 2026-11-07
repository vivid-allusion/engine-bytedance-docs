---
title: "Expression parameter"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically"
---

This topic describes the parameters that support configuration using expressions and the rules for configuring them.

## Function description

The values of some modifiable parameters in a MySQL instance are closely related to the instance's specifications. After you modify the instance configuration, you need to reset the running values for these parameters based on the new specifications to achieve an optimal running status. To improve the user experience and increase the efficiency of MySQL instances, RDS for MySQL provides the ability to configure these parameters as expressions.

Configuring parameters as expressions enables you to set their running values as expressions related to instance specifications. After a parameter is configured as an expression, RDS for MySQL automatically calculates a result based on the expression and the instance specifications, and sets the calculated result as the parameter's running value. The parameters that support expression\-based configuration and their default expressions are shown in the table below.

|Parameter name |Expression example |Expression description |
|---|---|---|
|`innodb_buffer_pool_instances` |`{LEAST(DBInstanceMemory/1073741824, 8)}` |The running value of the parameter is the minimum of `instance memory/1073741824` and `8`. |
|`innodb_buffer_pool_size` |`{DBInstanceMemory*3/4}` |The running value of the parameter is `3/4 of the instance memory`. |
|`innodb_lru_scan_depth` |`{BY_STORAGE_TYPE(1024, 100)}` |The value is based on the storage type of the instance.<br><br><br>* When the storage type of the instance is local disk, the running value of this parameter is `1024`.<br><br>* When the storage type of the instance is cloud disk, the running value of this parameter is `100`. |
|`innodb_page_cleaners` |`{LEAST(DBInstanceMemory/1073741824, 8)}` |The running value of the parameter is the minimum of `instance memory/1073741824` and `8`. |
|`read_buffer_size` |`{LEAST(DBInstanceMemory/1048576*128, 262144)}` |The running Value of the Parameter is the minimum of `instance Memory/1048576*128` and `262144`. |
|`table_definition_cache` |`{LEAST(DBInstanceMemory/1073741824*512, 2048)}` |Takes the minimum value of `instance Memory/1073741824*512` and `2048` as the running parameter value. |
|`thread_cache_size` |`{LEAST(DBInstanceMemory/1073741824*512, 2048)}` |Takes the minimum value of `instance Memory/1073741824*512` and `2048` as the running parameter value. |
|`loose_innodb_default_index_merge_threshold` |`{BY_STORAGE_TYPE(50, 25)}`<br><br> |The value is based on the storage type of the instance.<br><br><br>* When the storage type of the instance is local disk, the running value of the parameter is `50`.<br><br>* When the storage type of the instance is cloud disk, the running value of the parameter is `25`. |
|`loose_thread_pool_size` |`{MAX(DBInstanceCpu, 2)}` |Takes the maximum value of `instance CPU Cores` and `2` as the running parameter value. |
|`max_connections` |`{MAP(DBInstanceCpu, DBInstanceMemory)}` |Takes the `Max connections` value from the [Product specifications list](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications#.6KeE5qC85YiX6KGo) that corresponds to the specifications of `instance CPU Cores` and `instance Memory` as the running parameter value. |
|`table_open_cache` |`{LEAST(DBInstanceMemory/1073741824*256, 2048)}` |The parameter value is the minimum value between `Instance Memory/1073741824*256` and `2048`. |
|`table_open_cache_instances` |`{LEAST(DBInstanceMemory/1073741824, 16)}` |The running Value of the Parameter is the minimum of `instance Memory/1073741824` and `16`. |
|`join_buffer_size` |`{LEAST(DBInstanceMemory/1048576*128, 262144)}` |The running Value of the Parameter is the minimum of `instance Memory/1048576*128` and `262144`. |

## Use cases

You can configure the running value of a parameter as an expression when you modify instance parameters, modify instance parameters in batches, or create a parameter template.

## Limitation

* Parameters that support expression configuration also support setting the running value to a specific value. However, when you set a specific value, different parameters have different rules for setting their running values after the instance configuration is modified. After the instance configuration is modified, some parameters continue to calculate and set a new running value according to the expression, while others continue to use the specific value set before the modification.

   * The parameters that have their running values recalculated are:

      * `innodb_buffer_pool_instances`

      * `innodb_buffer_pool_size`

      * `read_buffer_size`

      * `table_definition_cache`

      * `thread_cache_size`

      * `loose_thread_pool_size`

      * `join_buffer_size`

   * The following parameters retain their values from before the instance configuration was modified:

      * `innodb_page_cleaners`

      * `max_connections`

      * `table_open_cache`

      * `table_open_cache_instances`

* The values of the following parameters must meet the corresponding rules during configuration. If the rules are not met, the value is rounded down according to the expression rules while remaining within the parameter's value range.

   * The value of `innodb_buffer_pool_size` must be a multiple of 1024, and be greater than or equal to 50% and less than or equal to 85% of the instance memory.

   * The value of read_buffer_size must be a multiple of 4096.

   * The value of join_buffer_size must be a multiple of 128.

* When configuring an expression for an instance parameter, an expression for its running value must already be configured in the parameter template applied to the instance. System templates provided by RDS for MySQL already include expressions for the running values of parameters that support expression configuration. If you apply a System template to your instance, the running values of these parameters are automatically calculated based on the expressions.

## Expression syntax

Parameter expressions support the following variables and functions:

* Variable

   * `DBInstanceMemory`: The memory of the instance's primary node.

   * `DBInstanceCpu`: The number of CPU cores of the instance's primary node.

   > **tip**

   * > DBInstanceMemory and DBInstanceCpu are the memory and cores of the primary node of the instance. Even if the parameter only applies to read\-only nodes, its value is determined by the specifications of the primary node, and the running value is then calculated based on the expression.

   * > However, the **innodb_buffer_pool_size** parameter does not follow the preceding principles. Its calculation formula is:

      * > When the effective scope of this parameter applies only to primary and standby nodes (OnlyMasterSlaveNode), calculation is performed based on the **primary node specification**.

      * > When the effective scope of this parameter is AllNode, OnlyReadOnlyNode or CustomNode, calculation, verification and correction are performed independently for each target read\-only node based on the specification of that node.

* Functions

   |Functions |Function description |Examples |
   |---|---|---|
   |`LEAST(x, y)` |The smaller Value between x and y. |`{LEAST(DBInstanceMemory/1073741824*512, 2048)}` |
   |`MAX(x, y)` |Takes the larger value between x and y. |`{MAX(DBInstanceCpu, 2)}` |
   |`MAP(x, y)` |The value for max connections is determined by the mapping of x and y in the [Product specifications list](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications#.6KeE5qC85YiX6KGo). |`{MAP(DBInstanceCpu, DBInstanceMemory)}` |
