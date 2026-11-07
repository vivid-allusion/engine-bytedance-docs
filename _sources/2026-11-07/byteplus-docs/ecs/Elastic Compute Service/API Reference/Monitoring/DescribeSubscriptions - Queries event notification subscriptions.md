---
title: "DescribeSubscriptions - Queries event notification subscriptions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeSubscriptions"
---

Call the DescribeSubscriptions operation to query the list of event notification subscriptions.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSubscriptions&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|tMnfQ9">必选</span> `Sample value: DescribeSubscriptions`

The action that you want to perform. Value: DescribeSubscriptions.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|Gb9dot">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 20`

The number of entries returned on each page in a pagination query.


* Default value: 20

* Maximum value: 100

* Minimum value: 0



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**SubscriptionIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: SubscriptionIds.1=s-9ks1al1y9630lp******&SubscriptionIds.2=s-9ks1al1y9630lp******`

The subscription ID. A maximum of 100 subscription IDs is supported. To obtain subscription IDs, you can call [CreateSubscription](https://docs.byteplus.com/en/docs/ecs/CreateSubscription) to subscribe to event notifications or use this operation to query the list of subscribed notifications.


* Argument \- N: Specifies the serial number of the subscription ID.

* Separate multiple subscription IDs with `&`.



**Type** <span data-label="purple">string</span> `Optional` `Sample value: Notification`

The subscription type. Value:


* Notification: Message notification (SMS, email, internal message, and Feishu).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value: 6y6ug5ua2is5j0******`

The query credentials value returned by this call. If null is returned, this page is the last page.



**Subscriptions** <span data-label="purple">object[]</span> `Sample value: --`

The subscription list.


**CreatedAt** <span data-label="purple">string</span> `Sample value: 2022-11-18T19:11:46+08:00`

The creation time.



**EventTypes** <span data-label="purple">string[]</span> `Sample value: ["InstanceFailure:Succeeded", "AccountUnbalanced.Delete:Succeeded"]`

The list of event types.



**Id** <span data-label="purple">string</span> `Sample value: s-7uw3fs5vj0******`

The subscription ID.



**Type** <span data-label="purple">string</span> `Sample value: Notification`

The subscription type.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2022-11-18T20:11:57+08:00`

Update time.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeSubscriptions&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "DescribeSubscriptions",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "Subscriptions": [
            {
                "Id": "s-7uw3fs5vj0******",
                "EventTypes": ["AccountUnbalanced.Stop:Succeeded", "FileSystemReadOnly.Change:Succeeded"],
                "Type": "Notification",
                "CreatedAt": "2022-11-18T19:11:46+08:00",
                "UpdatedAt": "2022-11-18T20:11:57+08:00"
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
|400 |LimitExceeded.MinimumMaxResults |The number of specified MaxResults exceeds the minimum limit. |The value specified for MaxResults exceeds the lower limit. |
|400 |LimitExceeded.MaximumSubscriptionIds |The number of specified SubscriptionIds exceeds the maximum limit. |The number of specified subscription IDs exceeds the upper limit. |
|400 |LimitExceeded.MaximumMaxResults |The number of specified MaxResults exceeds the maximum limit. |The value specified for MaxResults exceeds the upper limit. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified value of Type is invalid. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
