---
title: "Lark authentication"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication"
---

This topic describes the complete process for activating and using a space via Lark. After you complete the steps in this topic, you have a Lark SSO\-integrated ArkClaw space, allowing enterprise employees to log in with one click in Lark.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Application scenario:</strong> Your enterprise already uses Lark for team collaboration and wants to reuse its existing account system to avoid creating separate accounts.</div>


<span id="A2hYWSp5"></span>
## Step 1: Configure Lark application and permissions

<span id="9mf7cXRg"></span>
### Step 1: Create a Lark enterprise application


1. Log in to the [Lark Open Platform](https://open.larksuite.com/app?lang=en-US), and click the "Create Custom App" button.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b31c06032762bd80dc2425cd0b74290.png) </span>


2. Provide an application name, description, and icon, and click "Create".


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7443ee122d65c2ba681e131e50f6158.png) </span>

<span id="C1WQ9cGJ"></span>
### Step 2: Configure Lark application permissions


1. (Optional) On the [Lark Open Platform](https://open.larksuite.com/app?lang=en-US), click the name of the custom application to enter the development page of the application (in this example, "ArkClaw"). If you are already on the application development page, skip this step.

2. In the directory tree on the left, select "Development Configuration \> Permissions & Scopes", and click the "Batch import/export scopes" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b0705e9a81f152c04d9961cdd6bb90f5.png) </span>

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
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76d832d98fa95b273dac27c8632ea5d9.png) </span>

4. Confirm the permissions are correct, and then click the "Add" button to complete the operation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec24fddde5a1e281674f6b404bd3c19e.png) </span>

5. Set the accessible data scope for the permission (by default, the same as the availability of the application). Save your settings and click "Confirm" to complete the operation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_953b30e4527a4096e0ae75e43de12757.png) </span>

6. In the left directory tree, select "App Versions \> Version Management & Release", and then click the "Create a version" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d871c7b7754827662954450441a874e.png) </span>

7. Provide an application version number and update description. Click the "Edit" button next to the "Availability" field to specify the effective scope of the configuration.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66576c9a5b227d4a5167e67fe9785ba4.png) </span>

8. Set the availability range of this enterprise application. To do so, add the Lark accounts of enterprise employees who need to use ArkClaw Enterprise and click the "Done" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can configure application availability settings to configure which employees have access to ArkClaw. If you do not need to restrict ArkClaw access across the enterprise, select "All members" to grant ArkClaw access to all employees in the enterprise.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_200a447882bce43f437410d424a09122.png) </span>

9. Click the "Save" button at the bottom of the page to create the version.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are not an enterprise Lark administrator, include a detailed description of your business scenario and application functionality when applying to create the application. This information helps your application get approved by the enterprise Lark administrator.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_efcc1f186b5accb8149b48dc553cb75b.png) </span>

10. Publish the application.

   * If your application does not require approval, click the "Publish" button in the upper\-right corner of the page to publish the application.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_283080243b0fe5909d54624d49c0000d.png) </span>

   * If your application requires approval, click "**Submit for Release Review**" in the upper\-right corner of the page. After the Lark administrator approves your application, publish the application.


<span id="2GrZcKpr"></span>
### Step 3: Obtain credentials


1. (Optional) On the [Lark Open Platform](https://open.larksuite.com/app?lang=en-US), click the name of the custom application to enter the development page of the application (in this example, "ArkClaw"). If you are already on the application development page, skip this step.

2. In the left directory tree, select "Basic Info \> Credentials & Basic Info", and then copy and save the App ID and App Secret.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d7a150e99b9304c5045ddb054db5d6c4.png) </span>


<span id="ZGGM0TSS"></span>
## Step 2: Grant permissions for accessing services

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><strong>Trigger condition:</strong> This step is triggered only when you activate ArkClaw for the first time. It is skipped for subsequent space activations with the same account.</div>


* <div data-tips="true" data-tips-type="default"><strong>Authorization scope:</strong> Authorize ArkClaw to access the following cloud services: VPC, ECS, PrivateLink, TOS, and MLP (see the Terms of Service for the actual service list).</div>


* <div data-tips="true" data-tips-type="default"><strong>Model permissions:</strong> Grant permissions to invoke all <strong>non\-Coding</strong> Plan models in ModelArk with a few clicks to facilitate model selection in ArkClaw later.</div>


