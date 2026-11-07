---
title: "CreateBackup"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/createbackup"
---

Call the CreateBackup API to manually create a backup for the target MongoDB instance.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information of all MongoDB instances in the target region, including the instance ID. |
|BackupType |String |No |Physical |Backup types. The value range is as follows:<br><br><br>* `Physical`: physical backup.<br><br>* `Logical`: logical backup.<br><br><br>tip<br><br>If this parameter is left blank, the backup list of all types under the current instance will be returned by default. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=CreateBackup&Version=2022-01-01 HTTP/1.1
Host: mongodb.volcengineapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-f9e5d782****",
    "BackupType": "Physical"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "CreateBackup",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
