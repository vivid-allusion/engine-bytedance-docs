---
title: "Creating tasks for batch instance operations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task"
---

You can create a task for batch instance operations to perform the same operation on multiple ECS instances at the same time. The operations include command delivery, file downloading, instance operations, and attribute modification.


* Command delivery: Execute relevant commands inside the instance by delivering scripts. For example, you can execute a specific command to view the IP address.

* File downloading: Download multiple target files at the same time to the specified instance.

* Instance operations: Perform O&M operations on instances, including starting, stopping, and restarting instances, and changing the operating system.

* Attribute modification: Modify the attributes of instances, including the instance names, hostnames, and descriptions.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

You have completed [preparations](https://docs.byteplus.com/en/docs/ecs/Preparation).

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. On the "CloudOps Orchestration" page, click the "Common tasks" tab.

5. Click the "Create task" button, refer to the table below, and select the task type and instances.

   
   <Tabs>
   <Tab zoneid="b8SbeAyZTf" title="Run command">
   <TabTitle>Run command</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">The instances must be in the <strong>Running</strong> status.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Cloud assistant client is installed. For operation details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">Installing cloud assistant Agent</a>.</div>
   
   
   
   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of O&M command that you want to execute. |Run command |
   |Command type |Select the type of O&M command that you want to execute. Valid values: Linux Shell, Python, Windows Bat, and Windows PowerShell. |Linux Shell |
   |Command contents |Enter a specific command according to your business requirements. This way, an O&M task is created to execute the command you enter. |\- |
   |Execute path |Enter the command execution path.<br><br><br>* For Linux instances, the default path is "/home".<br><br>* For Windows instances, the default path is "C:/Windows/System32". |/home |
   |Execute user |Specify a user that exists in an instance to execute commands to reduce security risks.<br><br><br>* The default user to execute commands is root in Linux.<br><br>* The default user to execute commands is system in Windows. |root |
   |**Select instances** |||
   |Select instances |Determine target (ECS) instances that meet the batch execution requirements using information such as instance name/ID, running status, and cloud assistant installation status, supporting the selection of multiple instances.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Instances without cloud assistant installed do not support batch execution. Please first <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">install the cloud assistant Agent</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can select up to 500 ECS instances.</div><br> |\- |
   
   
   
   </Tab>
   <Tab zoneid="oFvcJhbrQd" title="Download a file">
   <TabTitle>Download a file</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">The instances must be in the <strong>Running</strong> status.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Only one file can be uploaded per task.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Cloud assistant Agent installed, view operating details in <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">Install the cloud assistant Agent</a>.</div>
   
   
   
   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of O&M command that you want to execute. |Download a file |
   |File type |Default is HTTPS file, modification is not supported. |Retain the default value. |
   |File link |Fill in the link to the file to be downloaded, which is the link to the remote file accessed securely via the HTTPS protocol.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The maximum length of a file link is 2,000 characters.</div><br> |https://xx/xx or http://xx/xx |
   |File save path |Fill in the storage path after the file is downloaded, which is the complete path where the file is stored on the target ECS instance. |/root/testxx |
   |**Advanced settings** |||
   |File owner |Optional. The user to which the file belongs after the file is uploaded. |\- |
   |File group |Optional. The user group to which the file belongs after the file is uploaded. |\- |
   |File permissions |Optional. The permission on the file after the file is uploaded. For example, if you set this parameter to 644, the owner has read and write permission on the file, and users in the same group and public users have read\-only permission on the file. |644 |
   |Override the existing file |Select whether the downloaded file overwrites the existing file. By default, the downloaded file overwrites the existing file. |Default configuration |
   |**Select instances** |||
   |Select instances |Determine target (ECS) instances that meet the batch execution requirements using information such as instance name/ID, running status, and cloud assistant installation status, supporting the selection of multiple instances.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Instances without cloud assistant installed do not support batch execution. Please first <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">install the cloud assistant Agent</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can select up to 500 ECS instances.</div><br> |\- |
   
   
   
   </Tab>
   <Tab zoneid="Be1DI8F071" title="Instance actions">
   <TabTitle>Instance actions</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default"><strong>Start</strong>: Only instances in the <strong>stopped</strong> status can be started.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Stop: Only instances in the <strong>running</strong> status can be stopped.</div>
   
   
   * <div data-tips="true" data-tips-type="default"><strong>Restart</strong>: Only instances in the <strong>Running</strong> status can be restarted.</div>
   
   
   * <div data-tips="true" data-tips-type="default"><strong>Replace the operating system</strong> After you change the operating system, the system volume ID is changed, and the original system volume data is cleared and released. This operation is irreversible. Proceed with caution. For more usage limits, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Changing-OS#.5pON5L2c6K-05piO">Precautions</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Cloud assistant Agent installed, view operating details in <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">Install the cloud assistant Agent</a>.</div>
   
   
   
   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of task for which you want to execute O&M commands. |Instance actions |
   |Action type |Select the type of operation you want to perform. Valid values:<br><br><br>* **Start**: Start the instances in the **Stopped** status.<br><br>* **Stop**: Stop the instances in the **Running** status. The stop methods include "Stop" and "Forced stop". The stop modes include "Normal Mode" and "Economical Mode". For information about stop modes, see [Stop modes](https://docs.byteplus.com/en/docs/ecs/Stopping-instances#.5YGc5q2i5qih5byP).<br><br>   * Stop: the default and regular method that follows the standard procedure for stopping ECS instances.<br><br>   * Forced stop: The running ECS instances are forced to stop, which is equivalent to a power\-off operation.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you perform a forced stop on instances other than bare metal instances, all cache data that has not been written to the storage devices is lost. We recommend that you do not perform this operation on instances that are running as expected.      </div><br>      <br><br>* **Restart**: Restart the instances that are in the **Running** status.<br><br>   * Restart: the default and standard restart mode.<br><br>   * Forced restart: Forcibly power off the running instance and then restart it.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">For instances other than bare metal instances, performing a forced restart will result in the loss of all cached data not stored to storage devices to be lost. Therefore, we recommend against performing this operation on instances running normally.      </div><br>      <br><br>* **Replace the operating system**: This operation restores the instances to the initial status and is commonly used to recover instances from system failures. For more information, see [Changing operating systems](https://docs.byteplus.com/en/docs/ecs/Changing-OS).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend that you change operating systems for instances in the <strong>Stopped</strong> status. Otherwise, data that is being written may be lost. If your instances are not in the Stopped status, stop the instances. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Stopping-instances">Stopping instances</a>.   </div><br>    |Start |
   |**Select instances** |||
   |Select instances |Determine target ECS instances that meet batch operation requirements based on information such as instance name or ID, and running status. You can select multiple instances at the same time.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select up to 500 ECS instances.</div><br> |\- |
   
   
   
   </Tab>
   <Tab zoneid="NUHLAtGemx" title="Attribute modification">
   <TabTitle>Attribute modification</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">Only instances whose status is <strong>Running</strong> or <strong>Stopped</strong> support attribute modification.</div>
   
   
   * <div data-tips="true" data-tips-type="default">If the instance status is <strong>Running</strong>, changing the hostname automatically restarts the instances.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Instances created using CentOS 6.9/6.10 or Ubuntu 14.04 do not support hostname changes.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Cloud assistant Agent installed, view operating details in <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">Install the cloud assistant Agent</a>.</div>
   
   
   
   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of task for which you want to execute O&M commands. |Attribute modification |
   |Select instances |Determine target ECS instances that meet batch operation requirements based on information such as instance name or ID, and running status. You can select multiple instances.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select up to 500 ECS instances for a task.</div><br> |\- |
   |**Modify attributes** |||
   |Edit |Modify attributes of a single instance, including the instance name, hostname, and description. Specific steps are as follows:<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Hostname: The hostname is the computer name within the instance operating system and is used to identify the computer on the network.</div><br><br><br><br>1. Click the target instance.<br><br>2. Select the attribute to modify, and click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e81823b0ee4069426fd0a94281a42e26.png) </span> icon to modify the attribute. For more information, see [Naming rules for instances or hosts](https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames).<br><br>3. After you modify the attribute, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_db7fc7bed34063b7afd50b0c87fd8e79.png) </span> icon to save the modification. |\- |
   |Copy All |Use the name, hostname, or description of an instance as a template to modify the attributes of all selected instances at the same time. The attributes include the instance name, hostname, and description. Perform the following steps:<br><br><br>1. After you select an instance, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_403dc4928ec49d911ddc0d61dcfa6764.png) </span> icon in the corresponding attribute column.<br><br>2. Click the "Copy All" button to save your modification. ||
   |Copy up/Copy down |Use the name, hostname, or description attribute of an instance as a template to modify this attribute for all instances above or below this instance at the same time. Specific steps are as follows:<br><br><br>1. After you select the target instance, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76eccec8c178d92ccf910b343862d1f5.png) </span> icon in the "Image type" column of the instance.<br><br>2. Click the "Copy up" or "Copy down" button to save your modification. ||
   
   
   
   </Tab>
   </Tabs>
   

