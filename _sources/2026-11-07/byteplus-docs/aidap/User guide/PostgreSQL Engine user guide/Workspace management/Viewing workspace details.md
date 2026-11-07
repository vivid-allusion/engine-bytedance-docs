---
title: "Viewing workspace details"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Viewing_workspace_details"
---

This topic describes the steps to view workspace details in the AI Native Database Platform.

<span id="JHz8fRPv"></span>
## Background

The Workspace details page displays configuration, resource usage, branches, and monitoring information.


* Configuration includes the Workspace name, Workspace engine, compute expansion range, and traceability duration.

* Resource usage includes Workspace storage space, compute, branch compute, and branches.

* Branches display existing Workspace branches, including their name, compute, storage space, and last running time.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Six branches are displayed by default. To view more, click <strong>All branches</strong> in the top right corner to enter the <strong>Branch</strong> page.   </div>
   

* The monitoring tab displays compute monitoring information by branch, such as consumed compute and actual CPU usage (cores). For detailed information on monitoring metrics provided by the AI Native Database Platform, refer to [Viewing monitoring information](https://docs.byteplus.com/en/docs/330/PostgreSQL-Viewing_monitoring_information).


<span id="w1TRNZRb"></span>
## Prerequisites

A Workspace is created and its status is **Running**.

<span id="mn7u66cc"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to enter the workspace list.

4. In the workspace list, click the target Workspace name to access the workspace **Overview**.


<span id="zcFRHouD"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[DescribeWorkspaceDetail](https://docs.byteplus.com/en/docs/330/DescribeWorkspaceDetail) |Call the DescribeWorkspaceDetail API to query Workspace details. |
