---
title: "Access control"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Access-control-01"
---

Identity and Access Management (IAM) is a permission management service developed by BytePlus. You can use this service to limit different identities from accessing cloud resources. For example, you can authorize an IAM user to access multiple cloud resources, grant permissions on different cloud resources, and grant different permissions to different IAM users. This enables you to efficiently manage resource access permissions and prevents data leaks.

<span id="terms"></span>
## Terms


|Term |Description |
|---|---|
|BytePlus account |You can create BytePlus accounts on the BytePlus official site. By default, a BytePlus account has permissions to use all API actions and consoles within the account. You can use a BytePlus account to buy and upgrade resources, renew subscriptions, and cancel subscriptions. You can also view resource orders and bills. |
|IAM user |IAM users are identities created by using BytePlus accounts or by users that have the required permissions. IAM users are granted different permissions. For more information, refer to [Managing users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management). |
|User group |A user group is a collection of IAM users. An IAM user may belong to different user groups. The permissions of a user group are limited by the associated policy. After a user group is associated with a policy, the IAM users in the user group are granted the corresponding permissions. For more information, refer to [Managing user groups](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-group-management) and [Managing policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management). |
|Role |You cannot assume roles to directly access cloud services. You must assign roles to other identities. The identities can assume the roles to obtain temporary credentials to access cloud resources. For more information, refer to [Managing roles](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management). |
|Policy |Policies are used to describe permissions. IAM offers identity\-based policies and resource\-based policies. To grant permissions to IAM users, user groups, and roles, you must associate policies with them. |


<span id="iam-policies-for-cloud-enterprise-network-cen"></span>
## IAM policies for Cloud Enterprise Network (CEN)

By default, newly created IAM users, user groups, or roles do not have any permissions. You must use a BytePlus account to associate policies with them. This way, IAM users or user groups can perform operations on the specified cloud resources. IAM allows you to use default policies and custom policies.


* Default policies: Default policies for CEN are available in the IAM console. You can associate these policies with IAM users, user groups, or roles on demand.

   
   |Policy Name |Description |Supported Operations |
   |---|---|---|
   |CENFullAccess |Read and write permissions on CEN |This policy grants full permissions on CEN. For example, you can create, view, and delete resources. |
   |CENReadOnlyAccess |Read permissions on CEN |This policy grants only read permissions. You can only view resources. |
   

* Custom policies: If the default policies of IAM cannot meet your requirements, refer to [Managing policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management) and create custom policies.
