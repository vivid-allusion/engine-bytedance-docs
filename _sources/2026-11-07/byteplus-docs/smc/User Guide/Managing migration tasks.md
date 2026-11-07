---
title: "Managing migration tasks"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs"
---

This topic describes how to manage migration tasks that have been created and started.

<span id="2oHR36sT"></span>
## Prerequisites

You have created and started a migration task. For details, see [Creating and starting migration tasks](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task).

<span id="9UjoTuxj"></span>
## View migration task details

After a migration task starts, you can use task logs to view the progress and status and troubleshoot issues during migration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can view and receive event information on migration task status changes via the event monitoring feature, enabling you to learn task status changes at any time. For details, see <a href="https://docs.byteplus.com/en/docs/smc/Migration-Job-Incident-Monitoring">Migration task event monitoring</a>.</div>


* <div data-tips="true" data-tips-type="tip">After a successful migration, the platform will automatically release cloud resources created during the migration process, such as relay instances, volumes, and security groups. If the migration fails, manually release the relevant resources.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Select the corresponding tab based on the migration type of the task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7f0bb62988b57f541b6d4316a073a90e.png) </span>

5. You can view different information about the Migration Job on the task list page and task details page.

   
   <Tabs>
   <Tab zoneid="Qjjujezw" title="Task list page">
   <TabTitle>Task list page</TabTitle>
   
   You can view information such as job name, ID, status, precheck status, and migration target on the Migration Job list page.
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3f73b1939e23442d8f725419e29ab9da.png) </span>
   
   If the target migration task has the automatic incremental synchronization feature enabled,  you can click its task status to view the migration stage details when the task is in the **The incremental migration task is in progress** status.
   
   
   * Full migration stage example
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fdcc4118a363c907de51681d9ad5634c.png) </span>
   
   * Incremental migration stage example
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ad3e66ae836a4caa68ffd2fb07a5538.png) </span>
   
   * Final synchronization stage example
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39e5062ab20dbb32de840cd602f372c3.png) </span>
   
   
   </Tab>
   <Tab zoneid="MG2AjFEX" title="Task details page">
   <TabTitle>Task details page</TabTitle>
   
   You can click the target Migration Job name to go to the job details page, view full configuration information of the Migration Job, target information, migration disk configuration, and job logs.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">In the console, you can view log information of migration tasks from the past 180 days.</div>
   
   
   * <div data-tips="true" data-tips-type="default">You can also view the full migration task logs generated since the migration Agent started running from the Agent directory on the migration source.</div>
   
   
      * <div data-tips="true" data-tips-type="default">Linux operating system: Execute the <code>cat smc.log</code> command for viewing information such as SourceId (migration source ID) and migration logs.</div>
   
   
      * <div data-tips="true" data-tips-type="default">Windows operating system: View the Agent run log file smc.txt for details such as SourceId (migration source ID) and Agent running logs.</div>
   
   
   * **Server migration tab example**
   
      * Server migration task
   
         For migration tasks with the destination as ECS instances, you can view the task overview (for example, task name, type, network mode, and target instance) and log information.
   
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7abb8589eb8d5072576bd7edeaf1190f.png) </span>
   
      * Image migration task
   
         For migration tasks with the destination as ECS images, you can view the task overview (for example, task name, type, network mode, relay instance ID, and target image) and log information.
   
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fee7c3e2e65d0082240b0d9fa0c624d.png) </span>
   
   * **OS migration tab example**
   
      For migration tasks of operating system of BytePlus ECS instances, you can view the task overview (for example, task name, type, network mode, and migration method) and log information.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_709f31e842f6a0e1f4ed5029e63b8b23.png) </span>
   
   
   </Tab>
   </Tabs>
   


<span id="htOLq5DW"></span>
## Modify network mode​ of migration task 

