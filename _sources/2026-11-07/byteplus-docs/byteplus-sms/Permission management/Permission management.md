---
title: "Permission management"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/permissions-management"
---

BytePlus provides permission management capabilities to control access to message groups by different users/user groups/roles. You can create different accounts and configure different permission policies for them, achieving decentralized management of message groups. For more information about Identity and Access Management, refer to [IAM](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3) documentation. This document details on how to implement user and permission management in BytePlus SMS.

<span id="8bc0195b"></span>
## Basic concepts

This section lists the basic concepts of IAM. For details, see [IAM](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3) documentation.


|**Concept** |**Description** |
|---|---|
|Admin account |In BytePlus, the admin account is identified as the root user. The admin account is the owner of purchased BytePlus cloud resources, and is responsible for resource measurement and resource billing. By default, the admin account is granted all permissions. |
|User |"User" is an identity type. Users are created by the admin account or permission\-granted users. After users have been granted permissions (in other words, policies), they can access cloud resources through the BytePlus Console or API requests. |
|User groups |User groups are used to group users. A user can be added to multiple user groups for management. After a policy has been bound with a user group, the users in this user group will be given permissions defined in the policy. For more information, see [Creating a user group](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-group). |
|Policy |Policies are used to define permissions. After policies have been attached to users and roles, these users and roles are granted the permissions defined in these policies. |
|Project |The project management function is for you to manage cloud resources. For more information, see [About projects](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects). |
|message group |Defines the types of text messages that can be sent, which countries or regions the text messages are allowed to be sent to, the signature used, and the template available. For more information, see [Creating a message group](https://docs.byteplus.com/en/docs/byteplus-sms/docs-creating-a-message-group). |


<span id="c0d5bddf"></span>
## SMS default policies

BytePlus SMS provides the following two default policies.


|**Policy name** |**Description** |**Scope** |
|---|---|---|
|VolcSMSReadOnlyAccess |BytePlus SMS read\-only access policy |Read\-only access to SMS service, which only supports viewing relevant resources. |
|VolcSMSFullAccess |BytePlus SMS full access policy |Management permission for SMS service, including creating, viewing, and deleting relevant resources. |


Other common policies are:


* BillingCenterFullAccess: Full read and write access for Billing Center, including management access to all Billing Center pages and related OpenAPIs.

* BillingCenterReadOnlyAccess: Read\-only access to all aspects of Billing Center, including querying and exporting permissions for all Billing Center pages and related OpenAPIs.


<span id="ae74fa56"></span>
## Permission scope

BytePlus defines two types of scopes for Permission management.


|**Permission scope** |**Description** |
|---|---|
|Global |Global permissions for SMS service, combined with policies to have global read\-only or global read\-write permissions for SMS service. |
|Specified Project |Permissions for specified projects, combined with policies to have project read\-only or project read\-write permissions for SMS service, generally referring to read\-only or read\-write permissions for message groups within the project scope. For detailed operations on project management, refer to Project Management. |


<span id="b5a0fe41"></span>
## Use cases

The following lists two use cases to show how to grant a user permissions.


* User A, as a developer in the IT department, needs to call interfaces to apply for signatures, templates, and send messages. User A needs to be granted the VolcSMSFullAccess policy with a global permission scope.

* User B, an operation staff in a certain business, hopes to see the sending records of this business and analyze the sending results. User B needs to be granted the VolcSMSReadOnlyAccess policy with a permission scope specified project (the message group corresponding to this business).


<span id="e7a00ee7"></span>
## Grant user permissions

There are two ways to grant user permissions:


* Method 1: When creating a user, different permissions can be granted to the user. For more information, see [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb131b4575724816be55727da3b18fe4~tplv-goo7wpa0wc-image.image) </span>

* Method 2: On the **User** page, click the corresponding user, and click **Add Permission** in the permission operation area. For more information, see [Editing a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user). You can also remove user permissions here.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4aa432d3849142269af4799979a3ca36~tplv-goo7wpa0wc-image.image) </span>


<span id="0d8f1b73"></span>
## Remove user permissions


1. Go to the [User Management page](https://console.byteplus.com/iam/identitymanage/user) and select the user whose permissions you want to remove.

2. Select the permissions to be removed and click **Revoke** to remove the user's permissions.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/691ddf8b226a446882959c970c34fa51~tplv-goo7wpa0wc-image.image" width="1664px" />   </div>
