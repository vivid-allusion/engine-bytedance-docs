---
title: "Preparation tasks"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Preparation_tasks"
---

This document introduces the preparation tasks that operations administrators typically need to perform—such as BytePlus account preparation and service activation—before new users can use Lake AI Service (hereinafter referred to as LAS). This document outlines the key points for these preparation tasks.

# Browser recommendations

Google Chrome 36.0 or later is supported. For the best console experience, Google Chrome 100.0 or later is recommended.

# BytePlus account preparation

Before using LAS for the first time, prepare a BytePlus account. This document describes the procedures for primary\-account registration, verification, and sub\-account creation.

|Preparations |Details |Notes |
|---|---|---|
|Register a BytePlus primary account |* If your organization has never registered a BytePlus account, register an account and complete real\-name verification.<br><br>* If you already have a BytePlus account with enterprise real\-name verification, proceed to the subsequent steps. |* BytePlus LAS users are advised to complete enterprise identity verification. For assistance with account verification requirements, [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).<br><br>* Users with personal real\-name authentication cannot fully experience LAS features by default (for example, they cannot use operator service features). If users with personal real\-name authentication wish to access more features, they need to submit a ticket separately to apply. |
|Create a sub\-account |After registering the primary account, you can log in to the [Access Control Product Console](https://console.byteplus.com/iam/identitymanage/user), and on the **Identity Management \> Users** page, create sub\-users as needed. Assign different permission policies to each sub\-user, define role permissions with precision, and thereby ensure the security and privacy of business data. |* For details on the differences between primary accounts and sub\-accounts, see [IAM User Management](https://docs.byteplus.com/en/docs/CloudIdentity/Basic-user-management).<br><br>* When managing LAS product permissions for sub\-accounts, you can:<br><br>   * Add permission policies to sub\-accounts, such as **LASAIFullAccess, LASAIReadOnlyAccess** and other policies.<br><br>      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bac40f530e0644db8f5df43e31e0d0a4~tplv-goo7wpa0wc-topic.webp)<br><br>   * Add sub\-accounts to user groups: A user group is a collection of sub\-users, and the same sub\-user can belong to multiple user groups. When a user group is associated with a policy, users in the group will also have the corresponding policy permissions. For detailed operations, see [IAM User Group Management](https://docs.byteplus.com/en/docs/CloudIdentity/user-group-management). |
|(Optional) Create IAM roles |LAS currently also supports logging in and using the LAS Catalog feature using IAM roles. You can create IAM roles as needed. You can log in to the [Access Control Product Console](https://console.byteplus.com/iam/identitymanage/user), and create roles on the **Role Management** page. |* When creating roles for LAS:<br><br>   * You can select 'Account' as the trusted identity type.<br><br>   * You can also create custom permission policies for roles.<br><br>* When logging in to LAS using a role, for example, SSO login, after logging in, you can use the role to connect to services such as EMR Serverless and DataLeap, enabling read and write operations on databases and tables in Catalog. For details on SSO login operations, see [IAM Official Documentation](https://docs.byteplus.com/en/docs/CloudIdentity/User-login-settings).<br><br>   > **警告**<br>   <br><br>   > Authorization operations for Catalog via roles are currently not supported. Related requirements can be fulfilled through DataLeap.<br>    |

# Activate LAS service

## 申请开通白名单

Currently, LAS is in the invitation\-only testing phase. To activate and use LAS, [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to contact BytePlus technical support and request access to the product allowlist.

Notes:

1. Only the BytePlus primary account and IAM sub\-users with the LASAIFullAccess permission can activate the LAS service.

2. If the BytePlus primary account has completed only personal real\-name verification, users cannot access all LAS features by default, including data processing, online services, and resource management. To request access to additional features, [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).

3. After LAS is activated, charges will be incurred based on your usage and the billing items involved. No fees will be charged if the service is activated but not used. You can review the billing items and billing details in advance in the product billing section. For more information, see [Billing instructions](https://docs.byteplus.com/docs/Byteplus_LAS/Billing_instructions).

## Service activation

1. Log in to [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home?) **.**  If the current account is activating the service for the first time, you will be directed to the service activation page upon logging in to the LAS Console.

2. Service authorization. On your first login, follow the prompts on the interface and click "Authorize" to complete cross\-service access authorization, granting the LAS service account access to other products required by LAS.

3. On the right side of the interface, select the region to activate based on your actual business needs. Currently, LAS can be activated in the and Asia Pacific Southeast (Johor) regions.

4. Select the corresponding region, read and check "**I have read and agree to** the Service Agreement", then click **Enable Now** to complete the activation of the AI Data Lake service product.

5. (Optional) After enabling the service, if you log in to the LAS console and do not see the entry points for the following features on the console page, it is possible that your current operating account is a "personal real\-name authenticated" account. You can switch to an "enterprise real\-name authenticated" account to enable the service, or submit a ticket to apply for the corresponding features as needed for your business.

   |Features |Description |
   |---|---|
   |Data processing |Provides workflow orchestration capabilities for built\-in unstructured data processing operators, accelerating the data cleansing process. |
   |Dataset management |Provides dataset management capabilities, including data query, data editing, version management, data export, and more. |
   |Resource management |Manage multiple resources provided by LAS, including:<br><br><br>* Compute queues: Supports compute engines such as Spark and Ray for data computation and processing in RAG workflows.<br><br>* Online service queues: Used for online service deployment to ensure high real\-time performance and stable operation.<br><br>* Managed queues: Used for information hosting of other cloud product resources such as Kafka and VikingDB. |
   |Online services |The LAS product provides one\-stop service and model deployment functionality, allowing users to deploy models or services as online services with one click, and enabling access from the public network, VPC intranet, or by binding to CLB. Online services deployed on LAS support scaling, operations monitoring, and logging. |
