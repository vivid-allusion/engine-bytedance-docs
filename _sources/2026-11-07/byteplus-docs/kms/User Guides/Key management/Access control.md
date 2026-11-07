---
title: "Access control"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Access_control"
---

The Key Management Service (KMS) performs access control for resources by using the Identity and Access Management (IAM) service. The following content describes the resource types and operation permissions defined in KMS.

A BytePlus account has full operation permissions for resources owned by the account. IAM users and IAM roles must explicitly be granted operation permissions for specified resources.

<span id="resource-types"></span>
## Resource types


|**Resource Type** |trn |
|---|---|
|Abstract keyring container |trn:kms:${region}:${account}:keyrings/\* |
|Abstract key container |trn:kms:${region}:${account}:keyrings/${keyringName}/keys/\* |
|Keyring |trn:kms:${region}:${account}:keyrings/$ |
|Key |trn:kms:${region}:${account}:keyrings/${keyringName}/keys/$ |


<span id="operation-permissions"></span>
## Operation permissions

KMS defines an action for each API that requires access control, allowing you to specify IAM permission policies. The API actions are commonly in the format `kms:<api-name>`.

The following table lists the types of resources required by each API action of KMS.


|API |Action |Resource |
|---|---|---|
|[CreateKeyring](https://docs.byteplus.com/en/docs/kms/CreateKeyring) |kms:CreateKeyring |Abstract keyring container |
|[DescribeKeyrings](https://docs.byteplus.com/en/docs/kms/DescribeKeyrings) |kms:DescribeKeyrings |Abstract keyring container |
|[UpdateKeyring](https://docs.byteplus.com/en/docs/kms/UpdateKeyring) |kms:UpdateKeyring |Keyring |
|[QueryKeyring](https://docs.byteplus.com/en/docs/kms/QueryKeyring) |kms:QueryKeyring |Keyring |
|[CreateKey](https://docs.byteplus.com/en/docs/kms/CreateKey) |kms:CreateKey |Abstract key container |
|[DescribeKeys](https://docs.byteplus.com/en/docs/kms/DescribeKeys) |kms:DescribeKeys |Abstract key container |
|[UpdateKey](https://docs.byteplus.com/en/docs/kms/UpdateKey) |kms:UpdateKey |Key |
|[GenerateDataKey](https://docs.byteplus.com/en/docs/kms/GenerateDataKey) |kms:GenerateDataKey |Key |
|[Encrypt](https://docs.byteplus.com/en/docs/kms/Encrypt) |kms:Encrypt |Key |
|[Decrypt](https://docs.byteplus.com/en/docs/kms/Decrypt) |kms:Decrypt |Key |
|[AsymmetricEncrypt](https://docs.byteplus.com/en/docs/kms/AsymmetricEncrypt) |kms:AsymmetricEncrypt |Key |
|[AsymmetricDecrypt](https://docs.byteplus.com/en/docs/kms/AsymmetricDecrypt) |kms: AsymmetricDecrypt |Key |
|[AsymmetrcSign](https://docs.byteplus.com/en/docs/kms/AsymmetrcSign) |kms: AsymmetrcSign |Key |
|[AsymmetrcVerify](https://docs.byteplus.com/en/docs/kms/AsymmetrcVerify) |kms: AsymmetrcVerify |Key |
|[EnableKey](https://docs.byteplus.com/en/docs/kms/EnableKey) |kms:EnableKey |Key |
|[DisableKey](https://docs.byteplus.com/en/docs/kms/DisableKey) |kms:DisableKey |Key |
|[ScheduleKeyDeletion](https://docs.byteplus.com/en/docs/kms/ScheduleKeyDeletion) |kms:ScheduleKeyDeletion |Key |
|[CancelKeyDeletion](https://docs.byteplus.com/en/docs/kms/CancelKeyDeletion) |kms: CancelKeyDeletion |Key |


<span id="default-system-permissions"></span>
## Default system permissions

**KMSFullAccess**

```Plain Text
{
    "Version": "1",
    "Statement": [ 
        {
            "Effect": "Allow",
            "Action": "kms:*",
            "Resource": [
                "*"
            ]
        }
    ]
}

```


**KMSReadOnlyAccess**

```Plain Text
{
    "Version": "1",
    "Statement": [ 
        {
            "Effect": "Allow",
            "Action": "kms:Describe*",
            "Resource": [
                "*"
            ]
        }
    ]
}

```


**KMSCryptoUserAccess**

```Plain Text
{
    "Version": "1",
    "Statement": [ 
        {
            "Effect": "Allow",
            "Action": ["kms:GenerateDataKey", "kms:Encrypt", "kms:Decrypt"],
            "Resource": [
                "*"
            ]
        }
    ]
}

```