After a migration task has the pre\-check completed, you can modify the network mode based on the pre\-check results and your needs to avoid migration failures due to the network.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only <a href="https://docs.byteplus.com/en/docs/smc/Server-Migration-Task">server migration tasks</a> to ECS instances that are in <strong>Passed</strong> or <strong>Precheck failed</strong> status support network mode changes.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Select the "Migrate to server" tab.

5. Click the "... \> Change network mode" button in the Actions column on the right side of the target migration task.

6. Select the target network mode and click the "Confirm" button to complete the operation.


<span id="nJi5JRzb"></span>
## Change transfer speed limit for migration task

You can change the transfer speed limit for migration tasks in the console. This improves data transfer efficiency and prevents migration tasks from occupying excessive network resources and affecting normal business operations.


1. Log in [to the ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Select the corresponding tab based on the migration type of the task.

5. Click the "... \> Change network speed limit" button in the Actions column on the right side of the target migration task.

6. Enter the target speed limit in the pop\-up window, and click the "Confirm" button to complete the modification.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only a non\-negative integer is supported.</div>


* <div data-tips="true" data-tips-type="warning">Speed limit range: 0 ~ 2000. Note that:</div>


   * <div data-tips="true" data-tips-type="warning"><code>0</code> indicates no speed limit.</div>


   * <div data-tips="true" data-tips-type="warning">The speed limit must not exceed the bandwidth limit of the EIP associated with the target instance (migration destination of an ECS instance) or that of the temporary EIP associated with the relay instance (migration destination of an ECS instance image). Otherwise, this configuration is invalid, and SMC data transfer will be limited to the actual bandwidth.</div>


      <div data-tips="true" data-tips-type="warning">For example, for a migration task with the destination of an ECS  image, with the default bandwidth limit of the temporary EIP associated with the relay instance of 50 Mbps, the valid speed limit range is 0 ~ 50 Mbps. Even if you specify the speed limit to 60 Mbps, SMC data transfer will be limited to 50 Mbps. If you change the bandwidth limit of the EIP to 100 Mbps, the valid speed limit range is 0 ~ 100 Mbps.      </div>
      

* <div data-tips="true" data-tips-type="warning">If you change the speed limit during migration, the new speed limit will take effect based on the following rules:</div>


   * <div data-tips="true" data-tips-type="warning">For the "File replication" migration method, the new speed limit will take effect for data migration from the next mounted directory.</div>


   * <div data-tips="true" data-tips-type="warning">For the "Block replication" migration method, the new speed limit will take effect for data migration from the next disk.</div>



<span id="BAr0uiwS"></span>
## Perform final incremental synchronization

If you have enabled the automatic incremental synchronization feature when creating a migration task, you can manually trigger the final incremental sync during the business cutover phase to synchronize the last batch of incremental data from the source server to the cloud.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only migration tasks in the <strong>Incremental migration</strong> status support performing final incremental synchronization.</div>


* <div data-tips="true" data-tips-type="warning">Before performing the final incremental synchronization, please stop the business processes that continuously generate incremental data on the source server. This prevents newly generated data from failing to be synchronized to the target instance during the migration process, and ensures data integrity and consistency. For operation details, refer to <a href="https://docs.byteplus.com/en/docs/smc/Stop-generating-incremental-data-in-the-source-server">Stopping source server processes generating incremental data</a>.</div>


* <div data-tips="true" data-tips-type="warning">After performing the final incremental synchronization, the migration task will be closed, and new data from the migration source will no longer be automatically synchronized to the target instance.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. You can filter the target migration task by migration task ID/name.

5. Click the "Final sync" button in the Actions column on the right side of the target migration task.

6. In the pop\-up window, confirm the task information, check "I have known and dealt with it", and click the "Confirm" button to perform the final incremental synchronization.

   The execution of the final incremental synchronization operation will follow the rules below based on the current phase of the migration task:

   * If the migration task is in the incremental migration interval, the final synchronization will be triggered directly.

   * If the migration task is undergoing incremental synchronization, the final synchronization will be initiated upon the completion of the ongoing incremental synchronization process.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9f0422acf74fb8fc0c92ecb88005f3df.png) </span>

