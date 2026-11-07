---
title: "Migration process overview"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Migration_Process_Overview"
---

This topic is intended to help you understand the migration process of SMC. It facilitates your rapid migration of on\-premises servers, virtual machines, cloud servers from other cloud platforms (such as Alibaba Cloud, Huawei Cloud, and Tencent Cloud), or other types of servers to the BytePlus platform.

<span id=".6L-B56e75rWB56iL"></span>
## Migration process

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e3e7e8dd40602a6af80e0d752e88a8f4.png) </span>


1. [Preparations](https://docs.byteplus.com/en/docs/smc/Preparations): Prior to migrating the source server, you need to complete the necessary preparation steps, including platform account creation, account authentication, and source migration configuration.

2.  **(Optional)** [Create migration templates](https://docs.byteplus.com/en/docs/smc/Create_and_manage_migration_templates): Plan the target instance in advance using migration templates.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The migration template feature is currently in Beta. If you need a trial, please contact your account manager.   </div>
   

3. Import the migration source.

   * Import using the manually installed migration tool Agent: You need to log in to the source server, and manually install and start the migration tool Agent to import migration source information. [Learn more](https://docs.byteplus.com/en/docs/smc/Import_Migration_Sources).

   * One\-click import from the console: You do not need to log in to the source server. You can batch import migration source information in the SMC console with one click.

4. Adjust the source server configuration based on the migration source precheck result. [Learn more](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck).

5. Create a migration task in the console. [Learn more](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task).

6. Adjust the source server and target instance configuration based on the migration task precheck results. [Learn more](https://docs.byteplus.com/en/docs/smc/Precheck_item_description).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the source server does not pass the migration precheck, adjust the source server configuration based on the migration precheck result and perform the one\-click migration operation again. <a href="https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck">Learn more</a>.   </div>
   

7. [View the migration result](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs).


<span id=".54q25oCB6K-05piO"></span>
## State description

<span id=".6L-B56e75rqQ54q25oCB"></span>
### Migration source status


|Status |Description |
|---|---|
|Online |The migration source is communicating normally with SMC, and a migration task can be created. |
|Migrating |The migration source is in the process of data migration. |
|Abnormal |The migration tool Agent reports a heartbeat anomaly or exits unexpectedly.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can execute the <code>./smc_manage start</code> command in the migration source to restart the migration tool Agent and continue reporting migration source information.</div><br> |
|Offline |The migration tool Agent stops running. |


<span id=".6L-B56e75Lu75Yqh54q25oCB"></span>
### Migration task status


|Status |Description |
|---|---|
|Preparing |Temporary resources required for migration are being created. |
|Migrating |The task with the "Auto incremental synchronization" feature not enabled is migrating source server data. |
|To start |The migration task is awaiting manual start. |
|Initialization |Creating a destination instance based on the migration template. |
|Incremental migration |The task with the "Auto incremental synchronization" feature enabled is migrating source server data. It includes the following three stages:<br><br><br>* **Full migration**: The initial migration stage, where all data from the source server is being migrated.<br><br>* **Incremental migration**: The incremental synchronization stage, where only the data changed since the last synchronization is being synchronized based on the auto incremental synchronization cycle.<br><br>* **Final sync**: The final stage of migration, where the last incremental synchronization is being performed. |
|Paused |The migration task is paused. |
|Paused |The migration task is paused. |
|Succeeded |The migration operation is completed. |
|Failed |The migration failed. |
|Terminating |The migration task is being terminated. |
|Terminated |The migration task is terminated. |
|Clearing |Temporary resources associated with the migration task are being cleaned up. |
|Abnormal |The migration task is abnormal due to the unexpected exit of the migration tool Agent.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can execute the <code>./smc_manage start</code> command in the migration source to restart the migration tool Agent so that the migration task can continue. Alternatively, you can <a href="https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs#TxngLf54">terminate the migration task</a> and <a href="https://docs.byteplus.com/en/docs/smc/Clean-up-task-resources">clean up the task resources</a> to end the task.</div><br> |
