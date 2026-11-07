---
title: "Preparation"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Preparation_sq"
---

This document is intended for operations and maintenance administrators and platform administrators who are using EMR for the first time.

Before using EMR, it is recommended to complete the preparation in the following order:


1. Prepare the Volcano Engine primary account.

2. When the primary account first accesses the console, complete service activation and authorization.

3. Decide whether to create sub\-users based on use cases.

4. Grant the required permission policies to sub\-users.

5. Once preparation is complete, you can proceed with subsequent business operations.


<span id="a57b49c3"></span>
# Primary account preparation


1. Register an account. If your enterprise has never registered a Volcano Engine account before, you must first [register a Volcano Engine account ](https://console.volcengine.com/auth/signup/).

2. Complete account [real-name verification ](https://www.volcengine.com/docs/6261/64935?_vtm_=a106466.b106468.0_0.0_0.0.2431_7633364552918697512&lang=zh)as instructed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Personal real\-name authentication is only applicable to individuals. If an enterprise user uses personal real\-name authentication, the account will belong to the individual real\-name entity. Subsequent personnel changes that lead to account disputes may affect the normal operation of the enterprise user's business.   </div>
   

   * To use the full EMR product services, a primary account with enterprise real\-name verification is required. Personal verification only allows login to the EMR console and does not permit cluster purchases.

   * For more differences between personal and enterprise real\-name verification, see: [What are the differences between personal and enterprise real-name verification?](https://www.volcengine.com/docs/6261/64934?lang=zh)

3. When logging in to the EMR console for the first time, please [Service activation](https://docs.byteplus.com/docs/E-MapReduce/Preparation_sq#a24f91cf).

4. (Optional) Create sub\-users. To finely distinguish user permissions, facilitate team collaboration, and ensure the security and privacy of business data, it is recommended to create sub\-users for the primary account and grant corresponding permissions. For details, see [Create sub-users](https://docs.byteplus.com/docs/E-MapReduce/Preparation_sq#2c738326).

   * The primary account has all EMR access permissions by default, including console and API permissions.

   * For the differences between primary accounts and sub\-users, see [What is a primary account?](https://www.volcengine.com/docs/6261/1399492?lang=zh) [What is a sub-user?](https://www.volcengine.com/docs/6261/1399492?lang=zh).

5. (Optional) Create IAM user roles. A role is a virtual identity in the IAM system, used to grant certain access permissions within the account to various identity entities. Trusted identity entities can assume the role to access cloud resources within the account. To establish trust relationships for services, accounts, or identity providers, you can choose to create IAM roles. For details, see [Role management ](https://www.volcengine.com/docs/6257/64979?lang=zh).


<span id="a24f91cf"></span>
# Service activation

If you are logging in to the EMR console for the first time, you need to complete role authorization for EMR to access cloud resources. Please log in to the [EMR Console ](https://console.volcengine.com/emr)using the primary account. Follow the interface instructions to grant the system service role named **ServiceRoleForEMR** to the primary account. After completion, the primary account can access other Volcano Engine cloud resources through the **ServiceRoleForEMR** role.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>ServiceRoleForEMR</strong>: The EMR service uses this role by default to access other Volcano Engine cloud services it depends on. This role has been granted the necessary permissions to operate products such as ECS (cloud server), VPC (private network/security group), EIP (elastic public IP), TOS (object storage), EBS (block storage), IAM (access control), Dataleap (big data development and governance suite), and RDS\-MySQL (database), allowing EMR to automatically invoke them during operation.</div>


<span id="2c738326"></span>
# Create sub\-users


1. The primary account logs in to the [Volcano Engine Access Console ](https://console.volcengine.com/iam/identitymanage/user). On the **User management \> user** page, click Create User to enter the user creation page. Set the user account, login method, and other basic information as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b7d10af287c4166b4303c65d5933019~tplv-goo7wpa0wc-image.image) </span>

2. Set permission policies for the user. The system provides preset permission policies for quick user authorization. You can also choose to grant custom permission policies to the user.

   * For information on how to select system preset permission policies, see [System preset permission configuration](https://docs.byteplus.com/docs/E-MapReduce/Preparation_sq#2ecfae0b).

   * For information on how to create custom permission policies, see. This method is suitable for scenarios where you are familiar with Volcano Engine cloud service APIs and need to grant fine\-grained permissions based on resources, actions, or role responsibilities. Before configuration, it is recommended to clarify the scope of services and operation permissions the user needs to access.

   * For more information about permission policies, see [Policy overview ](https://www.volcengine.com/docs/6257/65058?lang=zh).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3d91a25cc764bdab71e5b5e861a0be5~tplv-goo7wpa0wc-image.image) </span>

3. To add a user to a user group, switch to the Add User Group page, select the target user group. To create a new user group, click Create User Group on the right and submit the user group information.

   * Note: A user group is a collection of sub\-users. The same sub\-user can belong to multiple user groups.

   * When a user group is associated with a policy, users in the group will also have the corresponding policy permissions. For detailed operations, see [User group management ](https://www.volcengine.com/docs/6257/104988).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eecc21ee9b2f4e96ab94931920e2c74a~tplv-goo7wpa0wc-image.image) </span>


<span id="2ecfae0b"></span>
# System preset permission configuration

Before using EMR, users must be assigned the appropriate permissions by the primary account administrator. EMR includes three product types: EMR Serverless, EMR on ECS, and EMR on VKE. The system has preset basic permissions for each type, and the appropriate permission policy can be selected based on the product type.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The table below lists only the basic permission requirements. In actual use, additional permissions may need to be granted based on specific operations (such as uploading data to TOS, querying RDS, accessing VPC, and so on). You can grant permissions for the corresponding services separately in IAM.</div>


<span id="9b4f5d54"></span>
## EMR Serverless system preset permission configuration

<span id="3ab9c6f6"></span>
### EMR Serverless basic permissions


|**Preset permission policies** |**Note** |**Recommended type** |
|---|---|---|
|EMRServerlessFullAccess |This policy grants users full access to all EMR Serverless operations. |Applicable to administrators, creators, and developers |
|EMRServerlessReadOnlyAccess |EMR Serverless read\-only access permissions. |Applicable to regular users |
|EMRServerlessDeveloperAccess |The EMR Serverless developer role grants permissions required by general developers, such as viewing all EMR Serverless feature interfaces, managing jobs and job instances, operating the SQL editor, performing Submit Job operations, and more. (Queues can be viewed but cannot be created.) |Suitable for general developer users |


<span id="71f51681"></span>
### EMR Serverless common permissions


|**Preset permission policies** |**Note** |**Recommended type** |
|---|---|---|
|LASFullAccess |LAS full read and write permissions. |Applicable to administrators, creators, and developers |
|LASReadOnlyAccess |LAS read\-only access permissions. |Applicable to regular users |


For details on fine\-grained role and permission control, see [Queue permissions](https://docs.byteplus.com/docs/E-MapReduce/Queue_permissions) and [Permission management for the console: Grant permissions to IAM users](https://docs.byteplus.com/docs/E-MapReduce/si_permission_control).

<span id="5743a535"></span>
## System preset permission configuration for EMR on ECS


|**Preset permission policies** |**Note** |**Recommended type** |
|---|---|---|
|EMRFullAccess |This policy grants users full access to all EMR operations. |Applicable to administrators and creators |
|EMRDeveloperAccess |Developer access policy, granting users permissions for all operations except order\-related actions (create, release, expand) and payment of fees. |Applicable to developers and operations and maintenance personnel |
|EMRReadOnlyAccess |Read\-only access policy, allowing users to perform read\-only operations in the EMR console. |Applicable to regular users |


For details on fine\-grained role and permission control, see [Roles and permissions](https://docs.byteplus.com/docs/E-MapReduce/ecs_roles_and_permissions).

<span id="c3b0cb13"></span>
## System preset permission configuration for EMR on VKE


|**Preset permission policies** |**Note** |**Recommended type** |
|---|---|---|
|EMROnVKEFullAccess |Full access policy, grants users permission to perform all operations on EMR on VKE. |Applicable to administrators and creators |
|EMROnVKEDeveloperAccess |Developer access policy, grants users permission to perform all operations except for create, release, and scale, which involve orders and payment. |Applicable to developers and operations and maintenance personnel |
|EMROnVKEReadOnlyAccess |Read\-only access policy, allows users to perform read\-only operations in the EMR on VKE console. |Applicable to regular users |


For details on fine\-grained role and permission control, see [Roles and permissions](https://docs.byteplus.com/docs/E-MapReduce/ecs_roles_and_permissions).