6. If your migration target is an **ECS instance**, SMC will automatically restart the instance after incremental synchronization is completed.


<span id="8YJDKRfo"></span>
## Change automatic incremental synchronization configuration

If you enable the automatic incremental synchronization feature when creating a migration task, you can adjust the synchronization interval based on your needs before performing the final incremental synchronization.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the directory tree on the left side of any Region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. You can filter the target migration task by migration task ID/name.

5. Click the "... \> Set incremental migration" button in the Action column of the target migration task to access the incremental synchronization configuration page.

6. On the prompt page, you can modify the following synchronization rule configurations based on your needs.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Last synchronization time |You can use this parameter to check the time when the last synchronization for the current migration task was completed. |2024\-05\-16 17:38:31 |
   |Synchronization interval |You can use this parameter to modify the synchronization interval for incremental data for the migration task.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum interval is 1 hour, and the maximum is 7 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The platform will start incremental synchronization automatically at the time calculated by: the time when the migration task last completed + interval.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the change, the new sync frequency will take effect in the next sync cycle.</div><br> |0 day 1 hour |
   


<span id="B8h8O01M"></span>
## Manage destination

Before starting a migration task with destination type "Create new instance", you can create or modify the destination instance based on the destination status.

<span id="OEzT6FFZ"></span>
### Create destination instance

If you have not checked the option "Create the destination instance immediately after creating a migration task" or if you have modified the destination migration template, you can choose an appropriate time to create a destination instance manually based on your needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This operation is only supported when the destination status is <strong>To be created</strong>.</div>


* <div data-tips="true" data-tips-type="default">When creating destination instances in a batch, you can select up to 20 tasks at a time.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Click the "Immediately create" button in the "Destination" column to the right of the target task.

5. After you confirm the task information displayed on the prompt page, click the "Confirm" button to complete the operation.


<span id="Km1A3zTU"></span>
### Create new destination instance

If the destination instance has failed to be created via the migration template, you can create a new destination instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature is supported only when the destination status is <strong>Failed to create</strong>.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Click the "Recreate" button in the "Destination" column to the right of the target task.

5. After you confirm the task information displayed on the prompt page, click the "Confirm" button to complete the operation.


<span id="ubAPtWJ8"></span>
### Change destination

Before a migration task starts, you can change the destination instance based on your needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This feature is supported only when the destination status is <strong>To be created</strong>, <strong>Create success</strong>, or <strong>Failed to create</strong>.</div>


* <div data-tips="true" data-tips-type="default">When modifying destination instances in a batch, you can select up to 20 tasks at a time.</div>


