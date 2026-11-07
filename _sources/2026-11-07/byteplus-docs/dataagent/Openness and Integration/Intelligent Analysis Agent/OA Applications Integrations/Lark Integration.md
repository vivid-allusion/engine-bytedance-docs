---
title: "Lark Integration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Lark_Integration_"
---

The Intelligent Analysis Agent (hereafter referred to as the agent) supports functional integration with Lark. Through related capabilities, users can directly access the agent's mobile application from the Lark Workbench, connect to Lark data sources, or receive daily, weekly, or monthly reports pushed by the agent to their Lark personal account or groups, thereby enabling Lark integration and collaborative work. This article introduces the basic configuration operations for Lark integration.

<span id="e51cc091"></span>
# Feature overview

The basic configuration for Lark integration requires users to perform self\-built application and permission configuration operations on the Lark side, and to perform office platform integration operations on the agent side. After completing the configuration, Lark integration and collaborative work can be achieved.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article uses the Lark SaaS standard product as an example to introduce the configuration process on the Lark side. Caution: The configuration interface of the Lark Open Platform may vary depending on the user's deployment environment and version. For details, refer to <a href="https://open.larkoffice.com/document/develop-process/self-built-application-development-process">enterprise self\-built application development process</a>.</div>


<span id="c9e9e292"></span>
## Glossary


|Related terminology |Explanation |Usage scenario |
|---|---|---|
|[Lark Open Platform](https://open.feishu.cn/) |The backend for adding new applications, accessible to all developers |In scenarios where the intelligent agent is integrated, this backend is used to add applications |
|[Lark management console](https://feishu.cn/admin/index) |Lark organization management console, accessible only to Lark organization administrators |Approve application launch and grant relevant permissions to the application |
|Application administrator |The corresponding user role in the intelligent agent is system administrator |Responsible for completing the integration of Lark with the intelligent agent platform |
|Enterprise organization administrator |The corresponding user role in Lark is Lark organization administrator |Responsible for granting permissions and approving application launch in the Lark management platform |


<span id="15b305c6"></span>
## Process overview

The overall steps are as follows:


1. Lark side: Create application \-\> Configure permissions \-\> Publish application


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6c592efbae245b8adcd9b62585a5b45~tplv-goo7wpa0wc-image.image) </span>


1. Create Lark application: The agent's system administrator, who is usually also the application creator and administrator on the Lark Open Platform, creates an agent application on the Lark Open Platform.

2. Configure permission management: The agent's system administrator enables the relevant application permissions on the Lark Open Platform.

3. Publish Lark application: The agent's system administrator creates and applies to publish a new version of the application on the Lark Open Platform. After approval by the Lark organization administrator, the overall application configuration and launch are completed.

4. Agent side: Office platform integration.


The specific configuration methods will be introduced in detail in subsequent sections. For more questions related to Lark applications, refer to the documentation in the Lark Developer Platform Help Center.

<span id="f133c763"></span>
# Precautions


* When using Lark, you may encounter some functional differences between the Lark Open Platform and the Lark Open Platform. To configure integration with Lark, please contact after\-sales support via the bottom right corner of the official website.


<span id="c90d5ffc"></span>
# Lark configuration

<span id="1e602e29"></span>
## Create a Lark application


1. Open the enterprise [Lark Open Platform](https://open.feishu.cn/), click the avatar in the upper right corner, and select the enterprise to confirm the application push.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/258a5747f350435492dad3d5d0e14aff~tplv-goo7wpa0wc-image.image) </span>


2. Click "Create Application" to enter the developer console of the Lark Open Platform.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/053fbdf498834cb7b95d8a838264f68b~tplv-goo7wpa0wc-image.image) </span>

3. Click "Create Enterprise Self\-built Application" and fill in the required "Application Name", "Application Description", and "Application Icon" as prompted.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a4f249061e6405e824b631d5d6f2b2e~tplv-goo7wpa0wc-image.image) </span>


<span id="37b3fa2b"></span>
## Configure permission management

Before calling the Lark Open API, you need to enable the permissions required by the Agent for the application. In the developer console of the Lark Open Platform, click "Permission Management" to start configuring permissions for the application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e47b0785f5294d4c9e36bcfc8250ddbf~tplv-goo7wpa0wc-image.image) </span>

