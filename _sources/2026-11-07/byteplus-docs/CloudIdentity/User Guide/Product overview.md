---
title: "Product overview"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/ProductOverview"
---

<span id="overview"></span>
## Overview

Cloud Identity is a unified management platform that connects external identities with BytePlus cloud identities. Using Cloud Identity, you can centrally manage the BytePlus login methods for employees, synchronize employee identities to BytePlus with one click, and configure SSO for your enterprise identity management system to access multiple BytePlus accounts based on your organization's multi\-account structure. It enables real\-time management and synchronization of access permission changes resulting from employee onboarding, offboarding, transfer, or role adjustment.

<span id="basic-concepts"></span>
## Basic concepts


|Concept |Description |
|---|---|
|Cloud Identity instance |A service instance where all Cloud Identity resources are maintained. It is required for using Cloud Identity. Only the organization administrator account can create the Cloud Identity instance, and only one instance can be created. |
|User |Cloud Identity users, who have a one\-to\-one mapping with employee identities. As an identity type in BytePlus, Cloud Identity users can be uniquely associated with IAM users under specific accounts for SSO. Cloud Identity provides full lifecycle management of employee identities and permission management capabilities. We recommend that you centrally manage employee identities by using Cloud Identity. |
|Identity source |The user data in your enterprise identity management system. Cloud Identity supports synchronizing employee identities from your enterprise identity management system to BytePlus. |
|User synchronization |Cloud Identity supports user synchronization from pre\-integrated identity sources, including user identity information and identity source user IDs. It also supports both full synchronization and incremental synchronization. |
|Directory authorization scope |During the synchronization of employee identities from identity sources, you need to specify the directory scope of your employee that BytePlus can access. Information of employees out of scope will not be synchronized to BytePlus. |
|Organization |The organization service is a multi\-account management service provided by BytePlus for enterprise customers. For more information, refer to [Organization](https://docs.byteplus.com/en/docs/organization/BasicConcepts). |
|Account |The account within the organization. It comprises two types:<br><br><br>* Master account: The enterprise management account that creates the organization, possessing super administrator privileges over all member accounts. Only the master account can activate and use Cloud Identity, while other accounts can perform SSO login based on configurations set by the master.<br><br>* Member account: Within the organization, a member account is created or invited by the master account for centralized management. It also functions as a BytePlus main account, operating as a separate resource tenant with data and resources isolated from other accounts. |
|Multi\-account access management |You can authorize Cloud Identity users to access different accounts within the organization, including both administrator and member accounts, based on the multi\-account structure of the organization. |
|Permission set |A permission template managed in Cloud Identity that defines the scope of permissions after Cloud Identity users access BytePlus. Centrally managed in Cloud Identity, the permission contents are synchronized to the accounts during permission authorization. |
|Access authorization |Authorizing a Cloud Identity user to access an account within the organization generates one access authorization task.<br><br><br>* Role\-based access authorization: This method creates an identity provider for user SSO in the account to be accessed and synchronously creates a role and permissions corresponding to the permission set. During SSO, the employees can log in as the IAM role corresponding to the account to be accessed through SSO.<br><br>* User\-based access authorization: This method creates an identity provider for user SSO in the account to be accessed and synchronously creates an IAM user corresponding to the Cloud Identity user. During SSO, the employees can log in as the IAM user corresponding to the account to be accessed through SSO. |
|Login portal |A dedicated login portal provided by Cloud Identity for enterprises. It supports custom domain name configuration, SSO integration with the enterprise identity system, and identity mapping and permission control for employees when they log in to BytePlus. |


<span id="applicable-scenarios"></span>
## Applicable scenarios

The usage of Cloud Identity applies in the following scenarios when multiple employees in your enterprise need to access BytePlus cloud resources, and you have multiple BytePlus accounts:


* Synchronize and maintain employee identities in BytePlus;

* Grant employees permission to access cloud resources, configure SSO rules, and manage permission changes caused by employee onboarding, offboarding, transfer, or role adjustment.


For such scenarios, we recommend that you use Cloud Identity to synchronize employee identities to BytePlus.

<span id="special-note"></span>
## Special note

<span id="_1-rules-of-use"></span>
### 1. Rules of use

Take note of the prerequisites for using Cloud Identity are:


1. You have completed your account profile. [Go compltete.](https://console.byteplus.com/user/accountProfile/?hiddenNavbar=true)

2. You have activated the Organization service. [Otherwise, you must activate the Organization service.](https://console.byteplus.com/organization/serviceOpen/)

3. You are an organization administrator.


Only the organization administrator account can create the Cloud Identity instance, and only one instance can be created.

<span id="_2-relationship-between-cloud-identity-and-iam"></span>
### 2. Relationship between Cloud Identity and IAM

Cloud Identity and IAM are both access management tools provided by BytePlus.


* IAM manages resource access permissions for IAM users and roles within a single BytePlus account. To configure SSO using IAM, the configuration process shown in the following figure must be completed for each account.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_628d4309fc11605397e30786644287e8.png) </span>


* Based on the basic capabilities of IAM, Cloud Identity manages cross\-account resource access permissions and synchronizes employee identities to BytePlus. When configuring SSO by using Cloud Identity, you can implement SSO across multiple accounts with a one\-time configuration.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_46f4aa6bfec999c949e3dd69a352218b.png) </span>
