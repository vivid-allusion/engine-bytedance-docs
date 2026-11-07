---
title: "Configuring public network resolution of private domain names"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_public_network_resolution_of_private_domain_names"
---

This topic describes information on enabling or disabling the public network resolution of private domain names for workspaces using the Supabase engine.

<span id="NgRoWg2H"></span>
## Prerequisites

A workspace using the Supabase engine is created, and its status is **Running**.

<span id="fdeUuVC9"></span>
## Precautions


* This function is currently in invitation testing. If you need to use them, [submit a ticket](https://console.byteplus.com/workorder/create) to apply.

* Due to the complexity of the public network environment, the accuracy and timeliness of domain resolution cannot be guaranteed, and domain registration may experience second\-level delays. If you need to modify the virtual private cloud or subnet when enabling the public network resolution of private domain names, evaluate potential delay impacts in advance.


<span id="MBCZabBD"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** to enter the workspace list.

4. In the workspace list, click  **...**  \> **Configure** in the target workspace row to enter the **Workspace settings** page.

5. On the **Workspace settings** page, locate the **Public network resolution of private domain names** area, toggle the switch and click **Save** to enable or disable the public network resolution of private domain names.


<span id="wOnqltCz"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ApplyPrivateDNSToPublic](https://docs.byteplus.com/en/docs/aidap/ApplyPrivateDNSToPublic?lang=en) |Use the ApplyPrivateDNSToPublic API to enable or disable the public network resolution of private network domain names for the workspace. |
