---
title: "Using Redis with IAM user"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers"
---

BytePlus supports creating IAM users through the root account or users with management permissions. You can grant different permissions to different IAM users, enabling users with different identities under the same account to have different levels of access permissions, facilitating fine\-grained permission management. This topic describes how to use Cache for Redis through IAM users.

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


<span id=".cmVkaXMt5LqR5pyN5Yqh"></span>
### Redis cloud service

Before using the Redis cloud service through IAM users, you need to authorize the IAM user with relevant permissions for the Redis cloud service. The table below lists the system preset policies involved in the Redis cloud service for your reference.


|System predefined policies involved |Description |
|---|---|
|RedisFullAccess |All management permissions of Cache for Redis. IAM users with this permission will have read and write permissions for Cache for Redis within the scope of the policy's action, such as creating instances, deleting instances, and editing instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cache for Redis supports association with other cloud services (such as VPC, EIP). Therefore, if IAM users need to use other cloud services, you must also add corresponding management or read\-only policies for those services. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers#.5YW25a6D5bi46KeB5LqR5pyN5Yqh">Other common cloud services</a>.</div><br> |
|RedisReadOnlyAccess |Read\-only access permission of Cache for Redis. After adding this permission, users can view the Redis instances within the scope of the policy's action. |


<span id=".5YW25a6D5bi46KeB5LqR5pyN5Yqh"></span>
### Other common cloud services

Cache for Redis supports association with other cloud services (such as VPC, EIP). The following lists the system preset policies for some common cloud services for your reference.


