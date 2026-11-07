---
title: "Apply parameter template"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/applying_a_parameter_template"
---

This topic describes the procedure for applying parameter templates.

## Background

Use the parameter template feature when you need to manage instance parameters in batches or apply batch parameter modifications to multiple instances.

RDS for MySQL provides two types of templates: system templates and customized templates.

* System template

   System templates are targeted parameter settings provided by RDS for MySQL for different business scenarios to ensure reliability, such as high\-performance parameter templates for superior performance. The following system templates are provided by RDS for MySQL:

   |Template type |Template description |Data synchronization method |Value of sync_binlog |Value of innodb_flush_log_at_trx_commit |
   |---|---|---|---|---|
   |Default parameter template |Highest data security, but slower read/write speed. |Semisynchronous |1 |1 |
   |High\-performance parameter template |Data security is moderate, but the read/write speed is the fastest. |Asynchronous |1000 |2 |
   |Asynchronous parameter template |Higher data security and faster speed. |Asynchronous |1 |1 |

   > **tip**

   * > When you create an instance, the system automatically selects the default parameter template that matches the instance version you chose.

   * > When you apply a system parameter template to an instance and select the scope of modification as **All nodes**, if the data synchronization method of the instance is different from the preset method of the system template, the data synchronization method will be adjusted automatically after applying the parameter template.

* Customized template

   You can create your own custom templates and fully customize the parameters according to your own business needs provided the values comply with parameter setting requirements. For more information about creating a custom parameter template, refer to [Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template).

## Precautions

* If the parameter template you choose contains parameters need to restart the instance to take affect, the instance will restart after applying the parameter template. If the parameter template that needs to be applied contains parameters that need to be restarted, the instance will be restarted after applying the parameter template. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database disconnection on the business. During the restart process of a read\-only node, the corresponding nodes will be unavailable, and the load of the current read\-only node will be transferred to other nodes that meet the conditions. Proceed after accurately evaluating the impact of the restart.

* If the value of a parameter in the template is a formula, it will be calculated separately according to the specifications of each node.

   * For the **`innodb_buffer_pool_size`** ** ** parameter, before template application, the system still verifies the calculated value of each target node one by one to check whether it falls within the **50%～85%**  range of the target node memory. If verification fails, the template application request for this instance **fails directly**.

   * The valid value that passes verification will be aligned and rounded according to **block_size** and `innodb_buffer_pool_chunk_size * innodb_buffer_pool_instances` after entering the **`asynchronous execution`** phase.

* When you apply a system parameter template to an instance and select the scope of modification as **All nodes**, if the data synchronization method of the instance is different from the preset method of the system template, the data synchronization method will be adjusted automatically after applying the parameter template.

* The underlying logic of MySQL will automatically adjust some parameters to preset limit values or integer multiples of preset values.he adjustment rules are as follows:

   * If the configured parameter value **exceeds the valid value range of the parameter**, the system will not perform automatic adjustment, and the modification operation will fail directly.

   * If the configured parameter value **falls within the valid value range of the parameter**, but does not meet the required multiple relationship of the parameter (e.g., `block_size`), the system **rounds the value down ** to the nearest compliant value during the asynchronous execution phase. Therefore, the final effective value may differ from the configured value.

   * But for the **`innodb_buffer_pool_size`** parameter, the system verifies each target node in the parameter modification application scope (`ParamApplyScope`) one by one, checks whether its value falls within the range of **50%～85%**  of the target node memory, and performs alignment rounding based on **`innodb_buffer_pool_chunk_size * innodb_buffer_pool_instances`**.

   * For details about the automatic parameter adjustment logic, refer to [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).

* Database instances of different kernel versions support different parameters. When modifying parameters of batch instances, the system will automatically ignore parameters that are not supported by the current kernel version of the instance. For detailed information on the modifiable parameters supported by different kernel versions, refer to the following documents:

   * If the database version is MySQL 5.7, refer to [List of modifiable parameters in MySQL 5.7](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7).

   * If the database version is MySQL 8.0, refer to [List of modifiable parameters in MySQL 8.0](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0).

   * If the database version is MySQL 8.4, refer to [List of modifiable parameters in MySQL 8.4](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_4).

   * For more information about parameter modification rules, refer to [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its parameter template feature to support project authentication. After the project\-based authentication capability is launched, historical customized parameter templates are automatically assigned to the "Global resources" project. For customized parameter templates under the "Global resources" project, you need to select the "All resources" project in the top navigation bar to view them.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

> **tip**

> If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Parametes**.

6. On the **MySQL parameter** tab, click **Apply parameter template**.

7. In the displayed dialog box, complete the following settings, and then click **OK**.

|**Configuration item** |**Description** |
|---|---|
|**Modify scope** |Select the node scope for applying the parameter template, such as **All nodes**, **Only primary and secondary nodes**, **Only read\-only nodes**, or **Specific read\-only node**. When an instance has multiple read\-only nodes and only needs to apply the parameter template to some read\-only nodes, you can select **Modify scope** as **Specified read\-only nodes** and check the target read\-only nodes in the **Read\-only node list**.<br><br>> **tip**<br><br><br><br>* > If the instance has no read\-only nodes, the modification scope is defaulted to all nodes.<br><br><br>* > Some parameters must be applied to all nodes and cannot be applied to some nodes. For more details, refer to [Parameter modification rules](https://docs.byteplus.com/en/docs/6313/).<br> |
|**Select template** |Select the parameter template to be applied from the drop\-down list. |
|**Data synchronization method** |Confirm the data synchronization method of the instance.<br><br>> **tip**<br><br><br>> When selecting a system template and the modification scope is **All nodes**, the data synchronization method will be adjusted according to the selected parameter template. The data synchronization method depends on the configuration of the parameter template.<br> |
|**Parameter changes** |After you select the modify scope and parameter template, the system provides information about the parameter changes that result from applying the template. This information includes the parameter name, the parameter value before modification, the parameter value after modification, whether the instance needs to be restarted, whether it involves a formula, and the involved formula.<br><br>> **tip**<br><br><br>> If there are parameter values configured as formulas in the parameter template, the parameter values will be calculated separately according to the specifications of each node, and the changes will be listed by node in the parameter change list.<br> |

> **tip**

> You can view the parameter templates recently used by the instance on the MySQL parameter tab. Click the template name to go to the parameter template page to view the detailed information of each parameter.
