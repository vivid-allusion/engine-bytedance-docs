---
title: "Viewing a task"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Viewing_a_task"
---

This topic introduces the procedure for viewing tasks in a workspace or branch.

<span id="8FTD9C4e"></span>
## Background

The AI Native Database Platform includes a task center feature that displays records of creation, deletion, and updates on workspaces or branches. It shows each task's name, associated branch, associated compute, creation time, and execution time.

The AI Native Database Platform provides entry points to the task center on both the workspace details page and the branch details page.


* In the workspace task center, tasks created from midnight the previous day to midnight the current day under the workspace are displayed by default. It supports viewing tasks within a maximum time range of seven days by creation time, as well as searching tasks by branch ID, hashrate ID, and task name.

* In the branch task center, tasks created from midnight the previous day to midnight the current day under the branch are displayed by default. It supports viewing tasks within a maximum time range of seven days by creation time, as well as searching tasks by hashrate ID and task name.


<span id="gVFv8Z5k"></span>
## Procedure


<Tabs>
<Tab zoneid="vJoSPsOM" title="View tasks in the Workspace">
<TabTitle>View tasks in the Workspace</TabTitle>

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** to enter the Workspace list

4. In the Workspace list, click the name of the target workspace row to access the workspace **Overview**.

5. In the upper right corner of the workspace **Overview** page, click **Task center** to view the workspace task list.


</Tab>
<Tab zoneid="sJky7jC3" title="View tasks in the Branch">
<TabTitle>View tasks in the Branch</TabTitle>

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the target workspace's **Branch management** page. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, click the **Task center** tab to view the branch's task list.


</Tab>
</Tabs>


<span id="INTYnz5t"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[DescribeOperations](https://docs.byteplus.com/en/docs/aidap/DescribeOperations) |Call the DescribeOperations API to query operation records. |