* <div data-tips="true" data-tips-type="default"><strong>Billing information</strong>: This step itself does not incur fees. Subsequent <strong>use </strong>of enabled models, ModelArk services, or Web Search incurs ‌pay\-as\-you\-go billing‌. The following services incur fees:</div>


   * <div data-tips="true" data-tips-type="default">ModelArk</div>


   * <div data-tips="true" data-tips-type="default">Online search</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. In the pop\-up window, carefully read the relevant service terms, and after confirming that everything is correct, select "I have read and agree to the Terms of ArkClaw Services".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c2f1ec730d3fb88c943f3a6ea8ef1f4.png) </span>

4. Click the "Activate and authorize" button to complete role authorization and model activation.


<span id="PS3nQfMf"></span>
## Step 3: Configure the ArkClaw service


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. On the service activation page, configure the relevant information according to the table below.

   
   |Configuration item |Description |
   |---|---|
   |**Basic information** ||
   |Space name |Set the ArkClaw space name. The platform automatically generates a name, which administrators can modify as needed. After the space is activated, the space name can be changed at any time. For details, see [Viewing space configuration information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information?lang=en#ftsmTKKb). |
   |**Employee access control** ||
   |Authentication |When configuring the enterprise's employee access control, select **Lark authentication** and configure the enterprise Lark application information where the enterprise system permissions are granted. This is used for other employees to log in and use ArkClaw later via their own Lark tenant SSO. |
   |App ID |Enter the App ID of the Lark application. |
   |App Secret |Enter the App Secret of the Lark application. |
   |**Space management type** ||
   |Select space management type |Select the management type for Claw instances in the current space. **This setting cannot be modified after the space is activated**.<br><br><br>* **Seat Management**: Subscription is based on the total number of seats. Seats of the same edition share a unified expiration date, and you do not need to manage the lifecycle of each Claw instance separately. Within the purchased seat quota, Claw instances can be provisioned or allocated as needed.<br><br>* **Instance Management**: Claw instances are managed individually. All Claw instances in the space are created, allocated, and managed separately. Each Claw instance has a separate resource lifecycle and must be managed individually.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Selecting the space management type is a beta feature and is available only after beta access is granted. If you need to use this feature, contact your account manager</strong>.</div><br> |
   |**Network configuration** ||
   |Space network configuration |The VPC CIDR block and subnet CIDR block for ArkClaw Enterprise. The platform will automatically create network resources such as VPCs, subnets, and security groups in the current region to set up the network environment for ArkClaw.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After an ArkClaw Enterprise space is activated, modifying the VPC CIDR block or subnet CIDR block is not supported. <strong>The ArkClaw private network is a beta feature and is available only upon activation. If needed, contact your account manager to activate it.</strong></div><br><br><br><br>* **Random network creation**:<br><br>   * No network configuration is required. The platform will create the VPC and subnet for ArkClaw using a randomly assigned private network segment.<br><br>   * If you need to access ArkClaw private network resources from another VPC later, ensure that the VPC address does not belong to the following network segments to avoid conflicts: `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`.<br><br>* **Specified network creation**:<br><br>   * If you need to connect to ArkClaw's VPC via Cloud Enterprise Network (CEN) or Transit Router (TR) in the future, specify an ArkClaw VPC CIDR block based on your network planning.<br><br>   * Click "Custom configuration" in the upper\-right corner of the card and enter the desired CIDR block for the custom VPC. The platform will create the VPC and subnet based on your input. Ensure the custom CIDR block does not belong to the following network segments: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/8`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, `169.254.0.0/16`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Reminder for overseas users:</strong> To prevent irreversible conflicts, when planning subnets for ArkClaw spaces interconnecting with overseas VPCs across regions, reference RFC1918 usage in those areas during subnet planning.   </div><br>    |
   

4. After configuration is completed, click the "Activate now" button to complete the service space configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">ArkClaw supports independent ArkClaw spaces for different projects.<strong> This beta feature is available only after activation.</strong> For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide?TagIDs=2,522,512,502&lang=en#rH30UfdE">Activating multiple spaces</a>.   </div>
   

   5. ModelArk API keys used in Foundation models have permission to invoke all models. A dialog box will appear to confirm this when space activation is complete. To manage the model scope, click "[Volcano Ark Management Console](https://console.byteplus.com/ark/region:cn-beijing/apiKey?apikey=%7B%7D&projectName=default)". If you do not need to manage the model scope, click "Got it" to close the dialog box.


<span id="Ai1qN7PP"></span>
## Step 4: Purchase ArkClaw Enterprise seats

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you selected "Instance Management" for "Select space management type" in the previous step to activate the ArkClaw space, skip this section</strong>.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. On the ArkClaw management page, click the "Buy now" button.

4. Specify an ArkClaw seat edition and quantity, and select a subscription duration.

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
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To share ModelArk Plans across multiple scenarios, we recommend purchasing an independent ModelArk Plan, obtaining independent API Keys directly from ModelArk, and then configuring the model via "Custom model source." For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Model_management?lang=en#MXrT1Usf">Configuring custom model pools</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Automatic renewal</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The "Automatic renewal" option is selected by default to prevent ArkClaw service suspension due to subscription expiration. You can manually cancel this option. If you do that, ensure you renew your subscription before expiration.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After "Auto\-renewal" is enabled, automatic renewal will be applied to all subsequent new purchases and change orders under the space.   </div>
   

   
   |Specifications |Applicable scenario |
   |---|---|
   |Starter edition |Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations. |
   |Standard edition |The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations. |
   |Premium edition |Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects. |
   |Ultimate edition |Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   

5. After configuration is complete, click "Purchase" and follow the on\-screen instructions to pay the fees. Once payment is successful, click "Go to console" to complete the service activation. Service activation takes approximately 3–5 minutes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Common reasons for service activation failure include incomplete enterprise real\-name authentication, VPC CIDR block conflicts, or insufficient resources. </strong>If activation still fails after confirming these are resolved, copy the error message displayed on the page and click <strong>Submit a ticket</strong> for assistance.   </div>
   

<span id="2wM9DZLQ"></span>
## Step 5: Configure callback information


1. In the left navigation pane of [ArkClaw Enterprise console ](https://console.byteplus.com/arkclaw/enterprise), select "Space Overview".

2. On the "Space overview" page, click the "copy" icon after the Lark authorization code redirect URL and then click "Configure".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d777814965ae6a32724ede36505b3d5.png) </span>

3. The page automatically redirects to the Lark Developer Platform "Security Settings" page for the Lark application with enterprise system permissions configured.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17ec1bd92e5c5e70290dc83f29027b94.png) </span>

