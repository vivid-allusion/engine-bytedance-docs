---
title: "DescribeScheduleEvents"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeScheduleEvents"
---

Call the DescribeScheduleEvents API to view the scheduled events of the current account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeScheduleEvents&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Limit |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 500. The default value is 10. |
|Offset |Integer |No |0 |The query offset for the current page. The minimum value is 0. The default value is 0. |
|EventId |String |No |4nbx88ea9dxa\*\*\*\* |Event ID. |
|InstanceId |String |No |vedbm\-ca12cbqv\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br> |
|BeginTime |String |No |2024\-03\-13T03:07:19Z |The time when event execution starts, in YYYY\-MM\-DDTHH:MM:SSZ format (UTC time). |
|EndTime |String |No |2024\-03\-13T03:07:19Z |The end time of the event execution, in the format YYYY\-MM\-DDTHH:MM:SSZ (UTC time). |
|Status |Array of String |No |pending |Event state. Value:<br><br><br>* `pending`: Waiting for execution.<br><br>* `executing`: Executing.<br><br>* `failure`: Execution failed.<br><br>* `finish`: Completed.<br><br>* `cancel`: Cancelled. |
|EventKind |Array of String |No |ModifyDBInstanceSpec |Event type. Value:<br><br><br>* `ModifyDBInstanceParameters`: Modify parameters.<br><br>* `ModifyDBInstanceSpec`: Configuration change.<br><br>* `UpgradeInstance`: Version upgrade.<br><br>* `RestartDBInstance`: Restart instance. |
|ProjectName |String |No |default |The name of the project to which the instance associated with the event belongs. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ScheduleTasksInfo |Array of [ScheduleTasksInfoObject](https://docs.byteplus.com/en/docs/265/57402#scheduletasksinfoobject) |Refer to the Sample response. |Event details. |
|Total |Integer |2 |Total number of events. |


<span id="scheduletasksinfoobject"></span>
### ScheduleTasksInfoObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountID |Long |210006\*\*\*\* |Account ID. |
|BeginTime |String |2024\-03\-13T03:07:19Z |The execution start time of the event (UTC). |
|EndTime |String |2024\-03\-13T03:07:19Z |The end time of the event execution (UTC time). |
|EventId |String |4nbx88ea9dxa\*\*\*\* |Event ID. |
|EventKind |String |ModifyDBInstanceSpec |Event type. Value:<br><br><br>* `ModifyDBInstanceParameters`: Modify parameters.<br><br>* `ModifyDBInstanceSpec`: Configuration change.<br><br>* `UpgradeInstance`: Version upgrade.<br><br>* `RestartDBInstance`: Restart instance. |
|InstanceID |String |vedbm\-ca12cbqv\*\*\*\* |Instance ID. |
|InstanceName |String |test |Instance name. |
|Message |String |\- |Event details. This parameter returns the error details of the event when the planned event fails to execute. |
|PlannedStartTime |String |2024\-03\-13T03:07:19Z |Scheduled execution time (UTC time). |
|Status |String |pending |Event state. Value:<br><br><br>* `pending`: Waiting for execution.<br><br>* `executing`: Executing.<br><br>* `failure`: Execution failed.<br><br>* `finish`: Completed.<br><br>* `cancel`: Cancelled. |
|RequestId |String |56bffd64\-dd72\-48f7\-b370\-c03f360d\*\*\*\* |Request ID. |
|ScheduleType |String |MaintainTime |Execution method for the planned event. Valid values:<br><br><br>* `MaintainTime`: Execute in the maintenance window.<br><br>* `SpecifiedTime`: Execute at a specified time, for example, modifying the event execution time to Execute now. |
|ProjectName |String |default |The affiliated project of the instance. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeScheduleEvents&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "Limit": 20,
    "Offset": 0,
    "Status": [
        "pending"
    ],
    "EventKind": [
        "ModifyDBInstanceParameters"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024031314111883597BAC11B7B598****-72c862",
        "Action": "DescribeScheduleEvents",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "ScheduleTasksInfo": [
            {
                "AccountID": 2100069027,
                "EventId": "y61wnejqtyga****",
                "EventKind": "ModifyDBInstanceParameters",
                "InstanceID": "vedbm-jnfxn2lf****",
                "InstanceName": "test_az",
                "Message": "",
                "PlannedStartTime": "2024-03-13T10:00:00Z",
                "ProjectName": "default",
                "RequestId": "",
                "ScheduleType": "MaintainTime",
                "Status": "pending"
            },
            {
                "AccountID": 2100069027,
                "EventId": "4gjplaoge55f****",
                "EventKind": "ModifyDBInstanceParameters",
                "InstanceID": "vedbm-osh2b3tf****",
                "InstanceName": "test_lm",
                "Message": "",
                "PlannedStartTime": "2024-03-13T17:00:00Z",
                "ProjectName": "default",
                "RequestId": "",
                "ScheduleType": "MaintainTime",
                "Status": "pending"
            }
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
