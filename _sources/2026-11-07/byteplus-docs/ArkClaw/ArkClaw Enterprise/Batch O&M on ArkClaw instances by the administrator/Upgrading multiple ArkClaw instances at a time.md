---
title: "Upgrading multiple ArkClaw instances at a time"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_multiple_ArkClaw_instances_at_a_time"
---

Regularly upgrading ArkClaw instances is a key measure to ensure the stable, secure, and efficient operation of the agent gateway. It addresses security risks in earlier versions to promote comprehensive system optimization and capability improvement. It also allows you to use new features to support business iteration. When the platform releases the latest version, we recommend upgrading ArkClaw instances to the latest version promptly. This topic describes how to upgrade multiple ArkClaw instances at a time.

<span id="IYw8O67d"></span>
## Background

ArkClaw instance versions are managed and released by the platform. After the platform releases the latest version, the administrator will receive an upgrade notification and a version update description. We recommend upgrading ArkClaw instances promptly. The detailed upgrade process is as follows:


1. After the administrator receives the notification on the latest version released by the platform, they can go to the version management page to preview detailed information about the version update.

2. The administrator creates an upgrade job. After the job is created, instance data is automatically backed up. If the backup fails, the upgrade task will be immediately terminated. If the backup succeeds, the upgrade process will start.

3. During the upgrade process, Core, Skill, and Plugin of the instances will be sequentially upgraded. If the upgrade fails, the instances will be automatically rolled back to the version before the upgrade to ensure the instances are available. If the upgrade succeeds, the upgrade process will end.

4. Regardless of whether the upgrade is successful, after the upgrade job is complete, you can go to the execution result page to view the upgrade result, status, and logs for each instance, and perform troubleshooting for instances that failed to be upgraded.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b6cfd8e15b26e986ea0e94d7661af59.png) </span>

<span id="eNZJ6vuB"></span>
## Limits


* The platform only maintains Core, Skill, and Plugin that are officially provided. For other items that you install, you need to maintain them yourself.

* Only instances in the "Running" state can be upgraded. During the upgrade, the service will be interrupted for about 10 to 20 minutes. To prevent normal business operations from being affected, we recommend performing upgrades in batches during off\-peak hours.

* Data automatically backed up when administrators upgrade ArkClaw instances will overwrite data manually backed up by administrators.

* ArkClaw uses the `x.y.z` format for version tagging, where `x` indicates the major version, and `y` and `z` indicate minor versions. Cross\-major\-version updates may contain incompatible changes, and one\-click upgrade to the latest version is not supported. Minor versions within the same major version support one\-click upgrade to the latest version. Upgrading to historical versions is not allowed.

   * Minor versions within the same major version are backward compatible and support one\-click upgrade to the latest version. Example: If the current version is 1.0.1 and the latest version is 1.2.0, both belong to the same major version. You can still upgrade directly from 1.0.1 to 1.2.0 with one click, even if there are intermediate minor versions in between.

   * Cross\-major\-version updates may involve incompatible changes. If you need to upgrade across major versions to the latest version, you need to complete the upgrade in multiple steps. Example: If the current version is 1.0.1 and the latest version is 2.2.3, the upgrade spans the major version 2.0.0. To upgrade to the latest version, you need to perform two steps: First upgrade from 1.0.1 to 2.0.0, and then upgrade from 2.0.0 to 2.2.3.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47fafad4a5be70d37e275dd9aab54bc1.png) </span>


<span id="8EEDFKv6"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To prevent uncontrollable factors from affecting normal business operations, we recommend first upgrading a small number of instances. After you confirm the instances are upgraded as expected, upgrade all instances.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **O&M \> Batch O&M**.

3. Click the **Version management** tab and click **Details** in the Actions column that corresponds to the target version to view detailed version update records, including version number/ID, update time, OpenClaw version, detailed update records, and the baseline versions of Core, Skill, and Plugin.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also click <strong>View details</strong> in the upgrade tip banner to view detailed information about the update records for the latest version.   </div>
   