4. Paste the Lark authorization code redirect URL copied from the ArkClaw space into the **Redirect URL** field and click "Add". This setting takes effect immediately.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d3ed325782eff27f9e88ac7046408911.png) </span>


<span id="8Ej7Iwbu"></span>
## Step 6: Import user information


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Organizations" \> "Users".

   2. On the Users page, import user information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Importing user information supports two methods: full synchronization and batch upload. This step demonstrates only full synchronization. For information about uploading information in batches, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Feishu_-_User_information_import">Importing user information</a>.   </div>
   

      1. Click the "Full sync" button.

   2. In the pop\-up window, click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information, then click "Go to Lark to authorize". For detailed authorization steps, see [Step 1: Configuring the Lark application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication#A2hYWSp5)[Configuring enterprise system permissions](https://docs.byteplus.com/en/docs/ArkClaw/Configure_enterprise_system_permissions#jtC4t9zf).

   3. After you grant the Lark application permissions, return to the dialog box and click "Refresh". After all required permissions are tagged as "Authorized", click "Completed" in the dialog box.

   4. After confirming that the Lark employee data are correctly synchronized, click "Confirm import" in the dialog box to complete the operation.

   5. (**Optional**) Synchronize employee information incrementally.

      1. Click "Add employee".

      2. Click the "Full sync" button in the pop\-up window.

      3. The system automatically syncs Lark employee data. After the sync is completed, confirm that the sync results are correct, then click "Confirm Import" in the dialog to complete the operation.

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the imported employee information is missing fields such as email or phone number, you need to manually supplement the missing employee information or sync and update the existing employee information in Lark. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=en#wAIx9Wfy">Updating user information</a>.      </div>
      

   3. Select "Space Overview" in the left navigation pane to obtain the employee login link.

   <span id="kjkeOjmk"></span>
   ## Step 7: Distribute employee login URL

Distribute the employee login link to employees who need to use ArkClaw through any messaging method (e.g., Lark or email) used in the enterprise. The employees can then log in and use ArkClaw via Lark SSO authentication.
