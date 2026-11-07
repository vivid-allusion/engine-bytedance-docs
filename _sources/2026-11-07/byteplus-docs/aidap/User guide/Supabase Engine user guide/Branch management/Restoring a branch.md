---
title: "Restoring a branch"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Restoring_a_branch"
---

This topic describes the procedure for restoring branch data.

<span id="uNqlkX9P"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="BUmVh6YT"></span>
## Precautions

When restoring a branch, the new branch will have the same Database, Authentication, and Edge Function as the Data source branch at the data synchronization target time. Storage metadata will be restored to the data source branch’s data at the specified restoration time point, but the object files corresponding to the metadata can only remain current temporarily.

<span id="kOCAFlhj"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to enter the target branch’s **Branch overview** page.

5. On the **Branch overview** page, click **Restore data** at the top\-right corner to enter the **Restore data** page.

6. On the **Restore data** page, select the **Restoration time point** and **Data source branch**. Then click **Restore data**, and click **OK** in the pop\-up dialog box.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The time range available for data recovery is determined by the later time between the creation time of the branch and the earliest traceability duration of the workspace.</div>


* <div data-tips="true" data-tips-type="default">If branch protection is enabled on the target branch, the new restored branch's account password will not match the original branch's account password and will be reset to a random password.</div>


* <div data-tips="true" data-tips-type="default">The data source branch can be the same as the branch initiating the data restoration.</div>


* <div data-tips="true" data-tips-type="default">After initiating the data restoration, the current branch will restore the data of the data source branch at the target restoration time point, and the current branch will become the child branch of the data source branch.</div>


* <div data-tips="true" data-tips-type="default">The data of the current branch at the time of initiating restoration (when pressing "OK" in the dialog box) will be saved in a new branch, named [current branch Name]_old_[UTC time of initiating restoration]. The parent branch of the new branch is identical to that of the current branch, replacing the current branch and serving as the parent branch for its child branches.</div>



<span id="5Ri87iBh"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[GetRestoreWindow](https://docs.byteplus.com/en/docs/aidap/GetRestoreWindow) |Call the GetRestoreWindow API to query the recoverable time period of a branch. |
|[BranchRestore](https://docs.byteplus.com/en/docs/aidap/BranchRestore) |Call the BranchRestore API to restore branch data to a specific time. |
