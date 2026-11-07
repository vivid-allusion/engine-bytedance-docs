---
title: "Deleting a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Deleting_a_workspace"
---

You can manually release workspaces based on business needs. This topic introduces the procedure for deleting a workspace.

## Prerequisites

* A workspace is created and confirmed as no longer needed.

* Workspace deletion protection is disabled. For more information, refer to [Configuring workspace deletion protection](https://docs.byteplus.com/en/docs/330/Supabase-Configuring_workspace_deletion_protection).

## Precautions

* Deleting a workspace permanently erases all compute resources and data, which cannot be recovered. Proceed with caution.

* After deleting a workspace, its IP resources are released and may be reused by other systems. You may not be able to obtain the same IP address again.

* AIDAP currently only supports the pay\-as\-you\-go billing method, deleting workspace means unsubscribing.

## Procedure

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Delete** in the target workspace row.

5. In the pop\-up page, enter the name of the workspace to be deleted in the Workspace name text box for confirmation, and then click **Delete**.

## Related APIs

|**API** |**Decscription** |
|---|---|
|[DeleteWorkspace](https://docs.byteplus.com/en/docs/330/DeleteWorkspace) |Call the DeleteWorkspace API to delete the Workspace. |