|Cloud service name |System predefined policies involved |Description |
|---|---|---|
|Virtual private cloud |VPCFullAccess |All management permissions of VPC. After adding this permission, users will have read and write permissions for the private network within the scope of the policy's action, such as creating a private network, associating a private network or subnet with a Redis instance and so on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify a project when you create a VPC, but you cannot specify a project when you create a subnet, which is by default under the same project as the VPC to which it belongs. The project changes of the VPC and the subnet are independent, that is, modifying the project to which the VPC belongs will not modify the project of the subnet under the current VPC at the same time. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Managing-projects">Managing projects</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you change the project to which the VPC belongs, you also need to change the project of the subnets under the VPC to ensure the consistency of the projects to which they belong. Otherwise, when IAM user with non\-global privileges creates a cloud resource (such as Cache for Redis), it will not be able to select a subnet or anomalies will be reported. For specific procedures for modifying projects, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project">Editing project</a>.</div><br> |
||VPCReadOnlyAccess |Read\-only access permission of the VPC. After adding this permission, users can view the private network and subnet information of the Redis instances within the scope of the policy's action. |
|Public IP |EIPFullAccess |All management permissions of the public IP (EIP). After adding this permission, users will have read and write access to public IPs within the policy's scope, such as applying for public IPs or associating public IPs with Redis instances and so on. |
||EIPReadOnlyAccess |Read\-only access permission for public IP (EIP). After adding this permission, users can view the public IP information of the Redis instances within the scope of the policy's action. |
|Cloud monitor |CloudMonitorFullAccess |All management permissions for cloud monitoring (CloudMonitor). After adding this permission, users will have read and write permissions for the monitoring and alerting of Redis instances within the scope of the policy's action, such as viewing the monitoring data of instances, adding alerting strategies to instances and so on. |
||CloudMonitorReadOnlyAccess |Read\-only access permission for cloud monitoring (CloudMonitor). After adding this permission, users can view monitoring data of Redis instances within the scope of the policy.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If IAM user needs to view monitoring information, this permission must be added for the IAM user within the <strong>global</strong> scope.</div><br> |
|Database workshop |DbwFullAccess |All management permissions of the Database workshop (DBW). After adding this permission, users will have read and write permissions for the DBW within the scope of the policy's action, such as using the DBW to log in to Redis instance and use the data interaction console function and so on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">IAM users with <code>DBWFullAccess</code> permission will have management permissions for Redis instances within the authorized scope (project or global), not subject to the constraint of the RedisFullAccess policy. Authorize with caution.</div><br> |
|Billing center |BillingCenterFullAccess |All read and write permissions of the billing center, including the management permissions of all pages and related OpenAPI of the billing center. After adding this permission, users will have read and write permissions for the billing center within the scope of the policy's action, such as recharging, renewing, and canceling subscriptions for instances through the billing center.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If IAM users need to perform operations such as recharging, renewing, or unsubscribing for Redis instance, add this permission for the IAM user within the <strong>global</strong> scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you convert a pay\-as\-you\-go Redis instance's billing type to subscription, even if the IAM user has the <code>BillingCenterFullAccess</code> permission for the instance under the corresponding project, you still need to re\-add the <code>BillingCenterFullAccess</code> permission for the IAM user within the <strong>global</strong> scope. Otherwise, the IAM user will receive a permission insufficiency error when unsubscribing or renewing the instance.</div><br> |
|Tag resources |TagFullAccess |This policy allows you to manage tag service\-related content within the account, for example, querying by tags and other related content. For more details about tags, refer to [Tag management](https://docs.byteplus.com/en/docs/redis/tag-management).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If IAM users need to add tags to Redis instance, they can directly see the existing tags under the root account in the drop\-down lists of tag keys and tag values. The root account needs to add this permission for the IAM user in the <strong>global</strong> scope. Otherwise, the drop\-down list seen by the IAM user is empty.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">IAM users can add new tags to an instance even without <code>TagFullAccess</code> permission. For specific procedures on adding tags, refer to <a href="https://docs.byteplus.com/en/docs/redis/associate-tag">Associating or adding tag</a>.</div><br> |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Some cloud resources are only effective globally and not within a specified project. Since some cloud resources only take effect at the global level and do not support taking effect within specified projects. Therefore, when IAM users use the Redis cloud service and the scope of the `RedisFullAccess` or `RedisReadOnlyAccess` policy granted to the IAM user is **project permissions**. To ensure that the IAM user can use the corresponding Redis functions normally, you also need to grant the IAM user the relevant permissions listed in the following table at the global level. Otherwise, the IAM user will receive insufficient permission error when using related functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can grant the IAM user <strong>Global permissions</strong> for Redis cloud service related features through custom policy. For more details about custom policy syntax, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax">Policy syntax</a>.</div>



|Function classification |Action involved |Scope of policy |Syntax example |
|---|---|---|---|
|Operation log |DescribeEventLogs |Global |If IAM users need to view Redis operation logs, you need to allow the IAM user to have the DescribeEventLogs action permission.<br><br>The syntax example is as follows.<br><br>```JSON```<br>```{```<br>```    "Statement": [```<br>```        {```<br>```            "Effect": "Allow",```<br>```            "Action": [```<br>```                "Redis:*DescribeEventLogs*"```<br>```            ],```<br>```            "Resource": [```<br>```                "*"```<br>```            ]```<br>```        }```<br>```    ]```<br>```}```<br> |
|Parameter templates |* DescribeParameterGroups<br><br>* DescribeParameterGroupDetail<br><br>* DescribeApplyParameterGroup<br><br>* DescribeSupportParameters<br><br>* CreateParameterGroup<br><br>* ModifyParameterGroup<br><br>* DeleteParameterGroup |Global |* If you only need to grant read\-only access to the parameter template for the IAM user, then you only need to allow the IAM user to have the DescribeParameterGroups and DescribeParameterGroupDetail action permissions.<br><br>   The syntax example is as follows.<br><br>   ```JSON```<br>```   {```<br>```       "Statement": [```<br>```           {```<br>```               "Effect": "Allow",```<br>```               "Action": [```<br>```                   "Redis:*DescribeParameterGroups*",```<br>```                   "Redis:*DescribeParameterGroupDetail*"```<br>```               ],```<br>```               "Resource": [```<br>```                   "*"```<br>```               ]```<br>```           }```<br>```       ]```<br>```   }```<br>```   ```<br>   <br><br>* If you want to grant full administrative permissions for the parameter template to IAM users, then you need to allow the IAM users to have full operational permissions for the parameter template.<br><br>   The syntax example is as follows.<br><br>   ```JSON```<br>```   {```<br>```       "Statement": [```<br>```           {```<br>```               "Effect": "Allow",```<br>```               "Action": [```<br>```                   "Redis:*DescribeParameterGroups*",```<br>```                   "Redis:*DescribeParameterGroupDetail*",```<br>```                   "Redis:*DescribeApplyParameterGroup*",```<br>```                   "Redis:*DescribeSupportParameters*",```<br>```                   "Redis:*CreateParameterGroup*",```<br>```                   "Redis:*ModifyParameterGroup*",```<br>```                   "Redis:*DeleteParameterGroup*"```<br>```               ],```<br>```               "Resource": [```<br>```                   "*"```<br>```               ]```<br>```           }```<br>```       ]```<br>```   }```<br>```   ```<br>    |
|Events |* DescribePlannedEvents<br><br>* ModifyPlannedEventExecuteTime |Global |* If you only need to grant read\-only access to the event center for IAM users, then you can simply allow the IAM user to have the DescribePlannedEvents action permission.<br><br>   The syntax example is as follows.<br><br>   ```JSON```<br>```   {```<br>```       "Statement": [```<br>```           {```<br>```               "Effect": "Allow",```<br>```               "Action": [```<br>```                   "Redis:*DescribePlannedEvents*"```<br>```               ],```<br>```               "Resource": [```<br>```                   "*"```<br>```               ]```<br>```           }```<br>```       ]```<br>```   }```<br>```   ```<br>   <br><br>* If you want to grant full administrative privileges of the event center to IAM users, then you need to allow the IAM user to have full operational privileges of the event center.<br><br>   The syntax example is as follows.<br><br>   ```JSON```<br>```   {```<br>```       "Statement": [```<br>```           {```<br>```               "Effect": "Allow",```<br>```               "Action": [```<br>```                   "Redis:*DescribePlannedEvents*",```<br>```                   "Redis:*ModifyPlannedEventExecuteTime*"```<br>```               ],```<br>```               "Resource": [```<br>```                   "*"```<br>```               ]```<br>```           }```<br>```       ]```<br>```   }```<br>```   ```<br>    |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Create IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log in to the <a href="https://console.byteplus.com/iam/identitymanage/user">IAM console</a> with root account or a user with administrator permissions to create IAM users.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating IAM users, you can directly add system pre\-defined policies for Redis and other associated services and specify the policy scope.   </div>
   

2. [Add permissions to IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the scope of the <code>RedisFullAccess</code> or <code>RedisReadOnlyAccess</code> policy granted to the IAM user is <strong>project permissions</strong>, to ensure the IAM user can use the corresponding Redis features, you must also <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy">create custom policy</a> for the IAM user and set the scope of these policies to <strong>global permissions</strong>. For details on related features and corresponding custom syntax examples, refer to <a href="https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers#.5rOo5oSP5LqL6aG5">Precautions</a>.   </div>
   

3. Log in to the [Redis console](https://console.byteplus.com/db/redis) with the IAM user and use Redis services.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure the security of cloud resources and reduce the risk of root account AK/SK leakage, we recommend creating separate AK/SK for IAM users to call Redis\-related API interfaces. For details on creating AK/SK, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey">Managing access key</a>.   </div>
   

&nbsp;
