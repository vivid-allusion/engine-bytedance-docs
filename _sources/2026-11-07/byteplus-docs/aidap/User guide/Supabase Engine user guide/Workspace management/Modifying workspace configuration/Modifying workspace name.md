---
title: "Modifying workspace name"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Modifying_workspace_name"
---

You can modify the workspace name in the AI Native Database Platform. This topic introduces how to modify a workspace name.

<span id="OAEm8A3H"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Configure** in the target workspace row to enter the **Workspace settings** page.

5. In the **Name ** area at the top of the **Workspace settings** page, enter the new workspace name and press Enter or click **Save**. The workspace name must meet the following rules:

   * Unique within the account.

   * Can only contain Chinese characters, letters (a\-z and A\-Z), digits, hyphens (\-), and underscores (_).

   * Must start with a Chinese character or letter (a\-z and A\-Z).

   * Must be 2 to 64 characters in length.


<span id="a5myiaml"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyWorkspaceName](https://docs.byteplus.com/en/docs/330/ModifyWorkspaceName) |Call the ModifyWorkspaceName API to change the workspace name. |
