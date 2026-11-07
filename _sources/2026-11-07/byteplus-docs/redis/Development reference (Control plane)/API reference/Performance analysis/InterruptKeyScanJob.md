---
title: "InterruptKeyScanJob"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/interruptkeyscanjob"
---

Call the InterruptKeyScanJob API to cancel specified expired key cleanup task.

## Request type

Synchronous request.

## Precautions

The status of the task to be canceled must be **Created** or **Running**. For more details on task statuses, refer to [Expired key cleanup task status](https://docs.byteplus.com/en/docs/redis/Expired_key_management#2GwsNtg2).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=InterruptKeyScanJob&serviceCode=Redis&version=2020-12-07&groupName=性能分析)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|JobId |String |Yes |scan\-sy01rcrwdhcwqg6gaq3g46r5uxt |Task ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeKeyScanJobs](https://docs.byteplus.com/en/docs/redis/describekeyscanjobs) API to query the list of key scanning tasks for the target Redis instance within the specified time period, including task ID information.<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=InterruptKeyScanJob&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "JobId": "scan-sy01rcrwdhcwqg6gaq3g46r5uxt"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "InterruptKeyScanJob",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
