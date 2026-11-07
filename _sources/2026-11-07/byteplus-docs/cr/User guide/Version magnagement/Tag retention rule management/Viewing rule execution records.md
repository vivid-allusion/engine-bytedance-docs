---
title: "Viewing rule execution records"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/view-execution-records-of-a-tag-retention-rule"
---

This topic describes how to view the execution records of a tag retention rule.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Procedure


1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Tag retention**.

4. Click the name of the target rule.

5. View execution task information.

   
   |Parameter |Name |
   |---|---|
   |Task ID |ID of the tag retention rule task. Click an ID to view details of image cleanup. |
   |Execution status |The execution status. Currently supported statuses:<br><br><br>* **Waiting**: The task has been triggered, but the previous task has not been completed. After the previous task is completed, the status changes to **In progress**.<br><br>* **In progress**: The image cleanup task is in progress.<br><br>* **Success**: The task is completed. You can click the task ID to view image cleanup details.<br><br>* **Fail**: The task execution failed. Troubleshoot based on the error message or [submit a work order](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000208). |
   |Execution progress |The progress of image cleanup, which is displayed as **the number of successful cleanups/total cleanups**. |
   |Execution method |The rule execution method.<br><br><br>* Manual trigger: The task will be executed immediately after you manually trigger the rule. You can execute the task by selecting the **Execute** action in the console.<br><br>* Timed trigger: The task is executed at a scheduled time. |
   

6. Click the ID of the target execution task to view information about retained or cleared images.
