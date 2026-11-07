---
title: "Request content for an event alert callback"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Content-of-a-webhook-request-of-the-event-type"
---

When an event rule is triggered and an aggregation condition for sending an alert notification is met, Cloud Monitor sends a POST request to the specified URL through the alert callback API. The request content for an event alert callback includes the callback request header and the callback request body.

<span id="01ad48d6"></span>
## Callback request header


|**Header Key** |**Header Value** |**Descriptions** |
|---|---|---|
|x\-volc\-trace\-id |Random UUID |This parameter is used for tracing the request. |
|x\-volc\-event\-id |{ event_id } |The event ID. |


<span id="2d375197"></span>
## Callback request body

<span id="71911fbe"></span>
### Data type

The request body is of the `application/json` data type.

<span id="282456e1"></span>
### Request body parameters


|**Parameters** |**Type** |**Sample value** |**Descriptions** |
|---|---|---|---|
|Type |String |Event |The alert type. Valid values:<br><br><br>* Event: the event alert<br><br>* Metric: the threshold alert |
|AccountId |String |21\*\*\*\*\*\*\*53 |The account ID. |
|Region |String |cn\-guangzhou |The region. |
|Source |String |ecs |The event source, which is the service type. |
|ProjectName |String |default |The project name. |
|Id |String |1658\*\*\*\*\*04000 |The unique ID of the event. |
|EventType |String |ecs:Disk:DiskError.Redeploy.Executing |The event name. |
|DescriptionCN |String |The disk is abnormal. Instance redeployment: in progress. |The event name in Chinese. |
|HappenedAt |Int64 |1664332705 |The time when the event occurs. |
|Details |Object |\- |The original event text. |
|Rules |Object |\- |The details of the event rule. For the specific format, refer to the **Rule structure** section of this topic. |


**Rule structure**


|**Parameters** |**Type** |**Sample value** |**Descriptions** |
|---|---|---|---|
|RuleId |String |1574\*\*\*\*\*\*\*\*\*\*8880 |The policy ID. |
|RuleName |String |Test event alert 1 |The policy name. |
|Level |String |notice |The alert level. Valid values:<br><br><br>* critical<br><br>* warning<br><br>* notice |


<span id="36dc027b"></span>
### Sample request body

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can ignore parameters without descriptions in the received request body. These parameters do not prevent you from obtaining the details of the alert notification.</div>


* <div data-tips="true" data-tips-type="tip">The Details field includes fixed fields and extended fields.</div>


   * <div data-tips="true" data-tips-type="tip">Fixed fields include specversion, id, source, type, volcpublishtime, volcregion, volcaccountid, volceventbusname, volcanresourcename, subject, and time. The fixed fields will be displayed even if they are left empty.</div>


   * <div data-tips="true" data-tips-type="tip">Extended fields: Apart from the fixed fields, all other fields are extended fields. Extended fields are custom fields defined by cloud services for specific event types.</div>



```JSON
{
    "Type":"Event",
    "AccountId":"21*****53",
    "Source":"ecs",
    "ProjectName":"default",
    "Id":"1658*****04000",
    "EventType":"ecs:Disk:DiskError.Redeploy.Executing",
    "DescriptionCN":"DiskError.Redeploy.Executing",
    "HappenedAt":1664332705,
    "Region":"cn-guangzhou",
    "Details":{
        "specversion":"1.0",
        "id":"1658*****04000",
        "source":"ecs",
        "type":"ecs:Disk:DiskError.Redeploy.Executing",
        "volcpublishtime":"2023-05-16T14:23:26+08:00",
        "volcregion":"cn-guangzhou",
        "volcaccountid":"21*****53",
        "volceventbusname":"default",
        "volcresourcename":"test_resource_name_A",
        "subject":"ecs:cn-north-1:21*****53:instance/test-instanceId-A/tag/test-instanceId-B",
        "time":"2023-05-16T14:23:26+08:00",
        "data":{
            "kafka":"kafka-boe"
        },
        "biz":"event_center_to_kafka",
        "sasl_user":"event_producer"
    },
    "Rules":[
        {
            "RuleId":"1574**********8880",
            "RuleName":"Test event alert 1",
            "Level":"notice"
        },
        {
            "RuleId":"1574**********8881",
            "RuleName":"Test event alert 2",
            "Level":"warning"
        }
    ]
}
```
