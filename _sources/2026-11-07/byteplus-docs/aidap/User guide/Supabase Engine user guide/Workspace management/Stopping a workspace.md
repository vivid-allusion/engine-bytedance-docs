---
title: "Stopping a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Pausing_a_workspace"
---

The AI Native Database Platform's workspace supports stop. After stopping, the workspace's compute will be released and no longer charged. This topic describes the steps to pause a workspace.

<span id="fkcNbmDL"></span>
## Prerequisites

A workspace using the Supabase engine has been created, and its status is **Running** or **Suspended**.

<span id="Si5bKI56"></span>
## Precautions

After a workspace is paused, it will no longer provide external services. During the pause period, only storage fees are charged, and no compute fees are charged. To continue using the workspace, start it. For more details, refer to [Starting a workspace](https://docs.byteplus.com/en/docs/330/Supabase-Starting_a_workspace).

The AI Native Database Platform also provides a suspend function for workspaces. No compute fees are charged during suspension. However, the workspace can be connected to and awakened from suspend without manual startup. For more details, refer to [Suspending a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Suspending_a_workspace?lang=en).

<span id="H5j7F1OH"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to enter the workspace list.

4. In the workspace list, click  **...**  \> **Stop** on the target workspace row to enter the **Stop workspace** confirmation dialog.

5. In the **Stop workspace** dialog, confirm the workspace's name and engine info, and then click OK to stop the workspace.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After successfully pausing the workspace, the Workspace status switches to <strong>Stopped</strong>.</div>
