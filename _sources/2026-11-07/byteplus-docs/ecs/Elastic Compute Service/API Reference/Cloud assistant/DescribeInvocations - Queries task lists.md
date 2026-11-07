---
title: "DescribeInvocations - Queries task lists"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInvocations_-_Query_task_list"
---

Call the DescribeInvocations operation to query the execution list and status of tasks.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

You can query the execution information of the last 60 days, and the maximum retention of execution information is 5000 entries.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInvocations&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|l3nXpn">必选</span> `Sample value: DescribeInvocations`

The action that you want to perform. Value: DescribeInvocations.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|c2eov9">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The project to which the resource belongs. A resource can only belong to one project.



**InvocationId** <span data-label="purple">string</span> `Optional` `Sample value: ivk-hz0jdfwd9f****`

The task execution ID.



**InvocationName** <span data-label="purple">string</span> `Optional` `Sample value: test`

The name of the executed task. Fuzzy search is supported.



**CommandId** <span data-label="purple">string</span> `Optional` `Sample value: cmd-hz0jdfwcsr****`

The command ID. You can call the [DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list) operation to query and obtain command IDs.



**CommandName** <span data-label="purple">string</span> `Optional` `Sample value: CommandTestName`

The command name. Fuzzy search is supported.



**CommandType** <span data-label="purple">string</span> `Optional` `Sample value: Shell`

The command type. Value:


* Shell (default): Indicates creating a Shell script that runs in a Linux instance.

* Python: Indicates creating a Python script.



**RepeatMode** <span data-label="purple">string</span> `Optional` `Sample value: Once`

The job execution mode. Value:


* Once: The job is executed immediately.

* Rate: The job is executed periodically.

* Fixed: The job is executed at the specified time.



**InvocationStatus** <span data-label="purple">string</span> `Optional` `Sample value: Success`

The job status. This parameter is determined by the command execution status of all instances specified by the job. Value:


* Pending: The command is waiting for verification and scheduling. If the command execution status of any instance is "Pending", the job status is "Pending".

* Scheduled: The periodically executed job (Rate) is successfully scheduled and is waiting for execution. If the command execution status of any instance is "Scheduled", the job status is "Scheduled".

* Running: The job execution is in progress. If the command execution status of any instance is "Running", the job status is "Running".

* Success: If the command execution status of all instances is "Success", the job execution status is "Success".

* Failed: If the command execution status of all instances is "Failed", the job execution status is "Failed".

* Stopped: A job in scheduled or periodic execution mode is manually stopped.

* PartialFailed: Some instances fail to execute the command in an immediately executed job.

* Finished: The job in periodic execution mode has been executed.



**PageNumber** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1~100.

* Default value: 10.



**ContentEncoding** <span data-label="purple">string</span> `Optional` `Sample value: Base64`

Specifies the encoding method for the returned command content. Value:


* PlainText: The command content is not Base64 encoded.

* Base64: The command content is Base64 encoded.



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with ampersands (&).

* Tag keys must be unique.



**TagFilters.N.Values.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The specified tag value when querying resources based on tags.


* The first N: specifies the serial number of the tag key. Value range: 1–10.

* The second N: specifies the serial number of the tag key. Value range: 1–3. You can query up to three tag values of the same tag key.

* Separate multiple key values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize** <span data-label="purple">integer</span> `Sample value: 1`

The number of entries per page.



**PageNumber** <span data-label="purple">integer</span> `Sample value: 10`

The page number of the query result.



**TotalCount** <span data-label="purple">integer</span> `Sample value: 17`

The total number of executed tasks.



**Invocations** <span data-label="purple">object[]</span> `Sample value: --`

The information of the executed job that meets the condition.


**Frequency** <span data-label="purple">string</span> `Sample value: 1d`

The execution frequency. When `RepeatMode=Rate`, the execution cycle is specified via the Rate expression.


* Format: <execution interval value\><execution interval unit\>.

* Supported units of the execution interval: minute (m), hour (h), and day (d).



**RepeatMode** <span data-label="purple">string</span> `Sample value: Rate`

The command execution mode.



**CommandProvider** <span data-label="purple">string</span> `Sample value: BytePlus`

The provider of the invoked command.



**CommandDescription** <span data-label="purple">string</span> `Sample value: Upgrade command.`

The description of the invoked command.



**EnableParameter** <span data-label="purple">boolean</span> `Sample value: true`

Indicates whether the invoked command enables the custom parameter feature. Value:


* true: Enabled.

* false: Not enabled.



**InstanceNumber** <span data-label="purple">integer</span> `Sample value: 3`

The number of instances (execution objects).​



**EndTime** <span data-label="purple">string</span> `Sample value: 2022-11-10T06:50:59Z`

The task end time.



**StartTime** <span data-label="purple">string</span> `Sample value: 2022-11-10T06:49:59Z`

The task start time.



**Timeout** <span data-label="purple">integer</span> `Sample value: 60`

The maximum timeout duration for the created command running on the ECS instance. Unit: seconds.



**WorkingDir** <span data-label="purple">string</span> `Sample value: /home`

The command execution path.



**Username** <span data-label="purple">string</span> `Sample value: root`

The user name for executing the command in the ECS instance.



**Parameters** <span data-label="purple">string</span> `Sample value: {\"username\":\"root\",\"password\":\"111@123\"}`

Custom parameters in the command.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This indicates parameters passed in when you execute commands by calling InvokeCommand or RunCommand.</div>




**CommandContent** <span data-label="purple">string</span> `Sample value: IyEvYmluL2Jhc****gdXBkYXRl`

