---
title: "Using the new RBAC authorization system of VKE"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Use_the_new_VKE_RBAC_authorization_system"
---

VKE has added more optimized permission management capabilities based on the original RBAC authorization system. This topic primarily describes how to effectively utilize the latest version of the RBAC authorization system for VKE to improve the flexibility and efficiency of permission management.

## Application scenarios

The new version of RBAC authorization system for VKE provides permission management capabilities for the following business scenarios:

|**Business scenario** |**Scenario description** |
|---|---|
|Grant permissions on all clusters to a specified IAM user or role in a batch operation |* **Grant cluster administrator permissions**: Designate an IAM user or role as the permission administrator of the cluster, which reduces the number of times that the root user needs to perform authorization and simplifies the permission management process.<br><br>* **Grant minimum permissions**: Grant the default minimum permissions to all IAM users within the root user, which allows them to only read the basic information of VKE clusters created by other IAM users and to create VKE clusters without repeated reauthorization. |
|Limit cluster RBAC permissions to enhance the security of permission management |**Prohibit anyone other than the permission administrator from viewing RBAC authorization details**: Only permission administrators are allowed to access and manage RBAC permissions, which enhances system security and prevents information leakage. |
|Audit permission changes to enhance compliance |* **Audit historical permission changes**: Record all operations on RBAC permissions, such as granting, modifying, and revoking them. Compliance audits and issue tracing are supported to ensure compliance with your organization’s policies and regulations.<br><br>* **Regularly review permissions**: Audit RBAC permissions for users regularly to ensure that any no longer needed are revoked promptly, reducing security and compliance risks. |
|Automatically manage permissions |**Integrate permission management with the CI/CD flow**: Integrate automatic granting and revocation of RBAC permissions for clusters with the continuous integration/continuous delivery (CI/CD) flow, which ensures that R&D and O&M teams can efficiently work in a secure environment. |
|Request permissions in case of emergency |**Grant temporary permissions**: You can request temporary RBAC permissions in specific and urgent situations. After approval, you can perform specific operations within a specified time period. The temporary authorization becomes invalid after this period. |

## API

The new RBAC system provides the following three OpenAPIs to help you address complex issues and improve the efficiency of permission management.

|**OpenAPI** |**Core feature** |
|---|---|
|[GrantPermission](https://docs.byteplus.com/en/docs/vke/GrantPermission) |Granting RBAC access permission to an IAM user or role. |
|[ListPermission](https://docs.byteplus.com/en/docs/vke/ListPermissions) |Queries RBAC access policy resource information that meets the conditions. |
|[RevokePermission](https://docs.byteplus.com/en/docs/vke/RevokePermission) |Revoke the RBAC permission granted to an IAM user or role by specifying the resource ID of the permission policy. |

## Using the new RBAC permission system

### Adding or restricting the use of RBAC OpenAPI in IAM

To better use the VKE RBAC permission management system and the corresponding OpenAPI, you need to update the IAM permission policy for the specified IAM user or role.  For detailed operations, see [Creating user-defined policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

* **Add permissions**: Use the [IAM console](https://console.byteplus.com/iam) or call the [CreatePolicy](https://docs.byteplus.com/en/docs/byteplus-platform/reference-createpolicy), or [UpdatePolicy](https://docs.byteplus.com/en/docs/byteplus-platform/reference-updatepolicy) API of IAM to configure the following custom policy and grant RBAC\-related OpenAPI permissions to the specified IAM user or role.

   ```json
   {
       "Statement": [
           {
               "Action": [
                   "vke:GrantPermission",
                   "vke:ListPermission",
                   "vke:RevokePermission"
               ],
               "Effect": "Allow",
               "Resource": "*"
           }
       ],
       "Version": "1"
   }
   ```

* **Restrict permissions**: Use the [IAM console](https://console.byteplus.com/iam) or call the [CreatePolicy](https://docs.byteplus.com/en/docs/byteplus-platform/reference-createpolicy), or [UpdatePolicy](https://docs.byteplus.com/en/docs/byteplus-platform/reference-updatepolicy) API of IAM to configure the following custom policy and deny (`"Effect": "Deny"`) the IAM user or role from using RBAC\-related OpenAPIs.

   > **tip**

   > The preset **VKEFullAccessPolicy** policy of VKE in IAM includes the permissions on the three RBAC\-related OpenAPIs by default. To restrict the RBAC authorization capability for certain IAM users or roles, you need to configure Deny permission rules in IAM.

   ```json
   {
       "Statement": [
           {
               "Action": [
                   "vke:GrantPermission",
                   "vke:ListPermission",
                   "vke:RevokePermission"
               ],
               "Effect": "Deny"
           }
       ],
       "Version": "1"
   }
   ```

### Using the new RBAC permission management capabilities in VKE

By [configuring RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions), you can manage operations and access to VKE cluster resources in a more secure and efficient manner, regularly audit and update RBAC permissions, and ensure that team workflows are secure and compliant.

* Quick granting of management permissions on all clusters

   The root user can use the [VKE console](https://console.byteplus.com/vke) or call the [GrantPermission](https://docs.byteplus.com/en/docs/vke/GrantPermission) API to grant **Account Cluster Level** (all_clusters) permissions to a specified IAM user or role with a few clicks. After authorization, the IAM user or role can manage all VKE clusters in the specified region, including existing clusters and new clusters created there.

* Regular RBAC permission audit

   We recommend that you regularly audit the RBAC permissions on VKE clusters within your account. The cluster permission administrator obtains the permission list of users by calling the [ListPermission](https://docs.byteplus.com/en/docs/vke/ListPermissions) API, and then adjusts RBAC permissions based on actual business requirements.
