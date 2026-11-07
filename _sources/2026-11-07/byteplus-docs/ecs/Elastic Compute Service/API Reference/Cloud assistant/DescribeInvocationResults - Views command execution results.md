---
title: "DescribeInvocationResults - Views command execution results"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInvocationResults_-_View_command_execution_results"
---

Call the DescribeInvocationResults operation to view the execution results of one or more tasks.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInvocationResults&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|xpnBQ2">必选</span> `Sample value: DescribeInvocationResults`

The action that you want to perform. Value: DescribeInvocationResults.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|IW9cVG">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**InvocationId ** <span data-label="purple">string </span><span data-api-tag="require|g38mpc">必选</span> `Sample value: ivk-hz0jdfwd9f****`

The job ID. You can call the [DescribeInvocations](https://docs.byteplus.com/en/docs/ecs/DescribeInvocations_-_Query_task_list) operation to query and obtain the job ID.



**InstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: i-bp1i7m****`

The instance ID.



**CommandId ** <span data-label="purple">string </span>`Optional` `Sample value: cmd-hz0jdfwcsr****`

The command ID.



**InvocationResultStatus ** <span data-label="purple">string </span>`Optional` `Sample value: Running`

The execution status of the command in one instance. Valid values:


* Pending: Initial status, indicating command execution is waiting for scheduling.

* Running: Command is being executed.

* Success: Command execution completes successfully.

* Failed: Command execution completes but fails.

* Timeout: Command execution times out.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries returned on each page in a pagination query.



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 100`

The total number of execution results.



**InvocationResults ** <span data-label="purple">object[] </span>`Sample value: --`

The information on command execution results that meet the conditions.


**ErrorMessage ** <span data-label="purple">string </span>`Sample value: Task execution timeout`

The error code of command execution failure.



**InvocationResultId ** <span data-label="purple">string </span>`Sample value: ivr-ycidmmvbm****`

The ID of the task execution result.



**InvocationId ** <span data-label="purple">string </span>`Sample value: ivk-ycidmmvbm9l8j****`

The ID of the executed task.



**CommandId ** <span data-label="purple">string </span>`Sample value: cmd-ybtvqkikdih96z8****`

The command ID.



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ychq95dknz5pk****`

The instance ID.



**InvocationResultStatus ** <span data-label="purple">string </span>`Sample value: Running`

The status of the command progress in one instance.



**Username ** <span data-label="purple">string </span>`Sample value: root`

The username for command execution in the instance.



**Output ** <span data-label="purple">string </span>`Sample value: success`

The output when a Base64\-encoded command is executed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Returned Base64\-encoded command execution information, up to 16 KB.</div>




**ExitCode ** <span data-label="purple">integer </span>`Sample value: 0`

The exit status code after the script is executed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a Linux instance, the exit code of a Shell command is its exit status.</div>




**ErrorCode ** <span data-label="purple">string </span>`Sample value: TaskExecutionTimeout`

Error codes displayed when command execution fails. Value:


* TaskDeliveryTimeout: Indicates that command delivery times out.

* TaskExecutionTimeout: Indicates that command execution times out.

* TaskExecutionFailed: Indicates that command execution fails.



**StartTime ** <span data-label="purple">string </span>`Sample value: 2023-06-30T09:00:45Z`

The time when the command execution begins in the instance.



**EndTime ** <span data-label="purple">string </span>`Sample value: 2023-07-01T09:00:45Z`

The time when the command execution is completed.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Version=2020-04-01&Action=DescribeInvocationResults&InvocationId=ivk-ycmpp**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json

{
    "ResponseMetadata": {
        "RequestId": "2023083016*****",
        "Action": "DescribeInvocationResults",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageSize": 10,
        "PageNumber": 1,
        "TotalCount": 1,
        "InvocationResults": [
            {
                "InvocationResultId": "ivr-ycmppwq****",
                "InvocationId": "ivk-ycmpp*****",
                "CommandId": "cmd-ycmpnj****",
                "InstanceId": "i-ycmd005****",
                "InvocationResultStatus": "Success",
                "Username": "root",
                "Output": "aGVsbG8gd29ybGQh",
                "ExitCode": 0,
                "StartTime": "2022-08-29T09:10:16Z",
                "EndTime": "2022-08-29T09:10:16Z",
                "ErrorCode": "",
                "ErrorMessage": ""
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
|400 |MissingParameter.InvocationId |The required InvocationId is not supplied. |The job ID cannot be empty. |
|400 |InvalidInvocationResultStatus.Malformed |The specified InvocationResultStatus is malformed. |The specified execution status of the command in the instance is invalid. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
