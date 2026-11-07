---
title: "DeleteDBAccount"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/deletedbaccount"
---

Call the DeleteDBAccount API to delete the specified account in the target MongoDB instance.

## Request type

Synchronization request.

## Precautions

* Only the deletion of high\-privileged accounts (i.e., with `AccountType` being `UserAdmin`) and normal accounts (i.e., with `AccountType` being `Normal`) is supported. The deletion of super administrator accounts (i.e., with `AccountType` being `Super`) is not allowed. For more details about different types of accounts, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview#.6LSm5Y-357G75Z6L).

* Once an account is deleted, it cannot be restored, and it may cause the connection using this account to be interrupted. Please operate with caution.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-7e0f6190\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|AccountName |String |Yes |apitest |The name of the account that needs to be deleted.<br><br>tip<br><br>You can call the [DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) API to query the account information under the target instance, including the account names. |
|AuthDB |String |No |testdb |The database to which the account belongs.<br><br>tip<br><br>If this parameter is not set, it is defaulted that the account to be deleted belongs to the admin database. |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DeleteDBAccount&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-7e0f6190****",
    "AccountName": "apitest",
    "AuthDB": "testdb"
}
```

## Response sample

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "DeleteDBAccount",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
