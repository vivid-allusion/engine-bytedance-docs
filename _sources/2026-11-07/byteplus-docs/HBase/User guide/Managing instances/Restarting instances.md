---
title: "Restarting instances"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Restarting_instances"
---

You can release all connections by restarting the HBase instance to resolve database connection or performance issues. This article describes how to restart the HBase instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The instance must be in the **Running** state.

* Some services may be unavailable during restart. Proceed with caution.

* It is recommended to restart the instance during off\-peak business hours and ensure that the business has a reconnection mechanism.

* A maximum of 100 instances can be selected for batch restart at the same time.


<span id=".6YeN5ZCv5Y2V5Liq5a6e5L6L"></span>
## Restart a single instance


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance** page, find the target instance and click **Restart instance** in the **Actions** column.

4. In the dialog box that pops up, confirm the instance information (such as instance ID, name, etc.) and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the instance status changes from <strong>Restarting</strong> to <strong>Running</strong>, it means the restart is successful and the database can now provide external services.   </div>
   

<span id=".5om56YeP6YeN5ZCv5a6e5L6L"></span>
## Batch restart instance


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, select multiple target instances.

4. Click **Restart instance** at the bottom of the **Instance list** page.

5. Confirm the instance information in the **Confirm restart of selected instance** pop\-up dialog box. After confirming that it is correct, click **OK**.

6. In the pop\-up **Batch tasks have been initiated** dialog box, view **Task progress**, and click **OK** after a task is completed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click the <strong>Terminate</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, tasks for instances that have not started to restart will no longer be performed and cannot be resumed. If you want to restart again, you need to initiate the restart task again.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[RestartDBInstance](https://docs.byteplus.com/en/docs/HBase/RestartDBInstance) |Call the RestartDBInstance interface to restart the instance. |