1. Log in to the[ ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Click the "Change destination" button in the Actions column to the right of the target task.

5. Select the new destination configurations based on your needs.

   
   |Parameter​ |Sub\-argument |Description |Sample value |
   |---|---|---|---|
   |Method |Based on migration template |Select a new migration template to create the destination instance. |Based on migration template |
   |Target region |\- |Select the region where the new destination is located. |China (Beijing) |
   |Migration templates |\- |Select the required new migration template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After selecting the new migration template, you need to <a href="https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs#OEzT6FFZ">create the destination instance</a> before the migration starts.</div><br> |g3i instance template |
   

6. Click the "Confirm" button to complete the operation.

7. You can choose an appropriate time to [create the destination instance](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs#OEzT6FFZ) in later operations based on your needs.


<span id="i3RVYNM7"></span>
## Start migration task

If you have not agreed to automatically start a migration task after pre\-check or have manually paused a migration task, you can start the corresponding migration task based on your needs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only <a href="https://docs.byteplus.com/en/docs/smc/Server-Migration-Task">server migration tasks</a> in <strong>Passed</strong>, <strong>Precheck failed</strong>, or <strong>Paused</strong> status support this operation.</div>


* <div data-tips="true" data-tips-type="warning">If the migration task is in <strong>Paused</strong> status, SMC will resume the migration based on the following rules:</div>


   <div data-tips="true" data-tips-type="warning">   
   |Task types |Migration stage |Description |
   |---|---|---|
   |Full migration task |\- |SMC will resume data transmission based on the migration progress at the time of pause. |
   |Incremental migration task |Full migration, incremental migration |SMC will resume data transmission based on the migration progress at the time of pause. |
   ||Final synchronization |SMC will initiate a new round of incremental migration to prevent incremental data loss. Example:<br><br>When the final synchronization was at 80% progress, you paused the migration task. Then, SMC will initiate a new synchronization process upon resuming the task, which indicates the final data synchronization will restart from 0%. |
      </div>
   

* <div data-tips="true" data-tips-type="warning">When starting migration tasks in a batch, you can select up to 50 tasks at a time.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Click the "Start" button in the Actions column to the right of the target task.

5. After you confirm the task information displayed on the prompt page, click the "Confirm" button to complete the operation.


<span id="jt57muDv"></span>
## Pause migration task

During the migration process, if you detect that the source server is under high load, you can pause the migration task and resume it once the server meets the migration requirements.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only<a href="https://docs.byteplus.com/en/docs/smc/Server-Migration-Task"> server migration tasks</a> in <strong>Migrating</strong> or <strong>The incremental migration task is in progress</strong> status support this operation.</div>


* <div data-tips="true" data-tips-type="warning">After a server migration task is paused, SMC will suspend data transmission and retain the transmission progress.</div>


* <div data-tips="true" data-tips-type="warning">When pausing migration tasks in a batch, you can select up to 50 tasks at a time.</div>


1. Log in to the[ ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Click the "Pause" button in the Actions column to the right of the target task.

5. After you confirm the task information displayed on the prompt page, click the "Confirm" button to complete the operation.


<span id="TxngLf54"></span>
## Terminate migration task

If you do not wish for the job to continue, you can terminate Migration Jobs that are **inmigration**, **Incrementing**, and **Abnormal** status.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Once the migration task is terminated, it cannot be restarted or resumed, and the associated migration source will be taken offline. If you need to migrate data from the same source server again, refer to <a href="https://docs.byteplus.com/en/docs/smc/Getting-Started">Quick start</a> to import the migration source again and create a new migration task.</div>


* <div data-tips="true" data-tips-type="warning">Since terminating a task in <strong>Abnormal</strong> status involves exception handling, the operation is estimated to take 5 minutes. Please be patient.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

3. In the top navigation bar, select the project to which the target task belongs.

4. Click the "... \> Terminate" button in the Actions column to the right of the target task.

5. After you confirm the task information displayed on the prompt page, click the "Confirm" button to complete the operation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d953c2cdcde517842c47752539932f9a.png) </span>

5. After termination succeeds, refer to [Clearing task resources](https://docs.byteplus.com/en/docs/smc/Clean-up-task-resources) to clear the temporary resources generated by the migration task.


<span id="m9Jk5vRY"></span>
## Delete migration task

You can delete migration tasks that are no longer used or do not need to be displayed, and you can also delete temporary resources created during the execution of the tasks.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only migration tasks in <strong>Success</strong>, <strong>Fail</strong>, or <strong>Terminate</strong> status can be deleted.</div>


* <div data-tips="true" data-tips-type="tip">To delete a task in <strong>Paused</strong> status, <a href="https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs#TxngLf54">terminate it</a> first and then proceed with deletion.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left directory tree under any region, select "Server Migration Center \> Migration Job".

2. In the top navigation bar, select the project to which the target task belongs.

3. Click the "... \> Delete" button in the Actions column of the target migration source.

4. On the deletion confirmation page, check the cloud resources you need to release along with the task, and click the "Delete" button to complete the operation.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The resource release operation is irreversible. Please make sure that releasing related resources will not affect your normal business operations.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6af7e08d7c12abfbcc241195aee2f54a.png) </span>
