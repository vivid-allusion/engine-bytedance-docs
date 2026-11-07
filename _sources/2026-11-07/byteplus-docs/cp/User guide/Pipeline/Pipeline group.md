---
title: "Pipeline group"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_group"
---

With the Pipeline group feature, you can categorize and manage pipelines under the workspace. This document describes how to create, edit, and delete groups, as well as how to move a pipeline to a different group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Ungrouped</strong> is a system preset group used to contain all pipelines not assigned to any group. You cannot rename or delete this group.</div>


<span id=".5Yib5bu65YiG57uE"></span>
## Create a group

Create a Pipeline group. After creating a new pipeline group, you can move the pipelines you want to manage to this group.


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace**.

3. Click the target workspace name to enter the selected workspace.

4. In the left navigation bar, select **pipeline** to open the **pipeline** page.

5. In the pipeline group area, click **+** 。

6. In the pop\-up "Create Pipeline Group" dialog box, enter the group name according to the prompts on the interface.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Pipeline group names must be unique within the same workspace.   </div>
   

7. Click **Comfirm** to complete the creation of the pipeline group.

   You can view the newly created group in the pipeline group area.


<span id=".56e75Yqo5rWB5rC057q_"></span>
## Mobile pipelines

Move the current pipeline's group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each pipeline can belong to only one group.</div>



1. In the pipeline list, select the target pipeline, and click  **`...`**  in the actions column.  **\> Move to**.

2. Select the target group name.

3. Click **OK** to move the current pipeline under the target group.


<span id=".57yW6L6R5YiG57uE"></span>
## Edit groups

You can modify the names of custom pipeline groups.


1. In the pipeline group area, hover the mouse over the target group card and click the edit icon.

2. In the pop\-up dialog box, modify the group name.

3. After making changes, click **OK**.


<span id=".5Yig6Zmk5YiG57uE"></span>
## Delete groups

Supports deleting pipeline groups that are no longer in use.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Once a group is deleted, it cannot be restored. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="danger">After a group is deleted, pipelines that originally belonged to that group will be automatically assigned to <strong>Ungrouped</strong>.</div>


1. Hover over the target pipeline group card in the pipeline group area, then click the delete icon.

2. In the secondary confirmation dialog, click **confirm** to delete the current group.
