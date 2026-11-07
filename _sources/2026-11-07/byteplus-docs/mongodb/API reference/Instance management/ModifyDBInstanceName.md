---
title: "ModifyDBInstanceName"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbinstancename"
---

Call the ModifyDBInstanceName API to modify the instance name of the target MongoDB Instance.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|InstanceNewName |String |Yes |test\-mongo |The new name of the modified instance. You can customize the instance name as needed. The instance name does not require uniqueness. The name must meet the following requirements at the same time:<br><br><br>* It cannot start with a number or a hyphen (\-).<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length must be 2 to 64 characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBInstanceName&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-e405f8e2****",
    "InstanceNewName": "mongo-test"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202202231605380102121450481807****",
        "Action": "ModifyDBInstanceName",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
