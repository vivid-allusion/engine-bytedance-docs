---
title: "CreateKeyScanJob"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createkeyscanjob"
---

Call the CreateKeyScanJob API to create expired key cleanup task for the target Redis instance.

## Request type

Asynchronous request.

## Precautions

After calling the CreateKeyScanJob API, the system will automatically execute a SCAN command to scan all data. At this time, the CPU load of the Instance will increase, which may affect the performance of the Instance. It is recommended that you execute this task during the off\-peak period of the service/business. For more details, please refer to [Expired key management](https://docs.byteplus.com/en/docs/redis/Expired_key_management).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateKeyScanJob&serviceCode=Redis&version=2020-12-07&groupName=性能分析)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfkmh6uiii87hla |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ScanKeyNumPerSecond |Integer |Yes |2000 |Number of expired keys scanned per second. Value range: An integer from 2000 to 100000. |
|TimeoutMinutes |Integer |Yes |30 |Scan timeout. Value range: An integer between 30 and 1440. Unit: minute. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|JobId |String |scan\-sy01rcrwdhcwqg6gaq3g46r5uxt |Task ID for the scan task. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateKeyScanJob&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cnlfkmh6uiii87hla",
    "ScanKeyNumPerSecond": 2000,
    "TimeoutMinutes": 30
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "CreateKeyScanJob",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "JobId": "scan-sy01rcrwdhcwqg6gaq3g46r5uxt"
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
