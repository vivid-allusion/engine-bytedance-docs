---
title: "Modifying workspace initial compute settings"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Modifying_workspace_initial_compute_settings"
---

This topic introduces how to modify workspace initial compute settings.

<span id="0y2hPsfY"></span>
## Background

The AI Native Database Platform supports configuring initial compute settings for a workspace. The initial compute settings include the Supabase service compute and the compute expansion range for the database management service, as well as whether to enable the function to automatically suspend compute when idle. The initial compute settings apply as the default settings when creating a new compute. Modifying the initial compute settings does not affect the existing compute.

<span id="SdPRhgxR"></span>
## Prerequisites

A Workspace is created and its status is **Running**.

<span id="aaadLvTO"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Configure** in the target workspace row to enter the **Workspace settings** page.

5. On the **Workspace settings** page, in the ** Initial compute settings** area, complete the configuration below and then click **Save.** 



|Configuration item |Decscription |
|---|---|
|Supabase service compute expansion range<br><br> |Configure the upper and lower limits of the Supabase service compute expansion range. The value range for both upper and lower limits is the same: [0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The ratio between the upper and lower limits should be greater than or equal to 1 and less than or equal to 8</div><br> |
|Database management service compute expansion range |Set the upper and lower limits of the compute expansion range for the database management service. The value range for both upper and lower limits is the same: [0.25\|0.5\|1\|2\|3\|4\|5\|6\|7\|8\|9\|10\|11\|12\|13\|14\|15\|16\|18\|20\|22\|24\|26\|28\|30\|32].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The ratio between the upper and lower limits should be greater than or equal to 1 and less than or equal to 8</div><br> |
|Automatically suspend compute when idle |Configure whether to enable Automatically suspend compute when idle.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Enabling this function requires setting the <strong>Idle duration before suspend</strong>.</div><br> |
|Wait for an idle duration before suspension |Set the threshold for the idle duration before compute is suspended. Value range: an integer from 300 to 604,800, in seconds. |


<span id="kMQnFR1B"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyComputeSettings](https://docs.byteplus.com/en/docs/330/ModifyComputeSettings) |Call the ModifyComputeSettings API to modify the compute settings of the Workspace. |
