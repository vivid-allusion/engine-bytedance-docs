---
title: "GPU defragmentation rule settings"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/GPU_defragmentation_rule_settings"
---

The queue administrator can set "GPU fragmentation resourcing rules" within the queue, which are designed to optimize the placement of GPU load from the resource group dimension, clean up the load that causes GPU fragmentation, and relieve queue queuing. Configure the content according to the user's rules, and the platform will perform GPU defragmentation when it detects that the task is in a queued state for a long time or within a fixed defragmentation cycle to improve GPU resource utilization.

**Scenario 1** An existing user has 3 8\-card machines. The current load situation of the user's three machines is [7 cards (4 + 2 + 1), 6 cards (4 + 2), and 7 cards (4 + 2 + 1) ]. At this time, the user wants to submit a 4\-card task, which will not run due to fragmentation.

**Scenario 2** A user now has eight 8\-card machines. The user schedules seven services, each with nine instances and one card per instance. This way, instances of each service are distributed across different machines, causing fragmentation to occur once users destroy certain services.

After activating the current rules, the fragmentation situation will be recognized by the platform. For example, in **scenario 1** , the platform will reposition the load, place the 1 and 2 card loads of the third machine on the other two machines, and the third machine can run the 4 card task.

<span id="使用前提"></span>
## **Premise of use**


* Owns one or more queues and is a queue administrator.


<span id="注意事项"></span>
## Precautions


* The platform\-supported defragmentation strategy is only effective for GPU resources, and the resource fragmentation phenomenon caused by the CPU cannot be handled temporarily.

* If the GPU load hitting the current rule causes fragmentation, it may be stopped by the platform.

* Queue rule changes take effect on the historical load in the queue. It is recommended to configure the rule immediately after creating the queue, and it is not recommended to change the rule frequently. Please notify the users of the queue in time after changing the rule, so as not to affect the operation of the historical load.

   * Or based on the above **scenario a** , if the user submits a 4 card GPU task queue rule has not been opened when, the load of the third machine will not be affected. At some point, the queue administrator starts the GPU collation rules for custom tasks, and the corresponding load may hit the rules and be stopped.


<span id="操作步骤"></span>
## **Procedure**


1. Log in to the Machine Learning Platform and click [Resource Group Management] \- [Queue] in the left navigation bar to enter the list page.

2. Click the queue name to enter the details page, click [Rule Settings], and turn on the "GPU Fragmentation Resource Decoration Rules" switch to configure the rules.

3. The rule configuration includes rule settings for both [inference services] and [custom tasks] payloads. The specific parameters are as follows:



|rule configuration |Description |
|---|---|
|sorting task type |Which tasks will hit the rules?<br><br><br>* All instances in "inference services": To ensure continuity of services, the platform starts new instances and deletes old ones after ensuring their stability. To reduce possible request interruptions during migration, it is recommended to configure a "graceful shutdown time" and implement this mechanism in your code.<br><br>* "Custom tasks" using idle resources: After checking, if the "Use idle resources" switch is turned on when the task is submitted by the current queue, the task may be stopped by hitting the current rule.<br><br>* Turn on "custom tasks" with automatic retry: After checking, if the "automatic retry" switch is turned on when the task is submitted by the current queue, the task may be stopped by hitting the current rule. |
|sorting strategy |* Optional rules:<br><br>   * "When a task in the queue is queued for a long time": When it is detected that such a task in the queue is queued for a long time, the defragmentation strategy for resources is automatically triggered immediately.<br><br>   * "Regular sorting": Users can configure the "execution time" of "inference services" according to their own business characteristics according to the cron statement. The platform will regularly execute the defragmentation rules according to the configured time. The check period for "custom tasks" defaults to half an hour.<br><br>* How are stopped tasks that hit a rule affected?<br><br>   * If a task is submitted with the "Auto Retry" switch turned on, it will be automatically resubmitted after it is stopped. In this case, there will be both old and new tasks with the same name in the task list.<br><br>   * The task Timeline will record the reason for stopping the task, as well as the task link automatically resubmitted by the platform. Tasks submitted automatically by the platform do not consume retries. |



* The cron statement is configured by minute, hour, date, month, and week, with a total of five parameters, allowing you to set a specific execution time for the task. The specific parameter configuration is shown in the following table:



|Parameter |Parameter Description |
|---|---|
|points |Represents minutes in execution time. Supports entering numbers between 0 and 59, and entering \* means matching any value, using the "," enumeration. |
|time |Represents the hour in the execution time. Supports entering numbers between 0 and 23, and entering \* means matching any value, using the "," enumeration. |
|day |Represents the date in the execution time. Supports entering numbers between 1 and 31, and entering \* means matching any value, using the "," enumeration. |
|month |Represents the month in the execution time. Supports entering numbers between 1 and 12, and entering \* means matching any value, using the "," enumeration. |
|week |Represents the week in the execution time. Supports entering numbers between 0 and 6, with 0 representing Sunday and \* matching any value, using the "," enumeration. |



* Error Message



|Cron statement |execution time |
|---|---|
|0 \* \* \* \* |Execute the strategy every hour. |
|0 0 \* \* \* |Execute the strategy at 00:00 every day. |
|0 0 \* \* 0 |Strategies are executed every Sunday at 00:00. |
|0 0 1,2 \* \* |Execute the strategy at 00:00 on the 1st and 2nd of each month. |
|0 12 \* \* \* |Execute the strategy at 12:00 every day. |



4. You can quickly view the configured rules for the current queue in the Queue Rules field on the Queue List page.
