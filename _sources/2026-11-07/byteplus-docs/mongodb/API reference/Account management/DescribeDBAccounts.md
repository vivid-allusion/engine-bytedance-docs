---
title: "DescribeDBAccounts"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbaccounts"
---

Call the DescribeDBAccounts API to query account information under the target instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|AccountName |String |No |root |Database account name. Fuzzy query is supported.<br><br>tip<br><br>If this parameter is not set, it means that the account name condition is not used for filtering. |
|AuthDB |String |No |admin |The database to which the account belongs. Fuzzy query is supported.<br><br>tip<br><br>If this parameter is not set, it means that the condition of the database to which the account belongs is not used for filtering. |
|PageSize |Integer |No |10 |Number of records per page, with a value being an integer between 1 and 1000, and the default value being 10. |
|PageNumber |Integer |No |1 |The page number of the instance information list, with a default value of 1. The value should not exceed the maximum value of the Integer data type, starting from 1. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |3 |The total number of all accounts. |
|Accounts |Object[] | |A list of account information. |
|AccountName |String |apitest |Name of account. |
|AccountPrivileges |Object[] | |A list of databases and permissions of the current account. |
|DBName |String |testdb |The database to which the current account belongs. |
|RoleName |String |readWrite |The role of the current account. |
|AccountType |String |UserAdmin |Account types. The value range is as follows:<br><br><br>* `Super`: Super administrator account, that is, the root account.<br><br>* `UserAdmin`: High\-privileged account, that is, an account with any permissions for the admin database.<br><br>* `Normal`: Normal account, that is, an account with no permissions for the admin database.<br><br><br>tip<br><br>For more details about different types of accounts in MongoDB, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview#account-type). |
|AuthDB |String |admin |The database to which the account belongs. |
|CreateTime |String |2024\-08\-09T09:24:56Z |The creation time of the account. The format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC). |
|ModifyTime |String |2024\-08\-09T09:24:56Z |The last update time of the account. The format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC). |
|AccountDesc |String |testdesc |The description information of the account.<br><br>tip<br><br>This parameter will only be returned when the account has description information set. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBAccounts&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-e405f8e2****",
    "AccountName": "root"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220308144759010212168072140B****",
        "Action": "DescribeDBAccounts",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Accounts": [
            {
                "AccountDesc": "root_account",
                "AccountName": "root",
                "AccountPrivileges": [
                    {
                        "DBName": "admin",
                        "RoleName": "root"
                    }
                ],
                "AccountType": "Super",
                "AuthDB": "admin",
                "CreateTime": "2024-08-09T09:24:56Z",
                "ModifyTime": "2024-08-09T09:24:56Z"
            },
            {
                "AccountDesc": "testdesc",
                "AccountName": "apitest",
                "AccountPrivileges": [
                    {
                        "DBName": "admin",
                        "RoleName": "readAnyDatabase"
                    },
                    {
                        "DBName": "config",
                        "RoleName": "read"
                    },
                    {
                        "DBName": "local",
                        "RoleName": "read"
                    }
                ],
                "AccountType": "UserAdmin",
                "AuthDB": "admin",
                "CreateTime": "2024-08-09T19:18:51Z",
                "ModifyTime": "2024-08-09T19:18:51Z"
            },
            {
                "AccountDesc": "testdesc",
                "AccountName": "testacc",
                "AccountPrivileges": [
                    {
                        "DBName": "config",
                        "RoleName": "read"
                    },
                    {
                        "DBName": "local",
                        "RoleName": "read"
                    }
                ],
                "AccountType": "Normal",
                "AuthDB": "testdb",
                "CreateTime": "2024-08-09T19:18:51Z",
                "ModifyTime": "2024-08-12T11:40:27Z"
            }
        ],
        "Total": 3
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
