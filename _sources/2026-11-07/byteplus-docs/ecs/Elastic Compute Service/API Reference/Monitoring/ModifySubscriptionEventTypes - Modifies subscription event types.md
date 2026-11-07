---
title: "ModifySubscriptionEventTypes - Modifies subscription event types"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifySubscriptionEventTypes"
---

Call the ModifySubscriptionEventTypes operation to modify subscription event types.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifySubscriptionEventTypes&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|vqsmCc">必选</span> `Sample value: ModifySubscriptionEventTypes`

The action that you want to perform. Value: ModifySubscriptionEventTypes.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|ktm7G8">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**EventTypes.N** <span data-label="purple">string[]</span> `Optional` `Sample value: EventTypes.1=DiskError.Redeploy:Inquiring&EventTypes.2=RebootInstance:Executing`

The event type. Up to 100 event types are supported. When this parameter is left empty or not provided, this indicates cancelling the subscription.


* Argument \- N: specifies the serial number of the event type.

* Separate multiple event types with &.

* Refer to [Subscribing to and modifying event types](https://docs.byteplus.com/en/docs/ecs/Subscribe_to_and_modify_event_types) for the value range details.



**SubscriptionId** <span data-label="purple">string</span> <span data-api-tag="require|AlNDNe">必选</span> `Sample value: s-6js1al1y9665lp******`

The subscription ID. To obtain subscription IDs, you can call [CreateSubscription](https://docs.byteplus.com/en/docs/ecs/CreateSubscription) to subscribe to event notifications or [DescribeSubscriptions](https://docs.byteplus.com/en/docs/ecs/DescribeSubscriptions) to query the list of subscribed notifications.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SubscriptionId** <span data-label="purple">string</span> `Sample value: s-oko349s7sie9m9j******`

The subscription ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifySubscriptionEventTypes&Version=2020-04-01&EventTypes.1=SystemFailure.Stop:Succeeded&EventTypes.2=SystemFailure.Stop:Succeeded&SubscriptionId=s-6js1al1y9665lp****** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20210611144510010225243100005******",
        "Action": "ModifySubscriptionEventTypes",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "SubscriptionId": "s-4shu38sa4mjx******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidEventTypes.Malformed |The specified EventTypes is malformed. |One or more specified event types are invalid. |
|400 |LimitExceeded.MaximumEventTypes |The number of specified EventTypes exceeds the maximum limit. |The number of specified event types exceeds the upper limit. |
|400 |MissingParameter.SubscriptionId |The required parameter SubscriptionId is not supplied. |The parameter SubscriptionId cannot be left empty. |
|404 |InvalidSubscription.NotFound |The specified subscription does not exist. |The specified subscription does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
