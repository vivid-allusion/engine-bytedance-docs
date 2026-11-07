---
title: "Creating temporary bandwidth upgrade tasks"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_a_temporary_bandwidth_upgrade_task"
---

You can use the orchestration feature to batch upgrade the temporary bandwidth of [Subscription](https://docs.byteplus.com/en/docs/ecs/Subscription) EIPs. This way, you can handle traffic peaks (during holidays, promotions, and other periods), thereby supporting the stable operation of your business while saving bandwidth costs during off\-peak hours.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact your account manager.</div>


<span id=".5qaC5b-1"></span>
## Concept


|Concept |Description |
|---|---|
|Temporary bandwidth upgrade |Temporarily increase the bandwidth upper limit of an EIP for a specific period to meet sudden business growth or temporary high traffic requirements. The bandwidth upper limit automatically reverts to its original value when the period ends. |
|Security block |A security measure that restricts the access to or usage of an EIP, implemented to safeguard network security and prevent the continuation of illegal or malicious activities. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have completed [preparations](https://docs.byteplus.com/en/docs/ecs/Preparation).

* The EIP pending temporary bandwidth upgrade is associated with an instance. For more information, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Limits |Description |
|---|---|
|EIP |Temporary bandwidth upgrades are only supported for Subscription EIPs. |
||Subscription EIPs in the blocked status do not support temporary bandwidth upgrade. |
|Time |The minimum duration for a temporary bandwidth upgrade is 1 hour, and the maximum duration is 720 hours (30 days). |
||When you upgrade the bandwidth of an EIP that is currently undergoing a temporary bandwidth upgrade, the new bandwidth upper limit cannot be lower than the current bandwidth upper limit, and the new restoration time (execution start time plus duration) must be later than the current restoration time (execution start time plus duration).<br><br>For example, if the restoration time for the first temporary bandwidth upgrade of an EIP is June 20, then the earliest restoration time for the second temporary bandwidth upgrade is June 21. |


<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


|Temporary bandwidth upgrade phase |Description |
|---|---|
|Before the upgrade |For fee changes related to temporary bandwidth upgrades. |
|Upgrading |You cannot decrease the bandwidth upper limit for an EIP undergoing a temporary bandwidth upgrade. We recommend that you specify an appropriate bandwidth upper limit before you initiate a temporary bandwidth upgrade. |
||EIPs undergoing a temporary bandwidth upgrade cannot be unsubscribed. If you want to unsubscribe an EIP of this type, you need to wait until the restoration time is reached and all [unsubscription rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management) are satisfied. |
|After the upgrade |When the temporary bandwidth upgrade expires, the bandwidth upper limit is automatically restored. This may disrupt business traffic transmission and cause packet loss. Evaluate the potential impact on your business and proceed with caution. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. On the "CloudOps Orchestration" page, click the "Common tasks" tab.

5. Click the "Temporary upgrade of bandwidth" menu.

6. Click the "Create task" button and configure the parameters described in the following table.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Select resource** |||
   |Resource scope |The type of resource on which you want to execute the O&M command. The default value is "EIP". |EIP |
   |Select Elastic IP (EIP) |Select EIPs that are eligible for batch operations based on information such as EIP name or ID, and association status. You can select multiple EIPs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select up to 100 EIPs at the same time.</div><br> |\- |
   |**Argument settings** |||
   |Execution mode |Supported task execution modes:<br><br><br>* **Execute immediately**: After the job is created, it is executed for one time immediately.<br><br>* **Timed execution**: The task is executed automatically once at the time you specify.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The execution time must be accurate to the minute and can not be earlier than the current time.   </div><br>   <br><br>* **Periodic execution (default)** : The task is executed automatically on a cycle starting from the specified start time, at intervals you specify (in minutes, hours, or days), and stops automatically at the specified end time. You need to configure the following information:<br><br>   * **Repeat cycle**: Specify the interval at which the job is executed repeatedly. The repeat interval must be longer than the timeout period. Value:<br><br>      * by minute: The minimum interval is 5 minutes.<br><br>      * by hour: The minimum interval is 1 hour.<br><br>      * by day: The minimum interval is 1 day.<br><br>   * **Start time**: Specify the time when the periodic job is first executed. This time must be later than the current time.<br><br>   * **Stop time**: Specify the time when the periodic task stops. The task automatically stops at this time.<br><br>      * If the task is not being executed at the stop time, it automatically stops and will never be executed again.<br><br>      * If the job is being executed at the stop time, it automatically stops after the execution is complete and will never be executed again.<br><br>      * If the interval between the stop time and the start time is less than one repeat cycle, the task is executed only once.<br><br>   * **Time zone**: Fixed to `GMT +08:00` (China Standard Time).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The execution interval is independent of the actual execution duration of the task and is calculated based on the "Start time" you specify. For example, if the start time for a job is <code>2022-12-20 11:00:00</code>, the repeat cycle is 1 hour, and the duration of the first execution is 3 minutes, the second execution starts at <code>2022-12-20 12:00:00</code>.   </div><br>    |Execute immediately |
   |Duration |Select the duration for temporary bandwidth. The valid duration ranges from 1 to 720 hours. The default duration is 4 hours. |4 hours |
   |Maximum bandwidth |Select the bandwidth upper limit for the EIP in the temporary upgrade. The valid upper limit ranges from 1 to 1,000 Mbps. The default upper limit is 100 Mbps. |100Mbps |
   |**Concurrency control** |||
   |Concurrency rate |* Specify the number of concurrent executions for a batch instance task, which refers to the maximum number of instances that can undergo operations or receive requests at the same time. For example, if you have 50 instances and set this parameter to 10, the task will be executed in 5 batches, and commands will be sent to 10 instances simultaneously in each batch.<br><br>* Value range: 1\-100. |10 |
   |Maximum error count |Specify the maximum number or percent of errors allowed while executing a temporary bandwidth upgrade task within a specific operation or scope.<br><br><br>* **Error count:**  Applicable to scenarios where the error count needs attention. Value range: 0\-100.<br><br>   * If the error count is set to 0, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the error count is set to 100, a maximum of 100 errors is allowed. That is, as long as the number of errors during the execution of a task does not exceed 100, the task will succeed, but if errors exceed 100 before the task is completed, the entire task will stop (fail).<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual number of failures across all batches of the task is less than or equal to the maximum number of errors you specify.      </div><br>      <br><br>* **Percent: ** Applicable to scenarios where the impact of errors on the entire task needs attention. Value range: 0\-100%.<br><br>   * If the maximum error percent is set to 0%, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the maximum error percent is set to 100%, the task will succeed regardless of the number of errors.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual failure rate (percentage of failed instances) across all batches of the task is less than or equal to the maximum error rate (percentage) you specify.      </div><br>       |Error quantity: 1<br><br> |
   |**Relevant Information** |||
   |Project |You can add the cloud assistant to the project and manage it in the project dimension, which helps maintain resource independence and data security. For more information about projects, see [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |default |
   |Tag |A tag is a key\-value pair used to identify resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to easily search and aggregate your resources. For more information about tags, see [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key1:Value1 |
   

7. Click "Create" to complete the actions.

8. After you confirm that the configuration information is correct, click the "Confirm" button to complete the operation.

   > The selected task is executed on the selected EIPs, which has a wide\-ranging impact. Confirm that all information is correct before you submit the request.   
   

<span id=".5ZCO57ut5q2l6aqk"></span>
### Subsequent steps


* After the task is created, the system automatically redirects to the temporary bandwidth upgrade tasks page and starts executing the task according to the specified execution method and execution time.

* After a task is created, the bills related to the task are automatically settled by using the subscription billing method. You can go to the [Billing center](https://docs.byteplus.com/en/docs/byteplus-platform/docs-viewing-all-orders) to view the bills. For more information, see [Subscription billing method](https://docs.byteplus.com/en/docs/ecs/Subscription).
