---
title: "CreateTrigger"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/CreateTrigger"
---

Create a trigger.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

Supported trigger types:


* Generic Webhook trigger: When Type is set to Webhook, the Webhook field in Configuration is required.

* Mirror source Webhook trigger: Type is CRWebhook. Webhook in Configuration and CR in Webhook are required.

* Scheduled trigger: Type must be set to Schedule, and Schedule in Configuration is required.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the service address corresponding to the region of your resources. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CreateTrigger&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateTrigger |The API name. The name of the current API is `CreateTrigger`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7d494e18ee414936c3d189a311676\*\*\*\* |Workspace ID of the trigger. |
|PipelineId |String |Yes |0f7ca5a42f4ce414933cfd116\*\*\*\* |Pipeline ID of the trigger |
|Name |String |Yes |Webhook\-demo\-update |Trigger name |
|Type |String |Yes |Webhook |Trigger type<br><br><br>* Webhook: General webhook trigger<br><br>* Schedule: Scheduled trigger<br><br>* CRWebhook: Image source Webhook trigger |
|Configuration |Object of [TriggerConfiguration](https://docs.byteplus.com/en/docs/292/73439#triggerconfiguration) |Yes |\- |Trigger configuration. |
|Description |String |no |Description |Trigger description. |
|Parameters |Array of [TriggerParameter](https://docs.byteplus.com/en/docs/292/73439#triggerparameter) |no |\- |Pipeline variables used when the pipeline is triggered by a trigger. |
|Resources |Array of [TriggerResource](https://docs.byteplus.com/en/docs/292/73439#triggerresource) |no |\- |The code source used when the pipeline is triggered by a trigger. |


<span id="triggerconfiguration"></span>
### TriggerConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Schedule |Object of [ScheduleConfiguration](https://docs.byteplus.com/en/docs/292/73439#scheduleconfiguration) |no |\- |Timed trigger configuration. |
|Webhook |Object of [WebhookConfiguration](https://docs.byteplus.com/en/docs/292/73439#webhookconfiguration) |no |\- |Configuration of webhook triggers. |


<span id="scheduleconfiguration"></span>
### ScheduleConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ScheduleConfig |String |Yes |44 17 \* \* 1 |Configure the scheduled trigger time using Crontab expressions. For configuration instructions, refer to the [official documentation](https://crontab.guru/). Crontab expressions use the UTC +8 time zone by default. |


<span id="webhookconfiguration"></span>
### WebhookConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Git |Object of [GitWebhookConfiguration](https://docs.byteplus.com/en/docs/292/73439#gitwebhookconfiguration) |no |\- |The Webhook configuration for the code source trigger. |
|CR |Object of [CRWebhookConfiguration](https://docs.byteplus.com/en/docs/292/73439#crwebhookconfiguration) |no |\- |The image source trigger webhook configuration |
|URL |String |Yes |https://cp.volces.com/v2/webhook/scm/eQKcyKfa702maKXrR_VoJi\*\*\*\* |The webhook URL can be generated using the CreatePipelineWebhookURL API. |


<span id="gitwebhookconfiguration"></span>
### GitWebhookConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ResourceId |String |Yes |c3e06107e5edcb4fb5329d9b\*\*\*\* |Associated code source ID. |
|Filters |Array of [WebhookEventFilter](https://docs.byteplus.com/en/docs/292/73439#webhookeventfilter) |no |\- |Trigger events and filters supported by the code source trigger If no configuration is set, all events will trigger pipeline execution by default. |


<span id="webhookeventfilter"></span>
### WebhookEventFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|EventType |String |Yes |Push |Trigger event types:<br><br><br>* Push: Code push<br><br>* Create a tag<br><br>* After the pull request is merged |
|Config |Object of [WebhookEventConfig](https://docs.byteplus.com/en/docs/292/73439#webhookeventconfig) |no |\- |Trigger event configuration, used for secondary filtering of trigger events that meet the criteria. |


<span id="webhookeventconfig"></span>
### WebhookEventConfig


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|References |Array of String |no |["main" ] |Filtered branches or tags.<br><br><br>* Push and PRMerged events support specifying filtered branches.<br><br>* The CreateTag event supports specifying TAGs for filtering. |


<span id="crwebhookconfiguration"></span>
### CRWebhookConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Filter |Object of [CRWebhookEventFilter](https://docs.byteplus.com/en/docs/292/73439#crwebhookeventfilter) |no |\- |Supported trigger actions and trigger conditions for image source triggers. By default, if no configuration is set, all events trigger the pipeline to run. |


<span id="crwebhookeventfilter"></span>
### CRWebhookEventFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|CREventType |String |no |CRPush |Trigger actions<br><br><br>* CRPush: Push images |
|Condition |String |no |"volcregion":"xxx" |Trigger conditions are used to further filter trigger events. Supports regular expressions. |


<span id="triggerparameter"></span>
### TriggerParameter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key |The dynamic variable Key. |
|Value |String |Yes |value |Dynamic variable Value |


<span id="triggerresource"></span>
### TriggerResource


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ResourceId |String |Yes |60cb460122422352a334\*\*\*\* |Code source ID. |
|Reference |String |Yes |master |Code reference for pipeline execution: can be a Commit ID, tag, or branch. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CreateTrigger&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "7d494e18ee414936c3d189a311676****",
    "PipelineId": "0f7ca5a42f4ce414933cfd116****",
    "Name": "Webhook-demo",
    "Type": "Webhook",
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


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |007a85e4ac034eb790b096705694\*\*\*\* |Trigger ID |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "CreateTrigger",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "007a85e4ac034eb790b096705694****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

Currently, this API does not have independent error codes. If an exception is returned when calling the API, refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
