---
title: "Resetting a branch"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Resetting_a_branch"
---

This topic introduces the steps to reset a branch.

<span id="DmkiN8pB"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="cXhYm6qG"></span>
## Precautions


* The following branches do not support reset:

   * Main branch

   * Branch without parent branch

   * Branch with child branch

   * Branch with enabled branch protection

* After resetting the branch, branch data will be reset to the parent branch data. If the branch protection of the parent branch is enabled, the account password of the child branch will no longer match the parent branch and will be reset to a random password.

* After resetting the branch, all connections of the branch will be disconnected.

* After resetting the branch, the branch's database connection string remain unchanged.


<span id="rEwtTgvc"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click  **...**  \> **Reset branch** in the target branch row to enter the reset branch setting page.

5. On the Reset page, confirm the branch information, then click **OK** to reset the branch.


<span id="JV2a9bxJ"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ResetBranch](https://docs.byteplus.com/en/docs/330/ResetBranch) |Call the ResetBranch API to reset the branch. |
