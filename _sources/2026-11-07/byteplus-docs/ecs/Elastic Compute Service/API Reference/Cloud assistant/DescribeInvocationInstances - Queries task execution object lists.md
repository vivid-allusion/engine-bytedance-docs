---
title: "DescribeInvocationInstances - Queries task execution object lists"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInvocationInstances_-_Query_the_task_execution_object_list"
---

Call the DescribeInvocationInstances operation to query the list of task execution objects.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInvocationInstances&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|MnkiyT">必选</span> `Sample value: DescribeInvocationInstances`

The action that you want to perform. Value: DescribeInvocationInstances.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|AEdFDk">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InvocationId** <span data-label="purple">string</span> <span data-api-tag="require|f70oT3">必选</span> `Sample value: ivk-hz0jdfwd9f****`

The task ID. You can call the [DescribeInvocations](https://docs.byteplus.com/en/docs/ecs/DescribeInvocations_-_Query_task_list) operation to query and obtain the task ID.



**InstanceId** <span data-label="purple">string</span> `Optional` `Sample value: i-bp1i7gg2em****`

The instance ID.



**PageNumber** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1~100.

* Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber** <span data-label="purple">integer</span> `Sample value: 1`

The current page number.



**PageSize** <span data-label="purple">integer</span> `Sample value: 10`

The number of entries returned on each page in a pagination query.



**TotalCount** <span data-label="purple">integer</span> `Sample value: 100`

The total number of execution results.



**InvocationInstances** <span data-label="purple">object[]</span> `Sample value: --`

The information about execution objects that meet the criteria.


**InvocationId** <span data-label="purple">string</span> `Sample value: i-bp1i7gg30r52z2em****`

The job ID.



**InstanceId** <span data-label="purple">string</span> `Sample value: i-bp1i7gg30r52z2em****`

The instance ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Version=2020-04-01&Action=DescribeInvocationInstances&InvocationId=ivk-ycmp***** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id="87o8SVhA"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308301616355A86D*******",
        "Action": "DescribeInvocationInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "InvocationInstances": [
            {
                "InvocationId": "ivk-ycmpp*****",
                "InstanceId": "i-ycmd0******"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common Error Codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |MissingParameter.InvocationId |The required InvocationId is not supplied. |The job ID cannot be empty. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
