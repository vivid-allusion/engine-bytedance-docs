---
title: "Stopping a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Stopping_a_workspace"
---

The AI Native Database Platform's workspace supports stop. After stopping, the workspace will stop external services and release compute. Compute charges will not be incurred during the stop period. This topic describes the steps to stop a workspace.

<span id="fkcNbmDL"></span>
## Prerequisites

A Workspace using the PostgreSQL engine is created, and its status is **Running** or **Suspended**.

<span id="Si5bKI56"></span>
## Precautions

After a workspace is paused, it will no longer provide external services. No compute fees will be charged during the stop period. To continue using the workspace, start it. For more details, refer to [Starting a workspace](https://docs.byteplus.com/en/docs/330/PostgreSQL-Starting_a_workspace).

<span id="H5j7F1OH"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Stop** on the target workspace row to enter the **Stop workspace** page.

5. On the **Stop workspace** page, confirm the Workspace name, engine information, and other details, then click OK to stop the Workspace.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After successfully stopping the workspace, the workspace status switches to <strong>Stopped</strong>.</div>
