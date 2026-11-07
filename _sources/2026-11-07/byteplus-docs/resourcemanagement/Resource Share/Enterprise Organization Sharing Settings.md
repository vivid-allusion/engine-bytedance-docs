---
title: "Enterprise Organization Sharing Settings"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Enterprise_Organization_Sharing_Settings"
---

The owner of a resource can share the resource with the organization and its OUs or member accounts only after the enterprise organization sharing feature is enabled by using an enterprise organization administrator account. After sharing with enterprise organization is enabled, the RS service can automatically grant or revoke the shared resource access permissions of the corresponding account based on the account changes under the organization or its OUs, without the need to enumerate each account. After resources are shared within an organization, accounts in the organization can access and use the shared resources without accepting invitations.

<span id="enabling-sharing-with-enterprise-organization"></span>
## Enabling sharing with enterprise organization


1. Log in to Resource management and go to [Resource sharing > Share settings](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/setting) in the left navigation bar.

2. Click Enable to enable sharing with enterprise organization.

3. After the enabling operation, a service\-linked role called ServiceRoleForResourceShare is created, which allows the RS service to access the information about the enterprise organization and its structure, and to share resources with the enterprise organization and its departments and member accounts.


<span id="disabling-sharing-with-enterprise-organization"></span>
## Disabling sharing with enterprise organization


1. Log in to Resource management and go to [Resource sharing > Share settings](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/setting) in the left navigation bar.

2. Click Disable to disable sharing with enterprise organization.

3. After the disabling operation, you cannot select Allow sharing with organization only when you create a shared unit, and you cannot add a shared unit from the enterprise organization. You can select only Allow sharing with any account, and you need to specify account ID to complete the creation of a shared unit.


&nbsp;
