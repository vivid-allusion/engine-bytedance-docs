---
title: "Slack authentication"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Slack_authentication"
---

This topic describes the complete process of activating and using a space via Slack.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This method uses the SSO capability provided by Slack and is suitable for organizations that use Slack for team collaboration.</div>


<span id="6vUbFkDp"></span>
## Step 1: Configure Slack and permissions

<span id="41fgnLYT"></span>
### Step 1: Create a Slack workspace


1. Log in to the [Slack console](https://slack.com/get-started?entry_point=redirect_flow#/landing).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65250e5449e36af5985c64b5c46f4704.png) </span>

2. Click the "Create a new workspace" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_896d47e4e474743594ef9650ff303870.png) </span>

3. Enter the name of the workspace, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59a81508d3247767b23a31ade3f8c43d.png) </span>

4. Customize your name and avatar as needed, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b5f61c767af3678a3cabb10bc19a3a1.png) </span>

5. To add colleagues to join the current workspace, click the "Next" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no information needs to be added, click the "Skip this step" button.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_70074b1c3730b03733c0d0bcd64f88a0.png) </span>

6. Select the Slack version. In the example provided in this topic, "Start with Limit Free Version" is selected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_057120c45046d3ced954007f255d65c2.png) </span>


<span id="Zu0yQN1Q"></span>
### Step 2: Create a Slack application


1. Log in to the [Slack API console](https://api.slack.com/apps), and then click the "Create an App" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f00241f88f8671763a71e77df1eb7751.png) </span>

2. In the pop\-up window, select "**From scratch**".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de0cdad6311f7b4c86901b9bf70959ac.png) </span>

3. Enter the name of the application and select the workspace where the application will be deployed, and then click the "**Create App**" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_019e5a68058a5e2d6af5a45cb53abb4c.png) </span>

4. In the left navigation pane of the application management page, select "**Features** \> **OAuth & Permissions"** .

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8601cb355497ad064de2c449d1d354ec.png) </span>

5. Scroll down to the **Scopes** section. In the "**User Token Scopes**" section, click the "**Add an OAuth Scope**" button, and then add the following three permissions in sequence: `openid`, `email`, and `profile`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47b60de0a7bc6a06c5e4a0f2216a895a.png) </span>


<span id="Gqcv3rkB"></span>
### Step 3: Configure application visibility


1. Log in to the [Slack console](https://slack.com/get-started?entry_point=redirect_flow#/landing).

2. Click the workspace name, and then click "Invite people to Ark".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5c751019eb300a43093a9baf70a8c71.png) </span>

3. Add the information of personnel who need to use ArkClaw Enterprise. Then, click the "Send" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08d29b63fe50abc141ca6cfd93412618.png) </span>


<span id="XhsBz8H0"></span>
### Step 4: Obtain credential information


1. In the left navigation pane of the application management page, select "**Settings** \> **Basic Information**".

2. In the **App Credentials** section, copy and properly save the **Client ID** and **Client Secret** information. These two values will be used when you configure ArkClaw Enterprise later.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c776590b2a1ab7e69f87cef0cd0ce693.png) </span>


<span id="KhMDBzT8"></span>
## Step 2: Grant permissions for accessing services

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Authorization is required only when activating the ArkClaw Enterprise services for the first time. If this is not your first time, please skip this section.</div>


* <div data-tips="true" data-tips-type="default">When activating the ArkClaw Enterprise for the first time, you need to first grant the permissions required by the ArkClaw Enterprise to access other cloud services. Meanwhile, the platform will automatically activate all non\-Coding Plan models of ModelArk.</div>


* <div data-tips="true" data-tips-type="default">The activation of the model and services does not incur any fees. After activation, if the associated billable services are used, charges will apply on a pay\-as\-you\-go basis with corresponding billing. The billable services are as follows:​</div>


   * <div data-tips="true" data-tips-type="default">ModelArk</div>


   * <div data-tips="true" data-tips-type="default">Online search</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. In the pop\-up window, carefully read the relevant service terms, and after confirming that everything is correct, select "I have read and agree to the Terms of ArkClaw Services".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c2f1ec730d3fb88c943f3a6ea8ef1f4.png) </span>

4. Click the "Activate and authorize" button to complete role authorization and model activation.


<span id="6VhGZMTT"></span>
## Step 3: Configure the ArkClaw service


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. On the service activation page, configure the relevant information according to the table below.

   
   |Configuration item |Description |
   |---|---|
   |Employee access control |When configuring the enterprise's employee access control, select **Slack authentication** and configure the Slack application information where the enterprise system permissions are granted. This is used for other employees to log in and use ArkClaw later via their own Slack accounts.<br><br><br>* **Client ID**: Enter the ID of the Slack application.<br><br>* **Client Secret**: Enter the Secret of the Slack application. |
   |Network configuration |The VPC CIDR block and subnet CIDR block for ArkClaw Enterprise. The platform will automatically create network resources such as VPCs, subnets, and security groups in the current region to set up the network environment for ArkClaw.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After an ArkClaw Enterprise space is activated, modifying the VPC CIDR block and subnet CIDR block is not supported.</div><br><br><br><br>* **Random network creation**:<br><br>   * No network configuration is required. The platform will create the VPC and subnet for ArkClaw using a randomly assigned private network segment.<br><br>   * If you need to access ArkClaw private network resources from another VPC later, ensure that the VPC address does not belong to the following network segments to avoid conflicts: `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`.<br><br>* **Specified network creation**:<br><br>   * If you need to connect to ArkClaw's VPC via Cloud Enterprise Network (CEN) or Transit Router (TR) in the future, specify an ArkClaw VPC CIDR block based on your network planning.<br><br>   * Click "Custom configuration" in the upper\-right corner of the card and enter the desired CIDR block for the custom VPC. The platform will create the VPC and subnet based on your input. Ensure the custom CIDR block does not belong to the following network segments: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/8`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, `169.254.0.0/16`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The ArkClaw private network is a beta feature and is available only upon activation. If needed, please contact your account manager to activate it</strong>.   </div><br>    |
   

