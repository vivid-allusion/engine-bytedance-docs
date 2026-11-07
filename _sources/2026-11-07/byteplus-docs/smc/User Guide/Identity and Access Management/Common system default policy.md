---
title: "Common system default policy"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Common-system-default-policy"
---

This article introduces some commonly used system default policies to help you quickly understand and use system policies for permission control.

<span id="access-control-system-default-policy"></span>
## Access control system default policy

<span id="administratoraccess"></span>
### AdministratorAccess

IAM identities (IAM users, user groups, roles) that are authorized by this policy can obtain administrative privileges for products that support all IAM capabilities, such as ECSFullAccess, VPCFullAccess, IAMFullAccess, and so on.

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="readonlyaccess"></span>
### ReadOnlyAccess

After being authorized for this policy, IAM identities (IAM users, user groups, roles) can obtain read\-only access to all IAM\-enabled products, such as ECSReadOnlyAccess, VPCReadOnlyAccess, IAMReadOnlyAccess, and so on.

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "*:*Describe*",
                "*:List*",
                "*:Get*",
                "*:Query*",
                "*:Check*",
                "*:Read*",
                "*:Desc*",
                "*:Search*",
                "tos:Head*",
                "rms:*Get*",
                "rtc:Find*",
                "cloud_trail:Lookup*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="iamreadonlyaccess"></span>
### IAMReadOnlyAccess

The IAM identity (IAM user, user group, role) authorized by this policy can obtain read\-only access to Access control (IAM), and can enter the Access control console to view Access control related information, excluding the view permission of the Secret Access Key.

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:Get*",
                "iam:ListUser*",
                "iam:ListRole*",
                "iam:ListGroup*",
                "iam:ListPolicy*",
                "iam:ListSAML*",
                "iam:ListIdentity*",
                "iam:ListProject*",
                "iam:ListAccount*",
                "iam:ListAttach*",
                "iam:ListVirtualMFADevices",
                "iam:ListThirdParty*",
                "iam:ListConsole*",
                "iam:ListService*",
                "iam:ListPlatformIdentity*",
                "iam:ListCategory*",
                "iam:ListSystem*",
                "iam:ListEntities*",
                "iam:ListIDP*",
                "iam:ListAccessKeys*",
                "iam:ListPolicies*",
                "iam:ListAppID*",
                "iam:ListResource*",
                "iam:ListTag*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="iamfullaccess"></span>
### IAMFullAccess

IAM identities (IAM users, user groups, roles) that are authorized for this policy gain full administrative access to Access control (IAM).

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="accesskeyfullaccess"></span>
### AccessKeyFullAccess

After being authorized by this policy, the IAM identity (IAM user, user group, role) can obtain all administrative rights of API an Access Key (Access Key), including key creation, deletion, status modification, query key list, and console view key Secret Access Key permissions.

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:CreateAccessKey",
                "iam:DeleteAccessKey",
                "iam:ListAccessKeys",
                "iam:UpdateAccessKey",
                "iam:ListSecretKeys"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="accesskeyreadonlyaccess"></span>
### AccessKeyReadOnlyAccess

IAM identities (IAM users, user groups, roles) that are authorized by this policy can obtain read\-only access to the API an Access Key (Access Key), including the ability to query the list of keys and view the Secret Access Key in the console.

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:ListAccessKeys",
                "iam:ListSecretKeys"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="tag-service-system-default-policy"></span>
## Tag service system default policy

<span id="tagfullaccess"></span>
### TagFullAccess

The IAM identity (IAM user, user group, role) authorized by the policy can obtain content related to the tag service in the management account, such as searching by tag and other related content.

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tag:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```
