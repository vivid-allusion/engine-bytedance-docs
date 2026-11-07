---
title: "Upgrading instance kernel minor version manually"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version"
---

RDS for MySQL allows you to manually upgrade the instance kernel minor version. This topic describes the detailed steps.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A newer kernel minor version is available for upgrade. On the **Summary** tab, in the **Configuration** section, check the prompt to the right of Database version. If the prompt is not "Latest", a new version is available for upgrade.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The maintenance cycle for an RDS for MySQL kernel minor version is at least six months, with no fixed duration. If an instance's kernel minor version exceeds its maintenance cycle, the system temporarily ignores the upgrade policy and automatically upgrades the kernel minor version. The automatic upgrade of an instance's kernel version depends only on its current kernel version, not its creation time. For detailed information about the kernel version maintenance cycle, refer to [Kernel minor version release note](https://docs.byteplus.com/en/docs/RDS_for_MySQL/kernal_version_release_notes).

* Upgrading the kernel minor version for cloud disk instances is not currently supported.

* After the instance completes the database kernel minor version upgrade, once the configured observation duration is exceeded, rollback to the original pre‑upgrade version and downgrade to a lower database version are no longer supported.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the Instances page, click the target instance name.

4. On the **Summary** tab, in the **Configuration** area, click **Upgradeable to MySQL 5.7.32_20241015** to the right of **Database version**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MySQL 5.7.32_20241015 is the latest kernel version released by RDS for MySQL at the time of viewing. The version changes as new kernel minor versions are released.   </div>
   

5. In the **Upgrade kernel version** window, complete the following settings and click **OK**.

   
   |Scope |Details |
   |---|---|
   |Upgradeable versions |Select the target kernel minor version from the dropdown list. Click ? to the right of the dropdown list. Check [kernel version release history](https://docs.byteplus.com/en/docs/RDS_for_MySQL/kernal_version_release_notes). |
   |Upgrade time |Select the time to upgrade the kernel version. You can choose:<br><br><br>* **Switch now**: Clicking OK starts the upgrade now.<br><br>* **Specific time period**: Execute the upgrade within the specified time period.<br><br>* **Maintenance window**: Execute the upgrade within the instance's maintenance window. |
   |Specific time period |If you select **Specific time**, you must set an upgrade time period.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting the upgrade time period across days is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The shortest time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the upgrade time period within the time frame prompted by the console.</div><br> |
   |Maintenance window |If you choose to upgrade within the **maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Observation duration |Set the observation duration after the instance upgrade. The value can be set to an integer between 0 and 72, in hours.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After the instance switches to the target version, the task enters the "Waiting for execution" state, and the instance state becomes "Upgrading". During this period, you can select "Cancel" to roll back the upgrade or "Execute now" to complete it. If the "Waiting for execution" state lasts longer than the observation duration, the system automatically completes the upgrade.</div><br> |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[UpgradeDBInstanceEngineMinorVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgradedbinstanceengineminorversion) |Call the UpgradeDBInstanceEngineMinorVersion API to upgrade the minor kernel version of an instance. |
