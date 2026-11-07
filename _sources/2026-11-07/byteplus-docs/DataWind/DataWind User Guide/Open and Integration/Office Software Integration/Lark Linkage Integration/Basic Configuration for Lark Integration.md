---
title: "Basic Configuration for Lark Integration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Basic_Configuration_for_Lark_Integration"
---

<span id="_1-概述"></span>
# Overview

Intelligent Data Insight (hereinafter referred to as DataWind) supports integration with Lark. Through these capabilities, users can directly access DataWind's mobile application from the Lark workspace, connect to Lark data sources, or receive daily, weekly, or monthly reports pushed by DataWind to individual or group chats in Lark, thereby enabling integration with Lark and collaborative work.

To achieve these effects, users need to perform operations such as creating custom applications and configuring permissions on the Lark open platform, and also configure subscriptions and alerts in DataWind. This article introduces the required basic configuration.

Note: The configuration interface of the Lark open platform is updated periodically. Please refer to the latest configuration interface.

<span id="_1-1-名词解释"></span>
## Terminology


|**Related terms** |**Explanation** |**Usage scenarios** |
|---|---|---|
|[Lark Open Platform](https://open.feishu.cn/) |The backend for adding new applications, accessible to all developers |In scenarios integrated with DataWind, used as the backend for adding applications |
|[Lark Management Backend](https://feishu.cn/admin/index) |Lark organization management backend, accessible only to Lark administrators |Approve application launch and grant relevant permissions to the application |
|Application administrator |The corresponding user role in DataWind is the system administrator, who completes the integration of Lark with the DataWind platform. | |
|Enterprise organization administrator |Management of personnel and departments in the Lark organization | |


<span id="_1-2-操作流程概览"></span>
## Overview of the operation process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5502b67295ae4ee1817442dcf6a4a857~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure above, the overall operation logic is as follows: the system administrator of your company's Intelligent Data Insight, who is usually also the application creator and administrator on the Lark open platform, creates an Intelligent Data Insight application on the Lark open platform, enables the relevant application permissions, and submits it for review by the organization administrator on Lark. Only after approval can the overall application configuration and launch be completed. The specific configuration methods will be introduced in detail in subsequent modules. For more questions about Lark applications, refer to the documentation in the Lark developer platform help center.

<span id="_2-基础配置"></span>
# Basic configuration

To enable integration with Lark, the following basic configuration is required. Please complete all the configuration steps below.

<span id="_2-1-创建飞书应用"></span>
## Create a Lark application


1. Open the enterprise [Lark open platform](https://open.feishu.cn/), click the avatar in the upper right corner, and select the enterprise to which the application will be pushed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9b5b2256afd4f8ea50b63e68e2fe67e~tplv-goo7wpa0wc-image.image) </span>

2. Click "Create Application" \- "Create Enterprise Custom Application", and fill in the required "Application Name", "Application Description", and "Application Icon" as prompted.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3556576733a24267b906cfef69bfbd2b~tplv-goo7wpa0wc-image.image) </span>

3. Click "Create an enterprise custom application" and fill in the required "Application name", "Application description", and "Application icon" as prompted.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e2198fe638c4edf8dd650fe23f7a1f6~tplv-goo7wpa0wc-image.image) </span>

4. After the application is successfully created, click the "Application Name" to open the application, then click the "Credentials and Basic Information" tab to switch pages. Here, you can obtain the "App ID" and "App Secret" values required for subsequent steps. (It is recommended to record the application credential information in advance, as it will be needed in later steps.)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eaedd09f22634bf492299313828899c7~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-权限管理配置"></span>
## Permission management configuration

In the developer console of the Lark open platform, go to the "Permission Management" module and click "Enable Permissions" to start configuring permissions for the application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f16c9a403e6e4cc0afc54aa4624e85d1~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-1-基础权限配置"></span>
### Basic permission configuration

Identity permissions and user identity permissions need to be enabled.

For application identity permissions, select the following basic permissions. After selecting multiple items, click "Enable in Bulk" to enable these permissions.


* Update address book

* Obtain basic address book information

* Obtain basic department information

* Obtain organizational structure information of address book departments

* Obtain basic user information

* Obtain user organizational structure information

* Obtain user ID

* Obtain user mobile number

* Obtain enterprise information

* Send messages as the application (only required for the on\-premises version; not needed for SaaS)

* Send messages in bulk to multiple users (only required for the on\-premises version; not needed for SaaS)


For user identity permissions, select the following basic permissions. After selecting multiple items, click "Enable in Bulk" to enable these permissions.


* View, edit, and manage the knowledge base

* View the knowledge base

* View, comment on, edit, and manage spreadsheets

* View, comment on, edit, and manage multi\-dimensional spreadsheets

* View, comment on, and export multi\-dimensional spreadsheets


Caution: The visible range of the address book in data permissions follows the application's available range by default. If the address book range is not large enough, it will not be possible to bind user IDs outside the address book range. It is recommended to refer to the diagram below and set the address book permission range to "All Members".

<span id="_2-2-2-使用表格与多维表格相关权限开通"></span>
### Enabling permissions related to spreadsheets and multi\-dimensional spreadsheets

To use data from spreadsheets or multi\-dimensional spreadsheets in the knowledge base as a data source, and to download data in Lark spreadsheet format, the following related permissions are required.


1. In the permission management interface, search for "Knowledge Base", select "View, edit, and manage knowledge base, view knowledge base", check the boxes, and then click "Bulk Enable".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02db4b524fbe42f2866f25704f34d26d~tplv-goo7wpa0wc-image.image) </span>

