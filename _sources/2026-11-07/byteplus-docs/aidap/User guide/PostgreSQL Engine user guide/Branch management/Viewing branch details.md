---
title: "Viewing branch details"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Viewing_branch_details"
---

This topic introduces the steps to view details of the branch.

<span id="6swcKm1L"></span>
## Background

On the **Branch overview** page, basic information, compute, account, database, child branch, and monitoring information of the branch are displayed.


* Basic information includes branch ID, parent branch, workspace, compute, storage space, and last running time.

* The Compute tab shows all compute resources of the branch, including each compute's name, ID, specifications, last start time, and recent scale\-down time.

* The Account tab shows all accounts of the branch, including each account's name, authorized databases, creation time, and update time.

* The Database tab shows all databases of the branch, including each database's name, associated account, creation time, and update time.

* The Child branch tab shows all child branches of the branch, including each child branch's name, branch ID, compute, storage space, creation time, and last running time.

* The Monitoring tab shows compute monitoring information of all workspace branches by branch, including branch compute consumption and actual CPU usage (core). For detailed information on monitoring metrics provided by the AI Native Database Platform, refer to [Viewing monitoring information](https://docs.byteplus.com/en/docs/330/PostgreSQL-Viewing_monitoring_information).

* The Task center tab displays tasks created in the current branch between 0:00 of the previous day and 24:00 of the current day. It supports viewing tasks within a maximum time range of seven days by creation time, as well as searching tasks by hashrate ID and task name. For more details, refer to [View tasks](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Viewing_a_task?lang=en).


<span id="QgpxgyiB"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="qrRlDWB1"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page and view branch details.


<span id="Ljh4UV4F"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[DescribeBranches](https://docs.byteplus.com/en/docs/330/DescribeBranches) |Call the DescribeBranches API to query the workspace's branch list. |
|[DescribeChildBranches](https://docs.byteplus.com/en/docs/330/DescribeChildBranches) |Call the DescribeChildBranches API to query the child branch list of a branch. |
|[DescribeBranchDetail](https://docs.byteplus.com/en/docs/330/DescribeBranchDetail) |Call the DescribeBranchDetail API to query detailed information about the branch. |
