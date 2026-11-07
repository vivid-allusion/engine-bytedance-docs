---
title: "Rename a branch"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/supabase-renaming-a-branch"
---

This topic introduces how to rename a branch.

## Prerequisites

* A workspace is created and its status is **Running**.

* The target branch status is **Running**.

## Procedure

1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)**Branch management** in the center navigation bar of the page, then click the icon![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png) to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click  **...**  \> **Rename** in the target branch row to enter the **Rename branch** page.

5. On the **Rename branch** page, enter the new branch name in the **Name** text box and click **Save** to rename the branch. The name must meet the following rules:

   * The length must be between 1 and 128 characters.

   * It can only contain letters (a~z and A~Z), numbers (0~9), hyphens (\-), and underscores (_).

   * It must start with a letter (a~z and A~Z) and end with a letter (a~z and A~Z) or a number (0~9).

## Related APIs

|**API** |**Decscription** |
|---|---|
|[UpdateBranch](https://docs.byteplus.com/en/docs/aidap/UpdateBranch) |Call the UpdateBranch API to modify the branch configuration. |
