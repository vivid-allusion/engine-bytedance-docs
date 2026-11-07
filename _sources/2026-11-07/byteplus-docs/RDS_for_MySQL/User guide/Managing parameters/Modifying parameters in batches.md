---
title: "Modifying parameters in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters_in_batches"
---

RDS for MySQL supports the batch parameter modification feature, allowing you to modify parameters for instances with consistent business requirements simultaneously. This topic describes the steps to modify parameters in batches.

## Prerequisites

* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* During batch parameter setting, ensure that the parameter modification requirements of all instances are consistent.

* If you want to configure a dynamic expression for the parameter when modifying the parameter, you need to confirm that the parameter supports dynamic configuration, and confirm that the dynamic expression has been configured for the parameter in the parameter template applied to the instance.

## Precautions

* To ensure instance stability, the console only allows modification of certain parameters. If the parameter you want to modify is unavailable, [submit a ticket](https://console.byteplus.com/workorder/create) for processing.

* For setting parameter values, please refer to the **Running value column** on the **MySQL parameter** tab on the console.

* Modifying some parameters requires an instance restart. For details, refer to the list of modifiable parameters: [MySQL 5.7](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7), [MySQL 8.0](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0), and [MySQL 8.4](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_4). Restarting the instance usually takes 30 to 60 seconds. During this process, one or two transient connections may occur. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to greatly reduce the impact of database connection interruptions on your business.

* The underlying logic of MySQL will automatically adjust some parameters to preset limit values or integer multiples of preset values.he adjustment rules are as follows:

   * If the configured parameter value **exceeds the valid value range of the parameter**, the system will not perform automatic adjustment, and the modification operation will fail directly.

   * If the configured parameter value **falls within the valid value range of the parameter**, but does not meet the required multiple relationship of the parameter (e.g., `block_size`), the system **rounds the value down** to the nearest compliant value during the asynchronous execution phase. Therefore, the final effective value may differ from the configured value.

   * But for the **`innodb_buffer_pool_size`** parameter, the system verifies each target node in the parameter modification application scope (`ParamApplyScope`) one by one, checks whether its value falls within the range of **50%～85%**  of the target node memory, and performs alignment rounding based on **`innodb_buffer_pool_chunk_size * innodb_buffer_pool_instances`**.

   * For details about the automatic parameter adjustment logic, refer to [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).

* Database instances of different kernel versions support different parameters. When modifying parameters of batch instances, the system will automatically ignore parameters that are not supported by the current kernel version of the instance. For detailed information on the modifiable parameters supported by different kernel versions, refer to the following documents:

   * If the database version is MySQL 5.7, refer to [List of modifiable parameters in MySQL 5.7](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7).

   * If the database version is MySQL 8.0, refer to [List of modifiable parameters in MySQL 8.0](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0).

   * If the database version is MySQL 8.4, refer to [List of modifiable parameters in MySQL 8.4](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_4).

   * For more details about parameter modification rules, refer to [Parameter modification rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules).

* Only batch modification of parameters for instances of the same database version is supported.

* A maximum of 100 instances can be selected at the same time for batch parameter modification.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project to which the instance belongs is not set, this operation should select the project as **All resources**.

3. On the **Instances** page, select multiple target instances with the same **database version**.

4. In the lower\-left corner of the **Instances** page, choose  **...**  \> **Modify parameters**.

5. In the popped\-up **Modify parameters** dialog box, after completing the following settings, click **OK**.

   1. Select the **Modification scope** of the parameters. You can select **All nodes**, **Only primary and secondary nodes**, or **Only read\-only nodes**.

   2. Find the target parameter, click the edit button in the Configuration value column of the target parameter, and enter the modified parameter **value** or expression.

   > **tip**

   * > You can change multiple parameters at the same time and submit the modifications together.

   * > Click **Cancel** to exit the **Modify parameters** dialog box.

   * > The parameter values involved in the selected instances may be different.

6. If the modified parameters include parameters that require restarting, the restart risk alert dialog box pops up, confirm that you can restart the instance, and then click **OK**.

7. In the pop\-up **Batch tasks have been initiated** dialog box, view **Task progress**, and click **OK** after a task is completed.

   > **tip**

   * > You can click the **Terminate** button in the **Batch tasks have been initiated** dialog box. After termination, tasks for instances that have not yet started changes will no longer be executed and cannot be recovered. If you want to make changes again, you need to re\-initiate the batch task.

   * > If the task execution fails, move the cursor to **Failure** in the **Execution result** column to view the failure reason.

## FAQ

### Why can't I find the parameter I need to modify in parameter management?

For security and stability reasons, only some parameters can be modified. For a list of modifiable parameters, refer to [List of modifiable parameters in MySQL 5.7](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7) and [List of modifiable parameters in MySQL 8.0](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0). If you cannot find the parameter you need to modify, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

### Does the instance need to be restarted after modification of parameters?

Some parameters require restarting the instance after modification. You can check the **Need restart?**  column under **Parameter configuration** \> **MySQL parameters** to see if you need to [restart the instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance). For details, refer to [Modifing parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/service_availability).

> **tip**

> Perform this operation during off\-peak hours and ensure that your application has a reconnection mechanism.

### Is it possible to modify the system parameter template?

The system parameter template cannot be modified. You can modify the c[ustom template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template) instead.

### How do I check the values of parameters that cannot be modified in RDS for MySQL?

Log on to [Database Workshop](https://console.byteplus.com/dbw) and use the SQL statement `SHOW variables like 'Parameter name'` to check.