6. Refer to the table below, configure concurrency control and related information.

   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |**Concurrency control** |||
   |Concurrency rate |* Specify the number of concurrent executions for a batch instance task, which refers to the maximum number of instances that can undergo operations or receive requests at the same time. For example, if you have 50 instances and set this parameter to 10, the task will be executed in 5 batches, and commands will be sent to 10 instances simultaneously in each batch.<br><br>* Value range: 1\-100. |10 |
   |Maximum error count |Specifies the maximum number or percent of errors allowed when executing a batch instance task within a specific operation or range.<br><br><br>* **Error count:**  Generally applies to scenarios where the error count needs attention, and the value range is 0\-100.<br><br>   * If the error count is set to 0, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the error count is set to 100, a maximum of 100 errors is allowed. That is, as long as the number of errors during the execution of a task does not exceed 100, the task will succeed, but if errors exceed 100 before the task is completed, the entire task will stop (fail).<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual number of failures across all batches of the task is less than or equal to the maximum number of errors you specify.      </div><br>      <br><br>* **Percent: ** Applicable to scenarios where the impact of errors on the entire task needs attention. Value range: 0\-100%.<br><br>   * If the maximum error percent is set to 0%, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the maximum error percent is set to 100%, the task will succeed regardless of the number of errors.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual failure rate (percentage of failed instances) across all batches of the task is less than or equal to the maximum error rate (percentage) you specify.      </div><br>       |Error quantity: 1<br><br> |
   |**Relevant Information** |||
   |Project |You can add the cloud assistant to the project and manage it uniformly by project dimension, which helps maintain resource independence and ensure data security. For more information about projects, see [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |default |
   |Tag |A tag is a key\-value pair used to identify resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your resources. For more information about tags, see [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key1:Value1 |
   

7. Click "Create".

8. After you confirm that the configuration information is correct, click the "Confirm" button to start task execution.

   > The selected task is executed on the selected instances, which has a wide\-ranging impact. Confirm that all information is correct before you submit the request.   
   

   <span id="TYkWXyDa"></span>
   ## Related documents

   You can also perform the following actions on the Instances page:

   * [Batch Send remote commands](https://docs.byteplus.com/en/docs/ecs/Batch_send_remote_commands)

   * [Downloading files to multiple instances](https://docs.byteplus.com/en/docs/ecs/Download_files_to_multiple_instances)

   * [Batch change instance attributes](https://docs.byteplus.com/en/docs/ecs/Changing-the-hostname-of-an-instance)
