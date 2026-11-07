---
title: "Modifying Workspace initial compute settings"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Modifying_Workspace_initial_compute_settings"
---

The AI Native Database Platform Workspace's initial compute settings include the compute expansion range and automatically suspend compute when idle configurations. The Workspace initial compute settings can be modified. This topic describes the procedure for modifying the Workspace initial compute settings.

<span id="oLWqSDf5"></span>
## Prerequisites

A workspace is created and its status is **Running**.

<span id="JpO4VGmq"></span>
## Precautions

The initial compute settings apply to all newly created primary or read\-only replica compute resources. Modifying these settings does not affect existing compute resources.

<span id="8cGqy148"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click the  **...**  \> **Configure** in the target workspace row to enter the **Workspace settings** page.

5. On the **Workspace settings** page, in the **Initial compute settings** area, complete the configuration below and then click **Save**.

   
   |Configuration item |Decscription |
   |---|---|
   |Compute expansion range |Configure the upper and lower limits of compute expansion. For detailed information about the compute specifications supported by the AI Native Database Platform, refer to [product specifications](https://docs.byteplus.com/en/docs/330/Product_specifications).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The ratio of the maximum compute to the minimum compute must be less than or equal to 8.</div><br> |
   |Automatically suspend compute when idle |Configure whether to enable Automatically suspend compute when idle. If enabled, the idle duration before suspend must be set, with a default value of 300 seconds.<br><br>After enabling automatic suspension of compute when idle, compute will be automatically suspended once the idle duration reaches the idle duration before suspension. |
   |Idle duration before suspension |Set the threshold for the idle duration before compute is suspended. Value range: an integer from 300 to 604,800, in seconds. |
   


<span id="bF7oQnfN"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyComputeSettings](https://docs.byteplus.com/en/docs/330/ModifyComputeSettings) |Call the ModifyComputeSettings API to modify the compute settings of the Workspace. |
