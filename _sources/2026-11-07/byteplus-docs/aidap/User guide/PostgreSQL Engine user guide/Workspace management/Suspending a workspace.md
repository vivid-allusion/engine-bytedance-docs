---
title: "Suspending a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Suspending_a_workspace"
---

AI Native Database Platform's workspace supports suspend. This topic describes the procedure for suspending a workspace.

<span id="p6wt6QK0"></span>
## Prerequisites

A workspace using the PostgreSQL engine is created, and its status is **Running**.

<span id="Y8devg1d"></span>
## Precautions

After suspending the workspace, connections will be interrupted, and compute resources will be released and no longer billed. Accessing the workspace again will restore its service.

<span id="6uB7Jlhk"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click the  **...**  \> **Suspend** in the target workspace row to enter the **Suspend workspace** page.

5. On the **Suspend workspace** page, confirm the Workspace name, engine information, and other details, then click **OK** to suspend the Workspace.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After successfully suspending the Workspace, its status switches to <strong>Suspended</strong></div>
