---
title: "CreateDBAccount"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/createdbaccount"
---

Call the CreateDBAccount API to create an account for the target MongoDB instance.

## Request type

Synchronous request.

## Precautions

It only supports creating high\-privileged accounts (i.e., `AccountType` is `UserAdmin`) and normal accounts (i.e., `AccountType` is `Normal`). For more details about different types of accounts, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview#.6LSm5Y-357G75Z6L).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-7e0f6190\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|AccountName |String |Yes |apitest |Set the name of the account. The name must meet the following conditions:<br><br><br>* The length is 1 to 32 characters.<br><br>* It consists of uppercase and lowercase letters, numbers, underscores (_), and hyphens (\-).<br><br>* It starts with a letter and ends with a letter or a number.<br><br>* The account name is not allowed to be the same as any of the following system\-reserved account names: `root`, `system_inspector`, `__system`, `mgr`.<br><br>   For example, you can set the account name to `test__system` or `__system__test`, but not to `__system`.<br><br>   tip<br><br>   ```Plain Text```<br>```   * Except for the `root` account, the above-mentioned system-reserved accounts will not be displayed on the MongoDB console. For more details, refer to [Viewing account details](../mongodb/viewing_account_information).```<br>```   * You don't need to pay attention to the permissions or operations of these system-reserved accounts. It is highly recommended not to perform any modification, deletion, or renaming operations on these reserved accounts, otherwise, it will affect the normal operation of the database account.```<br>```   ```<br>   <br><br>* The account name is not allowed to start with `vedb_mongodb_`.<br><br>   For example, you can set the account name to `testvedb_mongodb_`, but not to `vedb_mongodb_test`. |
|AccountPassword |String |Yes |Pwd@12\*\*\*\* |Account password. The password must meet the following requirements simultaneously:<br><br><br>* It can only contain uppercase and lowercase letters, numbers, and the following special characters `_#!@$%^&*()+=-`.<br><br>* The length should be 8 to 32 characters.<br><br>* It should contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.<br><br>* Weak passwords that are easily cracked (such as `Admin@123`) are not allowed.<br><br><br>tip<br><br><br>* If you use special characters in the password, you may need to escape them when connecting to the instance. For more details, refer to [Special characters that need to be escaped](https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf).<br><br>* You can also modify the account password through the [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) API after the account is created.<br><br>* For details about weak passwords prohibited in MongoDB, refer to [Weak password list](https://docs.byteplus.com/en/docs/mongodb/account-overview#.5byx5a-G56CB5YiX6KGo). |
|AuthDB |String |No |admin |The target database to which the account belongs.<br><br>tip<br><br>If this parameter is not set, the newly created account will default to belong to the `admin` database. |
|AccountDBPrivileges |Object[] |No | |The list of databases and permissions granted to the account.<br><br>tip<br><br>If this parameter is not set, by default, no permissions for any database will be granted to the account. |
|DBName |String |Yes |admin |The name of the database for which permissions need to be granted to the account.<br><br>Document Database for MongoDB allows granting relevant permissions to some system databases and your self\-created databases. Therefore, the allowable values for the database are as follows:<br><br><br>* System databases: including `admin`, `local`, and `config`.<br><br>* Other databases: that is, any database you create yourself, such as `testdb`.<br><br><br>tip<br><br><br>* For details about the permissions that can be granted for different types of databases, refer to [Database and account permissions](https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ).<br><br>* You can view the names of the databases in the current MongoDB instance through the [listDatabases](https://www.mongodb.com/docs/v5.0/reference/command/listDatabases/) command. |
|RoleNames |String[] |Yes |read |The database permissions to be granted for the account.<br><br>For Document Database for MongoDB, the permissions that can be granted for different databases are as follows:<br><br><br>* `admin` database: The account is allowed to be granted the `read`, `userAdmin`, `readAnyDatabase`, `readWriteAnyDatabase`, `userAdminAnyDatabase`, `dbAdminAnyDatabase`, `clusterMonitor` and `backup` permissions in the `admin` database.<br><br>* `local` database: Only the `read` permission is allowed to be granted for the account in the `local` database.<br><br>* `config` database: Only the `read` permission is allowed to be granted for the account in the `config` database.<br><br>* Other databases: The account is allowed to be granted the `read`, `readWrite`, `dbAdmin`, `userAdmin` and `dbOwner` permissions in the databases you create yourself.<br><br><br>tip<br><br><br>* Multiple permissions can be passed in simultaneously, separated by English commas (,).<br><br>* For details about the permissions that can be granted for different types of databases, refer to [Database and account permissions](https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ). |
|AccountDesc |String |No |testdesc |The remarks information of the account. The remarks information needs to meet the following conditions simultaneously:<br><br><br>* The length is 0 to 256 characters.<br><br>* It can contain numbers, Chinese, English, underscores (_), and hyphens (\-).<br><br><br>tip<br><br>If this parameter is not set, the remarks information of the account defaults to empty. |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample

Create a database accountin the admin database with the following permissions:

* Have the `userAdmin`, `readAnyDatabase`, `readWriteAnyDatabase`, `userAdminAnyDatabase`, `dbAdminAnyDatabase`, `clusterMonitor` and `backup` permissions for the `admin` database.

* Have `read` permission for the `local` database.

* Have `read` permission for the `config` database.

* Have the `read`, `readWrite`, `dbAdmin`, `userAdmin` and `dbOwner` permissions for the self\-built database `testdb`.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=CreateDBAccount&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-replica-7e0f6190****",
    "AccountName": "apitest",
    "AuthDB": "admin",
    "AccountPassword": "Pwd@12****",
    "AccountDesc": "test_desc",
    "AccountDBPrivileges": [
        {
            "DBName": "admin",
            "RoleNames": [
                "read",
                "userAdmin",
                "readAnyDatabase",
                "readWriteAnyDatabase",
                "userAdminAnyDatabase",
                "dbAdminAnyDatabase",
                "clusterMonitor",
                "backup"
            ]
        },
        {
            "DBName": "config",
            "RoleNames": [
                "read"
            ]
        },
        {
            "DBName": "local",
            "RoleNames": [
                "read"
            ]
        },
        {
            "DBName": "testdb",
            "RoleNames": [
                "read",
                "readWrite",
                "dbAdmin",
                "userAdmin",
                "dbOwner"
            ]
        }
    ]
}
```

## Response sample

```json
{
    "ResponseMetadata": {
        "RequestId": "2023060411042010023228002****",
        "Action": "CreateDBAccount",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
