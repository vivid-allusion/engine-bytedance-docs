---
title: "SMC IAM policy types"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/SMC-IAM-policy-types"
---

This topic describes the types of Identity and Access Management (IAM) policies and those related to Server Migration Center (SMC) for you to learn IAM policies quickly. Two IAM policy types are supported: the system default policy and the custom policy. You can use system default policies to grant IAM identities directly. If the system default policies can not meet your needs, you can use custom policies to grant permissions precisely and manage resources flexibly.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policies

<span id=".U01D57O757uf6aKE6K6-562W55Wl"></span>
### SMC system default policies

The IAM platform provides default SMC\-related policies in advance, with details in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can directly assign these system default policies to IAM entities (IAM users, user groups, or roles). <strong>System default policies are for authorization only and can not be edited or modified</strong>.</div>



|System default policy name |Description |
|---|---|
|SMCFullAccess |After this policy is assigned, the IAM identity (user, user group, or role) obtains full management permissions for Server Migration Center (SMC), including importing migration sources and creating migration tasks. |
|SMCBatchMigrationAccess |After this policy is assigned, the IAM identity (user, user group, or role) obtains the batch migration permissions in Server Migration Center (SMC) and can use the feature of [one-click import of migration source in the console](https://docs.byteplus.com/en/docs/smc/One-click_import_from_the_console). |
|SMCReadOnlyAccess |After this policy is assigned, the IAM identity (user, user group, or role) obtains read\-only access to Server Migration Center (SMC). This access is restricted to viewing information only, such as migration sources and migration tasks. |


<span id=".U01D5o6n5Yi25Y-w5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
### Roles or policies required by SMC console features


|Console feature |Required cloud service |Required role/policy |
|---|---|---|
|Import migration sources/Create migration tasks |ECS |Permissions associated with SMCFullAccess, ECSFullAccess, VPCFullAccess, and EIPFullAccess need to be granted to IAM users. |
||Image ||
||Virtual Private Cloud ||
||EIP ||
||Volume ||
||Snapshot ||
||Security group ||
|View migration sources/migration tasks |\- |Permissions associated with SMCFullAccess or SMCReadOnlyAccess need to be granted to IAM users. |


<span id=".U01D5Lqn5ZOB57O757uf6aKE6K6-562W55Wl6K-m5oOF"></span>
### Details of the SMC\-related system default policies

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For other system default policies, navigate to Policy Management console for more information.</div>


<span id=".U01DRnVsbEFjY2VzcyDnrZbnlaXor6bmg4U="></span>
#### SMCFullAccess policy details

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "smc:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="SMCReadOnlyAccess"></span>
#### SMCReadOnlyAccess policy details

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "smc:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policies


|Type |Description |
|---|---|
|Custom policy type |Custom policies are divided into identity\-based policies and resource\-based policies, depending on the entity to which they are associated. |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |
|Create a custom policy |When authorizing as the root user or an IAM user with IAM management permissions, if the system default policies do not meet your requirements, you can configure fine\-grained permissions through a custom policy. |


<span id=".55u45YWz5paH5qGj"></span>
## Related document

Common system default policies: This topic describes some of the commonly used system default policies to help you quickly understand and use system policies for permission management and control.

&nbsp;
