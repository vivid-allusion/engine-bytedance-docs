---
title: "DescribeDBInstanceSSL"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbinstancessl"
---

Call the DescribeDBInstanceSSL interface to query the SSL encryption settings of the target MongoDB instance, including whether the function has been enabled, the expiration time of the SSL certificate, and other information.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID. |
|SSLEnable |Boolean |true |Whether the SSL encryption function is enabled. The value range is as follows:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|SSLExpiredTime |String |2023\-10\-20T08:50:22Z |The expiration time of the SSL certificate, in the format of *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).<br><br>tip<br><br>This parameter will be returned only when the SSL certificate is valid (i.e., the value of `IsValid` is `true`). |
|IsValid |Boolean |false |Whether the SSL certificate is valid. The value range is as follows:<br><br><br>* `true`: Valid.<br><br>* `false`: Invalid. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBInstanceSSL&Version=2022-01-01 HTTP/1.1
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
        "RequestId": "202210201651430101742552020534****",
        "Action": "DescribeDBInstanceSSL",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mongo-shard-f9e5d782****",
        "IsValid": true,
        "SSLEnable": true,
        "SSLExpiredTime": "2023-10-20T08:50:22Z"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
