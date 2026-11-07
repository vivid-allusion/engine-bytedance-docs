---
title: "Creating lifecycle hooks"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Creating-a-lifecycle-hook"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

This topic describes how to create a lifecycle hook used to suspend target instances in a scaling group during automatic scaling operations, enabling you to perform required custom actions.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Lifecycle hook" tab.

4. Click the "Create Lifecycle Hook" button and configure the parameters based on the table below.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Name |The name of the lifecycle hook. Name changes are not supported after the lifecycle hook is created. |we01 |
   |Scaling Rule Type |Lifecycle hooks are triggered when scaling groups automatically perform scale\-in and scale\-out operations. |Scale\-in Event |
   |Timeout |The duration an instance remains in the suspended status. After the hook times out, the suspended status ends automatically, and the scaling operations continue based on the execution policy.<br><br>After you evaluate the execution time of your custom actions, set an appropriate timeout period. Value range: 30 seconds to 21600 seconds (6 hours). |1800s |
   |Execution Policy |Select the operation to be performed after an instance exits from the suspended state. Supported options include "Continue", "Reject", and "Roll back". For a detailed introduction to the instance\-targeted process after execution, refer to [Execution processes and policies](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl). |Continue |
   |The action of associating a hook |Configure whether to perform custom operations on multiple instances in the suspended status via Cloud assistant. With Cloud assistant enabled, O&M commands can be easily executed, which applies to scenarios where instances need to be added or removed in batches.<br><br><br>* Before enabling Cloud assistant, you need to first create the required O&M commands and confirm that the related instances have Cloud assistant Agent installed. For detailed operations, refer to [Introduction to associating lifecycle hooks with Cloud assistant](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.55u45YWz5Yqf6IO9). |Cloud assistant |
   |Parameter​ |This parameter needs to be configured only when the action of associating a hook is "Cloud assistant". Select the required Cloud assistant command and enter values for the command parameters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The operation duration of Cloud assistant depends on the command you select. We recommend setting the hook timeout period longer than the command execution time. Otherwise, the lifecycle hook may time out before the command execution completes, which may impact your business.</div><br> |\-\- |
   

5. Click "Confirm" to complete the operation.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After the lifecycle hook is triggered for a scaling group, select the "Instance Management" tab. Then, you can see that the corresponding instance changes to the "Adding/removal suspended" status. At this point, you can log in to the instance to perform custom operations.

When Cloud assistant is enabled for command execution, you can view the command execution result in the ECS console. For details, refer to [Viewing job execution results](https://docs.byteplus.com/en/docs/ecs/View-job-execution-results).


* If the command is executed before the lifecycle hook times out, the suspended status of instances ends immediately, and the scaling operation continues based on the "Continue" policy.

* If the command execution times out or fails before the lifecycle hook times out, the suspended status of instances ends immediately, and the scaling operation continues based on the execution policy of the lifecycle hook.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[CreateLifecycleHook](https://docs.byteplus.com/en/docs/as/CreateLifecycleHook)
