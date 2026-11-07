---
title: "Deleting or canceling application update tasks"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deleting_or_canceling_application_update_tasks"
---

You can cancel or delete an application update task based on your needs:


* **Cancel**: Cancel a task that is in the **Running** state to terminate its ongoing execution. Cancelled tasks cannot be re\-executed. Proceed with caution.

* **Delete**: Delete a task that is not in the **Running** state. After a task is deleted, you cannot view the execution records of the task but the operation of related services will not be affected. Deleted tasks cannot be recovered. Proceed with caution.


<span id="LKw1rWm0"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. On the "CloudOps Orchestration" page, click the "Common O&M tasks" tab and select "App update".

5. In the "Actions" column of the target task, click the "Cancel" or "Delete" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the task state is not <strong>Running</strong>, the task cannot be canceled. That is, the "Cancel" button is not displayed.   </div>
   

7. After you confirm that the information of the task to be canceled or deleted is correct, click the "Confirm" button to complete the operation.
