---
title: "rights management"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/rights_management"
---

The rights management on BytePlus is mainly realized through Identity and Access Management IAM (see [Common concepts](https://docs.byteplus.com/docs/mlp/76491)). The main account (or users with related rights) usually creates sub accounts (sub\-users) for different members according to the responsibilities and work content of the team members, and realizes fine grain Identity and Access Management by giving the corresponding rights policies to the sub accounts. For security reasons, when assigning policies to sub accounts, follow the principle of least privilege. This article introduces how to manage rights on Machine Learning Platform from three aspects: users, user groups and policies.

<span id="用户"></span>
# user

BytePlus provides a [User] module to manage all sub\-users under this account. Under this module, you can create, delete, and configure permissions for sub\-users.

<span id="创建子用户"></span>
## Create child user

**premise of use**

Log in as the main account or as a user with Identity and Access Management privileges.

**Procedure**


1. Login to the [Identity and Access Management console user page ](https://console.byteplus.com/iam/identitymanage/user).

2. Click [User] \- [New User] in the left navigation bar to enter the basic information settings page. The key parameters are as follows:



|Parameter |Parameter Description |
|---|---|
|user name |Fill in the name of the child user. Required. |
|console login |Configure a sub account and password for the new user, giving the user access to the platform through the console (web page). **Optional** .<br><br><br>* **Users who need to access the platform through a web page need to enable this permission.**  |
|Automatic key generation |Generate AK/SK for users. **Optional** .<br><br><br>* AK/SK as an important user identity certificate, **strongly recommended to open.**  **Daily use of OpenAPI/SDK/command line tools requires AK/SK authentication.**  **After obtaining the AK/SK, please keep it safe and do not disclose it.**  |



3. After completing the above configuration, click [Next step] to enter the permission setting page. Give users different permissions by checking different **policies**

4. After checking, submit the form to complete the creation of the sub\-user, and then you can manage the user in the [Users] list/details page.


<span id="修改用户的权限"></span>
## Modify user permissions

**premise of use**


1. Log in as the main account or as a user with Identity and Access Management privileges.

2. There is \> = 1 user in [User].


**Procedure**


1. Log in to the BytePlus console and click [Identity and Access Management] under the user name in the upper right corner of the top to enter the corresponding page.

2. In the left navigation bar, click [Users] to enter the user list, and click the name of the user to be modified to enter the user details page. Under this page, you can complete operations such as changing the policy or role associated with the user, adding/deleting keys, and resetting passwords.


<span id="管理当前用户的密钥（ak-sk）"></span>
## Manage the current user's keys (AK/SK)

**premise of use**


1. Log in with the main account or a user with [Key Management] privileges.


**Procedure**


1. Log in to the BytePlus console, click [Key Management] under the user name in the upper right corner of the top to enter the corresponding page, and perform operations such as new, view, copy, disable, and delete the key as needed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ae6eb148e1349c39bef2df26bf9f94b~tplv-goo7wpa0wc-image.image) </span>

<span id="管理子用户的密钥（ak-sk）"></span>
## Manage keys for sub\-users (AK/SK)

**premise of use**


1. Log in as the main account or as a user with Identity and Access Management privileges.


**Procedure**


1. Log in to the BytePlus console and click [Identity and Access Management] under the user name in the upper right corner of the top to enter the corresponding page.

2. Click [User] to enter the corresponding page, click a user's name to enter the user details page and click [Key].

3. Under this page, create, view, copy, disable, delete, and other operations for the key as needed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea9ad704700e4c0faa93d46a1b99b376~tplv-goo7wpa0wc-image.image) </span>

<span id="用户组"></span>
# User group

A user group is a collection of users (sub accounts), and by associating several permission policies on the user group, members of the user group can enjoy these permissions. If a user joins multiple user groups at the same time, the user's permissions will be a combination of the permissions of multiple user groups.

Usually, if the main account contains multiple sub accounts and needs to divide permissions in the form of groups, you can consider using the [User Group] function, which can realize batch authorization of multiple sub accounts and avoid duplicate authorization for each sub account.

<span id="创建用户组及授权"></span>
## Create User Groups and Authorizations

**premise of use**


1. Log in as the main account or as a user with Identity and Access Management privileges.


**Procedure**


1. Create a new user group: Log in to the BytePlus console and click [Identity and Access Management] under the user name in the upper right corner of the top to enter the corresponding page. Click [User Group] to enter the user group list page, click [New User Group], and fill in the user group name in the pop\-up page to Create a user group.

2. Add User: Click [User Group] to enter the corresponding page and click the name of the user group you want to join to enter the user group details page. Click [Add User] and tick the corresponding user in the pop\-up page to join the user group.

3. Associated permissions for user groups: Click [Permissions] \- [Global Permissions] \- [Add Permissions] on the user group details page, and check the corresponding policy in the policy list to quickly grant corresponding permissions to all users in the user group.

4. User group permissions and users support dynamic Add, when insufficient permissions or new users can re\-enter the user group details page Add permissions or users.


<span id="移除用户"></span>
## Remove user

A user group can not only add new users, but also remove existing users from the user group, and the removed user will lose all the permissions assigned to that user group.

**premise of use**


1. Log in as the main account or as a user with Identity and Access Management privileges.


**Procedure**


1. On the Identity and Access Management page, click User Group to enter the corresponding page and then click the name of the user group to enter the user group details page.

2. The user group details page will display all users in the user group. Click [Remove] after the user name you want to remove to remove the user from the user group. At this time, the corresponding permissions of the user will be Withdrawn.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a2622f79d4c4a2ea0b86fb722755009~tplv-goo7wpa0wc-image.image) </span>

