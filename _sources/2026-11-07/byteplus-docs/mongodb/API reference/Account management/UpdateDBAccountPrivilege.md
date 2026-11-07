---
title: "UpdateDBAccountPrivilege"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/updatedbaccountprivilege"
---

Call the UpdateDBAccountPrivilege API to modify the privileges or account description of a specified account in the target MongoDB instance.

## Request type

Synchronous request.

## Precautions

* Different account types support different information modifications through the UpdateDBAccountPrivilege API. Among them:

   * High\-privileged accounts (i.e., `AccountType` is `UserAdmin`) and normal accounts (i.e., `AccountType` is `Normal`):

      * Support modifying the database privileges and account description of super or normal accounts through the current API.

      * For more details about different types of accounts, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview#.6LSm5Y-357G75Z6L).

   * Super administrator account (i.e., `AccountType` is `Super`):

      * Only support modifying the account description of the super administrator account through the current API.

      * The privileges of the super administrator account only support being reset to the initial state and cannot be modified to specific privileges. You can reset the super administrator account privileges through the [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) API. For more details, refer to [Reset root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account).

* Modifying the account permissions may cause errors such as no access permission when the current account connects to the corresponding database, thereby affecting the business. Please operate with caution. For more details, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges)

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-7e0f6190\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|AccountName |String |Yes |apitest |The name of the account whose permissions or account description need to be modified.<br><br>tip<br><br>You can call the [DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) API to query all the account information under the target MongoDB instance, including the account name. |
|AuthDB |String |No |admin |The database to which the account belongs.<br><br>tip<br><br>If this parameter is not set, it is defaulted that the account whose permissions need to be modified belongs to the admin database. |
|AccountDBPrivileges |Object[] |No | |The list of database permissions to be modified for the account.<br><br>tip<br><br><br>* If this parameter is not set, by default, no permissions of the account in any database will be modified.<br><br>* Modifying the account permissions may cause errors such as no access permission when the current account connects to the corresponding database, thereby affecting the business. Please operate with caution.<br><br>* It is not allowed to leave both the `AccountDBPrivileges` and `AccountDesc` parameters empty simultaneously. |
|DBName |String |Yes |admin |The name of the database for which permissions need to be granted to the account.<br><br>Document Database for MongoDB allows granting relevant permissions to some system databases and your self\-created databases. Therefore, the allowable values for the database are as follows:<br><br><br>* System databases: including `admin`, `local`, and `config`.<br><br>* Other databases: that is, any database you create yourself, such as `testdb`.<br><br><br>tip<br><br><br>* For details about the permissions that can be granted for different types of databases, refer to [Database and account permissions](https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ).<br><br>* You can view the names of the databases in the current MongoDB instance through the [listDatabases](https://www.mongodb.com/docs/v5.0/reference/command/listDatabases/) command. |
|RoleNames |String[] |Yes |read |Database permissions that need to be granted to the account.<br><br>The permissions that can be granted to accounts for different databases in Document Database for MongoDB are as follows:<br><br><br>* `admin` database: Accounts are allowed to be granted `read`, `userAdmin`, `readAnyDatabase`, `readWriteAnyDatabase`, `userAdminAnyDatabase`, `dbAdminAnyDatabase`, `clusterMonitor` and `backup` permissions in the `admin` database.<br><br>* `local` database: Only `read` permission is allowed to be granted to accounts in the `local` database.<br><br>* `config` database: Only `read` permission is allowed to be granted to accounts in the `config` database.<br><br>* Other databases: Accounts are allowed to be granted `read`, `readWrite`, `dbAdmin`, `userAdmin` and `dbOwner` permissions in the databases you create yourself.<br><br><br>tip<br><br><br>* For details of the permissions that can be granted for different types of databases, refer to [Database and account permissions](https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ).<br><br>* This permission modification is an overwriting modification, that is, the permission list of `RoleNames` in `AccountDBPrivileges` will overwrite the permissions of the account in the corresponding `DBName` database.<br><br>* If this parameter is left blank, it means to clear all the permissions of the current account in the corresponding `DBName` database. Please operate with caution. |
|AccountDesc |String |No |testdesc |Modify the description of the account. The remarks information must meet the following conditions simultaneously:<br><br><br>* The length is 0 to 256 characters.<br><br>* It can contain numbers, Chinese, English, underscore (_), and hyphen (\-).<br><br><br>tip<br><br><br>* If this parameter is not set, the original remarks information of the account will not be modified by default.<br><br>* It is not allowed to leave both the `AccountDBPrivileges` and `AccountDesc` parameters empty simultaneously. |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample 1

Change the account description of root account to `super account root`. The request example is as follows.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=UpdateDBAccountPrivilege&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-7e0f6190****",
    "AccountName": "root",
    "AccountDesc": "super account root"
}
```

## Response sample 1

```json
{
    "ResponseMetadata": {
        "RequestId": "2023060411042010023228002****",
        "Action": "UpdateDBAccountPrivilege",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Request sample 2

Modify the permissions of the apitest account in the testdb database. The modified permissions are as follows:

* Clear all permissions of apitest in the testdb1 database.

* Grant apitest the `read` and `readWrite` permissions in the testdb2 database.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=UpdateDBAccountPrivilege&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-replica-7e0f6190****",
    "AccountName": "apitest",
    "AuthDB": "testdb",
    "AccountDBPrivileges": [
        {
            "DBName": "testdb1",
            "RoleNames": []
        },
        {
            "DBName": "testdb2",
            "RoleNames": [
                "read",
                "readwrite"
            ]
        }
    ]
}
```

## Response sample 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "UpdateDBAccountPrivilege",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
