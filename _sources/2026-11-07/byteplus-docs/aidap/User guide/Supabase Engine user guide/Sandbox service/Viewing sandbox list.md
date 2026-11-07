---
title: "Viewing sandbox list"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Viewing_sandbox_list"
---

The **sandbox list** page displays all **running** sandboxes under the current branch, supporting search by sandbox ID, download logs, and stop sandbox.

<span id="nHafTyFz"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target current branch is in **running** status.


<span id="kI7WhDdY"></span>
## Precautions


* The sandbox list displays by branch dimension and only shows sandbox under the current branch.

* Each sandbox has remaining TTL and will be automatically reclaimed and removed from the list upon expiration.

* The sandbox list only shows sandbox in **running** status; stopped, stopping, or reclaimed sandbox are no longer shown.

* Once sandbox reaches the remaining TTL, the system automatically reclaims it and removes it from the list. Download logs to keep in time.


<span id="fPedZZUr"></span>
## Procedure

<span id="T3EXkkRN"></span>
### **Viewing sandbox list**


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, select **Sandbox service** \> **Sandbox list** tab.

6. The page displays all running sandboxes under the current branch in a list format.


<span id="zE6QKbi6"></span>
### Search by sandbox ID


1. Enter the sandbox ID (full ID or prefix match supported) in the search box above the list.

2. The list automatically filters the matching sandboxes.


<span id="cKrdTwIO"></span>
### Refresh list

Click the refresh icon at the top right of the list to manually fetch the latest sandbox list.

<span id="1t2QAWl9"></span>
### Download logs


1. Click  **...** \> **Download logs** at the end of the target sandbox row.

2. The page shows "Log downloaded successfully" at the top, and the browser automatically downloads the log file (filename: {Source template}\-{Sandbox ID}.log).


<span id="fd0XiejE"></span>
### Stop sandbox


1. Click  **...** \> **Stop** at the end of the target sandbox row.

2. Confirm the prompt on the pop\-up **Stop sandbox** page: Confirm stopping sandbox {Sandbox ID}? The sandbox will no longer be available after stopping.

3. Click **Stop** to submit the action. Stop request submitted. The sandbox is removed from the list.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Stop actions cannot be undone. The sandbox becomes unavailable after stopping and is removed from the list. Download logs before stopping if you want to keep the execution records.</div>


<span id="p0jol0Fy"></span>
## Field description


|**Field** |**Decscription** |
|---|---|
|Sandbox ID |Unique identifier of the sandbox, displaying the current status tag of the sandbox (such as **running**). |
|Source template |Name of the source template for the sandbox, such as base or opencode. |
|Specification |Sandbox resource specifications, such as 500m CPU / 1024MiB, 2000m CPU / 4096MiB. |
|Started by |User who executed the create sandbox action, for example System Admin. |
|Started at |Sandbox creation and start time. |
|Update time |Last update time of the sandbox status or configuration. |
|Remaining TTL |Remaining survival time before the sandbox is automatically reclaimed, for example, 14 {num, plural, one {minute} other {minutes}}. |
