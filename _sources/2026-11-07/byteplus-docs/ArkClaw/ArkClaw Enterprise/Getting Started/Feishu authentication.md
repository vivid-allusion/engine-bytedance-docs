---
title: "Feishu authentication"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication"
---

This topic describes the complete process of activating ArkClaw Enterprise spaces via **Feishu SSO**.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This method leverages ‌Feishu applications' SSO capability‌ and suits enterprises that already use Feishu for team collaboration and want to ‌reuse their existing Feishu account system to avoid creating separate accounts.</div>


<span id="tXfPdJrI"></span>
## Step 1: Configure the Feishu application and permissions

<span id="RpjL5hcx"></span>
### Step 1: Create an enterprise Feishu application


1. Log in to the [Feishu Open Platform](https://open.larkoffice.com/app?lang=zh-CN) and click "Create Custom App".

2. Provide an application name, description, and icon, and click "Create".


<span id="XT7ufHFt"></span>
### Step 2: Configure Feishu application permissions


1. (Optional) On the[ Feishu Open Platform](https://open.larkoffice.com/app?lang=zh-CN), click the name of the custom application to enter the development page of the application (in this example, "ArkClaw"). If you are already on the application development page, skip this step.

2. In the directory tree on the left, select "Development Configuration" \> "Permissions & Scopes", and click the "Batch import/export scopes" button.

3. On the "Import" tab, replace the original example with the following permissions, and click the "Next, Review New Scopes" button.

   ```Python
   {
     "scopes": {
       "tenant": [
         "contact:user.base:readonly",
         "contact:user.email:readonly"
       ],
       "user": []
     }
   }
   ```
   

4. After confirming the permissions are correct in the pop\-up window, click the "Add" button to complete the operation.

5. Set the accessible data scope for the permission (by default, the same as the availability of the application). Save your settings and click "Confirm" to complete the operation.

6. In the directory tree on the left, select "App Versions" \> "Version Management and Release", and click the "Create a version" button.

7. Provide an application version number and update description. Click the "Edit" button next to the "Availability" field to specify the effective scope of the configuration.

8. Set the availability range of this enterprise application. To do so, add the target departments or the Feishu accounts of enterprise employees who need to use ArkClaw Enterprise and click "Done".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can configure application availability settings to configure which employees have access to ArkClaw. If you do not need to restrict ArkClaw access across the enterprise, select "All members" to grant ArkClaw access to all employees in the enterprise.   </div>
   

9. Click the "Save" button at the bottom of the page to complete the version creation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are not an enterprise Feishu administrator, include a detailed description of your business scenario and application functionality when applying to create the application. This information helps your application get approved by the enterprise Feishu administrator.   </div>
   

10. Publish the application.

   * If your application does not require approval, click the "Publish" button in the upper\-right corner of the page to publish the application.

   * If your application requires approval, click the "Submit for release" button in the upper\-right corner of the page. After the enterprise Feishu administrator has approved your application, publish the application.


<span id="8sxPMihw"></span>
### Step 3: Obtain enterprise authentication information


1. (Optional) On the[ Feishu Open Platform](https://open.larkoffice.com/app?lang=zh-CN), click the name of the custom application to enter the development page of the application (in this example, "ArkClaw"). If you are already on the application development page, skip this step.

2. In the left directory tree, select "Basic Info" \> "Credentials & Basic Info", and then record the App ID and App Secret.


<span id="2orpKEw3"></span>
## Step 2: Grant permissions for accessing services

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><strong>Trigger condition:</strong> This step is triggered only when you activate ArkClaw for the first time. It is skipped for subsequent space activations with the same account.</div>


* <div data-tips="true" data-tips-type="default"><strong>Authorization scope:</strong> Authorize ArkClaw to access the following cloud services: VPC, ECS, PrivateLink, TOS, and MLP (see the Terms of Service for the actual service list).</div>


* <div data-tips="true" data-tips-type="default"><strong>Model permissions:</strong> Grant permissions to invoke all <strong>non\-Coding Plan</strong> models in ModelArk with a few clicks to facilitate model selection in ArkClaw later.</div>


* <div data-tips="true" data-tips-type="default"><strong>Billing information:</strong> This step itself does not incur fees. Subsequent <strong>use</strong> of enabled models, ModelArk services, or Web Search incurs ‌pay\-as\-you\-go billing‌. The following services incur fees:</div>


   * <div data-tips="true" data-tips-type="default">ModelArk</div>


   * <div data-tips="true" data-tips-type="default">Online search</div>


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. In the pop\-up window, carefully read the relevant service terms. After you confirm the terms, select "I have read and agree to the Terms of ArkClaw Services"..

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c2f1ec730d3fb88c943f3a6ea8ef1f4.png) </span>

3. Click "Activate and authorize" to complete role authorization and model activation.


<span id="fPcVI5By"></span>
## Step 3: Configure the ArkClaw service


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. On the service activation page, configure the relevant information according to the table below.

   
   |Configuration item |Description |
   |---|---|
   |**Basic information** ||
   |Space name |Set the ArkClaw space name. The platform automatically generates a name, which administrators can modify as needed. After the space is activated, the space name can be changed at any time. For details, see [Viewing space configuration information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information?lang=en#ftsmTKKb). |
   |**Employee access control** ||
   |Authentication |Configure access control settings for enterprise employees. Select **Feishu authentication**, and configure the Feishu application information where the enterprise system permissions are granted. This allows other employees to log in and use ArkClaw via their Feishu tenant SSO.<br><br><br>* App ID: Enter the App ID of the Feishu application.<br><br>* App Secret: Enter the App Secret of the Feishu application. |
   |**Space management type** ||
   |Select space management type |Select the management type for Claw instances in the current space. **This setting cannot be modified after the space is activated**.<br><br><br>* **Seat Management**: Subscription is based on the total number of seats. Seats of the same edition share a unified expiration date, and you do not need to manage the lifecycle of each Claw instance separately. Within the purchased seat quota, Claw instances can be provisioned or allocated as needed.<br><br>* **Instance Management**: Claw instances are managed individually. All Claw instances in the space are created, allocated, and managed separately. Each Claw instance has a separate resource lifecycle and must be managed individually.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Selecting the space management type is a beta feature and is available only after beta access is granted. If you need to use this feature, contact your account manager</strong>.</div><br> |
   |**Network configuration** ||
   |Space network configuration |The VPC CIDR block and subnet CIDR block for ArkClaw Enterprise. The platform will automatically create network resources such as a VPC, subnet, and security group for the ArkClaw space in the current region, establishing the network environment required for the ArkClaw space to operate in.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After an ArkClaw Enterprise space is activated, modifying the VPC CIDR block or subnet CIDR block is not supported.</div><br><br><br><br>* **Random network creation**:<br><br>   * No network configuration is required. The platform will create the VPC and subnet for ArkClaw using a randomly assigned private CIDR block.<br><br>   * If you need to access ArkClaw VPC resources from another VPC later, ensure that the VPC address does not belong to the following CIDR blocks to avoid conflicts: `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, and `9.0.0.0/8`.<br><br>* **Specified network creation**:<br><br>   * If you need to connect to ArkClaw's VPC via Cloud Enterprise Network (CEN) or Transit Router (TR) in the future, specify an ArkClaw VPC CIDR block based on your network planning.<br><br>   * Click "Custom configuration" in the upper\-right corner of the card and enter the desired CIDR block for the custom VPC. The platform will create the VPC and subnet based on your input. Ensure the custom CIDR block does not belong to the following network segments: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/8`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, `169.254.0.0/16`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The ArkClaw VPC feature is in beta and available only upon activation. If you need to use this feature, contact your account manager</strong>.   </div><br>    |
   

3. After configuration is completed, click the "Activate now" button to complete the service space configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">ArkClaw supports independent ArkClaw spaces for different projects.<strong> This is a beta feature available only after a successful feature request.</strong> For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide?TagIDs=2,522,512,502&lang=en#rH30UfdE">Activating multiple spaces</a>.   </div>
   

   4. ModelArk API keys used in Foundation models have permission to invoke all models. A dialog box will appear to confirm this when space activation is complete. To manage the model scope, click "[Volcano Ark Management Console](https://console.byteplus.com/ark/region:cn-beijing/apiKey?apikey=%7B%7D&projectName=default)". If you do not need to manage the model scope, click "Got it" to close the dialog box.


<span id="2bGpjS7T"></span>
## Step 4: Purchase ArkClaw Enterprise seats

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you selected "Instance Management" for "Select space management type" in the previous step to activate the ArkClaw space, skip this section</strong>.</div>



1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. On the ArkClaw management page, click "Buy now".

3. Specify an ArkClaw seat edition and quantity, and select a subscription duration.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Minimum order quantity for an ArkClaw seat purchase</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The minimum order quantity for a single purchase of ArkClaw seats is 5. Orders with fewer than 5 seats cannot be placed.   </div>
   

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
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To share ModelArk Plans across multiple scenarios, we recommend purchasing an independent ModelArk Plan, obtaining independent API Keys directly from ModelArk, and then configuring the model via "Custom model source." For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Model_management?lang=en#MXrT1Usf">Configuring custom model pools</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Automatic renewal</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The "Automatic renewal" option is selected by default to prevent ArkClaw service suspension due to subscription expiration. You can manually cancel this option. If you do that, ensure you renew your subscription before expiration.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After "Auto\-renewal" is enabled, automatic renewal applies to all subsequent new purchases and change orders under the space.   </div>
   

   
   |Specifications |Applicable scenario |
   |---|---|
   |Starter edition |Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations. |
   |Standard edition |The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations. |
   |Premium edition |Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects. |
   |Ultimate edition |Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   

4. After configuration is complete, click "Purchase" and follow the on\-screen instructions to pay the fees. Once payment is successful, click "Go to console" to complete the service activation. Service activation takes approximately 3–5 minutes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Common reasons for service activation failure include incomplete enterprise real\-name authentication, VPC CIDR block conflicts, or insufficient resources. </strong>If activation still fails after confirming these are resolved, copy the error message displayed on the page and click <strong>Submit a ticket</strong> for assistance.   </div>
   

<span id="Yr94Sjs5"></span>
## Step 5: Configure callback information


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Space Overview". To the right of the Feishu authorization code redirect URL, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_853b8594d5dded0729fe89fbec66a9dc.png) </span>icon, and then click "Configure".

   2. You will be automatically redirected to the "Security Settings" page of the Feishu application configured with enterprise system permissions in the [Feishu Developer Console](https://open.larkoffice.com/app?lang=zh-CN).

   3. Paste the Feishu authorization code redirect URL copied from the ArkClaw space into the **Redirect URL** field and click "Add". This setting takes effect immediately.


<span id="M6z6KsDu"></span>
## Step 6: Import user information


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the Users page, import user information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Importing user information supports two methods: full synchronization and batch upload. This step demonstrates only full synchronization. For information about uploading information in batches, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Feishu_-_User_information_import">Importing user information</a>.   </div>
   

      1. Click the "Full sync" button.

   2. In the pop\-up window, click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information, then click "Go to Feishu to authorize". For detailed authorization steps, see [Step 1: Configuring the Feishu application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication)[Configuring enterprise system permissions](https://docs.byteplus.com/en/docs/ArkClaw/Configure_enterprise_system_permissions#jtC4t9zf).

   3. After Feishu permissions are successfully enabled, return to the dialog and click the "Refresh" button. Once all required permissions are tagged as "Authorized", click "Sync data" in the dialog.

   4. After confirming that the Feishu employee data are correctly synchronized, click "Confirm import" in the dialog box to complete the operation.

   5. (**Optional**) Synchronize employee information incrementally.

      1. Click "Add employee".

      2. Click the "Full sync" button in the pop\-up window.

      3. The system automatically syncs Feishu employee data. After the sync is complete, verify that the results are correct and then click "Confirm import" in the dialog to complete the operation.

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If fields such as email address and mobile number are missing from the imported employee information, you can either manually complete the missing information or synchronize existing employee information from Feishu. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=en#wAIx9Wfy">Updating user information</a>.      </div>
      

4. Select "Space Overview" in the left navigation pane to obtain the employee login link.


<span id="qtl4LbXY"></span>
## Step 7: Distribute employee login URL

Distribute the employee login link via any messaging channel (such as Feishu or email) adopted by your enterprise to employees who need to use ArkClaw. Employees can log in and use ArkClaw via Feishu SSO authentication.
