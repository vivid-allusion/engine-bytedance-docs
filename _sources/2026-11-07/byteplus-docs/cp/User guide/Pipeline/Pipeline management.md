---
title: "Pipeline management"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_management"
---

After you create a pipeline, you can manage it. This article introduces pipeline management operations.

<span id=".5rWB5rC057q_5YiX6KGo"></span>
## Pipelines

The pipeline list displays all pipelines under the current workspace.


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace**.

3. Click the name of the target workspace to switch to it.

4. Select **pipeline** in the left navigation bar, and enter the pipeline page.

   The pipeline list displays all pipelines under the current workspace by default. In addition to basic information such as name and recent run status, the **recent run record** column displays in detail the sequence number of the most recent run record for the current pipeline, the trigger method, the code branch used, the run time, and other details.

   
   |Serial number |Feature introduction |
   |---|---|
   |1 |Toggle display of the **all pipelines** list and the **favorite pipelines** list. |
   |2 |Display pipeline group information. You can switch between groups to display their pipelines. Among these, **Ungrouped** is a system preset group and does not support renaming or deletion. |
   |3 |Toggle display **Runnable**/**Draft**/**List of all pipelines.**  |
   |4 |Fuzzy search pipelines by name |
   |5 |Refresh the pipeline list. |
   


<span id=".5pS26JeP5rWB5rC057q_"></span>
## Favorite pipelines

With the favorites feature, you can add key pipelines to your favorites list to make them easier to find.


1. In the pipeline list, select the target pipeline, click the favorite icon in the Actions column, and add the current pipeline to the favorites list.


<span id=".57yW6L6R5rWB5rC057q_"></span>
## Edit a pipeline

Supports modification of the pipeline's basic information, process orchestrations, triggers, variables, cache directories, notification reminders, and other related content.


1. Select the target pipeline in the pipeline list, and click  **`...`**   **\> Edit**, go to the process orchestration tab of the current pipeline.

2. Edit each parameter as needed. For detailed information, please refer to [create pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

3. Click **Save** to complete pipeline editing.


<span id=".5aSN5Yi25rWB5rC057q_"></span>
## Copy a pipeline

By using the pipeline copy feature, you can quickly create a new pipeline by making modifications based on the target pipeline.


1. In the pipeline list, select the target pipeline, and click the **Actions** column's  **`...`**   **\> Copy**

2. In the pop\-up dialog box for copying a pipeline, set the following parameters.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Pipeline name |Support custom pipeline names. Pipeline names must be unique within a workspace. |
   |Workspace |Select the workspace for the copied pipeline.<br><br><br>* **Current workspace**: Copy the pipeline to the current workspace.<br><br>* **Other workspaces**: Copy the pipeline to other workspaces. |
   

3. Click **confirm** to enter the process orchestration tab for the current pipeline copy.

4. Modify parameters as needed. For a detailed introduction, refer to [Create pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When copying a pipeline within the same workspace, private variables are not copied.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Caution: When copying a pipeline across workspaces, some parameters cannot be fully copied. Please review the orchestration configuration of the pipeline after copying.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not copy code source, triggers, or privacy variables.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Whether pipeline variable groups, deployment clusters, and applications can be successfully replicated depends on whether the sharing scope of these resources includes the target workspace.   </div>
   

5. Click **Save** to complete the pipeline copy.


<span id=".5Yig6Zmk5rWB5rC057q_"></span>
## Delete a pipeline

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deleting the pipeline, the operation cannot be undone. Please proceed with caution.</div>



1. In the pipeline list, select the target pipeline, and click **Actions** column's  **`...`** .  **\> delete**, a confirmation dialog will pop up.

2. After confirming, click **delete** to delete the pipeline.