4. On the **Version management** tab, click **Update to this version** in the Actions column that corresponds to the latest version to go to the batch job creation page and configure the version upgrade job as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also click <strong>Create update job</strong> in the upgrade tip banner to go to the batch job creation page and configure the version upgrade job based on your business requirements.   </div>
   

   
   |Category |Configuration item |Description |
   |---|---|---|
   |Basic information |Job name |The preset job name. You can modify it based on your business requirements. |
   ||Description |The remarks or description of the current job. When multiple jobs exist, we recommend entering the differences in the description to prevent confusion. |
   |Execute command |Command type |The type of O&M command. Version upgrade jobs use "Upgrade task" by default. |
   ||Execution Policy |The execution policy for upgrade jobs includes immediate and scheduled execution.<br><br><br>* **Immediate**: Once the version upgrade job is created, the upgrade task will start immediately.<br><br>* **Scheduled**: Once the version upgrade job is created, the upgrade task will not start until the scheduled time.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend performing upgrade jobs randomly, instead of concurrently, to reduce the load pressure during the upgrade process. For example, 00:02, 01:23, and 02:45.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If multiple upgrade jobs are created, we recommend keeping an interval of longer than 30 minutes between any two adjacent jobs.</div><br> |
   ||Maximum concurrency |The number of ArkClaw instances to be upgraded concurrently. The default value is 100.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The actual number is affected by environment health status, resource account bandwidth, and storage load. If the upgrade fails due to resource shortage, we recommend reducing this value.</div><br> |
   |Object |Object |ArkClaw instances to be upgraded. Click **Add**, select the ArkClaw instances to be upgraded, and then provide multiple instance filter criteria, such as the current version, excluded version, instance name, instance ID, associated user, user ID, and tag.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can only add ArkClaw instances that are in the Running state.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can add up to 100 instances for each upgrade job. If more than 100 instances are added, they will be automatically split into multiple upgrade jobs.</div><br> |
   

5. After the upgrade job is created, you will be redirected to the Job list tab, and the upgrade job will run based on the configured execution policy. The common states of jobs are as follows:

   * **Succeeded**: All ArkClaw instances of the current job have been upgraded.

   * **Pending**: The current upgrade job has not started because the scheduled start time has not arrived yet.

   * **Execution failed**: All ArkClaw instances of the current job failed to be upgraded.

   * **Partial failure**: Only part of the ArkClaw instances of the current job have been upgraded.

6. After the upgrade is complete, click **Execution result** in the Actions column that corresponds to the target job to view the upgrade result, logs, status, and other information of each instance. Common states are as follows:

   * Succeed**ed**: The current instance has been upgraded to the latest version.

   * **Rollback succeeded**: The current instance failed to be upgraded, and it has rolled back to the version before the upgrade. ArkClaw can still be used as expected.

   * **Backup failed**: The data of the current instance failed to be backed up, and the upgrade task was interrupted. The instance remains at the version before the upgrade. ArkClaw can still be used as expected.


<span id="JfIxUM9l"></span>
## What to do next


* If the instance upgrade fails, you can go to the "Execution result" tab and click **Logs** in the Actions column to view detailed records for troubleshooting. The common causes for upgrade failures and solutions are as follows:

   
   |Common cause |Description |Solutions |
   |---|---|---|
   |Backup failed |The data of the ArkClaw instance failed to be backed up. This causes the upgrade job to be interrupted. |You can resolve this issue by retrying in most cases. If the backup constantly fails, try analyzing the logs to find the cause. |
   |Upgrade timeout |The upgrade job was terminated because the load was too high and it failed to complete within 1 hour. |Retrying usually resolves the issue. We recommend proceeding in batches to avoid upgrade job congestion. |
   |Instance status exception |The upgrade job cannot proceed because the instance is not in the "Running" state. This typically occurs in scheduled tasks. For example, a scheduled instance is created in the "Running" state, but the instance state changes when the scheduled task begins. |Adjust the instance to the "Running" state and try again. |
   |Upgrade the OpenClaw manually |The employee manually upgraded the OpenClaw version, causing a conflict with the version pushed by the platform. This leads to an upgrade failure.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend upgrading to the version pushed by the platform. Enterprise employees should not upgrade the OpenClaw or other core components to any other versions.</div><br> |Manually roll back the OpenClaw version to match the platform\-released version and then retry, or contact official technical support for assistance. |
   |Failed to upgrade the manually installed version |Enterprise employees manually installed tools such as Skills and Plugins that are not provided by the platform, which led to an upgrade failure.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend using the Skills and Plugins provided by the platform. Enterprise employees should not install tools obtained from other sources.</div><br> |Manually upgrade tools such as Skills and Plugins installed by employees and retry, or contact official technical support for assistance. |
   

* For instances that failed to upgrade but whose issue has been resolved, go to the "Execution result" tab and click **Retry failed task** to quickly create a new upgrade job.

* You can stop a task that has not been completed or executed. You can go to the job list and click **Stop** in the Actions column that corresponds to the target job to terminate the task.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you stop a task that is in progress, if the instance is in the "Rolling back" or "Backing up" state, the task will not be immediately interrupted, but will stop upon completion to ensure data integrity.   </div>
   

* If you encounter usage issues after the upgrade, you can go to the instance details page and use the data that is automatically backed up before the upgrade to quickly roll back the instance to the version before the upgrade. The data source is the backup data of the administrator.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">We do not recommend that you continue using the earlier version on the platform. You can use this method to quickly roll back to the version before the upgrade only if the latest version has issues that affect normal business operation.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">You still need to upgrade to the latest version after you roll back to the version before the upgrade by using backup data.   </div>
