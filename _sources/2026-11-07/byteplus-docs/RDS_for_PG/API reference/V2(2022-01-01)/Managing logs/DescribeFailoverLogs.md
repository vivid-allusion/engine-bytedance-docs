---
title: "DescribeFailoverLogs"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describefailoverlogs"
---

Call the DescribeFailoverLogs API to query the primary/secondary switchover log of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|QueryStartTime |String |No |2023\-07\-31T12:00:19Z |retrieve start time. Format: `yyyy-MM-ddTHH:mmZ` (UTC time). t refers to the start of a specific time; z refers to the time zone offset, for example, Beijing time offset is +0800. The default value is the instance creation time, meaning the query starts from the instance creation. |
|QueryEndTime |String |No |2023\-07\-31T12:00:19Z |The query end time must be later than the start time, and the interval between the start and end times should be less than 31 days. Format: `yyyy-MM-ddTHH:mmZ` (UTC time). The default value is the request initiation time. |
|Limit |Integer |No |1000 |Records per page. The maximum is 1,000, the minimum is 1, and the default value is 500. |
|Context |String |No |[1690808035000,100367578,8388608,null] |Index information, used to load more logs on page turn. Pass through the previously returned context value to retrieve subsequent log content. The default value is empty. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of switchover logs. |
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|FailoverLogs |Array of [FailoverLogs](https://docs.byteplus.com/en/docs/61/15756#failoverlogs) |Refer to the sample response. |Switch primary node log list. |
|Context |String |[1690808035000,100367578,8388608,null] |Index information. Use the last backup file as the index for return. Can be used as the parameter for the next request. Select when loading more. |


<span id="failoverlogs"></span>
### FailoverLogs


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NewMasterNodeId |String |postgres\-21a3333b\*\*\*\*\-0 |New primary node ID. |
|OldMasterNodeId |String |postgres\-21a3333b\*\*\*\*\-1 |Old primary node ID. |
|FailoverType |String |System |Switch type.<br><br><br>* `System`: system automatic primary\-secondary switch.<br><br>* `User`: user manual primary\-secondary switch. |
|FailoverTime |String |2020\-06\-18T01:40:44Z |Switch time between primary and secondary nodes. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeFailoverLogs&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-21a3333b****",
    "QueryStartTime": "2023-07-31T12:00:19Z",
    "Limit": 50
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230801163925C4433796666B3E75888D",
        "Action": "DescribeFailoverLogs",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Context": "[1690808035000,100367578,8388608,null]",
        "FailoverLogs": [
            {
                "FailoverTime": "2023-10-16T12:13:39.000Z",
                "FailoverType": "User",
                "NewMasterNodeId": "postgres-21a3333b****-gsss-867dddc678-j5zdt",
                "OldMasterNodeId": "postgres-21a3333b****-c945c486b-kn294"
            },
            {
                "FailoverTime": "2023-10-16T12:13:39.000Z",
                "FailoverType": "User",
                "NewMasterNodeId": "postgres-21a3333b****-c945c486b-kn294",
                "OldMasterNodeId": "postgres-21a3333b****-gsss-867dddc678-j5zdt"
            }
        ],
        "InstanceId": "postgres-21a3333b****",
        "Total": 2
    }
}
```
