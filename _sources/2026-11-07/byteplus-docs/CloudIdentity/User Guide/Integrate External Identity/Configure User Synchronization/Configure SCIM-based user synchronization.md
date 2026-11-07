---
title: "Configure SCIM-based user synchronization"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Configure-SCIM-based-user-synchronization"
---

<span id="scenarios"></span>
## Scenarios

When you initialize the cloud identities of your enterprise, you must use your identity management platform as the "identity source" of your cloud identities to import employee identities into Cloud Identity.

If the number of employees that need to log in is small, you can create users with the same names on Cloud Identity and manually perform management operations such as addition, deletion, update, and query. For details, refer to [Basic user management](https://docs.byteplus.com/en/docs/CloudIdentity/Basic-user-management).

If the number of employees that need to log in is large, you can directly synchronize all users of your enterprise identity source by using the method described in this topic.

<span id="prerequisites"></span>
## Prerequisites


1. You have activated [Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/Activate-Cloud-Identity).

2. You are an organization master account, such as the root user or an authorized IAM user.

3. Your enterprise identity source supports the user synchronization protocol of System for Cross\-domain Identity Management (SCIM) 2.0.


<span id="basic-process-of-user-synchronization-based-on-scim-2-0"></span>
## Basic process of user synchronization based on SCIM 2.0

SCIM standardizes the principles and APIs for data sharing between identity systems. Cloud Identity receives identity data synchronized from an enterprise identity provider (IdP) based on the SCIM protocol.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cdcbc0da715d17dc8c5aa7fb38078d38.png) </span>

<span id="procedure"></span>
## Procedure

<span id="_1-operations-on-cloud-identity"></span>
### 1. Operations on Cloud Identity


1. Log in to the BytePlus console, and go to the [User management > User synchronization settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/) page.

2. Click **Configure identity source**, and select SCIM.

3. On the User synchronization settings page, obtain the following necessary configuration information.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d0507310560c14d9481486a2fb4f245a.png) </span>

   1. Obtain the SCIM endpoint information under the identity source.

   2. Click the button on the right side of the page to generate an SCIM key. Note:

      1. **The generated key is displayed only once. Save it securely.** 

      2. Maintain regular key rotation for the security of your enterprise information. You can generate up to two SCIM keys for rotation. We recommend that you delete the keys that you no longer use at the earliest opportunity.


<span id="_2-operations-in-the-enterprise-identity-system"></span>
### 2. Operations in the enterprise identity system

Add Cloud Identity as a trusted SCIM application on the enterprise IdP based on the endpoint and SCIM key obtained from Cloud Identity in the preceding step. You can use one of the following configuration methods based on your IdP:


1. Create a Cloud Identity application.

2. Enter the SCIM endpoint obtained in the preceding step.

3. Enter the SCIM key obtained in the preceding step. Pay attention to the validity period of the key for a timely rotation.

4. Process fields to be synchronized on your IdP based on the specific situation of the IdP. For more information, refer to [APIs of SCIM 2.0 supported by Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/APIs-of-SCIM-supported-by-Cloud-Identity).

   1. For fields that do not need to be synchronized, we recommend that you delete them.

   2. For characters not supported in Cloud Identity fields, we recommend that you process them by using regular expressions.


After you perform the preceding operations, the configuration is completed.

As synchronizations are initiated from the enterprise IdP, you can initiate and debug the first synchronization based on the guidance of the IdP. On your enterprise IdP, you can view the error messages returned by the SCIM APIs of Cloud Identity. On the [User management > User synchronization settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/) page, you can view the records of written users and user groups.

<span id="what-to-do-next"></span>
## What to do next

After you create a user, you can [configure user login settings](https://docs.byteplus.com/en/docs/CloudIdentity/User-login-settings).
