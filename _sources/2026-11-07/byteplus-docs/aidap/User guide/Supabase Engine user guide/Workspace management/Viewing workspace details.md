---
title: "Viewing workspace details"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Viewing_workspace_details"
---

This topic describes the steps to view workspace details in the AI Native Database Platform.

<span id="JHz8fRPv"></span>
## Background

The workspace details page displays configuration, resource usage, branches, and monitoring information.


* Configuration includes the workspace name, engine, network protocol type, virtual private cloud, and subnet used by the workspace.

* Resource usage includes storage space, compute, Supabase compute, and storage usage of the workspace.

* Branches display existing Workspace branches, including their name, compute, storage space, and last running time.


<span id="w1TRNZRb"></span>
## Prerequisites

A Workspace is created and its status is **Running**.

<span id="mn7u66cc"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to access the workspace list.

4. In the workspace list, click the target workspace name to access the workspace **Overview** page.


<span id="zcFRHouD"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[DescribeWorkspaceDetail](https://docs.byteplus.com/en/docs/330/DescribeWorkspaceDetail) |Call the DescribeWorkspaceDetail API to query Workspace details. |
