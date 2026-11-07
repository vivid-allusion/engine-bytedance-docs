---
title: "Viewing branch details"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Viewing_branch_details"
---

This topic introduces the steps to view details of the branch.

## Background

On the **Branch overview** page, basic information, Supabase service compute and connection information, database management service compute information, child branch list, usage statistics, and monitoring information are displayed.

* Basic information of the branch includes Branch ID, Parent branch, Workspace, and Last running time.

* On the **Supabase service** tab, you can obtain the Supabase private network connection string, Supabase public network connection string, and access to the Supabase console. It displays the Supabase compute name, specifications, last start time, and recent scale\-down time.

* On the **Database management service** tab, the database management service compute name, ID, specifications, last start time, and recent scale\-down time are displayed.

* On the **Child branch** tab, all child branches are displayed with each child branch's name, branch ID, compute, storage space, creation time, and last running time.

* On the **Usage statistics and monitoring** tab, usage statistics of the branch and monitoring information of all branches in the Workspace are displayed. Usage statistics include Supabase compute, database compute, database storage usage, storage usage, storage vector bucket data storage, Sandbox compute. Monitoring information includes Supabase actual CPU usage, Supabase memory usage, and other monitoring metrics. For more details, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/aidap/Supabase-Monitoring_metrics).

* On the **Task center** tab, tasks created in the current branch between 0:00 of the previous day and 24:00 of the current day are displayed. It supports viewing tasks within a maximum time range of seven days by creation time, as well as searching tasks by hashrate ID and task name. For more details, refer to [View tasks](https://docs.byteplus.com/en/docs/aidap/Supabase-Viewing_a_task?lang=en).

## Prerequisites

* A workspace is created and its status is **Running**.

* The target branch status is **Running**.

## Procedure

1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)**Branch management** in the center navigation bar of the page, then click the icon![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png) to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page and view branch details.

## Related APIs

|**API** |**Decscription** |
|---|---|
|[DescribeBranches](https://docs.byteplus.com/en/docs/330/DescribeBranches) |Call the DescribeBranches API to query the workspace's branch list. |
|[DescribeChildBranches](https://docs.byteplus.com/en/docs/330/DescribeChildBranches) |Call the DescribeChildBranches API to query the child branch list of a branch. |
|[DescribeBranchDetail](https://docs.byteplus.com/en/docs/330/DescribeBranchDetail) |Call the DescribeBranchDetail API to query detailed information about the branch. |
