---
title: "Batch apply parameter template"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/applying_parameter_templates_in_batches"
---

This topic describes the procedure for batch applying parameter templates.

## Prerequisites

* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A parameter template has been created. For detailed steps, refer to [Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template).

## Precautions

* If the parameter template you choose contains parameters need to restart the instance to take affect, the instance will restart after applying the parameter template. The time to restart the instance depends on the load state of the instance, which will cause the business to flash out once or twice. Please operate with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database disconnection on the business. During the restart process of a read\-only node, the corresponding nodes will be unavailable, and the load of the current read\-only node will be transferred to other nodes that meet the conditions. Proceed after accurately evaluating the impact of the restart.

* Batch application parameter template operations are supported only for instances with the same database version. In a batch application parameter template operation, up to 10 instances can be selected.

* When the parameter value in a parameter template is a formula, the system calculates the parameter value for each node individually based on its specifications. After applying the same parameter template to different instances, the value of the same parameter may vary. When adjusting a parameter that requires a restart, the system compares the new value with the instance's current value. If the new value is the same as the current value, the instance will not be restarted for that parameter.

   * For the **`innodb_buffer_pool_size`** ** ** parameter, before template application, the system still verifies the calculated value of each target node one by one to check whether it falls within the **50%～85%**  range of the target node memory. If verification fails, the template application request for this instance **fails directly**.

   * The valid value that passes verification will be aligned and rounded according to **`block_size`** and `innodb_buffer_pool_chunk_size * innodb_buffer_pool_instances` after entering the **asynchronous execution phase**.

* When you apply a system parameter template to an instance and select the scope of modification as **All nodes**, if the data synchronization method of the instance is different from the preset method of the system template, the data synchronization method will be adjusted automatically after applying the parameter template.

* The underlying logic of MySQL will automatically adjust some parameters to preset limit values or integer multiples of preset values.he adjustment rules are as follows:

   * If the configured parameter **value exceeds the valid value range of the parameter**, the system will not perform automatic adjustment, and the modification operation will fail directly.

   * If the configured parameter **value falls within the valid value range of the paramete**r, but does not meet the required multiple relationship of the parameter (e.g., `block_size`), the system **rounds the value down** to the nearest compliant value during the asynchronous execution phase. Therefore, the final effective value may differ from the configured value.

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

3. On the **Instances** page, select multiple target instances.

4. In the lower\-left corner of the **Instances** page, choose  **...**  \> **Apply parameter template**.

5. On the **Batch apply parameter template** page, confirm the selected instances and select the template to apply and click **Next step**.

6. Complete the following settings on the **Batch apply parameter template** page and click **OK**.

   * **Modify scope**: Select the node range to which the parameter template is applied, such as **All nodes**, **Only primary and secondary**, **Only read\-only**, or Specified read\-only nodes.

      > **tip**

      > If none of the selected instances have read\-only nodes, the modification scope will be set with **All nodes** by default.

   * **Data synchronization method**: Confirm the data synchronization method of the instance.

      > **tip**

      > When selecting a system template and the modification scope is **All nodes**, the data synchronization method will be adjusted according to the selected parameter template. The data synchronization method depends on the configuration of the parameter template.

   * **Parameter changes**: The parameter changes list displays the changes to the parameters of the selected instance after a parameter template is applied. It includes the parameter name, value before application, value after modify, whether a restart is needed, details on involved formulas, and the corresponding node.

      > **tip**

      > If there are parameter values configured as formulas in the parameter template, the parameter values will be calculated separately according to the specifications of each node, and the changes will be listed by node in the parameter change list.

   > **tip**

   > If the selected parameter template contains parameters that need to be restarted, the restart risk alert dialog box pops up, confirm that you can restart the instance, and then click **OK**.

7. In the pop\-up **Batch cancel** dialog box, view **Task progress**, and click **OK** after all tasks are completed.

   > **tip**

   * > You can click the **Terminate** button in the **Batch cancel** dialog box, and the task of the instance that has not started changing after termination will no longer proceed and cannot be resumed. If you want to make changes again, you need to re\-initiate the batch task.

   * > If the task execution fails, place the cursor on **Failure** in the **Execution result** column to view the failure reason.
