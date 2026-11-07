---
title: "Modify parameters"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters"
---

This topic describes the procedure for modifying parameters.

## Precautions

* To ensure instance stability, you can modify only some parameters in the console. For a list of modifiable parameters, refer to [MySQL 5.7](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7) and [MySQL 8.0](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0). If you cannot find the parameter you want to modify, [submit a ticket](https://console.byteplus.com/workorder/create).

* To set parameter values, refer to the **Value range** column in the **MySQL parameters** tab on the console.

* Some parameters take effect only after the instance is restarted. To check whether a restart is required, refer to the **Need restart?**  column in the **MySQL parameters** tab. Restarting the instance usually takes 30 to 60 seconds. During this process, one or two transient connections may occur. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to greatly reduce the impact of database connection interruptions on your business.

* The underlying logic of MySQL will automatically adjust some parameters to preset limit values or integer multiples of preset values.he adjustment rules are as follows:

   * If the configured parameter value exceeds the **valid value range of the parameter**, the system will not perform automatic adjustment, and the modification operation will fail directly.

   * If the configured parameter **value falls within the valid value range of the parameter**, but does not meet the required multiple relationship of the parameter (e.g., `block_size`), the system **rounds the value down** to the nearest compliant value during the asynchronous execution phase. Therefore, the final effective value may differ from the configured value.

   * But for the **`innodb_buffer_pool_size`** parameter, the system verifies each target node in the parameter modification application scope (`ParamApplyScope`) one by one, checks whether its value falls within the range of **50%～85%**  of the target node memory, and performs alignment rounding based on **`innodb_buffer_pool_chunk_size * innodb_buffer_pool_instances`**.

* For more detailed information about parameter modification rules, refer to [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).

## Prerequisites

* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* If you want to configure a dynamic expression for the parameter when modifying the parameter, you need to confirm that the parameter supports dynamic configuration, and confirm that the dynamic expression has been configured for the parameter in the parameter template applied to the instance.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

> **tip**

> If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click the **Parameters** tab at the top of the page.

6. On the **MySQL parameters** tab, click **Modify parameters**. Based on the value range of the target parameter, enter a new value or expression in the **Running value** column.

   > **tip**

   > Click **Undo** previous step to cancel the current parameter modification. You can click **Undo** previous step multiple times to undo the previous modifications.

7. After the modification is completed, click **Submit** in the upper\-left corner of the page, and click **OK** in the pop\-up **Confirm parameter change** dialog box.

   > **tip**

   * > You can change multiple parameters at the same time and submit the modifications together.

   * > For double\-node instances, in the **Confirm parameter change** dialog box, you can set the scope of parameter modification to all nodes, only primary and secondary nodes, only read\-only nodes, or specific read\-only node.

   * > If an instance has multiple read\-only nodes and you want the parameter modification to apply only to some of them, set the **Modify scope** to **Specific read\-only node** and select the target read\-only nodes from the **Read\-only node** list.

## Related API

|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceparameters) |Call the DescribeDBInstanceParameters API to query instance parameters. |
|[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceparameters) |Call the ModifyDBInstanceParameters API to modify instance parameters. |

## FAQ

### Why can't I find the parameter I need to modify in parameter management?

For security and stability reasons, only some parameters can be modified. For a list of modifiable parameters, refer to [List of modifiable parameters in MySQL 5.7](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7) and [List of modifiable parameters in MySQL 8.0](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0). If you cannot find the parameter you need to modify, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

### Does the instance need to be restarted after modification of parameters?

Some parameters require restarting the instance after modification. You can check the **Need restart?**  column under **Parameter configuration** \> **MySQL parameters** to see if you need to [restart the instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance). For details, refer to [Modifing parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/service_availability).

> **tip**

> Operate during business off\-peak hours and ensure the application has a reconnection mechanism.

### Is it possible to modify the system parameter template?

The system parameter template cannot be modified. You can modify the c[ustom template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template) instead.

### How do I check the values of parameters that cannot be modified in RDS for MySQL?

Log on to [Database Workshop](https://console.byteplus.com/dbw) and use the SQL statement `SHOW variables like 'Parameter name'` to check.
