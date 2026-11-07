---
title: "Workspace management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Workspace_management"
---

Workspaces are a data management and isolation method provided by Server\-side Monitoring. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. This topic describes how to create and manage workspaces.

<span id="34bvhbxd"></span>
## Limits

Up to 20 workspaces can be created in the same region.

<span id="RqCwwaZW"></span>
## Create workspaces


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, select **Platform Setting \> Workspace Management** to access the workspace management page.

3. Click **Create** to open the workspace creation page. Configure the parameters as needed and click **Confirm**.

   
   |Parameter |Description |
   |---|---|
   |workspace |Provide a custom name for the workspace. The name is the unique identifier of the workspace and cannot be modified. |
   |Delete protection |This feature is disabled by default. When deletion protection is enabled, workspace deletion via the console or API is prohibited to prevent accidental deletion that could affect normal business operations. To delete this workspace later, disable deletion protection first before you delete it. |
   |Project |The project to which the workspace belongs. Projects are a platform\-provided resource management mechanism that allows you to group resources for different business applications or projects. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
   |Tags |Add labels to the workspace. A label is used to identify the workspace. You can combine labels with selectors to filter workspaces. A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 20 tags.</div><br> |
   

4. (Optional) Return to the workspace management page. Find the workspace in the workspace list and click **Parameter management** in the Actions column on the right side of the list. Configure parameters as required for your business scenario, such as system, probe, and storage settings. For more details, see [Parameter management](https://docs.byteplus.com/en/docs/apmplus/parameter_management).


<span id="GfC8XMUb"></span>
## Managing workspaces

After the workspace is successfully created, you are redirected to the workspace management page, where you can perform the following operations:


|Actions |Description |
|---|---|
|View the AppKey |When the workspace is created, a dedicated AppKey is automatically generated for it. You can use this AppKey as the data reporting credential.<br><br>Find the target workspace, and in the AppKey column, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01b9d5143251b6fc05ea4ca32d1eb9ca.png) </span> to display the AppKey information in plain text. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cc51686137d11e32a92036eca0fc484.png) </span> to copy the AppKey. |
|Edit |Find the target workspace and click **Edit** in the Actions column on the right side of the workspace list. You can edit the workspace description, deletion protection setting, and tags.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Deletion protection for the Default workspace cannot be modified.</div><br> |
|Parameter management |Find the workspace in the workspace list and click **Parameter management** in the Actions column on the right side of the list. Configure parameters as required for your business scenario, such as system, probe, storage, and performance profiling settings. For more details, see [Parameter management](https://docs.byteplus.com/en/docs/apmplus/parameter_management). |
|Delete |To permanently delete a workspace that is no longer needed, find it in the list and click **Delete** in the Actions column on the right side.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><br>* <div data-tips="true" data-tips-type="danger">Deleting a workspace will remove all resources within it. This operation is irreversible‌. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">The Default workspace cannot be deleted.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">To delete a workspace with deletion protection enabled, disable deletion protection first before deletion.</div><br> |
