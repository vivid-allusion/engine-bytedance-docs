---
title: "Access authorization overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-access-authorization"
---

BytePlus VOD verifies the identities of users making requests and confirms that they have the necessary permissions to perform the requested operation. This article provides an overview of the essential concepts related to access authorization in BytePlus VOD.

<span id="0d0c0262"></span>
## Key concepts

<span id="e9488410"></span>
### IAM

IAM (Identity and Access Management) is a permission management system used to control access to cloud resources for different identities (for example, users and roles), ensuring resource security and improving multi\-user collaboration. For more information, see [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

<span id="7a18d07d"></span>
### Admin account

When you sign up for a BytePlus account, your account is identified as the admin account. The admin account pays for and has full control over all resources in the account.

<span id="a31b3b77"></span>
### Sub account

The admin account can create sub\-accounts (IAM users) and assign specific permissions (Policy) to them for access control. For more information, see [Access authorization overview](https://docs.byteplus.com/docs/byteplus-vod/docs-access-authorization).

<span id="49c690f4"></span>
### Policy

A policy is a set of permissions defined in a specific syntax structure. It specifies the operations, resource scope, and conditions under which permissions are effective. By default, new IAM users have no permissions, and the admin account must attach policies to them to grant permissions. After being granted permissions, IAM users can manage and access cloud resources in the admin account. To ensure data security, it is important to follow the principle of least privilege when granting permissions, providing IAM users with only the necessary permissions.

There are two types of policies:


* System default policies: These are collections of policies created and managed by BytePlus for common permissions. System default policies can only be used for authorization and cannot be modified by users. For details, see [BytePlus VOD system default policies](https://docs.byteplus.com/docs/byteplus-vod/docs-creating-iam-users#cb54f3b2).

* Custom policies: These are policies created and edited by users for more granular permission management scenarios.


<span id="1bc974b5"></span>
### Project

Projects are a resource management method provided by BytePlus. A project is a set of resources. When you create cloud product resources, you can choose to associate the resources with a specified project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To learn how to create a project, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project">Creating a project</a>.</div>


In BytePlus VOD, you can associate the spaces and applications with a specified project. The relationship between spaces, applications, and projects is shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fde4b940506f48d7b9a024b971d6484e~tplv-goo7wpa0wc-image.image) </span>

Suppose:


* The admin account associates BytePlus VOD **Space A** and **Space B** with **Project 1**, and grants **Sub\-account 1** permissions for **Project 1**.

* The admin account associates BytePlus VOD **Space C** with **Project 2**, and grants **Sub\-account 2** permissions for **Project 2**.


Then:


* Sub\-account 1 can only view and use the resources and data in **Space A** and **Space B** when using the BytePlus VOD console or OpenAPI, and does not have access to **Space C**.

* Sub\-account 2 can only view and use the resources and data in **Space C** when using the BytePlus VOD console or OpenAPI, and does not have access to **Space A** and **Space B**.


<span id="6d276704"></span>
### Access key

Access keys serve as the credentials for making requests to the BytePlus API. An access key consists of an access key ID (AK) and a secret access key (SK). Currently, BytePlus VOD supports the following types of access keys:


* Admin account's AK/SK: Each admin account can have up to two pairs of enabled or disabled AK/SK. The AK/SK associated with the admin account has full permissions for all resources in the account. However, if these credentials are leaked, it can pose a significant security risk and potentially result in resource loss. Therefore, it is not recommended to use the admin account's AK/SK to access BytePlus VOD services.

* Sub\-account's AK/SK: It is highly recommended to create sub\-accounts, assign necessary permissions, and then use their AK/SK to access BytePlus VOD services.


<span id="0b796523"></span>
## BytePlus VOD system default policies

The following table lists the system default policies provided by BytePlus VOD.


|Policy name |Description |
|---|---|
|VodFullAccess |Full read and write access to VOD. The user can configure all resources within VOD. |
|VodReadOnlyAccess |Full read access to VOD. The user can view all resources within VOD. |
|VodQualityAccess |Read\-only access to the VOD quality platform for basic operation and debugging. |
|VODQualityFullAccess |Full read and write access to the VOD quality platform for operation and debugging. The user can configure all resources within the VOD quality platform. |
