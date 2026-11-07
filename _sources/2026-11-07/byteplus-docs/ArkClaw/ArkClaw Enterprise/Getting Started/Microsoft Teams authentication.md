---
title: "Microsoft Teams authentication"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Microsoft_Teams_authentication"
---

‌This topic describes the full process for provisioning and using an ArkClaw space via **Microsoft Teams authentication**.‌ After you complete the steps in this topic, you will have a Microsoft Teams SSO\-integrated ArkClaw space, allowing enterprise employees to log in with one click in Microsoft Teams.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This method leverages the SSO capabilities of Microsoft Teams and is suitable for enterprises that currently use Microsoft Teams for team collaboration.</div>


<span id="qdtqhsWI"></span>
## Step 1: Configure the Microsoft Teams application and permissions

<span id="tn1f8See"></span>
### Step 1: Application registration


1. Go to the [Microsoft 365 Admin Center](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) and click the "New Registration" button.

2. Configure the application name. Select "Single tenant only" for Supported account types. ArkClaw currently does not support cross\-tenant identity integration in multi\-tenant mode. Selecting the wrong option will cause subsequent employee logins to fail. **Redirect URI**: Leave this field blank during this step. You need to provide a value later, after obtaining the callback address from the ArkClaw side.


<span id="LOx9t1w0"></span>
### Step 2: Obtain enterprise authentication information


1. After the application is created, copy and save the Application (Client) ID and Directory (Tenant) ID.

2. Click the "Add Certificate or Secret" button to go to "Manage \> Certificates and Secrets".

3. In "Manage \> Certificates and Secrets", click the "New Client Secret" button.

4. After completing the description and expiration time, click the "Add" button.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The Client Secret will immediately become invalid upon reaching its expiration time, and all employees' Microsoft 365 SSO logins will be completely interrupted. Suggestions:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Set the ‌validity period to 12 or 24 months‌.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Create a ticket to create a new Client Secret ‌7 days before expiration and replace the old one with it in ArkClaw.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After replacement, retain the old Client Secret for at least 24 hours before deleting it to facilitate phased rollback.   </div>
   

5. Copy and save the string displayed in the **Value** column as the Client Secret. **This string can be viewed only once after creation. Immediately save it to a secure location**.


<span id="hmRSX2aD"></span>
## Step 2: Grant permissions for accessing services

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><strong>Trigger condition</strong>: This step is triggered only when you activate ArkClaw for the first time. It will be skipped for subsequent space activations with the same account.</div>


* <div data-tips="true" data-tips-type="default"><strong>Authorization scope:</strong> Authorize ArkClaw to access the following cloud services: VPC, ECS, PrivateLink, TOS, and MLP (see the Terms of Service for the actual service list).</div>


* <div data-tips="true" data-tips-type="default"><strong>Model permissions:</strong> Grant permissions to invoke all <strong>non\-Coding Plan</strong> models in ModelArk with a few clicks to facilitate model selection in ArkClaw later.</div>


* <div data-tips="true" data-tips-type="default"><strong>Billing information:</strong> This step itself does not incur fees. Subsequent <strong>use</strong> of enabled models, ModelArk services, or Web Search will incur ‌pay\-as\-you\-go billing‌. The following services incur fees:</div>


   * <div data-tips="true" data-tips-type="default">ModelArk</div>


   * <div data-tips="true" data-tips-type="default">Web search</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. In the pop\-up window, carefully read the relevant service terms, and after confirming that everything is correct, select "I have read and agree to the Terms of ArkClaw Services".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c2f1ec730d3fb88c943f3a6ea8ef1f4.png) </span>

4. Click the "Activate and authorize" button to complete role authorization and model activation.


<span id="sKmzdW0J"></span>
## Step 3: Configure the ArkClaw service


