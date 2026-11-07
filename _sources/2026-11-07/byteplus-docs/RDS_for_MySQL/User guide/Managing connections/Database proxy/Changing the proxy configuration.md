---
title: "Changing the proxy configuration"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations"
---

This article describes how to change the proxy configuration of an instance.

## Precautions

* Database connections might be briefly interrupted during the modification of the proxy configuration. Proceed with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database disconnection on the business.

* You cannot modify the proxy configuration for an instance if its database proxy service was enabled before 00:00:00 on November 20, 2024 (Beijing time) and has not been disabled and re\-enabled since. In this case, the database proxy feature is in a free, basic state.

## Prerequisites

The database agent function of the instance is enabled.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. On the **Instances** page, click the instance name of the target instance to enter the **Instances** page.

5. Click the **Connectivity** tab. In the **Database proxy** section, click **Modify configuration** to the right of **Proxy configuration**.

6. In the **Modify proxy configuration** dialog box that appears, configure the settings, select the checkbox to confirm the billing rules, and then click **OK**.

   |Parameter |Description |
   |---|---|
   |Number of proxy cores |Set the number of proxy cores.<br><br>> **tip**<br><br><br><br>* > For a multiple\-node instance,<br><br><br>   * > The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br><br>   * > The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`.<br><br><br>* > For a double\-node instance,<br><br><br>   * > The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5` (round up the result).<br><br><br>   * > The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.5`.<br> |
   |Switch time |Select the switch time of the change. You can choose **Execute now** or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the modification order.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br>> **tip**<br><br><br>> If you select to change the specification during the maintenance window, RDS for MySQL will immediately perform prerequisite actions such as resource scheduling and data synchronization after the modification order is submitted, and the instance status will be switched to Modifying. The route will be switched after the maintenance window starts. After the task is completed, the instance status will change to Running.<br> |
   |Specific time period |If you select **Specific time period**, you need to set the time period for the specification change.<br><br>> **tip**<br><br><br><br>* > Time periods cannot be set across days.<br><br><br>* > The minimum time period is two hours.<br><br><br>* > Set the time period within the time range indicated in the console.<br> |
   |Maintenance window |If you choose to modify the configuration during the **Maintenance window**, you need to confirm the instance's **maintenance window**.<br><br>> **tip**<br><br><br><br>* > You can click **Edit** to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br>* > After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see [Changing the execution time of a task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task).<br> |

## Related API

|API |Description |
|---|---|
|[ModifyDBProxySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyspec) |Call the ModifyDBProxySpec API to modify the proxy configuration of an instance. |