2. In the permission management interface, click "Enable Permissions". In the **User Identity Permissions** module, check the following basic permissions. After selecting multiple permissions, click "Bulk Enable" to enable them.

* View, comment on, edit, and manage all files in the cloud space

* View, comment on, edit, and manage multi\-dimensional tables

* View, comment on, and export multi\-dimensional tables

* View, comment on, edit, and manage spreadsheets

* View, comment on, and export spreadsheets


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c1a504102ff42c9a4ab265b2ee7e2ec~tplv-goo7wpa0wc-image.image) </span>

Note: The permission configuration interface of the Lark Open Platform may be updated periodically. Please refer to the latest permission configuration interface. It is recommended to select all permissions related to cloud documents.

<span id="_2-2-3-飞书部门相关权限开通"></span>
### Enabling department\-related permissions in Lark

To add Lark departments for direct use in DataWind, additionally enable the following permissions in DataWind.


1. In the developer console of the Lark Open Platform—Permission Management, check: Read the address book as the application, obtain department organizational structure information, obtain user email information, obtain user mobile number, obtain user ID, obtain basic department information, and obtain basic user information. After selecting multiple permissions, click "Bulk Enable" to enable them.

2. Search for "Obtain enterprise", select "Obtain enterprise information", and then click "Bulk Enable".

3. To enable the dashboard to support contacting its owner with one click, also select the "Obtain and update group information" permission.


In the developer console of the Lark Open Platform—Permission Management,you search for "Obtain and update", select "Obtain and update group information", and then click "Bulk Enable".

Note: The permission configuration interface of the Lark Open Platform may be updated periodically. Please refer to the latest permission configuration interface. It is recommended to select all relevant permissions.

<span id="_2-2-4-权限审批与飞书审批流联动相关权限开通（建议开启）"></span>
### Enabling permissions for approval workflow and Lark approval flow integration (recommended)

The private deployment version of DataWind supports integration between the approval workflow and the Lark approval flow. To enable the [Permission Approval Integration with Lark](https://docs.byteplus.com/docs/DataWind/Permission_Approval_Integration_with_Lark) feature, the following permissions must be enabled: "View, create, update, and delete approval application information; query approval lists; access approval applications; obtain user ID." After selecting multiple permissions, click "Bulk enable" for these permissions.

Note: The permission configuration interface of the Lark Open Platform may be updated periodically. Please refer to the latest permission configuration interface. You can select all the relevant permissions here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fef3b8376137471ea166234cc014e21e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-5-飞书消息发送相关权限开通"></span>
### Enabling permissions for Lark message sending

To obtain and send one\-on\-one and group messages to users, the "Obtain and send one\-on\-one and group messages" permission must be enabled. Search for "Obtain and send one\-on\-one and group messages", select this permission, and enable it. This permission allows sending one\-on\-one messages to users within the application's availability scope, sending group messages to groups where the bot is present, and receiving all one\-on\-one messages sent by users to the bot.

Contact the Lark organization administrator and log in to the Lark admin console to perform the following operations:

Caution: The prerequisite for Step 1 and Step 2 is that the application has already been published. If the application has not been published, please publish it first and then complete these two steps.


1. Click Enterprise Management \-\> Application Management \-\> Find the application.

2. Select available members and configure the selection as all members.

3. After the Lark organization administrator completes the configuration, the application administrator returns to the Lark Open Platform. Click "Security Settings" and add the following URL information in the "Redirect URL" input box.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48a77fe2b595403e8e4b4351a950d1ed~tplv-goo7wpa0wc-image.image) </span>


* Add for SaaS


https://console.volcengine.com/bi/datawind/#

https://console.volcengine.com/bi/datawind#/dataManage

https://console.volcengine.com/bi/datawind/auth#/dataManage

