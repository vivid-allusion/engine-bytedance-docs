---
title: "Create appropriate sub accounts"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Create_appropriate_sub_accounts"
---

When using the v2 API or when queue permissions are managed via IAM on the console, you can refer to the following to grant appropriate permissions to the account for security and reasonable permission levels.

&nbsp;

<span id="2c314fd8"></span>
## Resource Manager

When a child user acts as a resource administrator and needs to operate and maintain resources on the Machine Learning Platform (MLP), the required permissions mainly involve:


* Global configuration: Configure companion cloud infrastructure resources on MLP, such as Private network VPC, Mirror repository CR, File storage PFS or CloudFS, Logging Services TLS, and Monitoring VMP.

* Resource group: Resource Create and lifecycle management module on MLP, which needs to pay the resource purchase fee and configure the cloud network, storage and other resources associated with the resource.

* Queues: The resource management module on MLP, through which resource quotas can be allocated to each group and individual users, and it is also the permission management of the MLP platform. Create additional load jobs when only the usage permissions of the queue are available. The queue administrator can directly manage the lifecycle of all payloads within the queue.

* Load: Administrative privileges for Dev boxes, custom tasks, and inference services.


Therefore, the resource administrator subuser on MLP, for the sake of continuity of use recommendations, is granted the following permissions:


* MLPlatformAdminAccess: Machine Learning Platform (MLP) administrator privileges.

* IAMFullAccess: Identity and Access Management (IAM) administrator privileges.

* CRFullAccess: Container Registry (CR) administrator privileges.

* TOSFullAccess: Torch Object Storage (TOS) administrator privileges.

* TLS FullAccess: Torch Log Service (TLS) administrator privileges.

* VMPFullAccess: Vital Managed Service for Prometheus (VMP) administrator privileges.

* CFSFullAccess: Cloud File System (CLoudFS) administrator privileges. (If using CLoudFS products)

* vePFSFullAccess: File Storage (PFS) administrator privileges. (If using PFS products)


<span id="b97e644f"></span>
### MLPlatformAdminAccess default strategy

