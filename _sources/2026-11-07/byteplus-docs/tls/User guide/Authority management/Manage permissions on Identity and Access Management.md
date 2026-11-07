---
title: "Manage permissions on Identity and Access Management"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Managing_permissions_on_Identity_and_Access_Management"
---

Torch Log Service (TLS) is associated with IAM and allows you to use IAM to manage permissions on TLS resources and actions. This topic introduces IAM identity types, permission policies, service roles, and other information.

<span id="531501a6"></span>
## Introduction

The BytePlus account is the owner of BytePlus resources and has administrative permissions for all cloud resources under the account. To ensure account security, BytePlus provides Identity and Access Management (IAM) to control access to cloud resources by different user identities. You can create IAM users, IAM user groups, and IAM roles through the master account and add permissions to use TLS resources.

<span id=".6LSm5Y-357G75Z6L"></span>
## Account types

IAM consists of three identities: IAM user, IAM user group, and IAM role.


* An IAM user is an entity identity type created by the BytePlus account or an IAM user with administrator privileges. New IAM users do not have any permissions and need to be authorized to access and operate cloud resources.

* IAM user groups are used to classify IAM users with the same responsibilities, thus improving the management efficiency of IAM users and their permissions.

* The IAM role is a virtual user that does not have permanent identity credentials. It can only obtain temporary identity credentials (STS Tokens) that can customize the timeliness and access rights through STS (Security Token Service). The IAM role needs to be played by a trusted entity. After successful playing, the trusted entity will obtain the STS Token of the IAM role and access cloud resources.


<span id="fd0369cc"></span>
## Permission policy

The permission policy is a set of permissions described by the syntax structureIn a policy. You can specify actions, resources, and effects based on the principle of least privilege. It is used to meet the security control requirements of enterprises for minimizing permissions.

<span id="0b94dfba"></span>
### Policy Syntax

The policy authorization statement related to TLS contains effect, action, resource, and condition elements.

```SQL
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [],
      "Resource": [
        "*"
      ],
      "Condition": {
          "DateGreaterThanEquals": {
              "volc:CurrentTime":"2024-08-30T23:59:59Z"
          }
      }    
    }
  ]
}
```


<span id="c27d941a"></span>
### Policy classification

The permission policy of IAM is divided into system default policy and custom policy.

<span id="d1d093ba"></span>
#### System default policy

System default policies are created and maintained by BytePlus. You can only use them and cannot modify them.

TLS supports the following two system policies.


* TLSFullAccess: If you attach this policy to an IAM user, the IAM user is granted full permissions on TLS. The IAM user is allowed to use all features of TLS and perform all types of operations on your TLS resources. For example, the IAM user can create topics, modify index settings, delete topics, query logs, upload logs and perform other operations.

* TLSReadOnlyAccess: If you attach this policy to an IAM user, you grant the read\-only permissions on your TLS resources to the IAM user. The IAM user is allowed to read data, but cannot create, modify, or delete TLS resources.


<span id="a5d18d76"></span>
#### Custom policy

When the preset permission policy of the system cannot meet the actual needs of the scene, you can create a custom policy to achieve fine and minimal control of permissions. For example, allow an IAM user to view the resources of a project, allow or prohibit the operation permissions of an interface. For more information, refer to [Permissions policy template](https://docs.byteplus.com/docs/tls/Permissions_policy_template).

When you create a custom policy, you can specify actions, resources, and effects based on the principle of least privilege. For more information on the TLS resource types and actions that can be authorized using custom policies, please refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions) and [Authorizable resources](https://docs.byteplus.com/docs/tls/Authorizable_resources).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A BytePlus account has the permissions to call all API actions. If you use the credentials of an IAM user to initiate an API request, the IAM user must be granted the permissions to call the API action. Otherwise, you fail to call the API action. The permissions required for initiating an API request are determined by the authorization items of the API action. An IAM user can successfully call an API action only when the IAM user is attached with a policy that includes the required authorization items.</div>


<span id="03c07e49"></span>
## Service role

The corresponding service role is an IAM role for the BytePlus service as a trusted entity, aimed at solving the authorization access problem across cloud services. TLS supports the following service roles.


|Service role |Description |
|---|---|
|ServiceRoleForTLS |The ServiceRoleForTLS role has a set of preset permission policies that allow the TLS to access the specified resources under your account. For detailed instructions, please refer to [Authorize cross-service access](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access). |
