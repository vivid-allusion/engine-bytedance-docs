---
title: "Basic Configuration for Lark Integration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Basic_Configuration_for_Lark_integration"
---

The Intelligent Analysis Agent (hereafter referred to as Zhinengti) supports functional integration with Lark. Through these capabilities, users can directly access Zhinengti's mobile application from the Lark workspace, connect to Lark data sources, or receive daily, weekly, or monthly reports pushed by Zhinengti to individual or group chats in Lark, thereby enabling Lark integration and collaborative work. This article introduces the basic configuration procedures for Lark integration.

<span id="77d60f12"></span>
# Function overview

The basic configuration for Lark integration requires users to perform operations such as creating applications and configuring permissions on the Lark side, as well as integrating the office platform on the Zhinengti side. Once configuration is complete, Lark integration and collaborative work can be achieved.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article uses the Lark SaaS standard product as an example to introduce the configuration operation process on the Lark side. Caution: The configuration interface of the Lark open platform may vary depending on the user's deployment environment and version. For details, refer to <a href="https://open.larkoffice.com/document/develop-process/self-built-application-development-process">enterprise self\-built application development process</a>.</div>


<span id="fc032f4e"></span>
## Glossary


|Related terminology |Note |Usage scenario |
|---|---|---|
|[Lark open platform](https://open.feishu.cn/) |The backend for adding new applications, which can be operated by all developers |In scenarios involving integration with the intelligent agent, this backend is used to add applications |
|Lark management console |Lark organization management console, which can only be operated by Lark organization administrators |Approve application launch and grant relevant permissions to the application |
|Application administrator |The corresponding user role in the intelligent agent is system administrator |Responsible for completing the integration of Lark with the intelligent agent platform |
|Enterprise organization administrator |The corresponding user role in Lark is Lark organization administrator |Responsible for granting permissions and approving application launch in the Lark management platform |


<span id="631ed864"></span>
## Overview of the operation process

The overall steps are as follows:


1. Lark side: Create application \-\> Configure permissions \-\> Publish application

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6c592efbae245b8adcd9b62585a5b45~tplv-goo7wpa0wc-image.image) </span>

   1. Create Lark application: The Zhinengti system administrator, who is usually also the application creator and administrator on the Lark open platform, creates a Zhinengti application on the Lark open platform.

   2. Configure permission management: The Zhinengti system administrator enables the relevant application permissions on the Lark open platform.

   3. Publish Lark application: The Zhinengti system administrator creates and applies to publish a new version of the application on the Lark open platform. After approval by the organization administrator in Lark, the overall application configuration and launch are completed.

2. Zhinengti side: Office platform integration.


The specific configuration methods will be introduced in subsequent modules. For further questions regarding Lark applications, refer to the documentation in the Lark developer platform help center.

<span id="69c67d9d"></span>
# Precautions


* When using Lark, you may encounter some functional differences between the Lark Open Platform and the Lark Open Platform. To configure integration with Lark, please contact after\-sales support via the bottom right corner of the official website.


<span id="52b8048b"></span>
# Lark\-side configuration

<span id="c46aaca1"></span>
## Create a Lark application


1. Open the enterprise [Lark Open Platform](https://open.larkoffice.com/?lang=en-US), click the avatar in the upper right corner, and select the enterprise to confirm the application push.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31f75fadabe24d9f84921ebbacf84829~tplv-goo7wpa0wc-image.image) </span>

2. Click "Create Application" to enter the developer console of the Lark Open Platform.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/053fbdf498834cb7b95d8a838264f68b~tplv-goo7wpa0wc-image.image) </span>

3. Click "Create Enterprise Self\-built Application" and fill in the required "Application Name", "Application Description", and "Application Icon" as prompted.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a4f249061e6405e824b631d5d6f2b2e~tplv-goo7wpa0wc-image.image) </span>


<span id="6889e4b3"></span>
## Configure permission management

Before calling the Lark Open API, you need to enable the permissions required by the Intelligent Agent for the application. In the developer console of the Lark Open Platform, click "Permission Management" to start configuring permissions for the application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e55458cef594aa9ada6974efcdfd9e6~tplv-goo7wpa0wc-image.image) </span>

