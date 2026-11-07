---
title: "ModifyScheduleSqlTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifyschedulesqltask"
---

Call ModifyScheduleSqlTask interface to modify the scheduled SQL analysis task information.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyScheduleSqlTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the scheduled SQL analysis task. |
|TaskName |String |False |`schedule-sql-task-name` |The name of the scheduled SQL analysis task. |
|Description |String |False |`This is a test schedule sql task` |A brief description of the scheduled SQL analysis task.<br><br><br>* Does not support `<`, `'`, `\`, `\\`.<br><br>* The length range is 0 to 64 characters. |
|DestRegion |String |False |`cn-north-1` |The region where the target topic resides. |
|DestTopicID |String |False |`2a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of target topic that stores the result of the scheduled SQL analysis task. |
|Status |Integer |False |`0` |After completing the task configuration, whether to immediately start the scheduled SQL analysis task. Optional values are:<br><br><br>* 0: Turn off the task, you will need to manually start the task later.<br><br>* 1: Start immediately. |
|ProcessSqlDelay |Integer |False |`60` |The latency of each scheduling operation. The value range is 0 to 120, in seconds. |
|ProcessTimeWindow |String |False |`@m-15m,@m` |The time range for log query and analysis used when the scheduled SQL task is running. Specify a left\-closed and right\-open range for this parameter. After you specify a SQL time window, TLS initiates scheduled SQL tasks according to the specified scheduling cycle.<br><br>For example, you set: 1. the time when the system starts scheduling a scheduled SQL task to 10:00 on August 14, 2023. 2. the scheduling cycle to 1 hour. 3. the SQL time window to [@h\-1h,@h). 4. the execution latency to 10 seconds. After the scheduled SQL task is started, TLS generates 1 instance at 10:00:00 and starts executing the instance at 10:00:10, then analyzes the log data written during [09:00:00~10:00:00). Then, TLS creates the second instance at 11:00:00, starts executing the instance at 11:00:10, and analyzes the log data written during [10:00:00~11:00:00).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum SQL time window is 24 hours and the minimum window is 1 minute. If you set the SQL time window to longer than 24 hours, the executed instance may fail to run or the calculation results may be inaccurate due to excessive data. For more information on the syntax for SQL time windows, refer to <a href="https://arcosite.bytedance.net/sites/1698994260794/66040fd503c2af03142a46de/editor/6604101ed669b61225bc6d83/?docLang=en">SQL time window syntax</a>.</div><br> |
|Query |String |False |`* \| select *` |The query and analysis statement executed regularly by scheduled SQL tasks. Make sure the statement complies with the query and analysis syntax of TLS. For more information on the syntax, refer to [Query overview](https://docs.byteplus.com/en/docs/tls/Query-overview-2) and [Analysis overview](https://docs.byteplus.com/en/docs/tls/Analysis-overview). |
|RequestCycle |Object of [RequestCycle](https://docs.byteplus.com/en/docs/38/17253#requestcycle) |False |`{"Type": "Period", "Time": 1}` |The cycle based on which the system schedules the scheduled SQL task. The scheduling cycle determines the scheduling time for each instance.<br><br><br>* Type: Type of scheduling period. Optional values are:<br><br>   * Period: Scheduled at regular intervals, that is, scheduled once every certain period.<br><br>   * Fixed: Regular scheduling, that is, scheduled at a fixed time point every day.<br><br>* Time: The period of scheduling or the time point of regular execution (minutes from `00:00`), the value range is 1~1440, in minutes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you specify a scheduling cycle that is longer than or equal to the query time window. Otherwise, the scheduling may not be performed in a timely manner, which causes incorrect query results. For example, if the scheduling cycle is 10 minutes, the maximum SQL time window is 10 minutes.</div><br> |
|MaxRetryTimes |Integer |False |`3` |Default number of retries. |
|MaxTimeout |Integer |False |`300` |Maximum timeout, in seconds. |


<span id="requestcycle"></span>
### RequestCycle


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Time |Integer |True |`10` |The scheduling cycle or the time point for regular execution (the number of minutes from 00:00), the value range is 1~1440, in minutes. |
|Type |String |True |`Period` |Scheduling cycle types. Optional values:<br><br><br>* Period: Scheduled at regular intervals, that is, scheduled once every certain period.<br><br>* Fixed: Regular scheduling, that is, scheduled at a fixed time point every day.<br><br>* Cron: Utilizes cron expressions. |
|CronTab |String |False |`0 18 * * *` |Cron expressions are used by the logging service to schedule alarm tasks to run at specified times. Cron expressions have a minimum granularity of one minute and use a 24\-hour clock format. For example, `0 18 * * *` means the alarm task executes daily at 18:00 sharp. |
|CronTimeZone |String |False |`GMT+0800` |Set the **Type** to `Cron`, and you will also need to set the time zone. For a list of common time zones, please refer to [Select Time Zone](https://docs.byteplus.com/docs/6470/1347854). |
|DayOfWeeks |Integer |False |`0` |Count from 0 (Sunday) to 6 (Saturday). |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyScheduleSqlTask HTTP/1.1
Content-Type: application/json
{
    "TaskName": "test2",
    "Description": "This is a test schedule sql task",
    "TopicID": "c5c6b3a7-c730-4527-8d5f-e527b381****",
    "DestRegion": "cn-shanghai",
    "DestTopicID": "66b42cb6-3436-44ae-97bf-efab3043****",
    "Status": 1,
    "ProcessStartTime": 1689042649,
    "RequestCycle": {
        "Type": "Period",
        "Time": 1
    },
    "ProcessTimeWindow": "@m-m,@m",
    "Query": "",
    "ProcessSqlDelay": 0
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|404 |ScheduleSqlTaskNotExist |Task %s does not exist. |The scheduled SQL analysis task does not exist. |
|500 |InternalServerError |We encountered an unexpected server error . Please try again later. |Internal server error. |


&nbsp;
