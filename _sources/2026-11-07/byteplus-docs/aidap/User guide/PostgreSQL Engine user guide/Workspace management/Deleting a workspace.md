---
title: "Deleting a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Deleting_a_workspace"
---

You can manually release workspaces based on business needs. This topic introduces the procedure for deleting a workspace.

<span id="kSCvmLCS"></span>
## Prerequisites


* A workspace is created and confirmed as no longer needed.

* Workspace deletion protection is disabled. For more information, refer to [Configuring workspace deletion protection](https://docs.byteplus.com/en/docs/330/PostgreSQL-Configuring_workspace_deletion_protection).


<span id="du783bJp"></span>
## Precautions


* Deleting a workspace permanently erases all compute resources and data, which cannot be recovered. Proceed with caution.

* After deleting a workspace, its IP resources are released and may be reused by other systems. You may not be able to obtain the same IP address again.


<span id="bl7DkDQb"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Delete** on the target workspace row.

5. In the pop\-up page, enter the name of the workspace to be deleted in the Workspace name text box for confirmation, and then click **Delete**.


<span id="YlkGzBWy"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[DeleteWorkspace](https://docs.byteplus.com/en/docs/330/DeleteWorkspace) |Call the DeleteWorkspace API to delete the Workspace. |