```JSON
{
  "Statement": [
    {
      "Action": [
        "tos:HeadBucket",
        "tos:PutObject",
        "tos:GetObject",
        "tos:ListBucketMultipartUploads",
        "tos:ListMultipartUploadParts",
        "tos:ListBucket",
        "tos:ListBuckets",
        "tos:CreateBucket",
        "cfs:DescribeSfcsCachePolicies",
        "vepfs:List*",
        "vepfs:Describe*",
        "vepfs:Get*",
        "vpc:Describe*",
        "FileNAS:Get*",
        "FileNAS:List*",
        "ml_platform:*",
        "ml_maas:GetMaasRuntimeConfig"
      ],
      "Effect": "Allow",
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="4a869a2f"></span>
## Algorithm developer

When child users only need to develop, train, and inference models on the Machine Learning Platform (MLP), they can complete only developer privileges. The following permissions are primarily concerned with:


* Queue: Permissions to use resources within the queue.

* Load: Create and operationalize permissions for Dev boxes, custom tasks, and inference services.


Therefore, the resource administrator subuser on MLP is recommended to grant the following permissions for continuity of use:


* MLPlatformDeveloperAccess: Machine Learning Platform (MLP) algorithm developer rights.


<span id="889bb304"></span>
### MLPlatformDeveloperAccess default strategy

The developers of MLP present the policy, and grant the child users of the policy to have read and write permissions for Dev boxes, custom tasks, inference services, and deployments (only those created by themselves); they will also grant interface permissions such as Get and List for mirrors, experiment management, and other modules.

```Bash
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ml_platform:SignJwtToken",
        "ml_platform:JoinResourceQueue",
        "ml_platform:Get*",
        "ml_platform:List*",
        "ml_platform:Check*",
        "ml_platform:Describe*",
        "ml_platform:*Pipeline*",
        "ml_platform:*Asset*",
        "ml_platform:*Dataset*",
        "ml_platform:*Model*",
        "ml_platform:*AutoScaler*",
        "ml_platform:*Annotation*",
        "ml_platform:*TensorBoard*",
        "ml_platform:*Profile*",
        "ml_platform:*Tracking*",
        "ml_platform:*Image*",
        "ml_platform:*Rule*",
        "ml_platform:*Suspected*",
        "ml_platform:*Idle*"
      ],
      "Resource": [
        "*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "ml_platform:*DevInstance*",
        "ml_platform:*Job*",
        "ml_platform:*Customtask*",
        "ml_platform:*Service*",
        "ml_platform:*Deployment*",
        "ml_platform:*ResourceQueue*",
        "ml_platform:*ResourceGroup*"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringEquals": {
          "volc:PrincipalTrn": "${volc:ResourceTag/sys:ml_platform:createdby}"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": [
        "FileNAS:Get*",
        "FileNAS:List*",
        "FileNAS:Describe*",
        "cfs:DescribeSfcsCachePolicies",
        "vpc:Describe*",
        "vepfs:List*",
        "vepfs:Describe*",
        "vepfs:Get*",
        "cr:List*",
        "cr:Get*",
        "apig:Get*",
        "apig:List*",
        "quota:Get*",
        "vmp:List*",
        "vmp:Get*",
        "tos:GetObject",
        "tos:HeadBucket",
        "tos:AbortMultipartUpload",
        "tos:PutObject",
        "tos:ListBucketMultipartUploads",
        "tos:PutBucketCORS",
        "tos:ListMultipartUploadParts",
        "tos:ListBuckets",
        "tos:CreateBucket"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="be7e42b2"></span>
## Queue rights management

Queues are the resource quota management module of the Machine Learning Platform. If a child user needs to use resources to Create various loads, they need to join the queue first (either administrator or member). The following explains the role definition of the queue:


* Queue administrator: the manager of queue resources, which can manage queue members, idle resource lending, and the load statement cycle of members in the queue.

* Queue members: You can create payloads using resources within the queue.


<span id="acfca2c4"></span>
### Create Queues & Configure User Permissions


* Prerequisites

   * Requires MLPlatformAdminAccess permission

   * IAMFullAccess permission is required (if the permission is relatively large, you can configure a custom policy, refer to [Create appropriate sub accounts](https://docs.byteplus.com/docs/mlp/Create_appropriate_sub_accounts))

   * There is a running resource group



|step |operation introduction |
|---|---|
|Step1 |**Basic information about the completion queue**<br><br><br>* queue name<br><br>* load type<br><br>* Lending of idle resources (preemption of idle resources under the same resource group)<br><br>* Queue quota<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13850dda9fd040648ec5e0c1151f1a48~tplv-goo7wpa0wc-image.image) </span> |
|Step2 |**Assign queue permissions**<br><br><br>* When creating a resource group for the first time, you need to specify both administrators and members; support for selecting users or user groups.<br><br>   * When a user is selected, the platform will automatically Create a user group and add the selected user to the user group.<br><br>      * Administrator group name: q\-xxx\-admin\-group.<br><br>      * Member user group name: q\-xxx\-developer\-group.<br><br>* When authorizing the selected user/user group, the platform performs the following actions in turn:<br><br>   * Create the user group (when the user is selected, do this action).<br><br>   * Create custom policies.<br><br>   * Authorize custom policies to user groups.<br><br>   * Create and authorize.<br><br>* Custom policies for queues<br><br>   * When creating a queue, the platform automatically Creates an IAM Custom Policy and completes the policy authorization for the selected user group.<br><br>   * Administrator custom policy name: q\-xxx\-admin\-policy.<br><br>   * Member custom policy naming: q\-xxx\-developer\-policy<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88bda74e68934facb7049f481aec30cd~tplv-goo7wpa0wc-image.image) </span> |
|Step3 |**Manage user usage caps**<br><br><br>* On the queue details page, you can edit the user's usage limit, which supports both percentages and absolute values.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dddc1a10c6e43a9983203744890efb4~tplv-goo7wpa0wc-image.image) </span> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please note that the resource administrator needs to actively add IAM related policies to the members of the queue administrator, otherwise the queue administrator will not be able to edit the members of the queue normally.</div>


<span id="23733ff9"></span>
### Manage user permissions

Created after the queue, if you need to manage the list of administrators and members in the queue, you can edit [Manage Users] to achieve.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Adding users or policies directly to Identity and Access Management is not currently supported. If there is a queue member maintenance requirement, please continue to operate on the MLP console.</div>



* operating premise

   * The operator is the administrator of the queue

   * The operator should have `IAMFullAccess`permission (if the permission range is wide, you can configure custom policies, please refer to [MLP's permission management ](https://bytedance.larkoffice.com/docx/GRW2doEq2oYBJfxX7CIco9TonCf#share-VG3kdzfrEoSSk4xfE5Dcgp48nDe))



|step |operation introduction |
|---|---|
|Step1 |* Click [Manage Users] to enter the permission editing page.<br><br>* Select the users/user groups to add or remove<br><br>* Save the page when done.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2947483891a24a43b247725ce664017c~tplv-goo7wpa0wc-image.image) </span> |


<span id="f0dc68a3"></span>
## Introduction to queue administrators and member permissions

<span id="419a2a5d"></span>
### Administrator policy

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
          "trn:ml_platform:cn-hongkong:2100xxx:devinstance/*",
          "trn:ml_platform:cn-hongkong:2100xxx:job/*",
          "trn:ml_platform:cn-hongkong:2100xxx:service/*",
          "trn:ml_platform:cn-hongkong:2100xxx:deployment/*"
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
          "trn:ml_platform:cn-hongkong:2100xxx:resourcequeue/q-202504xxx7-txxxx"
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


<span id="b017b7ac"></span>
### Member strategy

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
        "trn:ml_platform:cn-hongkong:2100xxx:resourcequeue/q-202504xxx7-txxxx"
      ]
    }
  ]
}
```


<span id="396839d0"></span>
## Custom policy

<span id="7c4aabb2"></span>
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


<span id="0f186958"></span>
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
        "ml_platform:*DevInstance*" // Action
      ],
      "Resource": [
         // Yellow highlighted section {region}: {account ID}: {resource name}: {resource ID}
        "trn:ml_platform:cn-hongkong:2100xxx:devinstance/di-202503xxxx2-gtxxxj"
      ]
}
```