4. After configuration is completed, click the "Activate now" button to complete the service space configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">ArkClaw supports independent ArkClaw spaces for different projects. This <strong>is an allowlist\-restricted feature available only after a successful feature request</strong>. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide?TagIDs=2,522,512,502&lang=en#rH30UfdE">Activating multiple spaces</a>.   </div>
   

<span id="PZW6iv6T"></span>
## Step 4: Purchase ArkClaw Enterprise seats


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. On the ArkClaw management page, click the "Buy now" button.

4. Specify an ArkClaw seat edition and quantity, and select a subscription duration.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Minimum order quantity for an ArkClaw seat purchase</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The number of seats purchased per order for ArkClaw Enterprise must be at least 5 (inclusive).   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Different seat specifications apply to different scenarios. You can purchase a combination of seat specifications as needed. For more billing details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Billing_instructions">Billing instructions</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>AgentPlan purchases</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When purchasing ArkClaw seats, you may bundle AgentPlans at the same time. Alternatively, you may purchase seats only and bind AgentPlans later as needed.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Purchased AgentPlans cannot be canceled.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ArkClaw seats and AgentPlans do not have a one\-to\-one mapping. All Claw instances under an employee's account share the allocated AgentPlans.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>CodingPlan purchases</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Purchasing CodingPlans during space activation is currently not supported. If necessary, purchase or manage them after the space is activated. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_CodingPlan">Managing ModelArk Plans</a>.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">All Claw instances with access to the seat edition of CodingPlans share all CodingPlan resources for the seat edition.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Purchase and change restrictions</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Quantity thresholds</strong>: In a bundled purchase of ArkClaw seats and AgentPlans, the total number of AgentPlans in ArkClaw must be at least <strong>5</strong> (including those purchased in ArkClaw and ArkClaw\-managed ones from ModelArk). Each order supports a maximum of 1,000 AgentPlans (inclusive).   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Exclusiveness restriction: ModelArk Plans purchased in ArkClaw are not recommended for use outside ArkClaw scenarios.</strong> ArkClaw Enterprise will periodically rotate the API keys of managed ModelArk Plans, which may affect usage in other scenarios. If a ModelArk Plan is used for both ArkClaw and other purposes, we recommend purchasing it directly from ModelArk to obtain an APIKey and then configuring the model via "Custom model source". For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Model_management?lang=en#MXrT1Usf">Configuring custom model pools</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Automatic renewal</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The "Automatic renewal" option is selected by default to prevent ArkClaw service suspension due to subscription expiration. You can manually cancel this option. If you do that, ensure that you renew your subscription before expiration.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After "Auto\-renewal" is enabled, automatic renewal will be applied to all subsequent new purchases and change orders under the space.   </div>
   

   
   |Specifications |Applicable scenario |
   |---|---|
   |Starter edition |Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations. |
   |Standard edition |The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations. |
   |Premium edition |Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects. |
   |Ultimate edition |Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   

5. After configuration is complete, click "Purchase" and follow the on\-screen instructions to pay the fees. Once payment is successful, click "Go to console" to complete the service activation. Service activation takes approximately 3–5 minutes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If service activation fails, copy the error information as prompted on the page and click the "Submit ticket" button for assistance.   </div>
   

<span id="hYJBPaLe"></span>
## Step 5: Configure callback information


1. In the left navigation pane of [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Space Overview".

2. On the "Space overview" page, click the "copy" icon after the Slack authorization code redirect URL and then click "Configure".

3. In the left navigation pane of the Slack application management page, select **Features** \> **OAuth & Permissions**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_95f56b38615928a1b3267c8e7f9798fe.png) </span>

4. Scroll down the page. In the "**Redirect URLs**" section, click **Add New Redirect URL**and enter the domain name copied from the ArkClaw Enterprise console.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fc378f1950b02b537455d38d8f318630.png) </span>

5. Click "Add" and then click "**Save URLs**" to save the settings.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7079154ff9c5f073cd840745f2ec8f99.png) </span>


<span id="f08nK4rl"></span>
## Step 6: Distribute the employee login link

Distribute the employee login link to employees who need to use ArkClaw through any messaging method (e.g., Slack or email) used in the enterprise. The employees can then log in and use ArkClaw via Slack SSO authentication.