Based on the integration scenarios between the Agent and Lark, this document divides permissions into the following five modules. Users can select permission modules according to the desired integration effects in the Agent, and follow the steps to enable the Lark permissions required by the Agent for the application. Among them, "Basic Permissions" are fundamental for integration between the Agent and Lark and are mandatory:


|Usage scenarios for Lark integration in the intelligent agent |Permission module |Required or optional |
|---|---|---|
|* Basic integration between the intelligent agent and Lark |[Basic permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#5ac02561) |Required |
|* In the data preparation module, use data from tables or multi\-dimensional tables in the Lark "Knowledge Base" as the data source for the intelligent agent. For details, refer to [Lark Sheets](https://docs.byteplus.com/docs/dataagent/Lark_Sheets), [Lark Base Tables](https://docs.byteplus.com/docs/dataagent/Lark_Base_Tables). |[Table/multidimensional table-related permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#aba0b6ad) |Optional |
|* In the permissions module, add Lark departments to the intelligent agent to use them as department\-level user groups. For details, refer to [User Group Management](https://docs.byteplus.com/docs/dataagent/User_Group_Management). |[Lark department-related permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#7713726b) |Optional |
|* Approval flows can be integrated with Lark approval flows. For details, refer to [Permission Approval Integration with Lark](https://docs.byteplus.com/docs/dataagent/Permission_Approval_Integration_with_Lark).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, this feature is only supported in the on\-premises version of the intelligent agent.   </div><br>    |[Permission approval integration with Lark](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#20c9b20e) |Optional |
|* Send one\-on\-one messages to Lark users within the application's available scope<br><br>* Send group messages to the group chat where the Lark bot is located<br><br>* Receive all one\-on\-one messages sent by users to the Lark bot |[Lark message sending-related permissions](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#2d620d49) |Optional |


Introduction to permission types:


|Permission type |Introduction |
|---|---|
|Application identity permissions |* The application runs automatically when the user is not logged in<br><br>* The scope of resources that the application identity can operate |
|User identity permissions |* The application must perform operations as the logged\-in user<br><br>* The scope of resources that the logged\-in user can operate |


<span id="5ac02561"></span>
### Basic permissions


|Permission type |Configuration instructions |
|---|---|
|Application identity permissions |* Update address book<br><br>* Obtain basic address book information<br><br>* Obtain basic department information<br><br>* Obtain department organizational structure information from the address book<br><br>* Obtain basic user information<br><br>* Obtain user organizational structure information<br><br>* Obtain user ID<br><br>* Obtain user mobile number<br><br>* Obtain user ID by mobile number or email<br><br>* Obtain enterprise information<br><br>* Send messages as the application identity (only required for the private version, not needed for SaaS)<br><br>* Send messages in bulk to multiple users (only required for the private version, not needed for SaaS) |
|User identity permissions |* View, edit, and manage the knowledge base<br><br>* View the knowledge base<br><br>* View, comment, edit, and manage spreadsheets<br><br>* View, comment, edit, and manage multidimensional tables<br><br>* View, comment, and export multidimensional tables |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The visible scope of the address book in data permissions follows the application's available scope by default. If the address book scope is not large enough, it will result in being unable to bind user IDs outside the address book scope. It is recommended to refer to the diagram below and set the available scope to "All employees" in "Version management and release".</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5efadf85d5fc4c35aa26a6122eb56c02~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="aba0b6ad"></span>
### Table/multidimensional table\-related permissions


|Permission type |Configuration instructions |
|---|---|
|User identity permissions |* View, edit, and manage the knowledge base<br><br>* View the knowledge base<br><br>* View, comment, edit, and manage all files in the cloud space<br><br>* View, comment, edit, and manage multidimensional tables<br><br>* View, comment, and export multidimensional tables<br><br>* View, comment, edit, and manage spreadsheets<br><br>* View, comment, and export spreadsheets |
|||


<span id="7713726b"></span>
### Lark department\-related permissions


|Permission types |Configuration instructions |
|---|---|
|Application identity permissions |* Read the address book as the application identity<br><br>* Obtain department organizational structure information<br><br>* Obtain user email information<br><br>* Obtain user mobile number<br><br>* Obtain user user ID<br><br>* Obtain department basic information<br><br>* Obtain user basic information<br><br>* Obtain enterprise information<br><br>* Obtain and update group information<br><br>* View group information |
|||
|||


<span id="20c9b20e"></span>
### Permission approval integration with Lark


|Permission types |Configuration instructions |
|---|---|
|Application identity permissions |* View, create, update, and delete approval application\-related information<br><br>* Query approval list<br><br>* Access approval application<br><br>* Obtain user user ID |


<span id="2d620d49"></span>
### Lark message sending\-related permissions


1. Search to enable the following permissions.

   
   |Permission types |Configuration instructions |
   |---|---|
   |Application identity permissions |* Obtain and send single chat and group messages<br><br>* View group information |
   

2. Contact the Lark organization administrator and log in to the [Lark Admin Console](https://feishu.cn/admin/index) to perform the following operations:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The prerequisite for this step is that the application has already been published. If the application has not been published, please refer to <strong>Publish Lark application</strong> to complete the publishing operation before proceeding with this step.   </div>
   

   1. Enter the Lark Admin Console, click "Workbench" \- "Application Management", and locate the published application.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13c6e67d3bd545d097f73e050acdb341~tplv-goo7wpa0wc-image.image) </span>

   2. Select available members and configure available members as all members.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9d2fcc6a19c4b658c0991ee7ccdd398~tplv-goo7wpa0wc-image.image) </span>

3. After the Lark organization administrator completes the configuration, the DataAgent system administrator returns to the [Lark Open Platform](https://open.feishu.cn/app) and clicks "Security Settings".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6609d47609b471b992ee2cb55808ff8~tplv-goo7wpa0wc-image.image) </span>

   In the "Redirect URL" input box, add the following URL information. After entering, click "Add" to save.

   
   |Product versions |URL information to be added |
   |---|---|
   |SaaS |https://console.volcengine.com/bi/datawind/#<br><br>https://console.volcengine.com/bi/datawind#/dataManage<br><br>https://console.volcengine.com/bi/datawind/auth#/dataManage<br><br>https://console.volcengine.com/bi/datawind#/dataPrep<br><br>https://console.volcengine.com/bi/datawind/auth#/dataPrep<br><br>https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_sheet<br><br>https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_bitable<br><br>[https://console.volcengine.com/bi/datawind/data-agent/analytics-agent](https://console.volcengine.com/bi/datawind/data-agent/analytics-agent)<br><br>[https://console.volcengine.com/bi/datawind/data-agent/analytics-agent/](https://console.volcengine.com/bi/datawind/data-agent/analytics-agent/) |
   |On\-premises deployment |As follows, replace $HOST with the product's deployment domain name, without any path:<br><br>$HOST/bi<br><br>$HOST/bi#<br><br>$HOST/bi#/dataManage<br><br>$HOST/bi/auth#/dataManage<br><br>$HOST/bi#/dataPrep<br><br>$HOST/bi/auth#/dataPrep<br><br>$HOST/bi/#/prep/dataLink/authCallback/lark_sheet<br><br>$HOST/bi/#/prep/dataLink/authCallback/lark_bitable |
   


<span id="39ea040a"></span>
## Publish the Lark application


1. Create a new version. In the developer console of the Lark Open Platform, click "Version management and release," then click "Create version." Fill in the "Application version number," "Update description," and other information. Click "Save" to complete version creation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e66d7568f02498c88458aa606fbe419~tplv-goo7wpa0wc-image.image) </span>

2. Release a new version. After creating a new version, click "Confirm release."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24deeee70c0c4e028664e9acc597b440~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only users within the permitted scope can successfully search for, open, and use the web application normally.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the application administrator applies for publishing, the enterprise organization administrator will receive a notification message for the open platform application review. The review must be completed before subsequent configuration actions can proceed.   </div>
   

3. After completing the steps for creating and releasing a new version, click "Credentials and basic information," then copy the APP ID and APP Secret.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7570d88928e044b78bce120d992712b3~tplv-goo7wpa0wc-image.image) </span>


<span id="1ed04d9c"></span>
# Intelligent agent configuration

Log in to the intelligent agent as **system administrator**, click "System management," then click "Office platform integration" \- "Lark." Enter the APP ID and APP Secret obtained from **Lark side configuration**, select "Enable," and click "Submit" to complete the basic configuration for Lark integration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3acd82f194a446668dda47b3d20b9bd9~tplv-goo7wpa0wc-image.image) </span>
