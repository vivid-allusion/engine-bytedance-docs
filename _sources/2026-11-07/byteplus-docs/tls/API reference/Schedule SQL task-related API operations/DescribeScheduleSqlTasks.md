---
title: "DescribeScheduleSqlTasks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describeschedulesqltasks"
---

Call DescribeScheduleSqlTasks interface to view the details of all scheduled SQL analysis tasks in the specified region. Pagination queryis supported.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeScheduleSqlTasks**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectId |String |False |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The ID of the project which the source topic belongs. |
|ProjectName |String |False |`yyj-test` |The name of the project which the source topic belongs. |
|IamProjectName |String |False |`test` |The name of the IAM project. |
|TopicId |String |False |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The ID of the source topic. |
|SourceTopicName |String |False |`Topic name` |The name of the source topic. |
|TaskId |String |False |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The ID of the scheduled SQL analysis task. |
|TaskName |String |False |`test-task` |The name of the scheduled SQL analysis task. |
|Status |String |False |`0` |The status of the scheduled SQL task. |
|PageNumber |Integer |False |`10` |The page number for pagination queries. The default is 1, which means data will start being returned from the first page. |
|PageSize |Integer |False |`20` |The page size. Default is 20, maximum is 100. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|Tasks |Array of [DescribeScheduleSqlTaskResp](https://docs.byteplus.com/en/docs/38/17256#describeschedulesqltaskresp) |`[{"TaskId": "2de5d435-0480-4139-9c79-b4241e88****", "TaskName": "test2", "Description": "Test", "SourceProjectID": "abd6b3a7-c730-4527-8d5f-e527b381****", "SourceProjectName": "projectName", "SourceTopicID": "c5c6b3a7-c730-4527-8d5f-e527b381****", "SourceTopicName": "sourceTopicName", "DestRegion": "cn-Shanghai", "DestProjectID": "c4737fdd-0c72-4c1f-b35e-3ae4a02d****", "DestTopicID": "66b42cb6-3436-44ae-97bf-efab3043****", "DestTopicName": "destTopicName", "Status": 1, "ProcessStartTime": 1689042649, "RequestCycle": {"Type": "Period", "Time": 1}, "ProcessTimeWindow": "@m - m, @m", "CreateTimeStamp": 1689042649, "ModifyTimeStamp": 1689042649, "Query": "," ProcessSqlDelay " : 0}]` |The list of the scheduled SQL analysis tasks. |
|Total |Integer |`1` |The total number of tasks returned. |


<span id="describeschedulesqltaskresp"></span>
### DescribeScheduleSqlTaskResp


|Name |Type |Example |Description |
|---|---|---|---|
|Query |String |`* \| select count(*)` |The query and analysis statement executed regularly by scheduled SQL tasks. |
|Status |Integer |`0` |After completing the task configuration, whether to immediately start the scheduled SQL analysis task. Optional values are:<br><br><br>* 0: Turn off the task, you will need to manually start the task later.<br><br>* 1: Start immediately. |
|TaskId |String |`2de5d435-0480-4139-9c79-b4241e88****` |The ID of the scheduled SQL analysis task. |
|TaskName |String |`task-name` |The name of the scheduled SQL analysis task. |
|DestRegion |String |`cn-shanghai` |The region where the target topic resides. |
|Description |String |`This is a test ins.` |A brief description of the scheduled SQL analysis task. |
|DestTopicID |String |`d49a16d3-8711-445d-82a2-ab1689f4****` |The ID of target topic that stores the result of the scheduled SQL analysis task. |
|RequestCycle |Object of [RequestCycle](https://docs.byteplus.com/en/docs/38/17256#requestcycle) |`{"Type":"Period","Time":1}` |The cycle based on which the system schedules the scheduled SQL task. The scheduling cycle determines the scheduling time for each instance.<br><br><br>* Type: Type of scheduling period. Optional values are:<br><br>   * Period: Scheduled at regular intervals, that is, scheduled once every certain period.<br><br>   * Fixed: Regular scheduling, that is, scheduled at a fixed time point every day.<br><br>* Time: The period of scheduling or the time point of regular execution (minutes from `00:00`), the value range is 1~1440, in minutes. |
|DestProjectID |String |`c253c122-aa35-42bd-9a9e-30f47c95****` |The ID of target project. |
|DestTopicName |String |`dest-topic-name` |The name of target topic that stores the result of the scheduled SQL analysis task. |
|ProcessEndTime |Integer |`1702118732` |The end time of the scheduled SQL analysis task. The format is a timestamp in seconds. |
|CreateTimeStamp |Integer |`1702032332` |The creation time of the SQL analysis task. |
|ModifyTimeStamp |Integer |`1702032332` |The last modification time of the SQL analysis task. |
|ProcessSqlDelay |Integer |`0` |Delay time for each dispatch. The unit is seconds. |
|SourceProjectID |String |`d49a16d3-8711-445d-82a2-ab1689f4****` |The project ID to which the source topic belongs. |
|SourceTopicName |String |`topicName` |The name of the source topic. |
|ProcessStartTime |Integer |`1702032332` |The start time of the scheduled SQL analysis task, that is, the time to create the first instance. The format is a timestamp in seconds. |
|ProcessTimeWindow |String |`@m-m,@m` |The time range for log query and analysis used when the scheduled SQL task is running. |
|SourceProjectName |String |`d49a16d3-8711-445d-82a2-ab1689f4****` |The name of the source project. |
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
GET https://tls-{Region}.bytepluses.com/DescribeScheduleSqlTasks?&ProjectId=f3e901c3-b17f-42fd-aa8c-dc91a6c7****&ProjectName=&TopicId=f3e901c3-b17f-42fd-aa8c-dc91a6c7****&SourceTopicName=topic名称&TaskId=f3e901c3-b17f-42fd-aa8c-dc91a6c7****&TaskName=test-task&PageNumber=10&PageSize=20 HTTP/1.1
Content-Type: application/json
```


<span id="sample-response"></span>
## Sample Response

```json
{
    "Total":1,
    "Tasks":[
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
            "Status":1,
            "ProcessStartTime":1689042649,
            "RequestCycle":{
                "Type":"Period",
                "Time":1
            },
            "ProcessTimeWindow":"@m-m,@m",
            "CreateTimeStamp":1689042649,
            "ModifyTimeStamp":1689042649,
            "Query":"",
            "ProcessSqlDelay":0
        }
    ]
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|404 |ScheduleSqlTaskNotExist |Task %s does not exist. |The timed SQL analysis task does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
