---
title: "Switching blue and green instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Switching_between_blue_and_green_instances"
---

After you verify the upgrades or changes in the green instance and confirm that its performance, stability, and compatibility meet the expected standards, you can perform a blue\-green switch to quickly and smoothly migrate services from the blue instance to the green instance. This topic describes the steps to perform a blue\-green switch.

<span id="viPIvoCr"></span>
## Precautions


* The blue instance and the green instance will exchange metadata and connection endpoints except for the specification configuration. During the switch, the instance may become read\-only for minutes and experience multiple connection interruptions. Proceed with caution. Add a reconnection feature to your application to reduce the impact of such events on your services.

* If you modify the write mode of the green instance after creating the blue\-green deployment, you must rebuild the data on the green instance before the blue\-green switch.

* RDS for MySQL performs a pre\-check on the blue\-green deployment before the switch. For details about the pre\-check items, refer to [Check items list](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Pre-check_items_for_upgrading_instance_database_major_version).

* A green instance can be created for an instance with Transparent Data Encryption enabled. However, a blue\-green switch is not supported because Transparent Data Encryption cannot be disabled once it is enabled.

* If SSL encryption is enabled for the instance, it must be disabled before the blue\-green switch.

* The downtime for a blue\-green switch is usually less than a minute.

* Public network replication may extend the switch time due to bandwidth limitations or high latency.

* The blue\-green switch uses a DNS switch solution, and the IP address changes after the switch.

* After a blue\-green switch is executed, the synchronization link for the blue\-green deployment is automatically rebuilt. If the creation fails, an InstanceBlueGreenDtsRebuildTaskFailed event is sent for the instance in the Event Center of Cloud Monitor. For more details about viewing an event, refer to [Viewing an event](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_an_event).


<span id="nK91OAsa"></span>
## Prerequisites


* The blue\-green deployment has been created, and the state of both the blue and green instances in the target blue\-green deployment is **Running**. For more information, refer to [Creating a blue-green deployment](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment).

* A synchronization task has been created for the blue\-green deployment and its state is **Executing**. For more information, refer to [Creating a blue-green deployment synchronization link](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment).

* The target blue\-green deployment has not undergone a blue\-green switch.


<span id="Fe8ilHoY"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Instances** to view the list of RDS for MySQL instances.

4. On the **Instances** page, click the name of the target blue instance or green instance to go to the **Summary** tab.

5. Click the **Connectivity** tab. In the **Instance topology** area, click **Blue\-green switch** from the **Actions** drop\-down list on the **Green instance** card to go to the **Pre\-check** page.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you click the <strong>Blue\-green switch</strong> button, RDS for MySQL simultaneously initiates a pre\-check for the blue\-green deployment and displays the check results on the <strong>Blue\-green switch</strong> page. If a check item fails, the check result is marked as "Failed", "Warning", or "Prompt" on the page, depending on the impact level.   </div>
   

6. After the pre\-check is complete, view the pre\-check results on the **Pre\-check** page. After you resolve any issues based on the check results, click **Next step** to go to the **Switch configuration** page for the blue\-green switch.

   
   |**Check result** |**Description** |**Solution** |
   |---|---|---|
   |Failed |The problem must be resolved or fixed before the switch. The upgrade process cannot be continued until the problem is resolved. |Click **View repair suggestions and solutions** to get the repair suggestions and solutions. After the fix is complete, click **Re\-pre\-check** in the lower\-right corner of the **Blue\-green switch** page to run the pre\-check again. |
   |Warning |Repair or ignore this as needed. The upgrade process cannot continue until this is ignored. |Confirm whether there is any impact or risk to your services. If there is an impact, resolve the issues for the check items that have a **Failed** result and run the pre\-check again. If there is no impact, click **Ignore** in the **Actions** column of the check items list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If multiple check items have a Warning result, click <strong>Ignore all</strong> at the top of the list after confirming that there is no impact on your services.</div><br> |
   |Prompt |A prompt about the expected changes to the instance after the blue\-green switch. |No action is required. |
   

7. After you complete the following configurations on the **Switch configuration** page, click **Next step** to go to the **Switch summary** page of the blue\-green switch.

   
   |**Configuration item** |**Description** |
   |---|---|
   |Switch time |Select the switch time. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Switch now**: Executes immediately after the upgrade order is submitted.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period). |
   |Specific time period |If you choose to upgrade within a **specific time period**, you must set the upgrade time period.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to upgrade within the **maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Migrate endpoint |Select the connection endpoints to be retained during the blue\-green switch and specify their migration relationships. After the switch is complete, the instance will use the selected connection endpoints to provide services. After you click the  **+Add** button at the bottom of the **Migrate endpoint** list, you can select more custom connection endpoints from the drop\-down lists for the blue and green instances and specify the migration relationship. The following rules apply when you select connection endpoints and specify migration relationships:<br><br><br>* The default endpoint of the blue instance is migrated to the default endpoint of the green instance.<br><br>* The number of custom connection endpoints that you can select depends on the number of custom connection endpoints in the green instance. Multi\-node instances only support creating three custom read\-write direct endpoints. If your green instance is a multi\-node type, you can migrate only three custom endpoints from the blue instance.<br><br>* The source and target connection endpoints for the migration must have the same endpoint type and read/write mode.<br><br>* If public network resolution is enabled for the private network domain of the source connection endpoint, it is automatically enabled for the target connection endpoint after migration.<br><br>* Migrating connection endpoints with public network access enabled is not supported.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click Delete in the <strong>Actions</strong> column of the <strong>Migrate endpoint</strong> list to remove the selected custom connection endpoints.</div><br> |
   

8. The **Switch summary** page displays the following information for the blue and green instances in the blue\-green deployment: compatible version, kernel version, proxy information, specification, storage, instance type, allowlists, endpoint information, endpoint information to be migrated, and parameter information. After you confirm the information, click **Submit** to initiate the blue\-green switch.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After the blue\-green switch is initiated, the blue\-green switch page will close, and the instance state will change to <strong>Blue\-green switching</strong>. You can check the detailed progress of the upgrade task in the Task center.</div>


<span id="HQfv82jB"></span>
## Related API


|API |Description |
|---|---|
|[SwitchDBBlueGreen](https://docs.byteplus.com/en/docs/RDS_for_MySQL/SwitchDBBlueGreen) |Call the SwitchDBBlueGreen API to switch the blue\-green deployment. |
