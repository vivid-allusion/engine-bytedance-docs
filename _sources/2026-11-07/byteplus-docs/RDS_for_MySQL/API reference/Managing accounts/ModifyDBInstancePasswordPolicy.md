---
title: "ModifyDBInstancePasswordPolicy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/ModifyDBInstancePasswordPolicy"
---

Call ModifyDBInstancePasswordPolicy API to modify a custom password policy.

## Request type

Asynchronous request

## Precautions

The database kernel version must meet the following requirements:

* MySQL 5.7 instances: The kernel version must be MySQL 5.7.44_20260815 and above.

* MySQL 8.0 instances: The kernel version must be MySQL 8.0.43_20260815 and above.

* MySQL 8.4 instances: The kernel version must be MySQL 8.4.7_20260815 and above.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstancePasswordPolicy&serviceCode=rds_mysql&version=2022-01-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdlxxxx |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en) API to query the instance ID.<br> |
|PasswordPolicy |Object of [PasswordPolicy](https://docs.byteplus.com/en/docs/40/122492#passwordpolicy) |Yes |See the request example. |Custom password policy. |

### PasswordPolicy

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|Enabled |Boolean |Yes |true |Whether to enable the custom password policy. Values:<br><br><br>* `true`: Enabled.<br><br>* `false` (Default value): Disabled. |
|PolicyLevel |String |No |MEDIUM |Password strength level. Values are as follows:<br><br><br>* `LOW` (Default value): Low strength. Only the password length is verified. The password can be set as needed provided the length requirement is met.<br><br>* `MEDIUM`: Medium strength. The password length is verified, and the password must contain at least any three of uppercase letters, lowercase letters, numbers, and special characters.<br><br>* `STRONG`: High strength. The password length is verified, and the password must contain at least any three of uppercase letters, lowercase letters, numbers, and special characters.<br><br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > Since specifying a dictionary file is not supported currently, the verification rules for `MEDIUM` (medium strength) and `STRONG` (high strength) are the same.<br> |
|MinLength |Integer |No |8 |The minimum length of the password. The default value is 8, and the value range is 8~256.<br><br>> **tip**<br><br><br>> This parameter is required only when the `Enabled` parameter is set to `true`.<br> |
|NumberCount |Integer |No |1 |The number of digits that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > The configurable range of this parameter is dynamically adjusted based on the current values of the `MinLength`, `MixedCaseCount` and `SpecialCharCount` parameters.<br> |
|MixedCaseCount |Integer |No |1 |The minimum number of uppercase letters and lowercase letters that the password must contain respectively. The default value is 1, and the value range is 0~256. For example, when this parameter is set to 2, the password must contain at least 2 uppercase letters and 2 lowercase letters, meaning a total of at least 4 letters.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > The configurable range of this parameter is dynamically adjusted based on the current values of the `MinLength`, `NumberCount` and `SpecialCharCount` parameters.<br> |
|SpecialCharCount |Integer |No |1 |The number of special characters that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > The configurable range of this parameter is dynamically adjusted based on the current values of `MinLength`, `NumberCount`, and `MixedCaseCount`.<br> |

## Response parameter

null

## Sample

### Sample request

```json
POST /?Action=ModifyDBInstancePasswordPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-r3xq0zdlxxxx",
    "PasswordPolicy": {
        "Enabled": true,
        "MinLength": 8,
        "NumberCount": 1,
        "PolicyLevel": "MEDIUM",
        "MixedCaseCount": 1,
        "SpecialCharCount": 1
    }
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyDBInstancePasswordPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-north-1"
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
