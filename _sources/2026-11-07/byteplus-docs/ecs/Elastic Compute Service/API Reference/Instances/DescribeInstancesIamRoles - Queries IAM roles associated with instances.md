---
title: "DescribeInstancesIamRoles - Queries IAM roles associated with instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInstancesIamRoles"
---

Call the DescribeInstancesIamRoles operation to query the IAM roles that are associated with one or more ECS instances.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstancesIamRoles&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|go6go4">必选</span> `Sample value: DescribeInstancesIamRoles`

The operation that you want to perform. Valid value: DescribeInstancesIamRoles.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|xOndXy">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: InstanceIds.1=i-cm9tn4z1eohuu4d3****&InstanceIds.2=i-3tiegs1y963vj0****`

The instance ID. A maximum of 100 instance IDs are supported.


* Parameter \- N: specifies the serial number of the instance.

* Multiple instance IDs are separated by &.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of rows per page when you set up a pagination query.


* Maximum value: 100

* Default value: 10



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstancesIamRoles** <span data-label="purple">object[]</span> `Sample value: --`

The collection of IAM roles that meet the conditions.


**InstanceId** <span data-label="purple">string</span> `Sample value: i-3thhlu8byl4bwbha****`

The instance ID.



**RoleNames** <span data-label="purple">string[]</span> `Sample value: ["EcsTestRole"]`

The name of the IAM role associated with the instance.




**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeInstancesIamRoles&Version=2020-04-01&InstanceIds.1=i-cm9tn4z1eohuu4d3**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021110417394001022514606307******",
        "Action": "DescribeInstancesIamRoles",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstancesIamRoles": [
            {
                "InstanceId": "i-cm9tn4z1eohuu4d3****",
                "RoleNames": [
                    "EcsTestRole"
                ]
            }
        ],
        "NextToken": ""
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |LimitExceeded.MaximumInstanceIds |You've reached the limit on the number of InstanceIds that you can set. |The specified number of InstanceIds exceeds the maximum limit. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |You have exceeded the rate limit for resource requests. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
