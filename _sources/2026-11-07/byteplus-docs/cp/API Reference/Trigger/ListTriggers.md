---
title: "ListTriggers"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListTriggers"
---

Query the list of triggers for the current pipeline.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=ListTriggers&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListTriggers |The API name. The name of the current API is `ListTriggers`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7d496c3d189a311676\*\*\*\* |Workspace ID to which the trigger belongs. |
|PipelineId |String |Yes |0f7ca5e80f4c3cfd116\*\*\*\* |The ID of the pipeline to which the trigger belongs. |
|Filter |Object of [TriggerFilter](https://docs.byteplus.com/en/docs/292/73447#triggerfilter) |no |\- |Filter for the list of triggers to be queried. |
|PageNumber |Long |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Long |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="triggerfilter"></span>
### TriggerFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |no |["f4e68241db4c1ed401cae\*\*\*\*"] |Filter by trigger ID for an exact match. |
|Name |String |no |demo |Filter by Trigger name using fuzzy search. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=ListTriggers&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "WorkspaceId": "7d496c3d189a311676****",
    "PipelineId": "0f7ca5e80f4c3cfd116****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Items |Array of [Trigger](https://docs.byteplus.com/en/docs/292/73447#trigger) |\- |Trigger list. |
|PageSize |Long |10 |Page size. |
|PageNumber |Long |1 |The current page number. |
|TotalCount |Long |2 |Total number of triggers. |


<span id="trigger"></span>
### Trigger


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |f4e68241db4c1ed401cae\*\*\*\* |Trigger ID. |
|WorkspaceId |String |7d494e1889a311676\*\*\*\* |Trigger workspace. |
|PipelineId |String |0f7ca5a4fe80f4c3cfd116\*\*\*\* |Pipeline ID of trigger. |
|Name |String |GitWebhook\-demo |Trigger name |
|Description |String |This is a description. |Trigger descriptions. |
|Type |String |Webhook |Trigger type<br><br><br>* Schedule: Scheduled trigger<br><br>* Webhook: General webhook trigger<br><br>* GitWebhook: webhook trigger for code source<br><br>* CRWebhook: Image source Webhook trigger |
|Configuration |Object of [TriggerConfiguration](https://docs.byteplus.com/en/docs/292/73447#triggerconfiguration) |\- |The trigger configuration. |
|Creator |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73447#iamuser) |\- |The trigger creator. |
|CreateTime |String |2021\-07\-19T12:21:31Z |Trigger creation time. |
|UpdateTime |String |2021\-07\-19T12:22:31Z |Trigger update time. |
|Parameters |Array of [TriggerParameter](https://docs.byteplus.com/en/docs/292/73447#triggerparameter) |\- |Pipeline variables used when triggered by a trigger. |
|Resources |Array of [TriggerResource](https://docs.byteplus.com/en/docs/292/73447#triggerresource) |\- |Code source used when the pipeline is triggered. |


<span id="triggerconfiguration"></span>
### TriggerConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Schedule |Object of [ScheduleConfiguration](https://docs.byteplus.com/en/docs/292/73447#scheduleconfiguration) |\- |Timed trigger configuration. |
|Webhook |Object of [WebhookConfiguration](https://docs.byteplus.com/en/docs/292/73447#webhookconfiguration) |\- |Webhook trigger configuration |


<span id="scheduleconfiguration"></span>
### ScheduleConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ScheduleConfig |String |44 17 \* \* 1 |Use Crontab expressions to configure the time for scheduled triggers. For configuration instructions, see the [official documentation](https://crontab.guru/). Crontab expressions use the UTC+8 time zone by default. |


<span id="webhookconfiguration"></span>
### WebhookConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Git |Object of [GitWebhookConfiguration](https://docs.byteplus.com/en/docs/292/73447#gitwebhookconfiguration) |\- |Webhook configuration for the code source trigger. |
|CR |Object of [CRWebhookConfiguration](https://docs.byteplus.com/en/docs/292/73447#crwebhookconfiguration) |\- |Webhook configuration for the image source trigger |
|URL |String |https://cp.volces.com/v2/webhook/scm/eQKcyKfa702maKXrR_VoJi\*\*\*\* |The webhook URL can be generated through the CreatePipelineWebhookURL API. |


<span id="gitwebhookconfiguration"></span>
### GitWebhookConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ResourceId |String |c3e06107e5edcb4fb5329d9b\*\*\*\* |Associated code source ID. |
|Filters |Array of [WebhookEventFilter](https://docs.byteplus.com/en/docs/292/73447#webhookeventfilter) |\- |Supported trigger events and filters for code source triggers. If not configured, all events will trigger the pipeline to run by default. |


<span id="webhookeventfilter"></span>
### WebhookEventFilter


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|EventType |String |Push |Trigger event types:<br><br><br>* Push code<br><br>* CreateTag: TAG creation<br><br>* PRMerged: Once merge request is completed |
|Config |Object of [WebhookEventConfig](https://docs.byteplus.com/en/docs/292/73447#webhookeventconfig) |\- |Trigger event configuration, used to further filter trigger events that meet the criteria. |


<span id="webhookeventconfig"></span>
### WebhookEventConfig


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|References |Array of String |["main" ] |Filtered branch or tag.<br><br><br>* Push and PRMerged events support specifying branches to filter.<br><br>* The CreateTag event supports entering filter TAGs. |


<span id="crwebhookconfiguration"></span>
### CRWebhookConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Filter |Object of [CRWebhookEventFilter](https://docs.byteplus.com/en/docs/292/73447#crwebhookeventfilter) |\- |Supported trigger actions and trigger conditions for the image source trigger If no configuration is set, all events will trigger the pipeline to run by default. |


<span id="crwebhookeventfilter"></span>
### CRWebhookEventFilter


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|CREventType |String |CRPush |Trigger actions:<br><br><br>* CRPush: Image upload |
|Condition |String |"volcregion":"xxx" |Trigger conditions are used to further filter trigger events. Supports regular expressions. |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |account (main account) ID. |
|UserId |Long |28\*\*\*\* |Sub\-user (IAM user) ID. |


<span id="triggerparameter"></span>
### TriggerParameter


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Key |String |key |Dynamic variable Key. |
|Value |String |value |Value of the dynamic variable |


<span id="triggerresource"></span>
### TriggerResource


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ResourceId |String |60cb460122422352a334\*\*\*\* |Code source ID. |
|Reference |String |master |Code Reference used for pipeline runs; supports entering a Commit ID, Tag, or Branch. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "ListTriggers",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "cn-north-1"
    },
    "Result": {
        "Items": [
            {
                "Id": "f4e68241db4c1ed401cae****",
                "WorkspaceId": "7d494e1889a311676****",
                "PipelineId": "0f7ca5a4fe80f4c3cfd116****",
                "Name": "GitWebhook-demo",
                "Description": null,
                "Type": "GitWebhook",
                "Configuration": {
                    "Webhook": {
                        "Git": {
                            "ResourceId": "c3e06107edsfds29b****",
                            "Filters": [
                                {
                                    "EventType": "Push",
                                    "Config": {
                                        "References": [
                                            "main"
                                        ]
                                    }
                                }
                            ]
                        },
                        "URL": "https://cp.volces.com/v2/webhook/scm/FkLuvVzsxl2zVyQtbutMYnGBi3HYEmK9ZPofERuN1TJ1FbdFztPrsG7r****"
                    },
                    "Schedule": null
                },
                "CreateTime": "2023-10-12T17:30:03+08:00",
                "UpdateTime": "2023-10-12T17:30:03+08:00",
                "Creator": {
                    "AccountId": 140000****,
                    "UserId": ****
                },
                "Parameters": [
                    {
                        "Key": "demo_key",
                        "Value": "demo_val"
                    }
                ],
                "Resources": []
            }
        ],
        "PageSize": 10,
        "PageNumber": 1,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have independent error codes. If an exception occurs during API calls, please refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