<span id="系统预设策略"></span>
# System default policy

BytePlus provides [Policy Management] module for managing **system preset policies** and **user\-defined policies** . The preset strategy can satisfy most of the user's application scenarios.


|policy name |strategy statement |
|---|---|
|MLPlatformAdminAccess |* Full read and write strategy. All resources under the main account can be read and written when this policy is granted.<br><br>* This policy is the highest authority for the Machine Learning Platform and is recommended for platform administrators. |
|MLPlatformMemberAccess |* Developer strategy. Gives this policy the ability to read and write to all resources in the main account, but cannot Create a resource group.<br><br>* This policy applies to regular developers who are not administrators of the Machine Learning Platform. |
|MLPlatformDeveloperAccess |Developer rights for the new Machine Learning Platform. |
|MLPlatformReadonlyAccess |Read\-only strategy. Users given this policy can only view resources under the main account. |
|AccessKeyFullAccess |* Allows users to manage their own AK/SK policies.<br><br>* Users who are given this policy can Create/View/Disable/Delete their own AK/SKs, which is usually required for users operating off the console. |
|BillingCenterFullAccess (formerly BillFullAccess) |* Policies that allow users to manage financial\-related content within their accounts, such as bills, orders, etc.<br><br>* This strategy is often used in combination with MLPlatformAdminAccess, as transaction\-related permissions are required when **creating resource groups** . |
|TOSFullAccess |* BytePlus Torch Object Storage (TOS) full read and write strategy.<br><br>* This strategy is usually required when users directly use TOS to manage buckets, upload, download, and read and write data. |
|CFSFullAccess |* BytePlus Cloud File System (CloudFS) full read\-write policy.<br><br>* This policy is usually required when users need to mount the TOS shared file system and use cache acceleration capabilities. |
|CRFullAccess |* BytePlus Container Registry (CR) full read\-write policy.<br><br>* This strategy is usually required when users use CR directly, such as transferring offline historical mirrors to BytePlus. |
|IAMFullAccess |* BytePlus mirrors Identity and Access Management (IAM) full read\-write policies.<br><br>* This policy is usually required when a user is an administrator, managing other child users, and configuring permissions.<br><br>* **When the main account and the developers are not on the same team, it is recommended to configure this policy for one of the developers to facilitate rights management within subsequent development teams.**  |
|vePFSFullAccess |* BytePlus File Storage (PFS) full read\-write policy.<br><br>* This policy is typically required when a user mounts a PFS shared file system into a container for Dev boxes, custom tasks, or inference services. |


