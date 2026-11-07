---
title: "Modifying workspace traceability duration"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Modifying_workspace_traceability_duration"
---

You can modify the traceability duration of a workspace on the AI Native Database Platform. This topic describes the procedure for modifying the traceability duration of a workspace.

<span id="l09NstTg"></span>
## Prerequisites

A Workspace is created and its status is **Running**.

<span id="9NHZvYU7"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** in the middle navigation bar on the page to enter the workspace list.

4. In the workspace list, click  **...**  \> **Configure** on the target workspace row to enter the **Workspace settings** page.

5. On the **Workspace settings** page, locate the **Traceability duration** area, set the traceability duration by sliding the slider on the timeline and clicking **Save**, or entering a value in the textbox and pressing Enter. The traceability duration ranges from 1 to 720 hours.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If a decimal is entered in the textbox, it rounds to the nearest integer following standard rounding rules.   </div>
   

<span id="HMMm1xnY"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyWorkspaceSettings](https://docs.byteplus.com/en/docs/330/ModifyWorkspaceSettings) |Call the ModifyWorkspaceSettings API to modify the workspace's basic configuration. |
