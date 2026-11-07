---
title: "CreateSubscription - Subscribes to event notifications"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateSubscription"
---

Call the CreateSubscription operation to subscribe to system event notifications.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

For one `Type` (which indicates the subscription type), you can only subscribe to event notifications once by using this operation. To modify `EventTypes.N` (event type) of the specified `Type`, call the [ModifySubscriptionEventTypes](https://docs.byteplus.com/en/docs/ecs/ModifySubscriptionEventTypes) operation and pass in the subscription ID, which is the value of `SubscriptionId` in this operation.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateSubscription&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|2uh7cJ">必选</span> `Sample value: CreateSubscription`

The operation that you want to perform. Value: CreateSubscription.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|gYOc0G">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**EventTypes.N** <span data-label="purple">string[]</span> <span data-api-tag="require|qjdPmT">必选</span> `Sample value: EventTypes.1=SystemFailure.Stop:Succeeded&EventTypes.2=SystemFailure.Stop:Succeeded`

The event type. A maximum of 100 types is supported.


* Argument \- N: specifies the serial number of the event type.

* Separate multiple event types with &.

* Refer to [Subscribing to and modifying event types](https://docs.byteplus.com/en/docs/ecs/Subscribe_to_and_modify_event_types) for the value range details.



**Type** <span data-label="purple">string</span> <span data-api-tag="require|zk1c1e">必选</span> `Sample value: Notification`

The subscription type. Value:


* Notification: Message notification. Notification channels include SMS, email, internal message, and Feishu.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SubscriptionId** <span data-label="purple">string</span> `Sample value: s-4shu38sa4mjx******`

The subscription ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateSubscription&Version=2020-04-01&EventTypes.1=SystemFailure.Stop:Succeeded&EventTypes.2=SystemFailure.Stop:Succeeded&Type=Notification HTTP/1.1
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
        "Action": "CreateSubscription",
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
|400 |InvalidEventTypes.Malformed |The specified EventTypes is malformed. |The specified value of EventTypes is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified value of Type is invalid. |
|400 |LimitExceeded.MaximumEventTypes |The number of specified EventTypes exceeds the maximum limit. |The number of specified event types exceeds the upper limit. |
|400 |LimitExceeded.MaximumSubscriptions |You've reached the limit on the number of subscriptions that you can create. |The number of subscriptions exceeds the upper limit. Only one subscription of the same type can be created. |
|400 |MissingParameter.EventTypes |The required parameter EventTypes is not supplied. |The parameter EventTypes cannot be left empty. |
|400 |MissingParameter.Type |The required parameter Type is not supplied. |The parameter Type cannot be left empty. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
