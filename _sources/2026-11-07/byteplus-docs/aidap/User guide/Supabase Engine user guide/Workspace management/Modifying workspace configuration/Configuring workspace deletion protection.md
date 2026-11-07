---
title: "Configuring workspace deletion protection"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_workspace_deletion_protection"
---

The AI Native Database Platform offers a deletion protection function to prevent accidental workspace deletion. This topic describes the steps to configure the deletion protection function for a workspace.

<span id="o9FfIoXl"></span>
## Prerequisites

A Workspace is created and its status is **Running**.

<span id="MyCRdtNZ"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Configure** on the row of the target workspace to enter the **Workspace settings** page.

5. On the **Workspace settings** page, locate the **Deletion protection** area, toggle the switch and click **Save** to enable or disable the deletion protection function.


<span id="LMhNTdxj"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyWorkspaceSettings](https://docs.byteplus.com/en/docs/330/ModifyWorkspaceSettings) |Call the ModifyWorkspaceSettings API to modify the workspace's basic configuration. |
