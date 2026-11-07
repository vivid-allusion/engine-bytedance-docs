---
title: "ModifySystemEventDefaultAction - Modifies default O&M operations of events"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifySystemEventDefaultAction_-_Modify_the_default_operations_and_maintenance_actions_for_events"
---

Call the ModifySystemEventDefaultAction operation to modify the default O&M operation of an event.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifySystemEventDefaultAction&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|jRJTZJ">必选</span> `Sample value: ModifySystemEventDefaultAction`

The action that you want to perform. Value: ModifySystemEventDefaultAction.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|THFMSg">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**EventId** <span data-label="purple">string</span> <span data-api-tag="require|Wm9TKK">必选</span> `Sample value: e-3ti9101aju3vj0***`

The event ID. You can use the [event notification feature](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications) or call the [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) operation to query and obtain the event ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, this operation is supported only for a <code>DiskErrorDetected</code> event in the <code>Inquiring</code> status.</div>




**DefaultAction** <span data-label="purple">string</span> <span data-api-tag="require|OjyaXy">必选</span> `Sample value: Redeploy`

The default O&M operation for the event. Valid values:


* Redeploy: Indicates redeployment.

* ReplaceDisk: Indicates disk replacement.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This operation is not supported for local volumes partitioned via LVM or SRIOV   </div>
   



**OperatedStartAt** <span data-label="purple">string</span> `Optional` `Sample value: 2023-06-28T18:11:46+08:00`

The end time of the O&M time window for the event.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of the <code>DefaultAction</code> parameter is <code>Redeploy</code>, the value of this parameter is required in the RCF3339 format.</div>




**OperatedEndAt** <span data-label="purple">string</span> `Optional` `Sample value: 2023-06-29T18:29:38+08:00`

The start time of the O&M time window for the event.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of the <code>DefaultAction</code> parameter is <code>Redeploy</code>, the value of this parameter is required in the RCF3339 format.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**EventId** <span data-label="purple">string</span> `Sample value: e-3ti9101aju3vj0***`

The event ID.



**RelatedEventId** <span data-label="purple">string</span> `Sample value: e-98islk8pjuks9i***`

The event ID associated with the event.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifySystemEventDefaultAction&Version=2020-04-01&DefaultAction=Redeploy&EventId=e-3ti9101aju3vj0***&OperatedStartAt=2023-06-28T18:29:38+08:00&OperatedEndAt=2023-06-29T18:11:46+08:00 HTTP/1.1
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
        "Action": "ModifySystemEventDefaultAction",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "EventId": "e-3ti9101aju3vj0***",
        "RelatedEventId": "e-98islk8pjuks9i***"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDefaultAction.Malformed |The specified DefaultAction is malformed. |The specified value of DefaultAction is invalid. |
|400 |InvalidDefaultAction.Unsupported |The event related instance does not support the default action. |The instance associated with the system event does not support the default O&M operation. |
|400 |InvalidOperatedEndAt.Malformed |The specified OperatedEndAt is malformed. |The specified value of OperatedEndAt is invalid. |
|400 |InvalidOperatedStartAt.Malformed |The specified OperatedStartAt is malformed. |The specified value of OperatedStartAt is invalid. |
|400 |InvalidSystemEventTypeOrStatus.Unsupported |The specified system event type or status does not support set default action. |The type or status of the specified event does not support the default O&M operation. |
|400 |MissingParameter.DefaultAction |The required parameter DefaultAction is not supplied. |The parameter DefaultAction cannot be left empty. |
|400 |MissingParameter.EventId |The required parameter EventId is not supplied. |The parameter EventId cannot be left empty. |
|404 |InvalidSystemEvent.NotFound |The specified system event does not exist. |The system event does not exist. |
|409 |InvalidSystemEvent.Conflict |The default action for specified system event already set. |The default O&M operation for the specified event already exists. |
