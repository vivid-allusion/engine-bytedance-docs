---
title: "UpdateTrigger"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/UpdateTrigger"
---

The update trigger.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the service address for the Region where your resources are located. For details, see [Service addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=UpdateTrigger&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateTrigger |The API name. The name of the current API is `UpdateTrigger`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7d494e18ee414936c3d189a311676\*\*\*\* |Trigger workspace ID |
|PipelineId |String |Yes |0f7ca5a42f4ce414933cfd116\*\*\*\* |The ID of the pipeline to which the trigger belongs. |
|Id |String |Yes |c355e269e4149347635872ab\*\*\*\* |Trigger ID |
|Name |String |no |Webhook\-demo\-update |Trigger name |
|Description |String |no |This is a description. |The trigger description. |
|Configuration |Object of [TriggerConfiguration](https://docs.byteplus.com/en/docs/292/73442#triggerconfiguration) |no |\- |Trigger configurations. |
|Parameters |Array of [TriggerParameter](https://docs.byteplus.com/en/docs/292/73442#triggerparameter) |no |\- |Pipeline variables used when triggered by a trigger. |
|Resources |Array of [TriggerResource](https://docs.byteplus.com/en/docs/292/73442#triggerresource) |no |\- |Code source used when the pipeline is triggered by a pipeline trigger. |


<span id="triggerconfiguration"></span>
### TriggerConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Schedule |Object of [ScheduleConfiguration](https://docs.byteplus.com/en/docs/292/73442#scheduleconfiguration) |no |\- |The trigger configuration. |
|Webhook |Object of [WebhookConfiguration](https://docs.byteplus.com/en/docs/292/73442#webhookconfiguration) |no |\- |Configuration of webhook\-type triggers. |


<span id="scheduleconfiguration"></span>
### ScheduleConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ScheduleConfig |String |Yes |44 17 \* \* 1 |Use a Crontab expression to configure the scheduled trigger time. For configuration methods, see the [official documentation](https://crontab.guru/). By default, Crontab expressions use the UTC+8 time zone. |


<span id="webhookconfiguration"></span>
### WebhookConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Git |Object of [GitWebhookConfiguration](https://docs.byteplus.com/en/docs/292/73442#gitwebhookconfiguration) |no |\- |The webhook configuration for code source triggers |
|CR |Object of [CRWebhookConfiguration](https://docs.byteplus.com/en/docs/292/73442#crwebhookconfiguration) |no |\- |Webhook configuration for the mirror source trigger. |
|URL |String |Yes |https://cp.volces.com/v2/webhook/scm/eQKcyKfa702maKXrR_VoJi\*\*\*\* |The webhook URL can be generated using the CreatePipelineWebhookURL API. |


<span id="gitwebhookconfiguration"></span>
### GitWebhookConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ResourceId |String |Yes |c3e06107e5edcb4fb5329d9b\*\*\*\* |Associated code source ID |
|Filters |Array of [WebhookEventFilter](https://docs.byteplus.com/en/docs/292/73442#webhookeventfilter) |no |\- |Trigger events and filters supported by code source triggers. If no configuration is provided, all events will trigger the pipeline to run by default. |


<span id="webhookeventfilter"></span>
### WebhookEventFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|EventType |String |Yes |Push |Trigger event types<br><br><br>* Push code<br><br>* CreateTag: Create tag<br><br>* PRMerged: After the merge request is completed |
|Config |Object of [WebhookEventConfig](https://docs.byteplus.com/en/docs/292/73442#webhookeventconfig) |no |\- |Trigger event configuration, used for secondary filtering of trigger events that meet the criteria. |


<span id="webhookeventconfig"></span>
### WebhookEventConfig


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|References |Array of String |no |["main" ] |Filtered branches or tags.<br><br><br>* Push and PRMerged events support specifying filtered branches.<br><br>* The CreateTag event supports entering a filter TAG. |


<span id="crwebhookconfiguration"></span>
### CRWebhookConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Filter |Object of [CRWebhookEventFilter](https://docs.byteplus.com/en/docs/292/73442#crwebhookeventfilter) |no |\- |Trigger actions and conditions supported by the image source trigger If configuration is not set, all events will trigger pipeline execution by default. |


<span id="crwebhookeventfilter"></span>
### CRWebhookEventFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|CREventType |String |no |CRPush |Trigger actions:<br><br><br>* CRPush: push images |
|Condition |String |no |"volcregion":"xxx" |Trigger conditions are used for secondary filtering of trigger events that meet the criteria. Supports regular expressions. |


<span id="triggerparameter"></span>
### TriggerParameter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key |Key for dynamic variables |
|Value |String |Yes |value |Dynamic variable Value |


<span id="triggerresource"></span>
### TriggerResource


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ResourceId |String |Yes |60cb460122422352a334\*\*\*\* |Code source ID. |
|Reference |String |Yes |master |Code reference used for pipeline execution; you can specify a Commit ID, Tag, or Branch. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=UpdateTrigger&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "7d494e18ee414936c3d189a311676****",
    "PipelineId": "0f7ca5a42f4ce414933cfd116****",
    "Name": "Webhook-demo-update",
    "Id": "c355e269e4149347635872ab****",
    "Configuration": {
        "Webhook": {
            "URL": "https://cp.volces.com/v2/webhook/scm/FkLuvVzsxl2zVyQtbutMYnGBi3HYEmK9ZPofERuN1TJ1FbdFztPrsG7rMrWRmQ70****"
        }
    },
    "Parameters": [
        {
            "Key": "demo_key",
            "Value": "demo_val"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "UpdateTrigger",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not have dedicated error codes. If an exception occurs during an API call, refer to [the public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
