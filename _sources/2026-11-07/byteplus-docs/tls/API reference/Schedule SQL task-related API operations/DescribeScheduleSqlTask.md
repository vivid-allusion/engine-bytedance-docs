---
title: "DescribeScheduleSqlTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describeschedulesqltask"
---

Call DescribeScheduleSqlTask interface to view the details of the specified scheduled SQL analysis task.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeScheduleSqlTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |True |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The ID of the scheduled SQL analysis task. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|CreateTimeStamp |Integer |`1689042649` |The creation time of the scheduled SQL analysis task. |
|Description |String |`test` |A brief description of the scheduled SQL analysis task. |
|DestProjectID |String |`c4737fdd-0c72-4c1f-b35e-3ae4a02d\*\*\*\*` |The ID of target project. |
|DestRegion |String |`cn-shanghai` |The region where the target topic resides. |
|DestTopicID |String |`66b42cb6-3436-44ae-97bf-efab3043**` |Target log topic ID for storing timed SQL analysis result data. |
|DestTopicName |String |`destTopicName` |The name of the target topic. |
|ModifyTimeStamp |Integer |`1689042649` |The last modification time of the scheduled SQL analysis task. |
|ProcessEndTime |Integer |`1689042649` |The end time of a scheduled SQL task. The format is a second timestamp. |
|ProcessSqlDelay |Integer |`0` |Delay time for each dispatch. The unit is seconds. |
|ProcessStartTime |Integer |`1689042649` |The start time of the scheduled SQL task, which is when the first instance was created. The format is second timestamp. |
|ProcessTimeWindow |String |`@m-m,@m` |The time range for log query and analysis used when the scheduled SQL task is running. |
|Query |String |`*` |The query and analysis statement executed regularly by scheduled SQL tasks. |
|RequestCycle |Object of [RequestCycle](https://docs.byteplus.com/en/docs/38/17255#requestcycle) |`{"Type": "Period", "Time": 1}` |The cycle based on which the system schedules the scheduled SQL task. The scheduling cycle determines the scheduling time for each instance.<br><br><br>* Type: Type of scheduling period. Optional values are:<br><br>   * Period: Scheduled at regular intervals, that is, scheduled once every certain period.<br><br>   * Fixed: Regular scheduling, that is, scheduled at a fixed time point every day.<br><br>* Time: The period of scheduling or the time point of regular execution (minutes from `00:00`), the value range is 1~1440, in minutes. |
|SourceProjectID |String |`abd6b3a7-c730-4527-8d5f-e527b381\*\*\*` |the ID of the source Project. |
|SourceProjectName |String |`projectName` |the name of the source Project. |
|SourceTopicName |String |`sourceTopicName` |The name of the source topic. |
|Status |Integer |`1` |After completing the task configuration, whether to immediately start the scheduled SQL analysis task. Optional values are:<br><br><br>* 0: Turn off the task, you will need to manually start the task later.<br><br>* 1: Start immediately. |
|TaskId |String |`2de5d435-0480-4139-9c79-b4241e88\*\*\*\*` |The ID of the scheduled SQL analysis task. |
|TaskName |String |`test2` |The name of the scheduled SQL analysis task. |
|SourceTopicID |String | |The ID of the source topic. |


<span id="requestcycle"></span>
### RequestCycle


|Name |Type |Example |Description |
|---|---|---|---|
|Time |Integer |`10` |The scheduling cycle or the time point for regular execution (the number of minutes from 00:00), the value range is 1~1440, in minutes. |
|Type |String |`Period` |Scheduling cycle types. Optional values:<br><br><br>* Period: Scheduled at regular intervals, that is, scheduled once every certain period.<br><br>* Fixed: Regular scheduling, that is, scheduled at a fixed time point every day. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeScheduleSqlTask?&TaskId=f3e901c3-b17f-42fd-aa8c-dc91a6c7**** HTTP/1.1
Content-Type: application/json
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8 
{
    "TaskId":"2de5d435-0480-4139-9c79-b4241e88****",
    "TaskName":"test2",
    "Description":"test",
    "SourceProjectID":"abd6b3a7-c730-4527-8d5f-e527b381****",
    "SourceProjectName":"projectName",
    "SourceTopicID":"c5c6b3a7-c730-4527-8d5f-e527b381****",
    "SourceTopicName":"sourceTopicName",
    "DestRegion":"cn-shanghai",
    "DestProjectID":"c4737fdd-0c72-4c1f-b35e-3ae4a02d****",
    "DestTopicID":"66b42cb6-3436-44ae-97bf-efab3043****",
    "DestTopicName":"destTopicName",
    "Status": 1,
    "ProcessStartTime":1689042649,
    "RequestCycle":{
        "Type":"Period",
        "Time":1
    },
    "ProcessTimeWindow":"@m-m,@m",
    "CreateTimeStamp":1689042649,
    "ModifyTimeStamp":1689042649,
    "Query":"",
    "ProcessSqlDelay": 0
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|404 |ScheduleSqlTaskNotExist |Task %s does not exist. |The scheduled SQL analysis task does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
