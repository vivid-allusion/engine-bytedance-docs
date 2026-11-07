---
title: "ResetDBAccount"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/resetdbaccount"
---

Call the ResetDBAccount API to change password of specified account in target MongoDB instance or reset root account permissions to initial state.

## Request type

Asynchronous request.

## Precautions

* Different account types support different information modifications through the UpdateDBAccountPrivilege API. Among them:

   * High\-privileged accounts (i.e., `AccountType` is `UserAdmin`) and normal accounts (i.e., `AccountType` is `Normal`):

      * Support modifying the database privileges and account description of super or normal accounts through the current API.

      * For more details about different types of accounts, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview#.6LSm5Y-357G75Z6L).

   * Super administrator account (i.e., `AccountType` is `Super`):

      * Only support modifying the account description of the super administrator account through the current API.

      * The privileges of the super administrator account only support being reset to the initial state and cannot be modified to specific privileges. You can reset the super administrator account privileges through the [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) API. For more details, refer to [Reset root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account).

* Modifying the password may cause the database connection using the current account to be interrupted. Please operate with caution.

* If you use special characters in the password, you may need to escape them when connecting to the instance. For more details, refer to [Special characters that need to be escaped](https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|AccountName |String |Yes |root |Account name.<br><br>tip<br><br>You can call the [DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) API to query the account information under the target instance, including the account names. |
|AuthDB |String |No |testdb |The database to which the account belongs.<br><br>tip<br><br>If this parameter is not set, it is defaulted that the account for which the password needs to be modified belongs to the admin database. |
|AccountPassword |String |Yes |Test@12\*\*\*\* |The password of the database account. The password must meet the following requirements:<br><br><br>* It can only contain uppercase and lowercase letters, numbers, and the following special characters `_#!@$%^&*()+=-`.<br><br>* The length should be 8 to 32 characters.<br><br>* It must contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.<br><br>* Weak passwords that are easily cracked (such as `Admin@123`) are not allowed.<br><br><br>tip<br><br><br>* Modifying the password may cause the database connection using the current account to be interrupted. Please operate with caution.<br><br>* If you use special characters in the password, you may need to escape them when connecting to the instance. For more details, refer to [Special characters that need to be escaped](https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf).<br><br>* For details about weak passwords prohibited in MongoDB, refer to [Weak password list](https://docs.byteplus.com/en/docs/mongodb/account-overview#.5byx5a-G56CB5YiX6KGo). |
|ResetDBAccount |Boolean |No |false |Whether to reset the privileges of the root account to the initial state (that is, to complete the privileges that the super administrator account is allowed to be granted). The value range is as follows:<br><br><br>* `false` (default value): Do not reset.<br><br>* `true`: Reset.<br><br><br>tip<br><br><br>* This parameter only takes effect for the root account in the admin library (that is, `AuthDB` is `admin` and `AccountName` is `root`).<br><br>* For details of the complete privileges that the super administrator account is allowed to be granted, refer to [Database and account permissions](https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ). |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ResetDBAccount&Version=2022-01-01 HTTP/1.1Host: mongodb.ap-southeast-1.byteplusapi.comContent-Type: application/json; charset=utf-8X-Date: 20201103T104027ZAuthorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-e405f8e2****",
    "AccountName": "root",
    "AccountPassword": "Test@12****"
}
```

## Response sample

```json
{
    "ResponseMetadata": {
        "RequestId": "202203091439160102121681030B0B****",
        "Action": "ResetDBAccount",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
