---
title: "Content of event alert callback requests"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Content_of_the_event_alert_callback_request"
---

The content of an event alert callback request includes callback request headers and the callback request body. [Learn more](https://docs.byteplus.com/en/docs/cloudmonitor/Content-of-a-webhook-request-of-the-event-type).

<span id="bSeiIZGw"></span>
## Callback request headers


|**Header key** |**Header value** |**Description** |
|---|---|---|
|x\-volc\-trace\-id |Random UUID |Used for request tracking. |
|x\-volc\-event\-id |{ event_id } |The event ID. |


<span id="abMA7SBe"></span>
## Callback request body

<span id="KGkGEN6j"></span>
### Data type

The data type of the request body is `application/json`.

<span id="yMOLSPbJ"></span>
### Request body parameters


|**Parameter​**  |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |Event |The alert type. Valid value: Event. |
|AccountId |String |210035\*\*\*\* |The account ID. |
|Region |String |cn\-beijing |The region. |
|Source |String |ecs |The event source, which is the product type. |
|ProjectName |String |default |The project name. |
|Id |String |194069710419630\*\*\*\* |The unique event ID. |
|EventType |String |ecs:Disk:DiskError.Redeploy.Executing |The event name. |
|DescriptionCN |String |Instance redeployment caused by disk failures: in progress. |The Chinese name of the event. |
|HappenedAt |Int64 |1664332705 |The time when the event occurs. |
|Details |Object |\- |The original event text. |
|Rules |Object |\- |The event rule details. For the specific format, see **Rule structure**. |


**Rule structure**


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|RuleId |String |194069687426716\*\*\*\* |The policy ID. |
|RuleName |String |Test event alert 1 |The policy name. |
|Level |String |notice |The alert level.<br><br><br>* critical<br><br>* warning<br><br>* notice |


<span id="hQ05OAFA"></span>
### Sample request body

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can skip parameters with no description in the actually received request body. These parameters do not affect your ability to obtain detailed event notification information.</div>


* <div data-tips="true" data-tips-type="default">The Details field contains fixed fields and extended fields.</div>


   * <div data-tips="true" data-tips-type="default"><strong>Fixed fields</strong>: specversion, id, source, type, volcpublishtime, volcregion, volcaccountid, volceventbusname, volcresourcename, subject, and time. Fixed fields are displayed even if they are empty.</div>


   * <div data-tips="true" data-tips-type="default"><strong>Extended fields</strong>: Except for fixed fields, all other fields are extended fields. Extended fields are event types defined by cloud products. For information about how to view extended fields, see <a href="https://docs.byteplus.com/en/docs/ecs/Content_of_the_event_alert_callback_request#x7rtTo9C">Obtain detailed information about target events in JSON format</a>.</div>



```JSON
{
  "AccountId": "210035****",
  "Description": "Restart instance: Execution successful",
  "DescriptionCN": "Restart instance: Execution successful",
  "Details": {
    "data": {
      "EventId": "e-ydzexhbtxv38dekp****",
      "EventStatus": "Succeeded",
      "EventType": "RebootInstance",
      "ExtraInfo": {},
      "HappenAt": "2025-07-03T17:00:20+08:00",
      "InstanceId": "i-yds68jq22oqc6ili****",
      "InstanceName": "cm-data-test",
      "PrivateIpAddress": [
        "172.xx.xx.2"
      ],
      "PublicIpAddress": [],
      "WithGPUDevice": false
    },
    "datacontenttype": "application/json",
    "id": "194069710419630****",
    "project": "default",
    "resourceid": "i-yds68jq22oqc6ili****",
    "source": "ecs",
    "specversion": "1.0",
    "subject": "ecs:cn-beijing:210035****:instance/i-yds68jq22oqc6ili****",
    "time": "2025-07-03T17:00:20+08:00",
    "type": "ecs:Instance:RebootInstance.Succeeded",
    "volcaccountid": "210035****",
    "volceventbusname": "default",
    "volcprojectname": "",
    "volcpublishtime": "2025-07-03T17:00:20+08:00",
    "volcregion": "cn-beijing",
    "volcresourcename": "cm-data-test"
  },
  "EventType": "ecs:Instance:RebootInstance.Succeeded",
  "HappenedAt": 1751533220,
  "Id": "194069710419630****",
  "ProjectName": "default",
  "Region": "cn-beijing",
  "Rules": [
    {
      "Level": "critical",
      "RuleId": "194069687426716****",
      "RuleName": "test_ecs_event"
    }
  ],
  "Source": "ecs",
  "Type": "Event"
}
```


<span id="x7rtTo9C"></span>
## Obtain detailed information about target events in JSON format

The extended fields in the message body (event alert) returned by Cloud Monitor mainly originate from the data reported by cloud products when they report events. You can place this data in the `data` field nested under the `Details` field, as the callback request body for the event alert.


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, click "Event Center \> Cloud Service Event".

3. In the "Actions" column of the target event, click the "Details" button to view detailed information about the event in JSON format.
