---
title: "OAuth 2.0"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/OAuth"
---

ArkClaw Enterprise supports integration with your enterprise's existing identity provider (IdP) via OAuth 2.0/OIDC, enabling unified employee login and single sign\-on (SSO). This topic uses **BytePlus Agent Identity** and **Alibaba Cloud IDaaS** as examples to guide administrators through the entire process of creating an IdP application, activating an ArkClaw space, configuring protocol parameters, and providing the callback address. After the process is complete, administrators can provide employees with the employee login link for use.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Using other standard protocols enables you to activate ArkClaw Enterprise quickly. Relevant information will be used in the configuration procedure after ArkClaw Enterprise activation.</div>


* <div data-tips="true" data-tips-type="default">ArkClaw supports independent ArkClaw spaces for different projects.<strong> This is a beta feature available only after a successful feature request. </strong>For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide?TagIDs=2,522,512,502&lang=en#rH30UfdE">Activating multiple spaces</a>.</div>



<span id="psLeHYII"></span>
## Use BytePlus Agent Identity as an example

<span id="tJzSkrSt"></span>
### Step 1: Create a user pool


1. Log in to the [BytePlus Agent Identity console](https://console.byteplus.com/identity). In the left navigation pane, select "Identity management \> User pool".

2. Click the "Create user pool" button in the upper\-right corner and configure the user pool parameters.

   
   |Configuration item |Description |
   |---|---|
   |**User pool name** |Set a unique name for your user pool, for example, `my-app-users`. |
   |**Description** |Provide a brief description of the purpose of this user pool, for example, "for internal and external user management of the XX application". |
   |**Attributes for user pool login** |Select the identity identifier that users need to provide​​ in login attempts.<br><br><br>* Available options: **Username**, **Mobile number**, and **Email**<br><br>* Default options: **Username and Mobile number**<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration cannot be modified after creation.</div><br> |
   |**Attributes for user pool registration** |Select the identity identifier that a user must provide during the registration process.<br><br><br>* Available options: **Username**, **Mobile number, Email, Full name, First name, Last name, Middle name, and more**<br><br>* Default options: **Username and Mobile number** |
   |**Associated project** |* Select the project to which the user pool belongs. Projects facilitate resource isolation and management.<br><br>* You can select an existing project from the drop\-down list, or click **Create project** to create one. |
   |**Tag** |* Add tags to the user pool to facilitate resource categorization and filtering.<br><br>* Click **Add tag** to add a new key\-value pair.<br><br>* You can add up to 20 tags. |
   

3. Click the "Confirm" button.

   The system automatically creates a new user pool, which has a unique **user pool ID**, **TRN**, and **OIDC discovery endpoint**.


<span id="nb60nTTG"></span>
### Step 2: Create a client


1. On the result page, click "Create client".

2. Configure basic client settings.

   
   |Configuration item |Description |
   |---|---|
   |**Client name** |Provide a descriptive name for your application client, such as `my-webapp-client`. |
   |**Client type** |Select a client type based on your application type:<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For this scenario (integration with ArkClaw), select <strong>Web Application</strong>. Other options apply to different application types and are not covered in this topic.</div><br><br><br><br>* **Web application**: Traditional server\-rendered website applications developed with programming languages such as Java and PHP.<br><br>* **Single\-page application**: Frontend\-backend decoupled applications built with frameworks such as React and Vue.<br><br>* **Mobile application**: Native applications installed on smartphones or tablet devices, such as iOS and Android apps.<br><br>* **M2M (Machine\-to\-Machine)** : Backend service\-to\-service invocation without user interaction, such as scheduled cron jobs and microservices. |
   |**Allow callback URIs** |* After a user logs in and completes authorization, the system redirects the user to this URL. You can specify multiple URLs, with each placed on a separate line and starting with `http://` or `https://`.<br><br>* Leave this parameter empty for now. After completing Step 8, enter the "Authorization code redirect URL" provided by ArkClaw into this field. |
   

3. Click the "Confirm" button.

4. Click the name of the created client to obtain the Client ID and Client Secret. You need to specify these two parameter values in ArkClaw Enterprise as the client ID and secret.

   * Client ID **: ** The unique identifier **of** the client. It is used to identify the client application in authentication requests.

   * Client secret: The secret of the client identity. It is used to verify the client identity in authentication requests.


<span id="WuJnQoaW"></span>
### Step 3: Obtain enterprise authentication information


1. In the left navigation pane of the [BytePlus Agent Identity console](https://console.byteplus.com/identity), select  **"Identity management" \> "User pool"** .

2. Click the name of the user pool created in Step 1 to view user pool information.

3. Copy the "OIDC discovery endpoint discovery URL" and paste it into the address bar of the browser to open it.

4. Pretty\-print the output and retrieve the following endpoint information, which will be used for configuring protocol authentication parameters later to implement access authorization.

   * **authorization_endpoint**: The authorization endpoint.

   * **token_endpoint**: The token endpoint.

   * **userinfo_endpoint**: The user information endpoint.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use <strong>scopes_supported</strong> to configure the authorization scope.   </div>
   

<span id="zvDwzSoU"></span>
### Step 4: Grant permissions for accessing services

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><strong>Trigger condition:</strong> This step is triggered only when you activate ArkClaw for the first time. It will be skipped for subsequent space activations with the same account.</div>


* <div data-tips="true" data-tips-type="default"><strong>Authorization scope:</strong> Authorize ArkClaw to access the following cloud services: VPC, ECS, PrivateLink, TOS, and MLP (see the Terms of Service for the actual service list).</div>


* <div data-tips="true" data-tips-type="default"><strong>Model permissions:</strong> Grant permissions to invoke all <strong>non\-Coding Plan</strong> models in ModelArk with a few clicks to facilitate model selection in ArkClaw later.</div>


* <div data-tips="true" data-tips-type="default"><strong>Billing information:</strong> This step itself does not incur fees. Subsequent <strong>use</strong> of enabled models, ModelArk services, or Web Search will incur ‌pay\-as\-you\-go billing‌. The following services incur fees:</div>


   * <div data-tips="true" data-tips-type="default">ModelArk</div>


   * <div data-tips="true" data-tips-type="default">Web search</div>


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. In the pop\-up window, carefully read the relevant service terms, and after confirming that everything is correct, select "I have read and agree to the Terms of ArkClaw Services".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c2f1ec730d3fb88c943f3a6ea8ef1f4.png) </span>

3. Click "Activate and authorize" to complete role authorization and model activation.


<span id="5KECgBvq"></span>
### Step 5: Configure the ArkClaw service


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. On the service activation page, configure the relevant information according to the table below.

   
   |Configuration item |Description |
   |---|---|
   |**Basic information** ||
   |Space name |Set the ArkClaw space name. The platform automatically generates a name, which administrators can modify as needed. After the space is activated, the space name can be changed at any time. For details, see [Viewing space configuration information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information?lang=en#ftsmTKKb). |
   |**Employee access control** ||
   |Authentication |Configure access control information for enterprise employees. Select **Other standard protocols**. After you select another standard protocol, there is no need to configure authentication parameters on the activation page. |
   |**Space management type** ||
   |Select space management type |Select the management type for Claw instances in the current space. **This setting cannot be modified after the space is activated**.<br><br><br>* **Seat Management**: Subscription is based on the total number of seats. Seats of the same edition share a unified expiration date, and you do not need to manage the lifecycle of each Claw instance separately. Within the purchased seat quota, Claw instances can be provisioned or allocated as needed.<br><br>* **Instance Management**: Claw instances are managed individually. All Claw instances in the space are created, allocated, and managed separately. Each Claw instance has a separate resource lifecycle and must be managed individually.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Selecting the space management type is a beta feature and is available only after beta access is granted. If you need to use this feature, contact your account manager</strong>.</div><br> |
   |**Network configuration** ||
   |Space network configuration |The VPC CIDR block and subnet CIDR block for ArkClaw Enterprise. The platform will automatically create network resources such as a VPC, subnet, and security group for ArkClaw in the current region, establishing the network environment required for ArkClaw to operate in.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After an ArkClaw Enterprise is activated, modifying the VPC CIDR block or subnet CIDR block is not supported.</div><br><br><br><br>* **Random network creation**:<br><br>   * No network configuration is required. The platform will create the VPC and subnet for ArkClaw using a randomly assigned private CIDR block.<br><br>   * If you need to access ArkClaw VPC resources from another VPC later, ensure that the VPC address does not belong to the following CIDR blocks to avoid conflicts: `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, and `9.0.0.0/8`.<br><br>* **Specified network creation**:<br><br>   * If you need to connect to ArkClaw's VPC via Cloud Enterprise Network (CEN) or Transit Router (TR) in the future, specify an ArkClaw VPC CIDR block based on your network planning.<br><br>   * Click "Custom configuration" in the upper\-right corner of the card and enter the desired CIDR block for the custom VPC. The platform will create the VPC and subnet based on your input. Ensure the custom CIDR block does not belong to the following network segments: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/8`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, `169.254.0.0/16`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The ArkClaw VPC feature is in beta and available only upon activation. If you need to use this feature, contact your account manager</strong>.   </div><br>    |
   

3. After configuration is completed, click the "Activate now" button to complete the service space configuration.

   4. ModelArk API keys used in Foundation models have permission to invoke all models. A dialog box will appear to confirm this when space activation is complete. To manage the model scope, click "[Volcano Ark Management Console](https://console.byteplus.com/ark/region:cn-beijing/apiKey?apikey=%7B%7D&projectName=default)". If you do not need to manage the model scope, click "Got it" to close the dialog box.


<span id="ncz0ODZo"></span>
### Step 6: Purchase ArkClaw Enterprise seats

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you selected "Instance Management" for "Select space management type" in the previous step to activate the ArkClaw space, skip this section</strong>.</div>



1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. On the ArkClaw management page, click "Buy now".

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
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Exclusiveness restriction: ModelArk Plans purchased in ArkClaw are recommended for use only within ArkClaw.</strong>   </div>
   

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
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Common reasons for service activation failure include incomplete enterprise real\-name authentication, VPC CIDR block conflicts, or insufficient resources.</strong> If activation still fails after confirming these are resolved, copy the error message displayed on the page and click <strong>Submit a ticket</strong> for assistance.   </div>
   

<span id="wrQE59Xj"></span>
### Step 7: Configure protocol information


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Organizations" \> "Users".

2. On the "Users" page, select the "Login configuration" tab. In the "Basic configuration information" section, click "Edit".

3. Enter the configuration information.

   
   |Configuration item |Description |
   |---|---|
   |Client ID |The unique client identifier that identifies the current application. This unique client identifier is automatically generated when the application is registered with the IdP. |
   |Client secret |The key that ensures secure communication with the IdP. It is generated after the application is created at the IdP.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">‌Store this securely to prevent leakage. If you suspect the secret has been compromised, ‌promptly reset it in your IdP console and update the configuration accordingly in ArkClaw.</div><br> |
   |Authorization endpoint |The authorization endpoint (login redirect URI) provided by the IdP for initiating the OAuth authorization flow. |
   |Token endpoint |The endpoint used to exchange an authorization code for an access token. It must be obtained from the application configurations at the IdP. |
   |UserInfo endpoint |The endpoint that requests detailed information (such as username and email address) about the logged\-in user with the access token included. It must be obtained from the application configurations at the IdP. |
   |Authorization scope |* The scope of user information requested during login authorization. For example, whether to obtain only basic identity information or also obtain personal information (such as avatar and nickname), email address, and phone number. **You can directly select or manually enter the scope**.<br><br>* The following values are typically included:<br><br>   * openid: The unique user identifier that identifies the user.<br><br>   * profile: The personal information of the user, such as the avatar, nickname, and name.<br><br>   * email: The email address of the user.<br><br>   * phone: The phone number of the user.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The authorization scope must be consistent with that supported by the IdP. For details, see the official documentation of the corresponding IdP.</div><br><br><br><br>* The following content provides an example of the configuration result:<br><br>   * Administrators set the authorization scope to `openid`, `profile`, `email`, or `phone`.<br><br>   * When you log in for the first time, the page will display the following requested permission information:<br><br><br> |
   |Unique user identifier |* It is used to identify a user and match a logged\-in user with existing users in the system. This field is generated by the IdP.<br><br>* Enter the fields in the user information returned by the IdP. The fields must be **globally unique and not easily changed**, and their values must be in **English**.<br><br>   * **Recommend**: Enter user ID\-type fields, such as `sub` and `user_id`. If no user ID\-type fields are available, you can use `email`, which is more stable but may be changed. In such cases, user data needs to be updated.<br><br>   * **Not recommended**: Use fields such as `name` or `nickname`, which may be modified or duplicated.<br><br>* Method of viewing user attributes: Access the OIDC discovery URL (`https://****/.well-known/openid-configuration`), and view the list of supported attributes by using the `claims_supported` node. For example:<br><br><br> |
   |Enable PKCE |Adds an additional layer of security protection to the authorization code flow. If you select this option, the client (e.g., mobile app) uses PKCE to prevent authorization code interception, enhancing security. |
   |Unique identifier policy |Select based on the primary identity information used by your enterprise. When importing employee information or switching authentication methods later, the system will automatically merge accounts that share the same phone number or email address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The unique identifier policy is used to determine whether the same employee has been imported multiple times: When the employee list is imported again, the system will merge records for the same employee into a single entry based on the unique identifier you select. This field<strong> only determines the basis for merging and does not determine the login method</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Policy options:</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Email:</strong> Applicable to scenarios where employee email addresses are standardized and uniformly managed across the enterprise.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Mobile number:</strong> Applicable to scenarios involving external contractors or temporary accounts.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>After the unique identifier policy is applied, we recommend against changing it later</strong>: If you change it, existing employee records may not match newly imported employee records, resulting in duplicate accounts.</div><br> |
   

4. Click "Confirm".


<span id="eUbGLPlw"></span>
### Step 8: Configure callback information


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Space Overview". To the right of the OAuth 2.0 authorization code redirect URL, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_853b8594d5dded0729fe89fbec66a9dc.png) </span> icon to copy the URL.

   2. Log in to the [BytePlus Agent Identity console](https://console.byteplus.com/identity). In the left navigation pane, select "Identity management \> User pool".

   3. Click the name of the user pool `my-app-users` created in "Step 1", and switch to the "Client" tab.

   4. Edit the information about the client created in Step 2, paste the copied SSO authorization code redirect URL into "Allowed callback URIs", and then click the "Confirm" button.

5. In the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), copy the employee login link on the "Space Overview" page and use your internal channel to send the link to employees who need to use ArkClaw.


<span id="76nIqSeF"></span>
## Alibaba Cloud IDaaS

<span id="qrPBlEJb"></span>
### Step 1: Create an OAuth application


1. Log in to the [Alibaba Cloud IDaaS console](https://yundun.console.aliyun.com/?p=idaas), select the corresponding IDaaS instance, and click "Console" in the "Actions" column.

2. In the left navigation pane, click "Application Management" and then click "Add Application".

3. On the "Standard Protocols" tab, add an OIDC application.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">OIDC is built on the OAuth 2.0 framework. Alibaba Cloud EIAM natively supports OAuth 2.0 authorization.   </div>
   

<span id="y0YroGOh"></span>
### Step 2: Obtain enterprise authentication information

Obtain application credentials, which will be used to configure protocol\-based authentication during ArkClaw Enterprise activation.


* On the **General Configuration** tab of the OIDC application details page, obtain the client ID (**`client_id`**) and client secret (**`client_secret`**).

* On the **Login Access** tab of the OIDC application details page, obtain the authorization, token, and user information endpoints:

   * **Authorization Endpoint**: It typically follows the `https://<your instance domain>/oauth2/authorize` format.

   * **Token Endpoint**: It typically follows the `https://<your instance domain>/oauth2/token` format.

   * **UserInfo Endpoint**: It typically follows the `https://<your instance domain>/oauth2/userinfo` format.


<span id="oJCwXfKw"></span>
### Step 3: Grant permissions for accessing services

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><strong>Trigger condition:</strong> This step is triggered only when you activate ArkClaw for the first time. It will be skipped for subsequent space activations with the same account.</div>


* <div data-tips="true" data-tips-type="default"><strong>Authorization scope:</strong> Authorize ArkClaw to access the following cloud services: VPC, ECS, PrivateLink, TOS, and MLP (see the Terms of Service for the actual service list).</div>


* <div data-tips="true" data-tips-type="default"><strong>Model permissions:</strong> Grant permissions to invoke all <strong>non\-Coding Plan</strong> ModelArk with one click to facilitate model selection in ArkClaw later.</div>


* <div data-tips="true" data-tips-type="default"><strong>Billing information:</strong> This step itself does not incur fees. Subsequent <strong>use</strong> of enabled models, ModelArk services, or Web Search will incur ‌pay\-as\-you\-go billing‌. The following services incur fees:</div>


   * <div data-tips="true" data-tips-type="default">ModelArk</div>


   * <div data-tips="true" data-tips-type="default">Online search</div>


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. In the pop\-up window, carefully read the relevant service terms, and after confirming that everything is correct, select "I have read and agree to the Terms of ArkClaw Services".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c2f1ec730d3fb88c943f3a6ea8ef1f4.png) </span>

3. Click "Activate and authorize" to complete role authorization and model activation.


<span id="JkePbkui"></span>
### Step 4: Configure the ArkClaw service


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. On the service activation page, configure the relevant information according to the table below.

   
   |Configuration item |Description |
   |---|---|
   |**Basic information** ||
   |Space name |Set the ArkClaw space name. The platform automatically generates a name, which administrators can modify as needed. After the space is activated, the space name can be changed at any time. For details, see [Viewing space configuration information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information?lang=en#ftsmTKKb). |
   |**Employee access control** ||
   |Authentication |Configure access control information for enterprise employees. Select **Other standard protocols**. After you select another standard protocol, there is no need to configure authentication parameters on the activation page. |
   |**Space management type** ||
   |Select space management type |Select the management type for Claw instances in the current space. **This setting cannot be modified after the space is activated**.<br><br><br>* **Seat Management**: Subscription is based on the total number of seats. Seats of the same edition share a unified expiration date, and you do not need to manage the lifecycle of each Claw instance separately. Within the purchased seat quota, Claw instances can be provisioned or allocated as needed.<br><br>* **Instance Management**: Claw instances are managed individually. All Claw instances in the space are created, allocated, and managed separately. Each Claw instance has a separate resource lifecycle and must be managed individually.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Selecting the space management type is a beta feature and is available only after beta access is granted. If you need to use this feature, contact your account manager</strong>.</div><br> |
   |**Network configuration** ||
   |Space network configuration |The VPC CIDR block and subnet CIDR block for ArkClaw Enterprise. The platform will automatically create network resources such as a VPC, subnet, and security group for ArkClaw in the current region, establishing the network environment required for ArkClaw to operate in.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After an ArkClaw Enterprise is activated, modifying the VPC CIDR block or subnet CIDR block is not supported.</div><br><br><br><br>* **Random network creation**:<br><br>   * No network configuration is required. The platform will create the VPC and subnet for ArkClaw using a randomly assigned private CIDR block.<br><br>   * If you need to access ArkClaw VPC resources from another VPC later, ensure that the VPC address does not belong to the following CIDR blocks to avoid conflicts: `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, and `9.0.0.0/8`.<br><br>* **Specified network creation**:<br><br>   * If you need to connect to ArkClaw's VPC via Cloud Enterprise Network (CEN) or Transit Router (TR) in the future, specify an ArkClaw VPC CIDR block based on your network planning.<br><br>   * Click "Custom configuration" in the upper\-right corner of the card and enter the desired CIDR block for the custom VPC. The platform will create the VPC and subnet based on your input. Ensure the custom CIDR block does not belong to the following network segments: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/8`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, `169.254.0.0/16`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The ArkClaw VPC feature is in beta and available only upon activation. If you need to use this feature, contact your account manager</strong>.   </div><br>    |
   

3. After configuration is completed, click the "Activate now" button to complete the service space configuration.

   4. ModelArk API keys used in Foundation models have permission to invoke all models. A dialog box will appear to confirm this when space activation is complete. To manage the model scope, click "[Volcano Ark Management Console](https://console.byteplus.com/ark/region:cn-beijing/apiKey?apikey=%7B%7D&projectName=default)". If you do not need to manage the model scope, click "Got it" to close the dialog box.


&nbsp;

<span id="QzYM9zsv"></span>
### Step 5: Purchase ArkClaw Enterprise seats

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you selected "Instance Management" for "Select space management type" in the previous step to activate the ArkClaw space, skip this section</strong>.</div>



1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Claw Management" \> "Claws".

2. On the ArkClaw management page, click "Buy now".

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
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Exclusiveness restriction: ModelArk Plans purchased in ArkClaw are recommended for use only within ArkClaw.</strong>   </div>
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ArkClaw Enterprise <strong>periodically rotates</strong> managed ModelArk Plan API Keys. During rotation, previous API Keys are immediately invalidated. If you reuse such Keys in services outside ArkClaw, service access will also be disrupted by rotation.   </div>
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To share ModelArk Plans across multiple scenarios, we recommend purchasing an independent ModelArk Plans, obtaining independent API Keys directly from ModelArk, and then configuring the model via "Custom model source." For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Model_management?lang=en#MXrT1Usf">Configuring custom model pools</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Automatic renewal</strong>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The "Automatic renewal" option is selected by default to prevent ArkClaw service suspension due to subscription expiration. You can manually cancel this option. If you do that, ensure you renew your subscription before expiration.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After "Auto\-renewal" is enabled, automatic renewal will be applied to all subsequent new purchases and change orders under the space.   </div>
   

   
   |Specifications |Applicable scenario |
   |---|---|
   |Starter edition |Suitable for testing and light usage scenarios. |
   |Standard edition |Suitable for scenarios such as automated office work, process approval, and knowledge retrieval. |
   |Premium edition |Suitable for scenarios such as large\-scale data processing and long\-text parsing. |
   |Ultimate edition |Suitable for scenarios such as multimodal processing, multi\-agent collaboration, and complex loop tasks. |
   

4. After configuration is complete, click "Purchase" and follow the on\-screen instructions to pay the fees. Once payment is successful, click "Go to console" to complete the service activation. Service activation takes approximately 3–5 minutes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Common reasons for service activation failure include incomplete enterprise real\-name authentication, VPC CIDR block conflicts, or insufficient resources.</strong> If activation still fails after confirming these are resolved, copy the error message displayed on the page and click <strong>Submit a ticket</strong> for assistance.   </div>
   

<span id="cLAlxprD"></span>
### Step 6: Configure protocol information


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Organizations" \> "Users".

2. On the "Users" page, select the "Login configuration" tab. In the "Basic configuration information" section, click "Edit".

3. Enter the configuration information.

   
   |Configuration item |Description |
   |---|---|
   |Client ID |The unique client identifier that identifies the current application. This unique client identifier is automatically generated when the application is registered with the IdP. |
   |Client secret |The key that ensures secure communication with the IdP. It is generated after the application is created at the IdP.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It needs to be kept securely to prevent leakage.</div><br> |
   |Authorization endpoint |The authorization endpoint (login redirect URI) provided by the IdP for initiating the OAuth authorization flow. |
   |Token endpoint |The endpoint used to exchange an authorization code for an access token. It must be obtained from the application configurations at the IdP. |
   |UserInfo endpoint |The endpoint that requests detailed information (such as username and email address) about the logged\-in user with the access token included. It must be obtained from the application configurations at the IdP. |
   |Authorization scope |* The scope of user information requested during login authorization. For example, whether to obtain only basic identity information or also obtain personal information (such as avatar and nickname), email address, and phone number. **You can directly select or manually enter the scope**.<br><br>* The following values are typically included:<br><br>   * openid: The unique user identifier that identifies the user.<br><br>   * profile: The personal information of the user, such as the avatar, nickname, and name.<br><br>   * email: The email address of the user.<br><br>   * phone: The phone number of the user.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The authorization scope must be consistent with that supported by the IdP. For details, see the official documentation of the corresponding IdP.</div><br><br><br><br>* The following content provides an example of the configuration result:<br><br>   * Administrators set the authorization scope to `openid`, `profile`, `email`, or `phone`.<br><br>   * When you log in for the first time, the page will display the following requested permission information:<br><br><br> |
   |Unique user identifier |* It is used to identify a user and match a logged\-in user with existing users in the system. This field is generated by the IdP.<br><br>* Enter the fields in the user information returned by the IdP. The fields must be **globally unique and not easily changed**, and their values must be in **English**.<br><br>   * **Recommend**: Enter user ID\-type fields, such as `sub` and `user_id`. If no user ID\-type fields are available, you can use `email`, which is more stable but may be changed. In such cases, user data needs to be updated.<br><br>   * **Not recommended**: Use fields such as `name` or `nickname`, which may be modified or duplicated.<br><br>* Method of viewing user attributes: Access the OIDC discovery URL (`https://****/.well-known/openid-configuration`), and view the list of supported attributes by using the `claims_supported` node. For example: |
   |Enable PKCE |Adds an additional layer of security protection to the authorization code flow. If you select this option, the client (e.g., mobile app) uses PKCE to prevent authorization code interception, enhancing security. |
   |Unique identifier policy |Select based on the primary identity information used by your enterprise. When importing employee information or switching authentication methods later, the system will automatically merge accounts that share the same phone number or email address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The unique identifier policy is used to determine whether the same employee has been imported multiple times: When the employee list is imported again, the system will merge records for the same employee into a single entry based on the unique identifier you select. This field<strong> only determines the basis for merging and does not determine the login method</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Policy options:</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Email:</strong> Applicable to scenarios where employee email addresses are standardized and uniformly managed across the enterprise.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Mobile number:</strong> Applicable to scenarios involving external contractors or temporary accounts.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>After the unique identifier policy is applied, we recommend against changing it later</strong>: If you change it, existing employee records may not match newly imported employee records, resulting in duplicate accounts.</div><br> |
   

4. Click "Confirm".


<span id="GAbUUlFF"></span>
### Step 7: Configure callback information


1. In the left navigation pane of the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), select "Space Overview". To the right of the OAuth 2.0 authorization code redirect URL, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_853b8594d5dded0729fe89fbec66a9dc.png) </span> icon to copy the information.

   2. Log in to the [Alibaba Cloud IDaaS console](https://yundun.console.aliyun.com/?p=idaas), select the corresponding IDaaS instance, and click "Console" in the "Actions" column.

   3. In the left navigation pane​, click "Application Management". On the page that appears, click the name of the target application.

   4. In the "Application configuration information" section of the "Login access \> SSO" tab, replace the login redirect URI with the copied SSO authorization code redirect URL, and then click the "Save" buttion.

5. Return to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise), copy the employee login link on the "Space Overview" page, and use your internal channel to send the link to employees who need to use ArkClaw.
