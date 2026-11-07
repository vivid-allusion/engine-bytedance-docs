---
title: "Content variables"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/content_variables"
---

When configuring alarm notification content, variables can be added besides fixed text strings. This document describes the variable format and the supported variable list.

<span id=".5Y-Y6YeP5qC85byP"></span>
## Variable format

Content variables can be directly referenced in alarm notification content. The variable format is `{{variable name}}`, and the variable must be enclosed by double curly braces `{{ }}`. When Log Service sends alarm notifications, it automatically replaces variables in the notification content with the corresponding actual values. For example, for the content variable `{{AccountID}}`, Log Service replaces it with the BytePlus account ID of the current alarm policy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Variable names are case\-sensitive. When referencing variables in alarm notification content, the variable name must exactly match the <a href="https://docs.byteplus.com/docs/tls/content_variables#.5Y-Y6YeP5YiX6KGo">variable list</a>'s <strong>variable</strong> column.</div>


* <div data-tips="true" data-tips-type="tip">If the variable name or format is incorrect, Log Service replaces it with an empty string.</div>


* <div data-tips="true" data-tips-type="tip">If the referenced value is an object type, convert the format using the toJson or toString function, or iterate with a for loop; otherwise, the actual returned content may not meet expectations.</div>


* <div data-tips="true" data-tips-type="tip">If the referenced value is an array object type, you can access the child field value in the array object using the <code>{{a[i][j].b}}</code> format, for example, <code>{{QueryResult[0][0].count}}</code>.</div>



<span id=".5pSv5oyB55qE5YaF5a655Y-Y6YeP"></span>
## Supported content variables

<span id=".5Y-Y6YeP5YiX6KGo"></span>
### Variable list

The alarm notification content of the log service supports referencing the following variables.