<span id="817d4a31"></span>
# custom policy

When there are special permission requirements that cannot be met by some preset policies, users can write custom policies to meet their own customization needs.

During the writing process, users need to understand the Actions and Resources of the Machine Learning Platform. This part of the content is more complex. You can consult the relevant customer service staff through [ticket ](https://console.byteplus.com/workorder/create)when you actually need it.

<span id="7866772c"></span>
# Common configuration method v1

You are a user of Machine Learning Platform v1, and you can complete the division of the two common roles of developer and administrator on Machine Learning Platform by combining preset policies.

<span id="b289f710"></span>
## Resource Manager

Sub\-users need to have Machine Learning Platform ownership time (especially **purchasing resource groups, global configuration** ), and need to be assigned platform administrator privileges:


* MLPlatformAdminAccess (cannot stack with MLPlatformMemberAccess): Permission to perform all Machine Learning Platform operations, including resource purchase, queue allocation, global configuration.

* AccessKeyFullAccess

* BillFullAccess

* TOSFullAccess: As an administrator, you need to add this policy to manage data directly using the console interface of Torch Object Storage (TOS).

* CFSFullAccess: If ordinary developers need to mount the TOS shared file system into the container, as an administrator, it is **strongly recommended** to add this policy to facilitate the direct use of the Cloud File System (CloudFS) console interface to manage CloudFS instances.

* vePFSFullAccess: If regular developers need to mount the PFS shared file system into a container, as an administrator, they need to add this policy to make it easier to directly use the console interface of PFS to manage the corresponding instance.

* CRFullAccess: Adding this policy as an administrator makes it easier to transfer historical mirrors to BytePlus directly using the BytePlus Container Registry (CR).

* VPCFullAccess: Add this policy as an administrator to facilitate network\-related global configuration.

* IAMFullAccess: As an administrator, it is **strongly recommended** to add this policy to facilitate direct operation of Identity and Access Management (IAM) Create new sub accounts and do permission management on sub accounts. **Especially in the case that the main account does not belong to the algorithm team, it is recommended to configure an administrator in the algorithm team and attach the IAM policy, so that when adding engineers, they can create sub\-users and Add appropriate permissions in time.** 


<span id="开发者"></span>
## algorithm developer

The most common sub\-users of a Machine Learning Platform are developers, such as algorithm engineers, data engineers, and others. This type of sub\-user needs to complete data processing, code development, model training, model deployment, and other important aspects on the platform, so they need most of the read and write permissions. In addition to this, there are also a considerable number of developers who need to manage their own API keys (AK/SK), otherwise they will not be able to complete authentication when accessing the Machine Learning Platform using OpenAPI, command line, and SDK. However, there are also certain differences among developers. The preset strategies required by different developers are as follows.


* Developers: Subusers who only perform machine learning tasks and cannot purchase resource groups and do not need to care about resource management.

   * MLPlatformMemberAccess

   * AccessKeyFullAccess

   * TOSFullAccess: This policy can be associated if you need to create a bucket and transfer data through the console page of BytePlus Torch Object Storage (TOS).

   * CRFullAccess: This policy can be associated if you need to pull or push mirrors through the BytePlus Container Registry (CR).

   * [Optional] CFSFullAccess: This policy can be associated if you need to mount the TOS shared file system into a container for use.

   * [Optional] vePFSFullAccess: You can associate this policy if you need to mount a PFS shared file system into a container for use.


<span id="默认的-tos-权限"></span>
## Default TOS permissions

The Machine Learning Platform will automatically create a TOS bucket for each main account (the name is prefixed with `ml-platform-auto-created-required`) to store the code and models uploaded locally by the user. Sub account needs to have the relevant permissions of this bucket when uploading files, so the platform adds the read and write permissions of this bucket by default in the preset policy MLPlatformAdminAccess and MLPlatformMemberAccess.


* When not using the preset policy, please contact the administrator (main account or sub account with IAM configuration permissions) to add the following to the custom policy and assign it to the corresponding sub account to avoid the sub account being unable to upload code and models locally due to lack of permissions.


```Plain
{
    "Action": [
        "tos:List*",     # 用于列举桶内文件
        "tos:Get*",      # 用于下载文件、获取桶相关信息等操作
        "tos:Put*",      # 上传文件
        "tos:Head*"      # 用于判断桶是否存在，获取桶元数据
    ],
    "Effect": "Allow",
    "Resource": [
        # 将上述权限的作用范围限制在平台自动创建的桶中
        "trn:tos:::ml-platform-auto-created-required-*",    
        "trn:tos:::ml-platform-auto-created-required-*/*"
    ]
}
```


<span id="068a3a9a"></span>
# Common configuration method v2

You are a Machine Learning Platform v2 user, please refer to the following for permission configuration.

<span id="4649fec2"></span>
## Resource Manager

When a child user acts as a resource administrator and needs to operate and maintain resources on the Machine Learning Platform (veMLP), the required permissions mainly involve:


* Global configuration: Configure companion cloud infrastructure resources on veMLP, such as Private network VPC, Mirror repository CR, File storage PFS or CloudFS, Torch Log Service TLS, and monitoring VMP.

* Resource group: Resource Create and lifecycle management module on veMLP, which needs to pay the resource purchase fee and configure the cloud network, storage and other resources associated with the resource.

* Queues: The resource management module on veMLP, through which resource quotas can be allocated to each group and individual users, and it is also the permission management of the veMLP platform. Create additional load jobs when only the usage permissions of the queue are available. The queue administrator can directly manage the lifecycle of all payloads within the queue.

* Load: Administrative privileges for Dev boxes, custom tasks, and inference services.


Therefore, the resource administrator subuser on veMLP, for the sake of continuity of use recommendations, is granted the following permissions:


* MLPlatformAdminAccess: Machine Learning Platform (veMLP) administrator privileges.

* IAMFullAccess: Identity and Access Management (IAM) administrator privileges.

* CRFullAccess: Container Registry (CR) administrator privileges.

* TOSFullAccess: Torch Object Storage (TOS) administrator privileges.

* TLSFullAccess: Torch Log Service (TLS) administrator privileges.

* VMPFullAccess: Managed Prometheus Services (VMP) administrator privileges.

* CFSFullAccess: Cloud File System (CLoudFS) administrator privileges. (If using CLoudFS products)

* vePFSFullAccess: File Storage (PFS) administrator privileges. (If using PFS products)


<span id="86b49f90"></span>
## algorithm developer

When child users only need to develop, train, and inference models on the Machine Learning Platform (veMLP), they can only need to authorize developers. The following permissions are primarily concerned with:


* Queue: Permissions to use resources within the queue.

* Load: Create and operationalize permissions for Dev boxes, custom tasks, and inference services.


Therefore, the resource administrator subuser on veMLP is recommended to grant the following permissions for continuity of use:


* MLPlatformDeveloperAccess: Machine Learning Platform (veMLP) algorithm developer rights. The child users granted to this policy will have read and write permissions for Dev boxes, custom tasks, inference services, and deployments (only those created by themselves); they will also grant interface permissions such as Get and List for mirror, experiment management, and other modules.


<span id="3beb9de2"></span>
## queue rights management

Queues are the resource quota management module of the Machine Learning Platform. If a child user needs to use resources to Create various loads, they need to join the queue first (either administrator or member). The following explains the role definition of the queue:


* Queue administrator: the manager of queue resources, which can manage queue members, idle resource lending, and the load statement cycle of members in the queue.

* Queue members: You can create payloads using resources within the queue.


<span id="2a2e7765"></span>
### Create Queues & Configure User Permissions


* Prerequisites

   * Requires MLPlatformAdminAccess permission

   * Need to have IAMFullAccess permission (if the permission is relatively large, you can refer to [自定义策略](https://docs.byteplus.com/docs/mlp/54011#817d4a31))

   * There is a running resource group



|step |operation introduction |
|---|---|
|Step1 |**Basic information about the completion queue**<br><br><br>* queue name<br><br>* load type<br><br>* Lending of idle resources (preemption of idle resources under the same resource group)<br><br>* Queue quota<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56852b8cd9214957ab07e6a47689fc8e~tplv-goo7wpa0wc-image.image) </span> |
|Step2 |**Assign queue permissions**<br><br><br>* When creating a resource group for the first time, you need to specify both administrators and members; support for selecting users or user groups.<br><br>   * If a user is selected, the platform will automatically Create a user group and add the selected user to the user group.<br><br>      * Administrator group name: q\-xxx\-admin\-group.<br><br>      * Member user group name: q\-xxx\-developer\-group.<br><br>* When authorizing the selected user/user group, the platform performs the following actions in turn:<br><br>   * Create the user group (when the user is selected, do this action).<br><br>   * Create custom policies.<br><br>   * Authorize custom policies to user groups.<br><br>   * Create and authorize.<br><br>* Custom policies for queues<br><br>   * When creating a queue, the platform automatically Creates an IAM Custom Policy and completes the policy authorization for the selected user group.<br><br>   * Administrator custom policy name: q\-xxx\-admin\-policy.<br><br>   * Member custom policy naming: q\-xxx\-developer\-policy.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b17f515f64c4be79dd3cbf9f25819d9~tplv-goo7wpa0wc-image.image) </span> |
|Step3 |**Manage user usage caps**<br><br><br>* On the queue details page, you can edit the user's usage limit, which supports both percentages and absolute values.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/645f04296e424495812eb4464037574e~tplv-goo7wpa0wc-image.image) </span> |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please note that the resource administrator needs to actively add IAM related policies to the members of the queue administrator, otherwise the queue administrator will not be able to edit the members of the queue normally.</div>


<span id="c93dffa6"></span>
### Manage user permissions

After the queue is created, if you need to manage the list of administrators and members in the queue, you can do it by editing [Manage Users].

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Adding users or policies directly to Identity and Access Management is not currently supported. If you need to maintain queue members, please continue to operate on the veMLP console.</div>



* operating premise

   * The operator is the administrator of the queue

   * The operator should have `IAMFullAccess`permission (if this permission is wide, you can configure a custom policy)



|step |operation introduction |
|---|---|
|Step1 |* Click [Manage Users] to enter the permission editing page.<br><br>* Select the users/user groups to add or remove<br><br>* Save the page when done.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b17f515f64c4be79dd3cbf9f25819d9~tplv-goo7wpa0wc-image.image) </span> |