Based on the usage scenarios for integration between the Intelligent Agent and Lark, this document divides permissions into the following five modules. Users can select permission modules according to the integration effects they want to achieve in the Intelligent Agent, and follow the steps to enable the Lark permissions required by the Intelligent Agent for the application. Among them, "Basic Permissions" are fundamental for integration between the Intelligent Agent and Lark and are mandatory:


|Usage scenarios for Lark integration in the intelligent agent |Permission module |Required or optional |
|---|---|---|
|* Basic integration between the intelligent agent and Lark |[Basic permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#5ac02561) |Required |
|* In the data preparation module, use data from tables or multi\-dimensional tables in Lark "Knowledge Base" as the data source for the intelligent agent. For details, refer to [Lark Sheets](https://docs.byteplus.com/docs/dataagent/Lark_Sheets), [Lark Base Tables](https://docs.byteplus.com/docs/dataagent/Lark_Base_Tables). |[Table/multidimensional table-related permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#aba0b6ad) |Optional |
|* In the permissions module, add Lark departments to the intelligent agent to use them as department\-level user groups. For details, refer to [User Group Management](https://docs.byteplus.com/docs/dataagent/User_Group_Management). |[Lark department-related permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#7713726b) |Optional |
|* Approval workflows can be integrated with Lark approval workflows. For details, refer to [Permission Approval Integration with Lark](https://docs.byteplus.com/docs/dataagent/Permission_Approval_Integration_with_Lark).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, this feature is only supported in the on\-premises version of Intelligent Agent.   </div><br>    |[Permission approval integration with Lark](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#20c9b20e) |Optional |
|* Send direct messages to Lark users within the application's available scope<br><br>* Send group messages to the group chat where the Lark bot is located<br><br>* Receive all direct messages sent by users to the Lark bot |[Lark message sending-related permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#2d620d49) |Optional |


Permission type introduction:


|Permission type |Introduction |
|---|---|
|Application identity permissions |* The application runs automatically when the user is not logged in<br><br>* The scope of resources that can be operated by the application identity |
|User identity permissions |* The application must perform operations as the logged\-in user<br><br>* The scope of resources that can be operated by the logged\-in user |


<span id="24affeb7"></span>
### Basic permissions


|Permission type |Configuration instructions |
|---|---|
|Application identity permissions |* Update address book<br><br>* Obtain basic address book information<br><br>* Obtain basic department information<br><br>* Obtain department organizational structure information from the address book<br><br>* Obtain basic user information<br><br>* Obtain user organizational structure information<br><br>* Obtain user ID<br><br>* Obtain user phone number<br><br>* Obtain user ID by phone number or email<br><br>* Obtain enterprise information<br><br>* Send messages as the application identity (only needs to be enabled for the private version, not required for SaaS)<br><br>* Send messages in batches to multiple users (only needs to be enabled for the private version, not required for SaaS) |
|User identity permissions |* View, edit, and manage the knowledge base<br><br>* View the knowledge base<br><br>* View, comment, edit, and manage spreadsheets<br><br>* View, comment, edit, and manage multidimensional tables<br><br>* View, comment, and export multidimensional tables |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The visible scope of the address book in data permissions follows the application's available scope by default. If the address book scope is not large enough, it will result in the inability to bind user IDs outside the address book scope. It is recommended to refer to the diagram below and set the available scope to "All employees" in "Version management and release".</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5efadf85d5fc4c35aa26a6122eb56c02~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="ca14c394"></span>
### Table/multidimensional table\-related permissions


|Permission type |Configuration instructions |
|---|---|
|User identity permissions |* View, edit, and manage the knowledge base<br><br>* View the knowledge base<br><br>* View, comment, edit, and manage all files in the cloud space<br><br>* View, comment, edit, and manage multidimensional tables<br><br>* View, comment, and export multidimensional tables<br><br>* View, comment, edit, and manage spreadsheets<br><br>* View, comment, and export spreadsheets |
|||


<span id="84d7d14c"></span>
### Lark department\-related permissions


|Permission types |Configuration instructions |
|---|---|
|Application identity permissions |* Read the address book using the application identity<br><br>* Obtain department organizational structure information<br><br>* Obtain user email information<br><br>* Obtain user phone number<br><br>* Obtain user ID<br><br>* Obtain department basic information<br><br>* Obtain user basic information<br><br>* Obtain enterprise information<br><br>* Obtain and update group information<br><br>* View group information |
|||
|||


<span id="be307724"></span>
### Permission approval and connection with Lark


|Permission types |Configuration instructions |
|---|---|
|Application identity permissions |* View, create, update, and delete approval application\-related information<br><br>* Query approval list<br><br>* Access approval application<br><br>* Obtain user ID |


<span id="05fecce1"></span>
### Lark message sending\-related permissions


1. Search for and enable the following permissions.

   
   |Permission types |Configuration instructions |
   |---|---|
   |Application identity permissions |* Retrieve and send one\-on\-one and group messages<br><br>* View group information |
   

2. Contact the Lark organization administrator and log in to the [Lark Admin Console](https://feishu.cn/admin/index) to perform the following operations:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The prerequisite for this step is that the application has already been published. If the application has not been published, please refer to <strong>Publish Lark application</strong> to complete the publication process before proceeding with this step.   </div>
   

   1. Enter the Lark Admin Console, click "Workbench" \- "Application Management", and locate the published application.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13c6e67d3bd545d097f73e050acdb341~tplv-goo7wpa0wc-image.image) </span>

   2. Select available members and set all members as available.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9d2fcc6a19c4b658c0991ee7ccdd398~tplv-goo7wpa0wc-image.image) </span>

3. After the Lark organization administrator completes the configuration, the DataAgent system administrator returns to the [Lark Open Platform](https://open.feishu.cn/app) and clicks "Security Settings".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6609d47609b471b992ee2cb55808ff8~tplv-goo7wpa0wc-image.image) </span>

   Add the following URL information in the "Redirect URL" input box, then click "Add" to save.

   
   |Product versions |Required URL information to add |
   |---|---|
   |SaaS |https://console.volcengine.com/bi/datawind/#<br><br>https://console.volcengine.com/bi/datawind#/dataManage<br><br>https://console.volcengine.com/bi/datawind/auth#/dataManage<br><br>https://console.volcengine.com/bi/datawind#/dataPrep<br><br>https://console.volcengine.com/bi/datawind/auth#/dataPrep<br><br>https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_sheet<br><br>https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_bitable<br><br>[https://console.volcengine.com/bi/datawind/data-agent/analytics-agent](https://console.volcengine.com/bi/datawind/data-agent/analytics-agent)<br><br>[https://console.volcengine.com/bi/datawind/data-agent/analytics-agent/](https://console.volcengine.com/bi/datawind/data-agent/analytics-agent/) |
   |On\-premises |As follows, replace $HOST with the product's deployment domain name, without any path:<br><br>$HOST/bi<br><br>$HOST/bi#<br><br>$HOST/bi#/dataManage<br><br>$HOST/bi/auth#/dataManage<br><br>$HOST/bi#/dataPrep<br><br>$HOST/bi/auth#/dataPrep<br><br>$HOST/bi/#/prep/dataLink/authCallback/lark_sheet<br><br>$HOST/bi/#/prep/dataLink/authCallback/lark_bitable |
   


<span id="9f861d7a"></span>
## Publish the Lark application


1. Create a new version. In the developer console of the Lark open platform, click "Version management and release", then click "Create version". Fill in the "Application version number", "Update description", and other information. Click "Save" to complete the version creation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e66d7568f02498c88458aa606fbe419~tplv-goo7wpa0wc-image.image) </span>

2. Release a new version. After creating a new version, click "Confirm release".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24deeee70c0c4e028664e9acc597b440~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only users within the allowed scope can successfully search for, open, and use the web application.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the application administrator applies for publication, the enterprise organization administrator will receive a notification from the open platform regarding the application review. The review must be completed before proceeding with subsequent configuration steps.   </div>
   

3. After completing the steps for creating and releasing a new version, click "Credentials and basic information", and copy the APP ID and APP Secret.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7570d88928e044b78bce120d992712b3~tplv-goo7wpa0wc-image.image) </span>


<span id="65227b8e"></span>
# Configuration on the intelligent agent side

Log in to the intelligent agent as **system administrator**, click "System management", then click "Office platform integration" \- "Lark". Enter the APP ID and APP Secret obtained from **Lark\-side configuration**, select "Enable", and click "Submit" to complete the basic configuration for Lark integration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3acd82f194a446668dda47b3d20b9bd9~tplv-goo7wpa0wc-image.image) </span>
