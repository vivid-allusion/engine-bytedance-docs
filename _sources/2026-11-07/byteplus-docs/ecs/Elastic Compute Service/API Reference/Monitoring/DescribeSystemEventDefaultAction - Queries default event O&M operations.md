---
title: "DescribeSystemEventDefaultAction - Queries default event O&M operations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeSystemEventDefaultAction_-_Query_the_default_maintenance_actions_for_events"
---

Call the DescribeSystemEventDefaultAction operation to query the default O&M operations of events.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSystemEventDefaultAction&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|2T4OgL">必选</span> `Sample value: DescribeSystemEventDefaultAction`

The action that you want to perform. Value: DescribeSystemEventDefaultAction.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|TKBYZj">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**EventId** <span data-label="purple">string</span> <span data-api-tag="require|eJvUkV">必选</span> `Sample value: e-3ti9101aju3vj0***`

The event ID. You can use the event notification feature or call the [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) operation to query and obtain the event ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DefaultAction** <span data-label="purple">string</span> `Sample value: Redeploy`

The default O&M operation for the event. Valid values:


* Redeploy: Indicates redeployment

* ReplaceDisk: Indicates disk replacement



**EventId** <span data-label="purple">string</span> `Sample value: e-3ti9101aju3vj0***`

The event ID.



**RelatedSystemEvent** <span data-label="purple">object</span> `Sample value: --`

The system event information.


**Category** <span data-label="purple">string</span> `Sample value: ResourceEvent`

The system event category. Value:


* ResourceEvent: resource\-targeted event

* TaskEvent: task\-related event



**CreatedAt** <span data-label="purple">string</span> `Sample value: 2021-06-29T18:11:46+08:00`

The creation time of the system event.



**ExtraInfo** <span data-label="purple">object</span> `Sample value: {"VolumeId": "vol-3tiegs1y963vj***","DeviceName": "/dev/sda"}`

The extended information about the system event.



**Id** <span data-label="purple">string</span> `Sample value: e-3tiegs1y963vj0******`

The system event ID.



**ImpactLevel** <span data-label="purple">string</span> `Sample value: Info - information`

The impact level of the system event. Value:


* Critical \- severe level

* Warning \- warning level

* Info \- information



**OperatedEndAt** <span data-label="purple">string</span> `Sample value: 2022-08-30T15:11:46+08:00`

The start time of the O&M time window.



**OperatedStartAt** <span data-label="purple">string</span> `Sample value: 2022-09-10T18:11:46+08:00`

The end time of the O&M time window.



**ResourceId** <span data-label="purple">string</span> `Sample value: i-3tiegs1y963vj0******`

The resource ID.



**Status** <span data-label="purple">string</span> `Sample value: Executing`

The system event status.



**Type** <span data-label="purple">string</span> `Sample value: SystemFailure_Stop`

The system event type.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2021-06-29T18:11:46+08:00`

The update time of the system event.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeSystemEventDefaultAction&Version=2020-04-01&EventId=e-3ti9101aju3vj0*** HTTP/1.1
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
        "Action": "DescribeSystemEventDefaultAction",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "DefaultAction": "Redeploy",
        "EventId": "e-3ti9101aju3vj0***",
        "RelatedSystemEvent": {
                "Id": "e-3ti9101aju3vj0******",
                "Category": "ResourceEvent",
                "CreatedAt": "2022-06-15T16:34:34+08:00",
                "UpdatedAt": "2022-06-15T16:34:49+08:00",      
                "ResourceId": "i-3ti9101aju3vj0******",
                "Type": "DiskError_Redeploy",
                "OperatedStartAt": "2022-08-30T15:11:46+08:00",
                "OperatedEndAt": "2022-09-10T18:11:46+08:00",
                "ExtraInfo": {
                       "DeviceName": "/dev/sda",
                       "VolumeId": "vol-3tiegs1y963vj0******"
                }
        },
        "NextToken": ""
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.EventId |The required parameter EventId is not supplied. |The parameter EventId cannot be left empty. |
|404 |InvalidSystemEvent.NotFound |The specified system event does not exist. |The system event does not exist. |
|404 |InvalidSystemEventDefaultAction.NotFound |The specified system event default action does not exist. |The default O&M operation for the specified event does not exist. |
