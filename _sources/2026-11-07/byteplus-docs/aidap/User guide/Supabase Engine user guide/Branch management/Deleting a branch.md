---
title: "Deleting a branch"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Deleting_a_branch"
---

This topic describes how to delete a branch.

<span id="NCRBiz1Y"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.

* It has been confirmed that the branch is no longer needed.


<span id="6w8eudJY"></span>
## Precautions


* The following branches cannot be deleted:

   * Default branch

   * Branch with child branch

* A deleted branch cannot be recovered. Proceed with caution.


<span id="FrKmNUgf"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the target workspace's **Branch management** page. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click  **...**  in the target branch row \> **Delete branch** to enter the branch deletion page.

5. On the Delete branch page, enter the name of the branch to be deleted in the branch name text box for confirmation, then click **Delete** to complete the branch deletion.


<span id="mw1qrDDO"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[DeleteBranch](https://docs.byteplus.com/en/docs/aidap/DeleteBranch) |Call the DeleteBranch API to delete a branch. |
