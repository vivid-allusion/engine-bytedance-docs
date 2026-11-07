---
title: "Creating warm-up tasks"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Creating-warm-up-tasks"
---

The TOS accelerator enables asynchronous warm\-up, pre\-caching relevant data within the acceleration scope. The next time the data is accessed, it loads faster. This topic introduces notes and steps for creating warm\-up tasks.

<span id="bc1b6931"></span>
## Notes


* Warm\-up tasks only cache data within the acceleration scope.

* Warm\-up tasks run for at least 15 minutes. Larger data volumes require more time to execute. Thank you for your patience.

* Warm\-up tasks use some of the accelerator’s read bandwidth. The warm\-up bandwidth is determined by the formula: Min{TOS accelerator bandwidth − Actual read request bandwidth, TOS accelerator bandwidth × 10%}. If the accelerator's bandwidth utilization is high, some objects may not be pre\-cached.


<span id="c4107c6f"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **TOS accelerator**.

3. On the **TOS accelerator** page, click the accelerator you want to manage.

4. On the accelerator details page, click the **warm\-up task** tab, and then click **Create warm\-up task**.

5. In the **New warm\-up task** dialog, configure the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |Destination |The name of your accelerator is displayed by default. |
   |Source |Set the path for the data to be pre\-cached. Requirements:<br><br><br>* You can only select a path that is configured for the acceleration strategy.<br><br>* You can add up to 10 paths. |
   |Description |The description for the warm\-up task. |
   |Execute immediately |Choose whether to run the warm\-up task right after it has been successfully created. |
   

6. Once you have finished configuring, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After creating a warm\-up task, you can view its status in the warm\-up task list. The task statuses are explained below.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Idle</strong>: The task has not started or has finished.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Executing</strong>: The task is in progress.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Stopping</strong>: The task is exiting from the executing state.   </div>
   

   ## Related operations     <span id=".55u45YWz5pON5L2c"></span>

   
   |**Category** |**Steps** |
   |---|---|
   |Start a warm\-up task |On the accelerator details page, go to the **warm\-up task** tab and click **Start** in the **Actions** column of the task you want to start. |
   |Stop a warm\-up task |On the accelerator details page, go to the **warm\-up task** tab and click **Stop** in the **Actions** column of the task you want to stop. |
   |Modify a warm\-up task |On the accelerator details page, go to the **warm\-up task** tab. Then, click **Modify** in the **Actions** column of the task you want to adjust. In the **Edit warm\-up task** dialog, modify the parameters as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only modify a warm\-up task when its status is idle.</div><br> |
   |Delete a warm\-up task |On the accelerator details page, go to the **warm\-up task** tab. Click **Delete** in the **Actions** column of the task you want to remove. Then, confirm the deletion by clicking **Delete** in the box that appears.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only delete a warm\-up task when its status is idle.</div><br> |
   |View task history |On the accelerator details page, go to the **warm\-up task** tab. Click **historical record** in the **Actions** column of the task you want to check. Then, view the task history in the box that appears. |
