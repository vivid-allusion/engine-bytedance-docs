---
title: "Manage applications"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_applications"
---

This topic describes how to manage registered enterprise applications and how to configure connector\-related policies.

<span id="W17wQou5"></span>
## Configure application permissions

Administrators can configure permissions for applications separately. Only authorized employees can view and use Agent and MCP applications. An MCP application can contain multiple tools, and permissions can be set at the application level or at the individual tool level.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise agent" or "Enterprise MCP" tab, click the target application card.

4. On the "Permission management" tab, click "Edit permissions" in the upper\-right corner.

5. Set the authorization type and permission scope of the application. Then, click “Confirm” to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To grant permissions on specific tools within an MCP application, click "Authorize Individually" in the Actions column for the target tool to configure permissions.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If both MCP application permissions and tool permissions are configured, the tool permissions take precedence. Example: When MCP application permissions are set to <strong>Deny all</strong> and the permission scope for Tool\-01 is set to <strong>Allow all</strong>, all members can still use Tool\-01 but cannot view or use other tools in the MCP application.   </div>
   


<span id="v9Es2Ea3"></span>
## Modify application information

Administrators can modify application information. The source of an application cannot be modified.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise agent" or "Enterprise MCP" tab, click the target application card.

4. On the application details page, click the "Edit" button in the upper\-right corner to modify application information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For an MCP from a custom source that uses OAuth JWT authentication, you can switch between exclusive credentials and shared credentials. If you switch from exclusive credentials to shared credentials, the system removes any previously enabled JWT identity tokens and no longer passes JWT tokens downstream.   </div>
   

5. After the modification, click the "Confirm" button to save the modification.


<span id="BAgfAFXx"></span>
## Manage connector visibility and operability policies

Advanced management settings allow enterprise administrators to configure visibility and operability policies for connectors in the employee\-side console.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">These advanced settings apply only to the current workspace and do not affect other workspaces.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Advanced management" tab, perform the following operations.

   
   |Actions |Description |
   |---|---|
   |Allow employees to create custom connectors |Controls whether employees can create custom connectors. This is applicable to scenarios where enterprises want to centrally manage the scope of external system integration.<br><br><br>* **Enable (default)** : Employees can create custom MCPs and other connectors.<br><br>* **Disable**: Employees cannot create custom MCPs and other connectors. Configured custom connectors are retained and can be used as expected. |
   |Allow employees to view and configure official preset connectors |Controls whether official preset connectors are displayed in the employee\-side console.<br><br><br>* **Enable (default)** : Employees can view official preset connectors and easily configure the connectors using their personal accounts.<br><br>* **Disable**: Employees cannot view or use official preset connectors. Configured connectors are retained and can be used as expected. |
   


&nbsp;

<span id="MvOQCnCK"></span>
## Review shared Claws

After an enterprise employee submits a request to create an  shared Claw from the employee portal, the resource can be created only after an enterprise administrator approves the request. Enterprise administrators can approve requests as needed to control the number of resources created and ensure usage compliance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">After a shared Claw is approved, it consumes one Claw seat for the space (not the seat for the requesting employee).</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. Click the "Pending registration review" button in the upper\-right corner of the page to navigate to the "Pending registration review" page.

4. Click the target request in the list to view its application description, update time, administrator, and other information.

5. Review requests submitted by employees.

   * **Approve requests**: After confirming that the application content meets enterprise requirements, click "Approve". In the dialog box, confirm the message and click "Approve" to complete the review.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the request is approved, the system automatically creates and registers the corresponding agent application in Application Center, with the source type being "Shared Claw ". To control the permission scope, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_applications?lang=en#W17wQou5">Configuring application permissions</a>.      </div>
      

   * **Reject requests**: After confirming that the application content does not meet enterprise requirements, click "Reject". Enter the reason for rejection in the pop\-up dialog box, and click "Reject" to complete the operation.


<span id="cUBogHKm"></span>
## Deregister an application

Administrators can deregister unused applications. Once deregistered, an application becomes unavailable. It can be registered again later if needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Deregistering an application will cause the application and its associated capabilities to become immediately unavailable, which may affect employees and workflows that are using the application</strong>. We recommend assessing the potential impact first and performing the operation during off\-peak business hours.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise agent" or "Enterprise MCP" tab, hover the mouse over the target application card and click the "Deregister" button.

4. In the pop\-up dialog box, click "Confirm" to complete deregistration.
