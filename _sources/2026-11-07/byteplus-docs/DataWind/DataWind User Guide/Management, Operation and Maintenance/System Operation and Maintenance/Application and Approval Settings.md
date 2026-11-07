---
title: "Application and Approval Settings"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Application_and_Approval_Settings"
---

DataWind supports three application and approval methods: contacting the resource administrator, proactively initiating an approval request (Feishu approval), and notifying the resource administrator via system email. This article introduces how to use the application/approval feature.

<span id="dcaef210"></span>
# Feature overview

The application/approval settings module is provided in system management.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb527f0270c24da4a6f0e2d455023366~tplv-goo7wpa0wc-image.image) </span>

**Application settings**:

In the "Application settings" module, administrators can configure the content displayed to users when they lack permissions. The following three application methods are available:


* Contact the resource administrator

* Initiate an approval request

* Notify the resource administrator via system email


**Approval settings**:

The "Approval settings" module appears only after "Initiate an approval request" is selected in application settings. In this module, the approval type can be set to Feishu approval.

To request permission for a resource, users can submit an application to the administrator. After receiving the application, the administrator can grant the user the required permissions in the system.

The product supports Feishu approval, allowing users to independently request permissions from resource owners. Once the owner approves, the applicant will obtain the corresponding permissions for the requested resource.

<span id="2d91fb39"></span>
# Precautions


* Both the email notification to the resource administrator and the Feishu approval feature require users to complete the relevant configuration in [办公平台集成](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628f8) first; otherwise, the "Application/approval settings" module will not be visible.

* The following application settings are supported in both private and SaaS environments:

   
   |Environment |Contact resource administrator |Initiate approval request |System email notification to resource administrator |
   |---|---|---|---|
   |On\-premises |✅ |✅ |✅ |
   |SaaS |✅ |❌ |✅ |
   


<span id="3c954cdb"></span>
# Feature introduction

<span id="565fd492"></span>
## Contact the resource administrator

Select application/approval settings in the left sidebar and click "Contact the resource administrator". The system will display a window prompting you to confirm whether to switch the application settings. Click "Close" on the old method to switch to the new application method.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After switching to the 'Contact Resource Administrator' application method, users can only contact the resource administrator and obtain permissions through the administrator's proactive authorization. Permissions cannot be obtained through the approval process. However, tickets that have already been submitted are not affected.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bed52b05478346318768c1547ba3e664~tplv-goo7wpa0wc-image.image) </span>

After successful configuration, when users access resources without permission, a pop\-up window will appear to notify them and provide the administrator's contact information.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b84f3ab4b0114494961e4f7953cc32ac~tplv-goo7wpa0wc-image.image" width="468px" /></div>


<span id="168c3343"></span>
## Initiate an approval request

The product supports Feishu Approval, allowing users to independently request permissions from resource owners. Once the owner approves, the applicant will receive the corresponding permissions for the requested resource, thereby lowering the barrier to data usage and reducing the time required for data or IT personnel to grant data access.


1. Click "Initiate approval request" and select "Feishu Approval".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c92c310bf9c416bb3e60c67cb7f2241~tplv-goo7wpa0wc-image.image) </span>

2. Before configuring Feishu Approval, you need to complete [(集成相关,不发布)Office Platform Integration](https://docs.byteplus.com/docs/undefined/69c3469a50cba904c1f57e28) and [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9). For detailed steps, see [(飞书集成相关,不发布)Permission Approval Integration with Lark](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62771). You can click the prompt on the page to go directly to the corresponding page to perform the operation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b5997b4b44246abb2c0b93d7214d072~tplv-goo7wpa0wc-image.image) </span>

3. In the pop\-up window, select the process administrator and approval process.

   * Process administrator: The process administrator can manage the configuration of approval templates and act as the fallback approver when there are no approvers in the process.

   * Approval process: After modifying the approval process configuration, approval tickets that have already been initiated are not affected; only tickets initiated after the modification will be subject to the new configuration.

4. Feishu approval process example.

   1. After successful configuration, when a user accesses a resource without permission, a pop\-up prompt will appear.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b84f3ab4b0114494961e4f7953cc32ac~tplv-goo7wpa0wc-image.image" width="468px" /></div>



2. When the user clicks the "Request permission" button, they will be redirected to the following interface to request permissions for the resource.

3. After submitting the request, the administrator will receive a notification and can choose to approve or reject the request. After the approver takes action, the applicant will also receive a notification indicating whether the request was approved or rejected.


<span id="8a404d8a"></span>
## System email notification to resource administrator

In the left sidebar, select Application/Approval Settings and click "System email notification to resource administrator". The system will display a pop\-up window asking you to confirm whether to switch the application settings. Click "Close" for the old method to switch to the new application method.

After successful configuration, when a user accesses a resource without permission, a pop\-up prompt will appear. When the user clicks the "System email notification to administrator" button, the administrator will receive an email notification.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b84f3ab4b0114494961e4f7953cc32ac~tplv-goo7wpa0wc-image.image" width="468px" /></div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a user's email address is missing from the system, email delivery may fail. After configuration, click the lightbulb icon to go to the page where you can confirm the user's email information.</div>
