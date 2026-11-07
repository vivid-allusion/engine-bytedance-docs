---
title: "Modifying workspace IP allowlist"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Modifying_workspace_IP_allowlist"
---

This topic describes the procedure for modifying the IP allowlist of a workspace using the Supabase engine.

<span id="HtqMur1k"></span>
## Prerequisites

A workspace using the Supabase engine is created, and its status is **Running**.

<span id="sSMS4BUT"></span>
## Precautions


* If all IP addresses are removed from the allowlist, the workspace allows access from all IP addresses.

* If the allowlist only contains the `127.0.0.1` address, the workspace denies access.

* CIDR\-format IP segments can be included in the allowlist, such as `192.168.0.0/24`, meaning the workspace allows access from IP addresses within this subnet.


<span id="T1SR6pgg"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to enter the workspace list

4. In the Workspace list, click  **...**  \> **Configure** in the target Workspace row to enter the **Workspace settings** page.

5. On the **Workspace settings** page, locate the ** IP allowlist** text box, modify the IP address or CIDR block list, then click **Save** to complete the IP allowlist modification.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The allowlist text box supports pasting.</div>


* <div data-tips="true" data-tips-type="default">Separate multiple addresses or CIDR blocks with Chinese or English commas, spaces, or line breaks.</div>


* <div data-tips="true" data-tips-type="default">A maximum of 300 IP addresses or CIDR\-format IP segments can be added to one allowlist.</div>



<span id="yBGGRvTv"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyAccessControlList](https://docs.byteplus.com/en/docs/330/ModifyAccessControlList) |Use the ModifyAccessControlList API to query the IP allowlist bound to the Workspace. |
