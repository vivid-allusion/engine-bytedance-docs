---
title: "DescribeKeyScanJobs"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describekeyscanjobs"
---

Call the DescribeKeyScanJobs API to query the list of expired key cleanup tasks of the target Redis instance within a specified time range.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeKeyScanJobs&serviceCode=Redis&version=2020-12-07&groupName=性能分析)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfkmh6uiii87hla |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|QueryStartTime |String |Yes |2025\-07\-07T13:00:00Z |Query start time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> The query start time needs to be earlier than the query end time.<br> |
|QueryEndTime |String |Yes |2025\-07\-07T13:30:00Z |Query end time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> The query end time must be later than the query start time.<br> |
|PageSize |Integer |No |10 |Number of records per page. The value is an integer from 1 to 1000, with a default of 10. |
|PageNumber |Integer |No |1 |Page number of the scan key task list. The value does not exceed the maximum value of the Integer data type; the starting and default values are both 1. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TotalJobsNumber |Integer |1 |Total number of scan tasks. |
|JobList |Array of [KeyScanJobInfo](https://docs.byteplus.com/en/docs/55/57420#keyscanjobinfo) |Refer to the Sample response. |Scan task information list |

### KeyScanJobInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|JobId |String |scan\-sy01rcrwdhcwqg6gaq3g46r5uxt |Task ID. |
|Status |String |Finished |Task status. For more details about task status, refer to [Expired key cleanup task status](https://docs.byteplus.com/en/docs/redis/Expired_key_management#2GwsNtg2). |
|StartTime |String |2025\-07\-07T13:15:13Z |Task start time. Format is `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|CreateTime |String |2025\-07\-07T13:15:13Z |The time when the task was created. Format is `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|FinishTime |String |2025\-07\-07T13:15:21Z |Task end time. Format is `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|TotalCount |Integer |10 |Total number of shards to analyze |
|CompletedCount |Integer |10 |Number of shards with completed analysis. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeKeyScanJobs&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cnlfkmh6uiii87hla",
	"QueryStartTime": "2025-07-07T13:00:00Z",
	"QueryEndTime": "2025-07-07T13:30:00Z",
	"PageSize": 10,
	"PageNumber": 1
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "DescribeKeyScanJobs",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "JobList": [
            {
                "CompletedCount": 10,
                "CreateTime": "2025-07-07T13:15:13Z",
                "FinishTime": "2025-07-07T13:15:21Z",
                "JobId": "scan-sy01rcrwdhcwqg6gaq3g46r5uxt",
                "StartTime": "2025-07-07T13:15:13Z",
                "Status": "Finished",
                "TotalCount": 10
            }
        ],
        "TotalJobsNumber": 1
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
