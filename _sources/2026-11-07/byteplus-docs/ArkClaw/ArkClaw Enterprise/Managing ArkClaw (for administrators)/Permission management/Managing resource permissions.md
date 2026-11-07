---
title: "Managing resource permissions"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_resource_permissions"
---

You can configure the authorization scope and operations for different resources (such as skill libraries, MCP, shared agents) based on their purpose. This accurately grants the required access to different departments, organizations, and individuals.

<span id="1Up5JoFS"></span>
## Configure/modify resource permission scope

<span id="bKbVX2U0"></span>
### Prerequisites


* To configure permission scope for specified departments, organizations, or individuals, you need to complete the following preparations in advance:

   * To configure permissions by **department**, make sure that you have created [a department](https://docs.byteplus.com/en/docs/ArkClaw/Managing_departments#RThcGR6H).

   * To configure permissions by **user group**, make sure that you have [created a user group](https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information#ReGX3H0s).

   * To configure permissions by **user**, make sure that you have [imported user information](https://docs.byteplus.com/en/docs/ArkClaw/Importing_user_information-).

* Before configuring resource permissions, confirm the following:

   * Skills library: You have uploaded custom skills.

   * MCP: You have completed the MCP registration. For details, see [Application management](https://docs.byteplus.com/en/docs/ArkClaw/Application_management#GFpXHMi7).

   * Shared agent: You have completed the registration of the Agent that comes from the "Shared Claw". For details, see [Application management](https://docs.byteplus.com/en/docs/ArkClaw/Application_management#Mxxy9IhZ).


<span id="4einD2HL"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Permissions".

3. In the corresponding resource tab, edit the permissions.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each resource has its own tab that contains the corresponding operations. The screenshots below use "Skill library" as an example for illustration.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you need to authorize specific Tools within an MCP, click the target MCP name to enter the details page, then grant permissions to the Tools individually.   </div>
   

   * **Edit permissions for a single resource**:

      Click the "Edit permission" button in the Actions column for the target resource.

   * **Batch edit resource permissions**:

      If you need to set the same permission scope for multiple resources at once, you can select the checkboxes in front of the target resource names, and then click the "Batch configure permissions" button below the list.

4. Select the authorization scope for the resources.

   
   |Parameter​ |Parameter description |
   |---|---|
   |Permission type |Authorization types of resources<br><br><br>* **All types**: Grant all types of permissions for the resource.<br><br>* **Split types**: Grant only some types of permissions for the resource. The split permission types vary across different resources.<br><br>   * Skill library: Downloadable.<br><br>   * MCP: Invoke application.<br><br>   * Shared agent: Invoke application. |
   |Permission scope |Authorization scope of resources.<br><br><br>* **Allow all**: Make this resource available to all enterprise employees who can use ArkClaw. For example, allow everyone to download skills from the target skill library.<br><br>* **Deny all**: Make this resource unavailable to all enterprise employees who can use ArkClaw. For example, do not allow anyone to download skills from the target skill library.<br><br>* **Controlled access**: Make this resource available to specified departments, user groups, or users. For example, only allow employees with permission to download skills from the target skills library. |
   

5. Click "Confirm" to complete the permission configuration.


<span id="nS9yJVmU"></span>
## View the resource permission scope


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), click "Organizations" \> "Permissions".

2. View the permission information of resources.

   * **View resource permission information**

      By switching tabs, you can view data and permission information for all resources, fully available resources, and access\-controlled resources, respectively.

   * **View permissions on a specified resource**

      Enter the name or ID of the target resource in the search box to query the specified resource.


&nbsp;