The command content.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The returned command content is based on the value of the <code>ContentEncoding</code> parameter in the request parameters in the corresponding encoding format.</div>




**InvocationStatus** <span data-label="purple">string</span> `Sample value: Stopped`

The overall execution status of the command, which depends on the execution statuses of all instances in this invocation.



**CommandType** <span data-label="purple">string</span> `Sample value: Shell`

The command type triggered by the job.



**CommandName** <span data-label="purple">string</span> `Sample value: Change login password of Linux instance`

The name of the command for the task execution after the task is triggered.



**CommandId** <span data-label="purple">string</span> `Sample value: cmd-ybtvqkikdih96****`

The command ID.



**InvocationDescription** <span data-label="purple">string</span> `Sample value: Upgrade Agent`

The task description.



**InvocationId** <span data-label="purple">string</span> `Sample value: ivk-ycicy97x4i5pkgw****`

The task execution ID.



**LaunchTime** <span data-label="purple">string</span> `Sample value: 2022-11-11T06:49:59Z`

The execution time.


* When `RepeatMode=Rate`, this indicates the first time the job is executed. The time format is RFC3339.

* When `RepeatMode=Fixed`, this indicates the time the job begins execution. The time format is RFC3339.



**RecurrenceEndTime** <span data-label="purple">string</span> `Sample value: 2022-11-21T06:49:59Z`

The cycle end time. This parameter is required only for periodic tasks (Rate). Format: RFC3339.



**ProjectName** <span data-label="purple">string</span> `Sample value: default`

The associated project.



**ParameterDefinitions** <span data-label="purple">object[]</span> `Sample value: --`

The custom parameter definition.


**Name** <span data-label="purple">string</span> `Sample value: Param`

The custom parameter name.



**Type** <span data-label="purple">string</span> `Sample value: String`

The custom parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (number) type.



**Required** <span data-label="purple">boolean</span> `Sample value: true`

Indicates whether the parameter is required. Value:


* true: Required.

* false: Not required.



**DefaultValue** <span data-label="purple">string</span> `Sample value: DefaultValue`

The default value of the custom parameter.



**MinLength** <span data-label="purple">integer</span> `Sample value: 1`

The minimum length of the custom parameter value (string).



**MaxLength** <span data-label="purple">integer</span> `Sample value: 50`

The maximum length of the custom parameter value (string).



**MinValue** <span data-label="purple">string</span> `Sample value: 10`

The minimum value (number) of the custom parameter.



**MaxValue** <span data-label="purple">string</span> `Sample value: 100`

The maximum value (number) of the custom parameter.



**DecimalPrecision** <span data-label="purple">integer</span> `Sample value: 2`

The number of decimal places allowed for the custom parameter value (number).




**Tags** <span data-label="purple">object[]</span> `Sample value: --`

The tag.


**Key** <span data-label="purple">string</span> `Sample value: Key1`

The tag name.



**Value** <span data-label="purple">string</span> `Sample value: Value1`

The tag value.




**InvocationName** <span data-label="purple">string</span> `Sample value: job-1`

The task name.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeInvocations&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202409061635234DA7C33EBA49099*****", 
        "Action": "DescribeInvocations", 
        "Version": "2020-04-01", 
        "Service": "ecs", 
        "Region": "cn-beijing"
    }, 
    "Result": {
        "PageNumber": 1, 
        "PageSize": 10, 
        "TotalCount": 1, 
        "Invocations": [
            {
                "InvocationId": "ivk-yddq****", 
                "InvocationName": "test", 
                "InvocationDescription": "", 
                "CommandId": "cmd-ezvd****, 
                "CommandName": "test", 
                "CommandType": "Shell", 
                "RepeatMode": "Once", 
                "Frequency": "", 
                "InvocationStatus": "Success", 
                "CommandContent": "bHM=", 
                "Parameters": "{}", 
                "Username": "root", 
                "WorkingDir": "/home", 
                "Timeout": 66, 
                "StartTime": "2024-09-06T06:53:21Z", 
                "EndTime": "2024-09-06T06:53:55Z", 
                "InstanceNumber": 1, 
                "EnableParameter": false, 
                "CommandDescription": "", 
                "CommandProvider": "", 
                "ParameterDefinitions": [ ], 
                "LaunchTime": "", 
                "RecurrenceEndTime": "", 
                "ProjectName": "default", 
                "Tags": []
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified command type is invalid. |
|400 |InvalidRepeatMode.Malformed |The specified RepeatMode is malformed. |The specified mode of command execution is invalid. |
|400 |InvalidInvocationStatus.Malformed |The specified InvocationStatus is malformed. |The status of the specified command is invalid. |
|400 |LimitExceeded.TagFilterKeys |You've reached the limit on the number of TagFilter Keys that you can set. |The upper limit of the number of tag filter keys is reached. |
|400 |MissingParameter.TagKey |The required parameter TagFiltersKey is not supplied. |The tag filter key cannot be empty. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidRegion |Service [ecs] is not available in region [cn\-beijing300]. |The specified region is invalid. |
|400 |InvalidArgument |InvalidArgument |The parameter is invalid. |
|400 |InvalidCommandType.Malformed |InvalidCommandType.Malformed |The specified command type is invalid. |
|400 |InvalidTagFilterKey.Malformed |InvalidTagFilterKey.Malformed |The specified tag key is invalid. |
|400 |InvalidTagFilterValue.Malformed |InvalidTagFilterValue.Malformed |The specified tag value is invalid. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
