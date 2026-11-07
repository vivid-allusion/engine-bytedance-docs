---
title: "Viewing workspace IP allowlist"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Viewing_workspace_IP_allowlist"
---

This topic describes the procedure for viewing the IP allowlist of a workspace using the Supabase engine.

<span id="GfQBZEvT"></span>
## Background

AI Native Database Platform provides access control capabilities to workspaces using the Supabase engine to enhance security. This capability supports creating an allowlist for the workspace, allowing access only from IP addresses added to the allowlist. When creating a workspace using the Supabase engine, the AI Native Database Platform automatically creates an allowlist named after the workspace ID and binds this allowlist to the workspace. The newly created allowlist does not contain any IP addresses.

<span id="5rdpSySe"></span>
## Prerequisites

A workspace using the Supabase engine is created, and its status is **Running**.

<span id="FSoKlfMD"></span>
## Precautions


* If the allowlist does not contain any IP address, the workspace allows access from all IP addresses.

* If the allowlist only contains the `127.0.0.1` address, the workspace denies access.

* CIDR\-format IP segments can be included in the allowlist, such as `192.168.0.0/24`, meaning the workspace allows access from IP addresses within this subnet.


<span id="ZJamNh64"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Configure** in the target workspace row to enter the **Workspace settings page**.

5. On the **Workspace settings** page, in the **IP allowlist** area, you can view the IP allowlist and all IP addresses it contains for the workspace.


<span id="xDMv0uqL"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[DescribeAccessControlList](https://docs.byteplus.com/en/docs/330/DescribeAccessControlList) |Call the DescribeAccessControlList API to query the IP allowlist bound to the workspace. |