<span id="ed6e157a"></span>
## Introduction to queue administrators and member permissions

<span id="524e8ce5"></span>
### administrator policy

Authority description:


1. The queue administrator has read and write permissions to any payload under the queue.

2. The queue administrator has read and write access to the queue.

3. When you authorize a queue administrator, the new administrator will be granted partial IAM privileges to manage the queue.


```JSON
{
    "Statement": [
      {
        "Effect": "Allow",
        "Action": [
          "ml_platform:*DevInstance*",
          "ml_platform:*Job*",
          "ml_platform:*Service*",
          "ml_platform:*Deployment*",
          "ml_platform:*CustomTask*"
        ],
        "Resource": [
          "trn:ml_platform:cn-beijing:2100xxx:devinstance/*",
          "trn:ml_platform:cn-beijing:2100xxx:job/*",
          "trn:ml_platform:cn-beijing:2100xxx:service/*",
          "trn:ml_platform:cn-beijing:2100xxx:deployment/*"
        ],
        "Condition": {
          "StringEquals": {
            "volc:ResourceTag/sys:ml_platform:resource_queue_id": "q-202504xxx7-txxxx"
          }
        }
      },
      {
        "Effect": "Allow",
        "Action": [
          "ml_platform:*DevInstance*",
          "ml_platform:*Job*",
          "ml_platform:*Service*",
          "ml_platform:*Deployment*",
          "ml_platform:*CustomTask*",
          "ml_platform:*ResourceQueue*"
        ],
        "Resource": [
          "trn:ml_platform:cn-beijing:2100xxx:resourcequeue/q-202504xxx7-txxxx"
        ]
      },
      {
        "Effect": "Allow",
        "Action": [
          "iam:AddUserToGroup",
          "iam:RemoveUserFromGroup",
          "iam:ListUsersForGroup",
          "iam:ListGroups",
          "iam:ListUsers",
          "iam:GetGroup",
          "iam:GetPolicy",
          "iam:AttachUserGroupPolicy",
          "iam:DetachUserGroupPolicy",
          "iam:ListEntitiesForPolicy"
        ],
        "Resource": [
          "*"
        ]
      }
    ]
  }
```


