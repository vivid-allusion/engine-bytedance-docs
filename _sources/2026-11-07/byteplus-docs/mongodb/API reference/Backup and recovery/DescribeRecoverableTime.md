---
title: "DescribeRecoverableTime"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describerecoverabletime"
---

Call the DescribeRecoverableTime API to query the recoverable time range of backup files in the target MongoDB instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-f9e5d782\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|RecoverableTimeInfo |Object[] | |When it is necessary to restore the instance to a specific point in time, the recoverable time range supported by the instance.<br><br>tip<br><br>If the returned data is empty, it means that the current instance cannot be restored. |
|EarliestRecoverableTime |String |2024\-04\-10T14:17:25Z |The earliest recoverable time point of the instance, in the format of *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).<br><br>tip<br><br>If the returned data is empty, it means that the current instance is not recoverable. |
|LatestRecoverableTime |String |2024\-04\-10T14:17:25Z |The latest recoverable time point of the instance, in the format of *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).<br><br>tip<br><br>If the returned data is empty, it means that the current instance cannot be recovered. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeRecoverableTime&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-shard-f9e5d782****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "DescribeRecoverableTime",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RecoverableTimeInfo": [
            {
                "EarliestRecoverableTime": "2024-04-10T14:17:25Z",
                "LatestRecoverableTime": "2024-04-10T14:17:25Z"
            }
        ]
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
