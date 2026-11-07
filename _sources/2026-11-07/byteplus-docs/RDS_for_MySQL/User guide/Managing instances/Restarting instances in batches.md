---
title: "Restarting instances in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_instances_in_batches"
---

RDS for MySQL supports a batch restart function, allowing you to restart multiple instances simultaneously when they experience full connections or performance problems. This topic describes how to batch restart instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* An instance restart will cause connection interruptions. Plan your business operations accordingly before restarting. Restart instances during off\-peak hours and ensure your application has an automatic reconnection mechanism.

* A maximum of 100 instances can be restarted at the same time.

* When instances are batch restarted, you cannot restart read\-only nodes separately.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. On the **Instances** page, select multiple target instances.

4. Click **Restart instance** in the lower\-left of the **Instances** page.

5. In the **Confirm restart of selected instances** dialog box, confirm the instance summary, complete the following configurations, and click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Force restart<br><br> |Select whether to enable force restart. When force restart is disabled, the restart may take an extended time or even fail due to factors like high replication latency. When force restart is enabled, the system restarts quickly, which might cause data loss or service interruption. Confirm that you can accept the risk.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Single node instances only support force restart. If a single\-node instance is included in the selected batch instances, force restart cannot be disabled.</div><br> |
   |Restart database proxy<br><br> |Select whether to restart the database proxy. If you choose not to restart, connections will not be interrupted when connection persistence is enabled and the session meets the [conditions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_connection_persistence).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This can be configured only when the database proxy is enabled for the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If some instances in the batch do not have database proxy enabled, this option is ignored for those instances.</div><br> |
   

6. In the pop\-up **Batch cancel** dialog box, view **Task progress**, and click **OK** after all tasks are completed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can click the <strong>Terminate</strong> button in the <strong>Batch cancel</strong> dialog box, and the task of the instance that has not started changing after termination will no longer proceed and cannot be resumed. If you want to make changes again, you need to re\-initiate the batch task.</div>


* <div data-tips="true" data-tips-type="tip">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason.</div>
