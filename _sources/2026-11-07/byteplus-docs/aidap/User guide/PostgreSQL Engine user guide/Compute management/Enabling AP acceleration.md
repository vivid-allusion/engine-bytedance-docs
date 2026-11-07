---
title: "Enabling AP acceleration"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Enabling_AP_acceleration"
---

This topic introduces the procedure to enable the AP acceleration function for the primary compute of a branch.

<span id="1LfahFeA"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="KGmf1pRv"></span>
## Precautions


* The AP acceleration function cannot be disabled once enabled.

* Only primary compute supports enabling the AP acceleration function.

* If DuckDB read\-only compute already exists under the branch, enabling AP acceleration for the primary compute is not supported.


<span id="JXSNLVPV"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page’s **Compute** tab, click the Primary compute row’s  ** …**  \> **Enable AP acceleration** to enter the **Enable AP acceleration** page.

6. On the **Enable AP acceleration** page, after confirming the compute information is correct, click **OK**.


<span id="xs9h2eC5"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyComputeAnalyticPolicy](https://docs.byteplus.com/en/docs/aidap/ModifyComputeAnalyticPolicy) |Call the ModifyComputeAnalyticPolicy API to enable the primary compute's AP acceleration function. |
