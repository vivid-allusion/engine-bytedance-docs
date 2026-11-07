---
title: "DescribeFailoverLogs"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describefailoverlogs"
---

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-55aee4ba\*\*\*\* |Instance ID. |
|Offset |Integer |No |0 |The query offset for the current page. The minimum value is 0. The default value is 0. |
|Limit |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value is 100. The default value is 10. |
|StartTime |String |No |2024\-06\-01 00:00:00 |The start time of the switchover log. The time format is `yyyy-MM-dd HH:mm:ss` (UTC time). |
|EndTime |String |No |2024\-07\-01 00:00:00 |The end time of the switchover log. The time format is `yyyy-MM-dd HH:mm:ss` (UTC time).<br><br>> **tip**<br><br><br>> The end time cannot be earlier than the start time.<br> |

## Response parameter

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total. |
|FailoverQueryInfos |Array of [FailoverQueryInfoObject](https://docs.byteplus.com/en/docs/40/15511#failoverqueryinfoobject) |Refer to the sample response. |Switch primary node log list. |

### FailoverQueryInfoObject

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ChangeTime |String |2024\-01\-17 20:21:19 |Switch time between primary and secondary nodes. Format: yyyy\-MM\-dd HH:mm:ss. |
|Details |String |\- |Switchover log details. |
|NewMaster |String |mysql\-d4942fd7\*\*\*\*\-0 |New primary node ID. |
|OldMaster |String |mysql\-d4942fd7\*\*\*\*\-1 |Old primary node ID. |
|HAChangeType |String |TakeOver |Switch type.<br><br><br>* `TakeOver`: the user manually switches the primary node.<br><br>* `FailOver`: the primary node is switched due to an instance failure. |
|Reason |String |\- |Reason for switching between primary and secondary nodes. |
|EventId |String |20260922171730FFD7B379FAD7\-6xxxx |The event ID associated with the primary/standby switchover. |
|EventName |String |SwitchDBInstanceHA |The event name associated with the primary/standby switchover. |
|HAChangeSource |String |User |The event source of the primary/standby switchover. Values are as follows:<br><br><br>* `User`: Customer.<br><br>* `System`: system. |

## Sample

### Sample request

```json
POST /?Action=DescribeFailoverLogs&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-d4942fd7****",
    "Offset": 1,
    "Limit": 10
}
```

Call the DescribeFailoverLogs API to query the primary\-secondary switchover logs of a MySQL instance.

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeFailoverLogs",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-north-1"
    },
    "Result": {
        "Total": 1,
        "FailoverQueryInfos": [
            {
                "Reason": "-",
                "Details": "-",
                "EventId": "20260922171730FFD7B379FAD7-6xxxx",
                "EventName": "SwitchDBInstanceHA",
                "NewMaster": "mysql-d4942fd7****-0",
                "OldMaster": "mysql-d4942fd7****-1",
                "ChangeTime": "2024-01-17 20:21:19",
                "HAChangeType": "TakeOver",
                "HAChangeSource": "User"
            }
        ]
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
