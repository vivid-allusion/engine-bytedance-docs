---
title: "Suspending a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Suspending_a_workspace"
---

AI Native Database Platform's workspace supports suspension. This topic describes the procedure for suspending a workspace.

<span id="p6wt6QK0"></span>
## Prerequisites

A workspace using the Supabase engine is created, and its status is **Running**.

<span id="Y8devg1d"></span>
## Precautions

After suspending the workspace, connections will be interrupted, and compute resources will be released and no longer billed. After suspending the workspace, the workspace’s Supabase service compute will be immediately suspended, and the database management service compute will suspend after 30 minutes. The workspace can restore its services after accessing the Supabase service again.

AI Native Database Platform also provides a stop function for workspaces. After stopping, the workspace will no longer provide external services, and compute will not be billed. However, the workspace must be manually started to restore services after stopping. If you confirm you will not use the workspace for a period of time, consider suspending it. For more details on pausing a workspace, refer to [Pausing a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Pausing_a_workspace?lang=en).

<span id="6uB7Jlhk"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Suspend** in the target workspace row to enter the **Suspend workspace** confirmation dialog.

5. On the **Suspend workspace** dialog page, confirm that the workspace name, engine information, and other details are correct, then click **OK** to suspend the workspace.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After successfully suspending the Workspace, its status switches to <strong>Suspended</strong></div>
