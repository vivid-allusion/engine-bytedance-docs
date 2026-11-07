---
title: "Upgrade instance database major version"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instances_database_major_version"
---

RDS for MySQL supports upgrading the major version of an instance, allowing you to upgrade eligible MySQL 5.7 instances to MySQL 8.0. This topic describes the procedure for upgrading database major version of the instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The major version upgrade feature of RDS for MySQL allows you to upgrade eligible MySQL 5.7 instances to MySQL 8.0. You can upgrade the major version of an instance immediately, during the maintenance window, or during a specific time period. RDS for MySQL also provides observation capabilities for upgrades, providing temporary read\-only endpoints to eligible instances for testing and verification. RDS for MySQL will create a temporary read\-only endpoint for the instance. You can use this temporary read\-only endpoint to verify the business impact of the major version upgrade. If the verification is successful, you can continue the upgrade task in the Task Center. If the verification results are not as expected, you can cancel the upgrade and roll back the instance.

During the upgrade, you can perform normal read‑and‑write operations, and data will be written to the RDS for MySQL 5.7 instance at this time. After the full‑volume data (data existing before the upgrade) in the RDS for MySQL 5.7 instance is migrated, incremental Binlog (incremental data, namely the data written to RDS for MySQL 5.7 during the upgrade) will be synchronized. The switch operation is performed after the data is fully caught up.

After you initiate a major version upgrade task for an instance, you can view the specific progress of the instance upgrade in the Task Center. The instance major version upgrade task includes the following seven stages. After completing phases such as task initialization, resource processing, data processing, and data catch\-up, the instance switches to the target version. The task then enters the 'Waiting to continue' phase (task status: Waiting for execution), while the instance status remains 'Upgrading'. During this period, you can select "Cancel" to roll back the upgrade or "Execute now" to complete it. The duration of the "Waiting to continue" phase is the configured observation duration. If the "Waiting for execution" state lasts longer than the observation duration, the system automatically completes the upgrade.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3fd569cdf7cce7dd0f968a0ecc86a487.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The 'Waiting for switch time' and 'Continue task' phases exist only if you select to upgrade during a maintenance window or a specific time period.</div>


* <div data-tips="true" data-tips-type="tip">During the 'Waiting for switch time' phase, you can use the temporary domain name (i.e., the domain name of the temporary terminal, which will have a <code>Temporary</code> label) to connect to the backend of the instance to be switched for read\-only testing. The username and password are the same as those of the current instance. The temporary domain name will be automatically removed after the switch is completed.</div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* There will be a flash disconnection of seconds during the upgrade switching phase. It is recommended to switch during the maintainable time period or during the business off\-peak period and add an application reconnection mechanism to significantly reduce the impact of database connection flash disconnection on the business.

* During the upgrade process, do not create accounts, delete tables, or perform DDL operations. These operations may cause abnormalities in the replication link, which can result in a failed upgrade.

* When upgrading the major version of a database instance, a temporary read\-only endpoint is created for testing and verification. If the database proxy is enabled for the instance before the upgrade, a temporary read\-only proxy endpoint and a temporary read\-only direct endpoint will be created for the instance during the upgrade process; if the database proxy function is not enabled for the instance, only a temporary read\-only direct endpoint will be created for the instance during the upgrade process. For more information about connection endpoints, refer to [Viewing connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_connection_endpoints).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the Endpoints list of the instance, the Endpoint name/ID column of the temporary endpoint will have a <code>Temporary</code> tag.   </div>
   

* Before entering the **Waiting for task to continue** stage, the backend has completed the preparatory work for the upgrade and switched the traffic. If features specific to MySQL 8.0 are applied to the instance at this point, canceling the upgrade task will fail.

* Upgrading the database major version for instances that use the RocksDB engine is not currently supported.

* Do not execute DDL statements during the upgrade to prevent replication interruptions between the primary and readonly instances due to version differences.

* After the instance completes the database kernel major version upgrade, once the configured observation duration is exceeded, rollback to the original pre‑upgrade version and downgrade to a lower database version are no longer supported.

* During the upgrade, you can perform normal read‑and‑write operations, and data will be written to the RDS for MySQL 5.7 instance at this time. After the full‑volume data (data existing before the upgrade) in the RDS for MySQL 5.7 instance is migrated, incremental Binlog (incremental data, namely the data written to RDS for MySQL 5.7 during the upgrade) will be synchronized. The switch operation is performed after the data is fully caught up.


<span id=".6KeE5YiZ5LiO6ZmQ5Yi2"></span>
## Constraints and limits


* You can only upgrade MySQL 5.7 instances to MySQL 8.0. You cannot upgrade MySQL 5.7 or MySQL 8.0 instances to MySQL 8.4.

