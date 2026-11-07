---
title: "RestartDBInstance"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/restartdbinstance"
---

Call the RestartDBInstance API to restart the target MongoDB instance.

## Request type

Asynchronous request.

## Precautions

* Only the instances in the **Running** status can be restarted.

* In the process of restarting an instance, access to some services will be affected for a short time. So take caution when performing this operation.

* We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=RestartDBInstance&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-f9e5d782****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202202231124340102120372301907****",
        "Action": "RestartDBInstance",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
