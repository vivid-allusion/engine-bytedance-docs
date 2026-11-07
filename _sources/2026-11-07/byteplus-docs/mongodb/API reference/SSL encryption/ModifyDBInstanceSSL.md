---
title: "ModifyDBInstanceSSL"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbinstancessl"
---

Call the ModifyDBInstanceSSL API to change the SSL encryption settings of the target MongoDB instance, including enabling/disabling the encryption function, or updating the SSL certificate validity period.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|SSLAction |String |No |Close |Perform corresponding operations on the SSL encryption function. The value range is as follows:<br><br><br>* `Open` (default): Enable the SSL encryption function.<br><br>* `Close`: Disable the SSL encryption function.<br><br>* `Update`: Update the validity period of the SSL certificate.<br><br><br>tip<br><br>The operation of updating the validity period of the SSL certificate is only supported after the SSL encryption function has been enabled. You can call the [DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/mongodb/describedbinstancessl) API to check whether the SSL function of the instance has been enabled. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBInstanceSSL&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-f9e5d782****",
    "SSLAction": "Close"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202202211539050101742350380678****",
        "Action": "ModifyDBInstanceSSL",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
