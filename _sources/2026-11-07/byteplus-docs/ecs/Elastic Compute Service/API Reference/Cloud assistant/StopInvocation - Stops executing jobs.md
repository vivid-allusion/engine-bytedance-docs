---
title: "StopInvocation - Stops executing jobs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/StopInvocation_-_Stop_executing_tasks"
---

Call the StopInvocation operation to stop a job in the "Running" status.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* The processes of the specified command running on all target ECS instances are to be stopped.

* Only jobs in scheduled or periodic execution mode can be stopped.

* After the process of a scheduled or periodic job is stopped, commands that have already started continue to run, but no subsequent executions are triggered.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=StopInvocation&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|CymO2y">必选</span> `Sample value: StopInvocation`

The action that you want to perform. Value: StopInvocation.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|KUvhWx">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InvocationId** <span data-label="purple">string</span> <span data-api-tag="require|1jWcmN">必选</span> `Sample value: ivk-2a745b41****`

The ID of the executed task



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InvocationId** <span data-label="purple">string</span> `Sample value: ivk-2a745b41****`

The ID of the executed task.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=StopInvocation&Version=2020-04-01&InvocationId=ivk-2a745b41**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2023082415303301022514515207C4****",
        "Action":"StopInvocation",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
        "InvocationId":"ivk-2a745b41****"
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
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be empty. |
|400 |LimitExceeded.MaximumInstanceIds |The specified InstanceIds exceeds the limit. |The number of instances exceeds the limit. |
|400 |InvalidOperation.Forbidden |The specified Invocation is not allowed to operate. |The specified job is in an inoperable status. |
|400 |InvalidInvocationRunningInstance.NotFound |No instance with an ongoing invocation is found. |The instance in which the job is being executed is not found in the query. |
|404 |InvalidInvocation.NotFound |The specified Invocation does not exist. |The specified job does not exist. |
|404 |InvalidInvocationInstance.NotFound |The specified instance is not included in the invocation. |The job does not involve the specified instance. |
|409 |InvalidInstanceIds.Conflict |The specified InstanceId already exists. |The specified instance ID already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |


&nbsp;