1. In the left navigation pane of the [ArkClaw Enterprise console ](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management \> Claws".

2. On the service activation page, configure the relevant information according to the table below.

   
   |Configuration item |Description |
   |---|---|
   |**Basic information** ||
   |Space name |Set the ArkClaw space name. The platform automatically generates a name, which administrators can modify as needed. After the space is activated, the space name can be changed at any time. For details, see [Viewing space configuration information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information?lang=en#ftsmTKKb). |
   |**Employee access control** ||
   |Authentication |Configure the access control information for enterprise employees. Select **Microsoft Teams**, and configure information of the application where the enterprise system permissions are granted. This is used for other employees to log in and use ArkClaw via their own accounts. |
   |Client ID |Enter the Client ID of the Microsoft Teams application, namely, the application (client) ID on the Azure AD application registration overview page. |
   |Client Secret |Enter the value of the Microsoft Teams application as the Client Secret, namely, the content in the Value column of the client secret created on the "Azure AD \> Certificates & secrets" page. |
   |Tenant ID |Enter the Tenant ID of the Microsoft Teams application, namely, the directory (tenant) ID on the Azure AD application registration overview page. |
   |**Space management type** ||
   |Select space management type |Select the management type for Claw instances in the current space. **This setting cannot be modified after the space is activated**.<br><br><br>* **Seat Management**: Subscription is based on the total number of seats. Seats of the same edition share a unified expiration date, and you do not need to manage the lifecycle of each Claw instance separately. Within the purchased seat quota, Claw instances can be provisioned or allocated as needed.<br><br>* **Instance Management**: Claw instances are managed individually. All Claw instances in the space are created, allocated, and managed separately. Each Claw instance has a separate resource lifecycle and must be managed individually.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Selecting the space management type is a beta feature and is available only after beta access is granted. If you need to use this feature, contact your account manager</strong>.</div><br> |
   |**Network configuration** ||
   |Space network configuration |The VPC CIDR block and subnet CIDR block for ArkClaw Enterprise. The platform will automatically create network resources such as VPCs, subnets, and security groups in the current region to set up the network environment for ArkClaw.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After an ArkClaw Enterprise space is activated, modifying the VPC CIDR block or subnet CIDR block is not supported.</div><br><br><br><br>* **Random network creation**:<br><br>   * No network configuration is required. The platform will create the VPC and subnet for ArkClaw using a randomly assigned private network segment.<br><br>   * If you need to access ArkClaw private network resources from another VPC later, ensure that the VPC address does not belong to the following network segments to avoid conflicts: `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`.<br><br>* **Specified network creation**:<br><br>   * If you need to connect to ArkClaw's VPC via Cloud Enterprise Network (CEN) or Transit Router (TR) in the future, specify an ArkClaw VPC CIDR block based on your network planning.<br><br>   * Click "Custom configuration" in the upper\-right corner of the card and enter the desired CIDR block for the custom VPC. The platform will create the VPC and subnet based on your input. Ensure the custom CIDR block does not belong to the following network segments: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/8`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, `169.254.0.0/16`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The ArkClaw private network is a beta feature and is available only upon activation. If needed, please contact your account manager to activate it</strong>.   </div><br>    |
   

3. After configuration is completed, click the "Activate now" button to complete the service space configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">ArkClaw supports independent ArkClaw spaces for different projects.<strong> This is a beta feature available only after a successful feature request.</strong> For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide?TagIDs=2,522,512,502&lang=en#rH30UfdE">Activating multiple spaces</a>.   </div>
   

   4. ModelArk API keys used in Foundation models have permission to invoke all models. A dialog box will appear to confirm this when space activation is complete. To manage the model scope, click "[Volcano Ark Management Console](https://console.byteplus.com/ark/region:cn-beijing/apiKey?apikey=%7B%7D&projectName=default)". If you do not need to manage the model scope, click "Got it" to close the dialog box.


<span id="KBCAt4In"></span>
## Step 4: Purchase ArkClaw Enterprise seats

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you selected "Instance Management" for "Select space management type" in the previous step to activate the ArkClaw space, skip this section</strong>.</div>



1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management \> Claws".

2. On the ArkClaw management page, click the "Buy now" button.

3. Specify an ArkClaw seat edition and quantity, and select a subscription duration.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Minimum order quantity for an ArkClaw seat purchase</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The number of seats purchased per order for ArkClaw Enterprise must be at least 5.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Different seat specifications apply to different scenarios. You can purchase a combination of seat specifications as needed. For more billing details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Billing_instructions">Billing</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Agent Plan Team purchases</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When purchasing ArkClaw seats, you may bundle Agent Plan Team packages at the same time. Alternatively, you may purchase seats only and bind packages later as needed.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Agent Plan Team purchases are non\-refundable.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ArkClaw seats and Agent Plan Team packages do not have a one\-to\-one mapping. All Claw instances under an employee's account share the allocated Agent Plan Team packages.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Coding Plan Team purchases</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Purchasing Coding Plan Team packages during space activation is currently not supported. If necessary, purchase or manage them after the space is activated. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_CodingPlan">Managing ModelArk Plans</a>.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">All Claw instances with access to the seat edition of Coding Plan Team packages share all Coding Plan Team resources for that seat edition.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Purchase and change restrictions</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Quantity limits</strong>: In a bundled purchase of ArkClaw seats and Agent Plan Team packages, the total number of Agent Plan Team packages in ArkClaw must be at least <strong>5</strong> (including those purchased in ArkClaw and ArkClaw\-managed ones from ModelArk). Each order supports a maximum of 1,000 Agent Plan Team packages (inclusive).   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Exclusiveness restriction: ModelArk Plans purchased in ArkClaw are recommended for use only within ArkClaw</strong>.   </div>
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ArkClaw Enterprise <strong>periodically rotates</strong> managed ModelArk Plan API Keys. During rotation, previous API Keys are immediately invalidated. If you reuse such Keys in services outside ArkClaw, service access will also be disrupted by rotation.   </div>
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To share ModelArk Plans across multiple scenarios, we recommend purchasing an independent ModelArk Plans, obtaining independent API Keys directly from ModelArk, and then configuring the model via "Custom model source." For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Model_management?lang=en#MXrT1Usf">Configuring custom model pools</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Automatic renewal</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The "Automatic renewal" option is selected by default to prevent ArkClaw service suspension due to subscription expiration. You can manually cancel this option. If you do that, ensure you renew your subscription before expiration.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After "Auto\-renewal" is enabled, automatic renewal will be applied to all subsequent new purchases and change orders under the space.   </div>
   

   
   |Specifications |Applicable scenario |
   |---|---|
   |Starter edition |Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations. |
   |Standard edition |The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations. |
   |Premium edition |Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects. |
   |Ultimate edition |Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   

4. After configuration is complete, click "Purchase" and follow the on\-screen instructions to pay the fees. Once payment is successful, click "Go to console" to complete the service activation. Service activation takes approximately 3–5 minutes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Common reasons for service activation failure include incomplete enterprise real\-name authentication, VPC CIDR block conflicts, or insufficient resources. </strong>If activation still fails after confirming these are resolved, copy the error message displayed on the page and click <strong>Submit a ticket</strong> for assistance.   </div>
   

<span id="tdk5nmgi"></span>
## Step 5: Configure callback information


1. In the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), on the "Space Overview" page, locate the **Teams authorization code redirect URL** field, click the copy icon on the right to copy the callback address to the clipboard, then click "Configure" to navigate to the Microsoft 365 Admin Center.

2. In the [Microsoft 365 Admin Center](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade), enter the application, select "Manage \> Authentication (Preview)", and on the "Redirect URI configuration" tab, click "Add Redirect URI".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your tenant has switched to the formal version, the menu item is <strong>Authentication</strong>.   </div>
   

3. Select "Web", paste the domain name copied from the ArkClaw Enterprise console. After the configuration is complete, click "Configure".


<span id="PR1CVncO"></span>
## Step 6: Distribute the employee login link

Distribute the employee login link via any message channel (for example, Microsoft Teams or email) adopted by the enterprise to employees who need to use ArkClaw. Employees can then log in via Microsoft Teams SSO authentication and use ArkClaw.
