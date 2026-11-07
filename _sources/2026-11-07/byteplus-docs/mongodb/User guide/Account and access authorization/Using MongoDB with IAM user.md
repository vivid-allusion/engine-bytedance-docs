---
title: "Using MongoDB with IAM user"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers"
---

BytePlus supports creating IAM users through the root account or users with management permissions. You can grant different permissions to different IAM users, enabling users with different identities under the same account to have different levels of access permissions, facilitating fine\-grained permission management. This topic describes how to use Document Database for MongoDB through IAM users.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* **IAM overview**

   Identity and Access Management (short for IAM) is a permission management system provided by BytePlus, used to control the access permissions of different identities to cloud resources. IAM provides a series of functions such as multi\-identity management, fine\-grained permission management, login access or API access with Single Sign\-On (SSO), security authentication, temporary token service, and operation auditing, meeting the needs of user permission separation and unified resource management in diverse scenarios. For more details about IAM, refer to [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

* **IAM policy**

   A policy is a description of permissions. IAM users, user groups, or roles need to be granted permissions by associating with the policy. The operation scope, resource scope, and permission activation conditions can be defined in a policy. IAM supports two types of policies: System default policy and user custom policy. For more details, refer to [About policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).

* **Scope of policy**

   IAM supports specifying the scope of policies for users. The following two scopes are currently supported:

   * **Global permissions**: The authorized policy takes effect on the resources within all projects (including newly added projects in the future) under the account.

   * **Project permissions**: The policy only takes effect on the resources within the specified project.


<span id=".5bi46KeB5LqR5pyN5Yqh57O757uf6aKE6K6-562W55Wl"></span>
## Predefined policies for common cloud service systems

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to the common predefined policies of the system, IAM also supports more fine\-grained permission management through custom policies. For more details on custom policies, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user-custom-policy">Manage custom policies</a>.</div>


<span id=".bW9uZ29kYi3kupHmnI3liqE="></span>
### MongoDB cloud service

Before using the MongoDB cloud service through IAM users, you need to authorize the IAM user with relevant permissions for the MongoDB cloud service. The table below lists the system preset policies involved in the MongoDB cloud service for your reference.


|System predefined policies involved |Description |
|---|---|
|MongoDBFullAccess |All management permissions of Document Database for MongoDB. IAM users with this permission will have read and write permissions for Document Database for MongoDB within the scope of the policy's action, such as creating instances, deleting instances, and editing instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Document Database for MongoDB supports association with other cloud services (such as VPC, EIP). Therefore, if IAM users need to use other cloud services, you must also add corresponding management or read\-only policies for those services. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers#.5YW25a6D5bi46KeB5LqR5pyN5Yqh">Other common cloud services</a>.</div><br> |
|MongoDBReadOnlyAccess |Read\-only access permission of Document Database for MongoDB. After adding this permission, users can view the MongoDB instances within the scope of the policy's action. |


<span id=".5YW25a6D5bi46KeB5LqR5pyN5Yqh"></span>
### Other common cloud services

Document Database for MongoDB supports association with other cloud services (such as VPC, EIP). The following lists the system preset policies for some common cloud services for your reference.


|Cloud service name |System predefined policies involved |Description |
|---|---|---|
|Virtual Private Cloud |VPCFullAccess |All management permissions of VPC. After adding this permission, users will have read and write permissions for the private network within the scope of the policy's action, such as creating a private network, associating a private network or subnet with a MongoDB instance and so on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify a project when you create a VPC, but you cannot specify a project when you create a subnet, which is by default under the same project as the VPC to which it belongs. The project changes of the VPC and the subnet are independent, that is, modifying the project to which the VPC belongs will not modify the project of the subnet under the current VPC at the same time. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Managing-projects">Managing projects</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you change the project to which the VPC belongs, you also need to change the project of the subnets under the VPC to ensure the consistency of the projects to which they belong. Otherwise, when IAM user with non\-global privileges creates a cloud resource (such as Document Database for MongoDB), it will not be able to select a subnet or anomalies will be reported. For specific procedures for modifying projects, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project">Editing project</a>.</div><br> |
||VPCReadOnlyAccess |Read\-only access permission of the VPC. After adding this permission, users can view the private network and subnet information of MongoDB instances within the scope of the policy's action. |
|Public IP |EIPFullAccess |All management permissions of the public IP (EIP). After adding this permission, users will have read and write access to public IPs within the policy's scope, such as applying for public IPs or associating public IPs with MongoDB instances and so on. |
||EIPReadOnlyAccess |Read\-only access permission for public IP (EIP). After adding this permission, users can view the public IP information of MongoDB instances within the scope of the policy's action. |
|Cloud monitor |CloudMonitorFullAccess |All management permissions for cloud monitoring (CloudMonitor). After adding this permission, users will have read and write permissions for the monitoring and alerting of MongoDB instances within the scope of the policy's action, such as viewing the monitoring data of instances, adding alerting strategies to instances and so on. |
||CloudMonitorReadOnlyAccess |Read\-only access permission for cloud monitoring (CloudMonitor). After adding this permission, users can view monitoring data of MongoDB instances within the scope of the policy.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If IAM user needs to view monitoring information, this permission must be added for the IAM user within the <strong>global</strong> scope.</div><br> |
|Database Workshop |DbwFullAccess |All management permissions of the Database Workshop (DBW). After adding this permission, users will have read and write permissions for the DBW within the scope of the policy's action, such as using the DBW to log in to MongoDB instance and use the data interaction console function and so on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If an IAM user needs to use DBW to log in to or manage MongoDB instances, they need to add this permission for the IAM user within the <strong>global</strong> scope.</div><br> |
|Billing center |BillingCenterFullAccess |All read and write permissions of the billing center, including the management permissions of all pages and related OpenAPI of the billing center. After adding this permission, users will have read and write permissions for the billing center within the scope of the policy's action, such as recharging, renewing, and canceling subscriptions for instances through the billing center.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If IAM users need to perform operations such as recharging, renewing, or unsubscribing for MongoDB instance, add this permission for the IAM user within the <strong>global</strong> scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you convert a pay\-as\-you\-go MongoDB instance's billing type to subscription, even if the IAM user has the <code>BillingCenterFullAccess</code> permission for the instance under the corresponding project, you still need to re\-add the <code>BillingCenterFullAccess</code> permission for the IAM user within the <strong>global</strong> scope. Otherwise, the IAM user will receive a permission insufficiency error when unsubscribing or renewing the instance.</div><br> |
|Tag resources |TagFullAccess |This policy allows you to manage tag service\-related content within the account, for example, querying by tags and other related content. For more details about tags, refer to [Tag management](https://docs.byteplus.com/en/docs/mongodb/tag-management).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If IAM users need to add tags to MongoDB instance, they can directly see the existing tags under the root account in the drop\-down lists of tag keys and tag values. The root account needs to add this permission for the IAM user in the <strong>global</strong> scope. Otherwise, the drop\-down list seen by the IAM user is empty.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">IAM users can add new tags to an instance even without <code>TagFullAccess</code> permission. For specific procedures on adding tags, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/associate-tag">Associating or adding tag</a>.</div><br> |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Allowlists which created before October 17, 2024, are only effective globally and not within a specified project. Therefore, if the scope of the `MongoDBFullAccess` or `MongoDBReadOnlyAccess` policy granted to the IAM user is **project permissions**, to ensure the IAM user can access or manage MongoDB's existing allowlists, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to add the allowlists that need to be accessed or managed to the IAM user's project. Otherwise, the IAM user will receive an insufficient permission error when using features related to the corresponding allowlist.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Create IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log in to the <a href="https://console.byteplus.com/iam/identitymanage/user">IAM console</a> with root account or a user with administrator permissions to create IAM users.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating IAM users, you can directly add system pre\-defined policies for MongoDB and other associated services and specify the policy scope.   </div>
   

2. [Add permissions to IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user).

3. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb) with the IAM user and use MongoDB services.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure the security of cloud resources and reduce the risk of root account AK/SK leakage, we recommend creating separate AK/SK for IAM users to call MongoDB\-related API interfaces. For details on creating AK/SK, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey">Managing access key</a>.   </div>
