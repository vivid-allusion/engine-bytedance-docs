---
title: "Enabling branch protection"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Enabling_branch_protection"
---

This topic introduces the steps to enable branch protection for the branch.

<span id="uW5XaAPG"></span>
## Background

After enabling branch protection for the branch, the branch cannot be directly deleted or reset. When creating a child branch, the child branch will have exactly the same data as the parent branch, such as database, account, and account password. If the branch protection of the parent branch is enabled, the account password of the child branch will no longer match the parent branch and will be reset to a random password. The branch with branch protection enabled will have the word `Protected` in its **Branch** name on the branch page.

<span id="bikH3qRL"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="ZkNEJljF"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click  **...**  \> **Enable branch protection** or ** Disable branch protection** in the target branch row to enter the branch protection settings page.

5. On the branch protection settings page, confirm the branch information, then click **OK** to enable or disable protection for the branch.


<span id="eebfKGMB"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[UpdateBranch](https://docs.byteplus.com/en/docs/330/UpdateBranch) |Call the UpdateBranch API to modify the branch configuration. |