<span id="47b62189"></span>
### member strategy

Queue member, can use this queue to create any load (the queue needs to support this load option), and has read and write permissions for the corresponding load Creator.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ml_platform:*DevInstance*",
        "ml_platform:*Job*",
        "ml_platform:*Service*",
        "ml_platform:*Deployment*",
        "ml_platform:*CustomTask*"
      ],
      "Resource": [
        "trn:ml_platform:cn-beijing:2100xxx:resourcequeue/q-202504xxx7-txxxx"
      ]
    }
  ]
}
```


<span id="d9694f52"></span>
## custom policy

<span id="f9aa8da6"></span>
### Queue Creator IAM Policy

If `IAMFullAccess`privileges are too large, consider Create a new custom policy and complete authorization.


* Go to [Identity and Access Management] \- [Policy], click [New Custom Policy], and complete the following policy configuration.

* Authorize the policy to the queue administrator.


```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetGroup",
                "iam:AddUserToGroup",
                "iam:CreateGroup",
                "iam:AttachUserGroupPolicy",
                "iam:CreatePolicy",
                "iam:DetachUserGroupPolicy",
                "iam:GetPolicy",
                "iam:RemoveUserFromGroup",
                "iam:GetUser",
                "iam:ListUsers",
                "iam:ListGroups",
                "iam:ListUsersForGroup",
                "iam:ListGroupsForUser",
                "iam:ListAttachedUserGroupPolicies",
                "iam:ListAttachedUserPolicies"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="b02a8616"></span>
### Change Resource Owner Strategy

If you only want to grant permissions to a user for a specific resource after the resource is created, you can do so through a custom policy. (You can also optionally set the target user as a queue administrator with read and write permissions for all payloads in the queue.)


* Go to [Identity and Access Management] \- [Policies] and click [New Custom Policy].

* Modify resource action, account id, resource name, and resource id.

* Authorize policies to specific child users.



|resource name |action |
|---|---|
|resourcegroup |*ResourceGroup* |
|service |*Service* |
|deployment |*Deployment* |
|devinstance |*DevInstance* |
|job |v2: *Job*<br><br>v1: *CustomTask* |
|resourcequeue |*ResourceQueue* |


```JSON
{
      "Effect": "Allow", 
      "Action": [
        "ml_platform:*DevInstance*" //action
      ],
      "Resource": [
         //yellow {region}: {accountId}: {resource name}: {resource id}
        "trn:ml_platform:cn-beijing:2100xxx:devinstance/di-202503xxxx2-gtxxxj"
      ]
}
```