https://console.volcengine.com/bi/datawind#/dataPrep

https://console.volcengine.com/bi/datawind/auth#/dataPrep

https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_sheet https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_bitable


* Add for independent deployment


As follows, replace $HOST with the product's deployment domain name, without any path:

$HOST/bi

$HOST/bi#

$HOST/bi#/dataManage

$HOST/bi/auth#/dataManage

$HOST/bi#/dataPrep

$HOST/bi/auth#/dataPrep

$HOST/bi/#/prep/dataLink/authCallback/lark_sheet

$HOST/bi/#/prep/dataLink/authCallback/lark_bitable

Select Add to save.

<span id="_2-3-总览与应用发布"></span>
## Overview and application publishing


1. In the "Overview" module, go to "Application Publishing" \- "Version Management and Publishing", click "Create Version", fill in the "Version Number" **,**  "Availability Status", and other fields, then click "Save" to complete the version creation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0608a543b5944b8a9a560012928dea7c~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure below, when prompted to publish, click "Apply for Online Publishing" to complete the application publishing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c6033442415410ca6b6c935ac47e60e~tplv-goo7wpa0wc-image.image) </span>

Caution: Only users within the availability scope can successfully search for, open, and use the web application normally. After the application administrator applies for publishing, the enterprise organization administrator will receive a notification from the open platform regarding the application review. The review must be completed before proceeding with subsequent configuration actions.


2. After completing the above configuration, copy the APP ID and APP Secret in the "Credentials and Basic Information" module.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca285072733b457cbad062984b2a77c2~tplv-goo7wpa0wc-image.image) </span>


3. Return to Intelligent Data Insight, log in as a system administrator, and enter them in **Enterprise Domain Management \-\> Office Platform Integration**. Click Submit to enable Lark integration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64961434f78b4cec86a75d8d3d30a0e6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-使用场景所需配置"></span>
# Configuration required for usage scenarios

<span id="_3-1-常见场景介绍"></span>
## Introduction to common scenarios


|Usage scenarios |Scenario introduction |Configuration steps |
|---|---|---|
|Account binding |DataWind supports binding users in DataWind with Lark accounts, including both single user binding and batch binding methods. |Please refer to the documentation [How to Bind Lark Accounts and Batch Create sers](https://docs.byteplus.com/docs/DataWind/How_to_Bind_Lark_Accounts_and_Batch_Create_sers) |
|Push Lark messages |After the administrator completes the basic integration of Lark (connecting the Lark application), including permission configuration, subscription and alert rules can be set in DataWind to push charts, dashboards, and data anomaly notifications to Lark and Lark groups. |Please refer to the documentation [How to push Lark Messages](https://docs.byteplus.com/docs/DataWind/How_to_push_Lark_Messages) |
|Integrate Lark data sources |DataWind supports uploading Lark spreadsheets and Lark multi\-dimensional spreadsheets to create datasets. For data updates, offline scheduled updates are supported. |Please refer to the documentation [How to Connect to a Lark Data Source](https://docs.byteplus.com/docs/DataWind/How_to_Connect_to_a_Lark_Data_Source) |
|Integrate the mobile app |An important part of the integrated Lark application is deploying the DataWind mobile app on the Lark mobile platform, enabling users to access and open DataWind directly from the Lark workspace. |Please refer to the documentation [How to Integrate with the Lark Mobile Client](https://docs.byteplus.com/docs/DataWind/How_to_Integrate_with_the_Lark_Mobile_Client) |
|Integrate ChatBI |DataWind supports leveraging large model capabilities on Lark to implement ChatBI, making it easier to access and understand data through natural language conversations in Lark. |Please refer to the documentation [How to Integrate ChatBI with Lark](https://docs.byteplus.com/docs/DataWind/How_to_Integrate_ChatBI_with_Lark) |


<span id="_3-2-更多场景（飞书群授权）"></span>
## Additional scenarios (Lark group authorization)

[Detailed Explanation of Permission Features](https://docs.byteplus.com/docs/DataWind/Detailed_Explanation_of_Permission_Features)Authorization can be performed through Lark groups. To configure a dashboard or dataset for a Lark group, complete the above [2. Basic Configuration], then authorize resources you have permission for in the dashboard or dataset. Follow the steps below to complete Lark group authorization for this account.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The authorization configured by a user is effective only for that user. For example, if user A configures Lark group authorization, user B must configure it again under their own account if needed.</div>


<span id="be2e6a96"></span>
# Caution

If you are using Lark, you may encounter some functional differences between the Lark Open Platform and the Lark Open Platform. To configure integration with Lark, please contact customer support via the bottom right corner of the official website for assistance.
