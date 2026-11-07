---
title: "Overview of SCIM-based user synchronization"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Overview-of-SCIM-based-user-synchronization"
---

<span id="overview-of-scim-based-user-synchronization"></span>
# Overview of SCIM\-based user synchronization

<span id="introduction"></span>
## Introduction

System for Cross\-domain Identity Management (SCIM) is a protocol for managing identities such as users and groups on the web. Based on SCIM, you can proactively synchronize the identities, such as users, user groups, and their relationships, in an enterprise identity management system, also known as an identity provider (IdP), to a service provider (SP) such as Cloud Identity by using the APIs of the standard protocol.


* For more information about the configuration process, refer to [Configure SCIM-based user synchronization](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-SCIM-based-user-synchronization).

* For more information about the API specifications, refer to [APIs of SCIM 2.0 supported by Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/APIs-of-SCIM-supported-by-Cloud-Identity).


<span id="precautions"></span>
## Precautions


* **Uniqueness of fields**: Cloud Identity requires the username, mobile phone number, and email address of a user and the name of a user group to be unique in a Cloud Identity instance. When you configure SCIM attribute mappings in your IdP, select attributes with unique values to map to the preceding fields. Additionally, during the synchronization of SCIM mappings, make sure that the values of the attribute mapped to the externalId field are unique across all users and across all user groups in your IdP.

* **Required fields**: Cloud Identity requires that each user have a username and each user group has a user group name. The absence of relevant values may cause SCIM synchronization failures.

* **Processing of multi\-value attributes**: SCIM in Cloud Identity does not support multi\-value attributes, such as multiple email addresses or mobile phone numbers for a user. During synchronization, if you use SCIM to synchronize multi\-value attributes to Cloud Identity, Cloud Identity automatically adopts the first value as the value of such an attribute. To avoid ambiguity, ensure that only one value is specified for each attribute.

* **Restrictions on users synchronized based on SCIM**: Users synchronized based on SCIM cannot be modified or deleted. Modifying or deleting them requires additional configuration on the IdP. For details, consult your IdP. If you delete the SCIM identity source on Cloud Identity, such users become modifiable and deletable.

* **Known issue about users deleted based on SCIM**: Cloud Identity does not support the enabling and disabling of users. For a deleted user, some IdPs change the status of the corresponding SP user to disabled. If your IdP has the same implementation, the corresponding Cloud Identity user still exists, without any changes to its status.

* **IdP configuration for starting SCIM synchronizations**: SCIM\-based synchronization and update intervals are controlled by your IdP, which proactively sends changes to its user or group information to Cloud Identity. After receiving these changes, Cloud Identity starts to update its user and group data. For more information about the update frequency, consult your IdP.
