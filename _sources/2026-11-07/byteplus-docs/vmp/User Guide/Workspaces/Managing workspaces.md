---
title: "Managing workspaces"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Managing-workspaces"
---

After you create a workspace, you can view, update, and delete the created workspace on the workspace management page based on your business requirements. This topic describes how to manage a workspace.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">VMP workspaces automatically created by cloud services are dedicated to these cloud services. Available management operations are governed by the permissions specified by the cloud service when it creates the workspace. All management operations can be performed only on the cloud service side. Editing, deleting, and other management operations are not allowed on the VMP side.</div>


<span id=".5pu05paw5bel5L2c5Yy6"></span>
## Update a workspace

After you create a workspace, you can modify the name and description of the workspace. After modification, the new configurations of the workspace take effect. Procedure:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. Click **Workspace** in the left navigation bar to go to the workspace list page.

3. In the workspace list, find the workspace that you want to update and click **Edit** in the **Actions** column.

4. After you modify the configurations of the workspace, click **Confirm** to apply the changes.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the name and description of the workspace can be modified.</div>


<span id=".5L-u5pS55bel5L2c5Yy66K6k6K-B5pa55byP"></span>
## Modify the workspace authentication method

You can modify the authentication method of an existing workspace, such as enabling or disabling custom authentication, or changing the type of custom authentication.


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. Click **Workspace **  in the left navigation bar.

3. On the Workspace page, click the name of the target workspace.

4. In the custom authentication section, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5bb0de622672b64b54090a8f43ac1b66.png) </span>icon to adjust custom authentication based on your business requirements. For parameter descriptions, see [Creating common workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id=".5Yig6Zmk5bel5L2c5Yy6"></span>
## Delete a workspace

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After a workspace is deleted, alerting rules associated with the workspace are set to the <strong>Deactivated</strong> status, and integration tasks associated with the workspace are set to the Paused state.</div>


* <div data-tips="true" data-tips-type="warning">After you delete a workspace, the data write and query capabilities of the workspace become unavailable. Proceed with caution.</div>



You can delete a workspace as follows:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. Click **Workspace** in the left navigation bar to go to the workspace list page.

3. In the workspace list, find the workspace that you want to delete and click **Delete** in the **Actions** column.

4. In the confirmation dialog box that appears, click **Confirm** to delete the workspace.