* When upgrading an instance, ensure that the instance state is **Running**.

* If the instance has a disaster recovery instance, you need to delete the disaster recovery instance first, and then rebuild it after upgrading the primary instance.

* Before upgrading, RDS for MySQL performs a pre\-check on the target instance. The pre\-check includes check items from the native MySQL [Upgrade Checker Utility](https://dev.mysql.com/doc/mysql-shell/8.4/en/mysql-shell-utilities-upgrade.html) and custom check items from RDS for MySQL. The check item results are categorized as Failed, Warning, and Note. You cannot upgrade the instance if there are failed check items. If there are check items with a Warning or Note result, you must fix them and run the pre\-check again, or ignore them before you can upgrade the instance. For details about the pre\-check items, refer to [Check items list](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Pre-check_items_for_upgrading_instance_database_major_version).


<span id="pmYi1jL2"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the Instances page, click the target instance name.

4. On the **Summary** tab, in the **Configuration information** section, point to **Upgrade version** to the right of **Database version**. In the pop\-up window, click **Upgrade major version**.

5. On the **Upgrade major version** page, modify or confirm the following configurations, and then click **Upgrade pre\-check**.

   
   |Parameter |Description |
   |---|---|
   |Instance ID/Name |Verify the ID and name for the major version instance to be upgraded. |
   |Instance type |Verify the type for the major version instance to be upgraded. |
   |Data validation latency threshold |Set the data validation latency threshold for data synchronization. Acceptable integer values range from 1 to 10. A smaller latency threshold may increase the time required to complete the upgrade. |
   |Target database version |Confirm the target upgrade version. Only MySQL 8.0.32 is currently supported. |
   |Node specification |Verify the node specification for the major version instance to be upgraded. |
   |Risk Identification |Confirm and select the potential risks of upgrading the instance major version. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The time required to pre\-check depends on the number of databases & tables of the instance. If the number of databases & tables under the instance is large, it may take more time to complete the pre\-check. Closing or refreshing the page will not interrupt the pre\-check process, and the background will continue. You can revisit the pre\-check page later or check the completion of the pre\-check in the Task center.   </div>
   

6. After completing the pre\-check, complete the following configurations on the **Upgrade major version** page and click **Upgrade**.

   
   |Parameter |Description |
   |---|---|
   |View and confirm the pre\-check results. |After the pre\-check is completed, the **Upgrade major version** page displays the check items that failed or require attention.<br><br><br>* Click **Details** in the **operation** column of the check items list to obtain potential problems, impacts, and solutions.<br><br>* Click **Ignore all** at the top of the check items list to ignore all problems, or click **Ignore** in the **operation** column to ignore problems one by one.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If a check item fails, it is marked as an error, warning, or notice, depending on its impact level. For "Error" check items, the problem must be resolved or fixed before the upgrade process can continue; for "Warning" and "Notice" check items, they can be fixed or ignored as needed. The upgrade process cannot continue until this is ignored.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Download MySQL Upgrade Utility log</strong> at the top of the check items list to obtain the <strong>MySQL Upgrade Utility</strong> upgrade log.</div><br> |
   |Upgrade time |Select the upgrade time. You can select **Execute now**, **Specific time period**, or **Maintenance window**.<br><br><br>* **Execute now**: Executes immediately after the order is submitted.<br><br>* **Specific time period**: Perform the specification change within the specified time period.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period). |
   |Specific time period |If you choose to upgrade within a **specific time period**, you must set the upgrade time period.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to upgrade within the **maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Observation duration |Set the observation duration after the instance upgrade. The value can be set to an integer between 1 and 72, in hours. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the upgrade starts, the Upgrade major version page will be closed, and the instance status will switch to <strong>Upgrading</strong>. You can check the detailed progress of the upgrade task in the Task center.</div>


* <div data-tips="true" data-tips-type="tip">If you choose to upgrade during the maintenance window or a specific time period, the instance upgrade task will have a <strong>Waiting for switch time</strong> phase. During this phase, you can:</div>


   * <div data-tips="true" data-tips-type="tip">Verify the business impact of the major version upgrade through the temporary read\-only endpoint.</div>


   * <div data-tips="true" data-tips-type="tip">In the Task center, choose to execute the upgrade task immediately, modify the task's switch time, or cancel the task.</div>


   * <div data-tips="true" data-tips-type="tip">After the instance switches to the target version, the task enters the <strong>Waiting for execution</strong> state, and the instance status becomes <strong>Upgrading</strong>. The instance will then enter the observation phase. During this period, you can select <strong>Cancel</strong> in the Task center to roll back the upgrade or <strong>Execute now</strong> to complete it. If the <strong>Waiting for execution</strong> state lasts longer than the set observation duration, the system automatically completes the upgrade.</div>
