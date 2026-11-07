---
title: "Starting a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Starting_a_workspace"
---

AI Native Database Platform workspaces support stopping. After stopping, the workspace will no longer provide external services. You can start the workspace to restore its services. This topic describes the procedure for starting a workspace.

<span id="YdXniXwe"></span>
## Prerequisites

A workspace using the Supabase engine is created, and its status is **Stopped**.

<span id="kyAy8epR"></span>
## Precautions

After starting the workspace, it will resume external services, and the workspace's compute consumption will be billed again.

<span id="j3ARVce2"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Start** in the target workspace row to enter the **Start workspace** dialog page.

5. In the **Start workspace** dialog, confirm the workspace's name and engine info, and then click **OK** to start the workspace.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After successfully starting the workspace, its status switches to <strong>Running</strong>.</div>