|Variable |Type |Meaning |Example |
|---|---|---|---|
|{{AccountID}} |String |The account ID to which the alarm policy belongs. |* Configuration example:<br><br>   `The alarm in the {{AccoutID}} account has been triggered.`<br><br>* Alarm notification example:<br><br>   The alarm in the `20000****6` account has been triggered. |
|{{UserName}} |String |The username of the BytePlus account to which the alarm policy belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is not recommended to use this variable in content templates for Feishu, DingTalk, WeCom, and custom Webhook channels, because the variable value will be empty in these channels.</div><br> |* Configuration example:<br><br>   `An alarm has been triggered for user {{UserName}}.`<br><br>* Alarm notification example:<br><br>   An alarm has been triggered for user. |
|{{ProjectName}} |String |Log project that triggers the alarm. |* Configuration example:<br><br>   `The project {{ProjectName}} triggered an alarm.`<br><br>* Alarm notification example:<br><br>   The project `http_module` triggered an alarm. |
|{{AlarmTopicName}} |String |The log topic that triggers the alarm. |* Configuration example:<br><br>   `The log topic {{AlarmTopicName}} triggered an alarm.`<br><br>* Alarm notification example:<br><br>   The log topic `http_module` triggered an alarm. |
|{{NotifyMsg}} |String |The rendered content of the original text in the alarm policy’s **additional notification content**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This variable is only supported in content templates.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Using this variable in the alarm policy’s <strong>additional notification content</strong> is not recommended.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Alarm notifications for alarm recovery types do not support this variable.</div><br> |* Configuration example:<br><br>   `Alarm notification content: {{NotifyMsg}}.`<br><br>* Example of **additional notification content** in the alarm policy:<br><br>   `The log topic {{AlarmTopicName}} under the account {{AccoutID}} triggered an alarm.`<br><br>* Alarm notification example:<br><br>   Alarm notification content: the log topic `http_module` under account `20000****6` triggered an alarm. |
|{{Message}} |String |The original content filled in the **additional notification content** of the alarm policy.<br><br>Do not parse the input alarm variables; send the original content directly. |* Configuration example:<br><br>   `Original notification content: {{Message}}.`<br><br>* Example of **additional notification content** in alarm policy:<br><br>   `{{AccoutID}} account's {{AlarmTopicName}} triggered an alarm.`<br><br>* Alarm notification example:<br><br>   Original notification content: `{{AccoutID}} account's {{AlarmTopicName}} triggered an alarm.` |
|{{Region}} |String |The region where the alarm policy's associated project is located. |* Configuration example:<br><br>   `The alarm policy {{Alarm}} in region {{Region}} has been triggered.`<br><br>* Alarm notification example:<br><br>   The alarm policy `exceeding limit alarm` in region `cn-beijing` has been triggered. |
|{{Alarm}} |String |Alarm policy name. |* Configuration example:<br><br>   `alarm policy {{Alarm}} has been triggered.`<br><br>* Alarm notification example:<br><br>   alarm policy `Limit Exceeded Alarm` has been triggered. |
|{{AlarmID}} |String |Alarm policy ID. |* Configuration example:<br><br>   `The alarm policy {{AlarmID}} has been triggered.`<br><br>* Alarm notification example:<br><br>   The alarm policy `7070267f-30da-4861-8d0a-01f4bc6****` has been triggered. |
|{{ExecuteQuery}} |[]String |**Query statements** configured in the alarm policy. |* Configuration example:<br><br>   `The current alarm policy's query and analysis statement is {{toJson(ExecuteQuery)}}.`<br><br>* Alarm notification example:<br><br>   The current alarm policy's query and analysis statement is `["* \| select RemoteAddr, pv from (select RemoteAddr, sum(case when ReqTime > 1000 then 1 else 0 end) as pv group by RemoteAddr) order by pv desc"]`. |
|{{Duration}} |String |Duration of the alarm in minutes. |* Configuration example:<br><br>   `The alarm duration is {{Duration}} minutes.`<br><br>* Alarm notification example:<br><br>   Duration of the alarm is`3`minute. |
|{{Condition}} |String |The **trigger condition** configured in the alarm policy. |* configuration example:<br><br>   `the trigger condition of the current alarm policy is {{Condition}}.`<br><br>* alarm notification example:<br><br>   the trigger condition of the current alarm policy is `$1.pv >= 3`. |
|{{HappenThreshold}} |Integer |The **alarm sending interval** configured in the alarm policy. |* Configuration example:<br><br>   `This alarm policy triggers an alert after meeting the conditions for {{HappenThreshold}} consecutive monitoring cycles`<br><br>* Alarm notification example:<br><br>   This alarm policy continues`5`If a monitoring period meets the trigger conditions, an alarm is sent. |
|{{Topics}} |[]String |The `monitored objects` configured in the alarm policy, meaning all log topics currently monitored by this alarm policy. |* Configuration example:<br><br>   `The monitored log topics include {{Topics\|join:','}}.`<br><br>* Alarm notification example:<br><br>   The monitored log topics include `ycyc,abab`. |
|{{TopicIds}} |[]String |The IDs of all log topics monitored by the alarm policy. |* Configuration example:<br><br>   `The monitored log topics include {{TopicIds\|join:','}}.`<br><br>* Alarm notification example:<br><br>   The monitored log topics include `a573686e-d097-4227-9fa5-612d0ae2****,4a7796bd-76a5-45ec-880b-680c45cb****`. |
|{{StartTime}} |String |The first trigger time in a complete alarm event.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A complete alarm event spans from <strong>alert trigger</strong> to <strong>alert recovery</strong>, where <strong>alert recovery</strong> marks the end of this alarm event.</div><br> |* Configuration example:<br><br>   `The first alarm trigger time is {{StartTime}}.`<br><br>* Alarm notification example:<br><br>   The first alarm trigger time is `2022-12-09 20:43:16`. |
|{{StartTimeUnix}} |Integer |The timestamp of the first alarm triggered in the alarm event. Format as a UNIX timestamp in seconds. |* Configuration example:<br><br>   `The timestamp of the first alarm trigger is {{StartTimeUnix}}.`<br><br>* Alarm notification example:<br><br>   The timestamp of the first triggered alert is `1670589796`. |
|{{NotifyTime}} |String |This alarm notification's time. |* Configuration example:<br><br>   `Alarm notification time is {{NotifyTime}}.`<br><br>* Alarm notification example:<br><br>   Alarm notification time is `2022-12-09 20:43:16`. |
|{{NotifyTimeUnix}} |Integer |The timestamp of this alarm notification. Format is a second\-level UNIX timestamp. |* Configuration example:<br><br>   `The alarm notification timestamp is {{NotifyTimeUnix}}.`<br><br>* Alarm notification example:<br><br>   The alarm notification timestamp is `1670589796`. |
|{{NotifyType}} |Integer |Alarm notification type.<br><br><br>* 1: alarm triggered<br><br>* 2: alarm recovered |* Configuration example:<br><br>   `The alarm notification type is {{NotifyType}}.`<br><br>* Alarm notification example:<br><br>   The alarm notification type is`1`. |
|{{Severity}} |String |The `alarm level` configured in the alarm policy, indicating the severity of the alarm.<br><br><br>* notice: notification.<br><br>* warning: warning.<br><br>* critical: critical. |* Configuration example:<br><br>   `Alarm level is {{Severity}}.`<br><br>* Alarm notification example:<br><br>   Alarm level is `notice`. |
|{{ConsecutiveAlertNums}} |Integer |Number of consecutive alerts. |* Configuration example:<br><br>   `The number of consecutive alerts is {{ConsecutiveAlertNums}}.`<br><br>* Alert notification example:<br><br>   The number of consecutive alerts is`3`. |
|{{TriggerParams}} |[]String |The actual value corresponding to the field in the trigger condition when the alarm is triggered. |* Configuration example:<br><br>   `The actual value of the field in the trigger condition is {{toJson(TriggerParams)}}.`<br><br>* Alarm notification example:<br><br>   The actual value of the field in the trigger condition is `["$1.count=100"]`. |
|{{DetailUrl}} |String |Link to the execution information page of the alarm policy. For details, refer to [Execution History](https://docs.byteplus.com/docs/6470/103029#.5p-l55yL5omn6KGM5L-h5oGv). |* Configuration example:<br><br>   `Click the link {{DetailUrl}} to view the execution history.`<br><br>* Alarm notification example:<br><br>   Click the link `https://console.byteplus.com/tls/region:tls+cn-beijing/project/a573686e-d097-4227-9fa5-612d0ae2****/alarms/7070267f-30da-4861-8d0a-01f4bc6d5****detail` to view the execution history. |
|{{QueryUrl}} |String |The link to the query and analysis page for the first execution statement in the alarm policy. |* Configuration example:<br><br>   `Log query details: {{QueryUrl}}`<br><br>* Alarm notification example:<br><br>   Log query details: `https://console.byteplus.com/tls/region:tls+cn-beijing/project/0abbb4ff-9eba-4079-af37-eec515e0****/search?topicId=&time=now-5m,now&codebase64=&hideTitle=false&hideTopic=false&hideIndexBtn=false&hideShareBtn=false` |
|{{QueryResult}} |[][]Object |Retrieve the execution results of the query and analysis statement when an alarm is triggered. Object type; it is recommended to convert the format using toJson or toString. For details, refer to [{{QueryResult}}](https://docs.byteplus.com/docs/tls/content_variables#queryresult).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Each execution statement returns up to 10 rows of results, with a maximum total length of 10 KB. You can add up to 3 execution statements, with a maximum total length of 30 KB.</div><br> |Refer to [QueryResult](https://docs.byteplus.com/docs/tls/content_variables#queryresult) as an example. |
|{{QueryResultStr}} |[]String |Return QueryResult as a string array.<br><br>Index access is not supported, meaning `{{QueryResultStr[0]}}` is not supported. |Refer to the example in [QueryResult](https://docs.byteplus.com/docs/tls/content_variables#queryresult). |
|{{QueryLog}} |[][]Object |Original log information matching the retrieval condition in the execution statement, excluding the filtering conditions in the analysis statement. Object type, it is recommended to convert the format using toJson or toString. For details, please refer to [QueryLog](https://docs.byteplus.com/docs/tls/content_variables#querylog).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Each execution statement returns up to 1,000 raw logs, with a maximum length of 10 KB. You can add up to 3 execution statements, with a total maximum length of 30 KB.</div><br> |For examples, refer to [QueryLog](https://docs.byteplus.com/docs/tls/content_variables#querylog). |
|{{QueryLogStr}} |[]String |Returns QueryLog results as a string array. Index access is not supported, such as `{{QueryLogStr[0]}}`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Returns up to 1000 original logs, with a total size limit of 10 KB.</div><br> |Refer to [QueryLog](https://docs.byteplus.com/docs/tls/content_variables#querylog) for an example. |
|{{QueryStartTime}} |Integer |The start time of the last execution statement in the alarm policy, in seconds Unix timestamp format. Refer to [How to check the execution statement number?](https://docs.byteplus.com/docs/tls/create_alarm_policies#.5aaC5L2V5p-l55yL5omn6KGM6K-t5Y-l57yW5Y-377yf) for the method to view the execution statement number. |* Configuration example:<br><br>   `{{QueryStartTime}}`<br><br>* Alarm notification example:<br><br>   `1699411640` |
|{{QueryEndTime}} |Integer |The end time of the last execution statement in the alarm policy, formatted as a Unix timestamp in seconds. For how to check execution statement IDs, see [how to check execution statement IDs?](https://docs.byteplus.com/docs/tls/create_alarm_policies#.5aaC5L2V5p-l55yL5omn6KGM6K-t5Y-l57yW5Y-377yf) |* Configuration example:<br><br>   `{{QueryEndTime}}`<br><br>* alarm notification example:<br><br>   `1699412200` |
|{{Results}} |[]QueryData |Query parameters and intermediate results, array type, with a maximum length of 3. For details, please refer to the [QueryData structure](https://docs.byteplus.com/docs/tls/content_variables#db54611c). |* Configuration example:<br><br>   `The start time of the first query is {%set result0=Results[0]%}{{result0.StartTime}}, the end time is {{result0.EndTime}}; the count value is {{result0.RawResultsCount}}; the query and analysis statement is {{result0.Query}}. RawResults:{{toJson(result0.RawResults)}}, RawResultsCount:{{result0.RawResultsCount}}，FireResult:{{toJson(result0.FireResult)}}`.<br><br>* Alarm notification example:<br><br>   The start time of the first query is `1701676139`, the end time is `1701677039`; the count value is`1`; the query and analysis statement is `*\| select count(*) as cnt`. RawResults:`[{"cnt":"0"}]`, RawResultsCount:`1`，FireResult:`{"cnt":"0"}`. |
|{{FireResults}} |[]Object |The data that triggered the alarm, i.e. the result after set operations, up to 100 entries. The actual length of `FireResults` exceeding 2KB will be truncated. |* Configuration example:<br><br>   `The data triggering the alarm is {{toJson(FireResults)}}.`<br><br>* Alarm notification example:<br><br>   The data triggering the alarm is `[{"cnt":"0"}]`. |
|{{FireResultsCount}} |Integer |total data amount after set operations on the number of query and analysis results that trigger the alarm, possibly more than 100. |* Configuration example:<br><br>   `Total data count generated when the alarm triggers is {{FireResultsCount}}`.<br><br>* Alarm notification example:<br><br>   Total data count generated when the alarm triggers is `10`. |
|{{SignInUrl}} |String |Alarm detail page link. |* Configuration example:<br><br>   `Click {{SignInUrl}} to view alarm details.`<br><br>* Alarm notification example:<br><br>   Click `https://console-embedded.xxx.com/api/passport/login/loginWithSigninToken?signinToken=czVXb1M0djlpZ&redirectURI=%2Ftls%2Fregion%3Atls%2Bxxxxxxx` to view alarm details. |


<span id="db54611c"></span>
### QueryData structure

`Results` variable represents query parameters and intermediate results. The available variables for reference are as follows.


|Variable |Data type |Description |Example |
|---|---|---|---|
|TopicId |String |ID of the target log topic for query and analysis. |fed25df2\-cc27\-4b0a\-8ad2\-773aef61\*\*\*\* |
|Query |String |Query and analysis statement. |error |
|StartTime |Integer |Query start time, formatted as a 10\-digit Unix timestamp. |1699411640 |
|EndTime |Integer |Query the end time in a 10\-digit Unix timestamp format. |1699412200 |
|RawResults |[]Object |Actual query results in an array format, up to 100 rows. If the actual length of `RawResults` exceeds 2KB, the excess part will be truncated. |[{"cnt":"0"}] |
|RawResultsCount |Integer |Total number of actual query data entries, which may exceed 100. |1 |
|FireResult |Object |The log content that triggered the alarm. Multiple original logs may have triggered the alarm policy; this parameter only returns the first original log that triggered the alarm. |{"cnt":"0"} |


<span id="queryresult"></span>
### QueryResult

**Variable description**

`QueryResult` structure represents the execution result of the query statement triggered by an alarm. Supports the following configurations:


* Directly click **Insert Variable** in the console, then click `QueryResult` to insert `{{toJson(QueryResult)}}`. This variable returns the complete execution results matched by all current (up to 3) executed statements in JSON format, which may contain a large amount of irrelevant content.

* Process its properties further using function syntax to return only specified fields of the execution result.

   This variable returns as an object type. When accessing each property, use a dot (.) to specify its attribute, such as `{{log.name}}`, `{{log.name}}`, `{{QueryResult[0][0].count}}`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The execution results of query statements can also be returned as a string array ([]string). If needed, the variable <code>QueryResultStr</code> can be referenced.</div>


* <div data-tips="true" data-tips-type="tip">Each executed statement returns up to 10 rows, with a total maximum length of 10 KB. Up to 3 executed statements can be added, with a total maximum length of 30 KB.</div>



**Example of returning specified field variables**


* Return specified fields from the execution results matched by all current (up to 3) executed statements

   ```json
   {%-for Results in QueryResult%}
   {%- for Result in Results%}
   {{Result.name}}
   {{Result.type}} 
   {{Result.double_key}} 
   {{Result.obj_key.key}} 
   {{Result['obj_key.key_double.data']}}
   {%endfor-%}
   {%endfor-%}
   ```
   

* Return the specified field of the **first** execution result matched by the **first** execution statement

   ```json
   {{QueryResult[0][0].name}}
   {{QueryResult[0][0].type}} 
   {{QueryResult[0][0].double_key}} 
   {{QueryResult[0][0].obj_key.key}} 
   {{QueryResult[0][0]['obj_key.key_double.data']}} 
   ```
   

* Return the specified field of the **first** execution result matched by the **second** execution statement

   ```json
   {{QueryResult[1][0].name}}
   {{QueryResult[1][0].type}} 
   {{QueryResult[1][0].double_key}} 
   {{QueryResult[1][0].obj_key.key}} 
   {{QueryResult[1][0]['obj_key.key_double.data']}} 
   ```
   

* Example content of QueryResult:

   ```json
   [
     [
       {
         "double_key": 1.1,
         "name": "xxx",
         "obj_key": {
           "key": 1,
           "key_double": {
               "data": 123
               }
         },
         "type": 1
       }
     ]
   ]
   ```
   


<span id="querylog"></span>
### QueryLog

**Variable description**

The `QueryLog` structure represents the raw log information matched by the retrieval conditions in the execution statement, excluding filtering conditions in the analysis statement. The following configurations are supported:


* Directly click **Insert variable** in the console, then click `QueryLog` to insert `{{toJson(QueryLog)}}`. This variable returns the complete raw log information matched by all (up to 3) execution statements in JSON format, which may include a large amount of irrelevant content.

* Use function syntax to further process its properties, returning only specific fields of the raw log information.

   The `QueryLog` variable returns as a two\-dimensional object array type. Under normal circumstances, each field should be accessed using a period (.) to specify the field, for example, `{{log.name}}` and `{{log.name}}`. When a field name contains spaces, use the format `{{log['']}}`, such as `{{log['key name']}}`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The original logs corresponding to QueryLog can also be returned as a string array. If needed, you can reference the variable <code>QueryLogStr</code>.</div>


* <div data-tips="true" data-tips-type="tip">Each execution statement returns up to 1000 original logs, with a maximum total length of 10 KB. You can add up to 3 execution statements, with a combined maximum length of 30 KB.</div>



**Example of variables returning specified fields of original logs**


* Example of notification content configuration:

   * Return the specified fields of original log information matched by all current \*\*(up to 3)\*\* execution statements

      ```json
      {%-for logs in QueryLog%}
      {%- for log in logs%}
      {{log.name}}
      {{log.type}} 
      {{log.double_key}} 
      {{log.obj_key.key}} 
      {{log['obj_key.key_double.data']}}
      {%endfor-%}
      {%endfor-%}
      ```
      

   * Return the specified fields of the **first** original log record matched by the **first** execution statement

      ```json
      {{QueryLog[0][0].name}}
      {{QueryLog[0][0].type}} 
      {{QueryLog[0][0].double_key}} 
      {{QueryLog[0][0].obj_key.key}} 
      {{QueryLog[0][0]['obj_key.key_double.data']}} 
      ```
      

   * Return the specified fields of the **first** original log record matched by the **second** execution statement

      ```json
      {{QueryLog[1][0].name}}
      {{QueryLog[1][0].type}} 
      {{QueryLog[1][0].double_key}} 
      {{QueryLog[1][0].obj_key.key}} 
      {{QueryLog[1][0]['obj_key.key_double.data']}} 
      ```
      

* Example of QueryLog content:

   ```json
   [
     [
       {
         "double_key": 1.1,
         "name": "xxx",
         "obj_key": {
           "key": 1,
           "key_double": {
               "data": 123
               }
         },
         "type": 1
       }
     ]
   ]
   ```
   


<span id="244b43bd"></span>
## Filter

The log service alarm variables support adding filters. Filters are chained calls used for secondary processing of variable data.

The format of variable filters is `{{variable|filter}}`. For example, the output of `{{toJson(FireResults)}}` is`{"a":123,"b":123}`you can use `{{toJson(FireResults)|escapejs}}` for unicode encoding, resulting in `\\u007b\\u0022\\u0061\\u0022\\u003a\\u0031\\u0032\\u0033\\u002c\\u0022\\u0062\\u0022\\u003a\\u0031\\u0032\\u0033\\u007d`.

<span id="39477523"></span>
### Filter list


|Filter |Description |Example |
|---|---|---|
|escape |Automatically escape special characters.<br><br>If special characters that should be escaped in received alert notifications are not escaped, use this filter to forcibly escape all output of specified strings or variables. |* Example reference:<br><br>   `{{"<script>"\|escape}}`<br><br>* Processing result:<br><br>   `&lt;script&gt;` |
|escapejs |Encode special characters in Unicode.<br><br>If the alarm notification content contains special characters that need Unicode encoding, use this filter to encode those characters in a specified string or variable. For detailed instructions, please refer to [How to handle special characters in alarm notification content?](https://docs.byteplus.com/docs/6470/1219479#7721beeb) |* Example reference:<br><br>   `{{"<script> alert('hello')</script>"\|escapejs}}`<br><br>* Processing result:<br><br>   `\u003Cscript\u003E alert\u0028\u0027hello\u0027\u0029\u003C/script\u003E` |


<span id="f87303b3"></span>
### Filter examples

The following example adds operation sets, the count of operation sets, query results, and other information to the alarm notification, with a link to a no\-login alarm detail page appended at the end. The query results section returns detailed information including query result details, log topic ID, and query retrieval statements.

```JSON
Operation Set：{{toJson(FireResults)}}
Number of operation sets: {{FireResultsCount}}
Query results: {{replace("*","\\*",toJson(Results))}}
        {%set result = Results[0]%}
        TopicId: {{result.TopicId}}
        Query: {{replace("*","\\*",result.Query)}}
        StartTime: {{result.StartTime}}
        EndTime: {{result.EndTime}}
        RawResults: {{toJson(result.RawResults)}}
        RawResultsCount: {{result.RawResultsCount}}
        FireResult: {{toJson(result.FireResult)}}
Alarm details: {{SignInUrl}}
```
