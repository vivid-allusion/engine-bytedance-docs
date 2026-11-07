---
title: "ListPipelines"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListPipelines"
---

Pipeline list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, select the service address that corresponds to the Region where your resources are located. For details, see [Service addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=ListPipelines&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListPipelines |The API name. The name of the current API is `ListPipelines`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |18be9d623fba45a1aca409f5e19c\*\*\*\* |Workspace ID |
|Filter |Object of [PipelineFilter](https://docs.byteplus.com/en/docs/292/73448#pipelinefilter) |no |\- |Filter conditions for pipelines to be queried. |
|PageSize |Long |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |
|PageNumber |Long |no |1 |The starting page number when querying. The default number is 1. |


<span id="pipelinefilter"></span>
### PipelineFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Name |String |no |foo |Filter pipeline names using fuzzy search. |
|Ids |Array of String |no |["9d3f01e4f7ee4293a7cfc0c2d4d6\*\*\*\*"] |Filter by pipeline ID for precise querying. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=ListPipelines&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "3f5f09a059124d6898a8543e678f****",
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Name": "test",
        "Ids": [
            "9d3f01e4f7ee4293a7cfc0c2d4d6****"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TotalCount |Long |10 |Total number of pipelines. |
|Items |Array of [Pipeline](https://docs.byteplus.com/en/docs/292/73448#pipeline) |\- |Pipeline list |
|PageSize |Long |10 |Page size. |
|PageNumber |Long |1 |The current page number. |


<span id="pipeline"></span>
### Pipeline


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |67d0485e1efb44128f0d990cdad6\*\*\*\* |Pipeline ID. |
|Name |String |pipelineName |Pipeline name. |
|WorkspaceId |String |9d3f01e4f7ee4293a7cfc0c2d4d6\*\*\*\* |Pipeline workspace ID. |
|Description |String |This is a description. |Pipeline description. |
|Spec |String | |Pipeline orchestration YAML description information. |
|Resources |Array of [PipelineResource](https://docs.byteplus.com/en/docs/292/73448#pipelineresource) |\- |Configuration related to pipeline resources currently refers to the code source. |
|Parameters |Array of [PipelineParameter](https://docs.byteplus.com/en/docs/292/73448#pipelineparameter) |\- |Pipeline variable configurations |
|Caches |Array of [PipelineCache](https://docs.byteplus.com/en/docs/292/73448#pipelinecache) |\- |Pipeline cache configurations. |
|Notification |Object of [PipelineNotification](https://docs.byteplus.com/en/docs/292/73448#pipelinenotification) |\- |Pipeline message notification configurations |
|Creator |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73448#iamuser) |\- |Pipeline creator. |
|CreateTime |String |2023\-05\-10T21:33:20Z |Pipeline creation time. |
|UpdateTime |String |2023\-05\-10T21:33:20Z |The pipeline update time. |


<span id="pipelineresource"></span>
### PipelineResource


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |669631b1495540a49915ede9893d\*\*\*\* |Code source ID. |
|Configuration |Object of [PipelineResourceConfiguration](https://docs.byteplus.com/en/docs/292/73448#pipelineresourceconfiguration) |\- |Code source configuration information. |


<span id="pipelineresourceconfiguration"></span>
### PipelineResourceConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Git |Object of [GitResourceConfiguration](https://docs.byteplus.com/en/docs/292/73448#gitresourceconfiguration) |\- |Git code source configuration. |


<span id="gitresourceconfiguration"></span>
### GitResourceConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|DefaultBranch |String |master |Default branch. |


<span id="pipelineparameter"></span>
### PipelineParameter


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Key |String |key1 |Variable keys |
|Value |String |val1 |Variable value. |
|Secret |Boolean |true/false |Whether the variable has turned on privacy settings.<br><br><br>* true: Turn on privacy settings. The default value of the variable is displayed as \*\*\*.<br><br>* false: Turn off privacy settings. The default value of the variable is displayed in plain text. |
|Dynamic |Boolean |true/false |Enable dynamic settings for the variable<br><br><br>* true: Variable is dynamic. Support modifying the runtime value of the current variable while running a pipeline.<br><br>* false: The variable is not a dynamic variable. Use default values when running the pipeline. |
|OptionValues |Array of String |["abc","bcd"] |When configuring optional values, the variable is treated as a single\-choice value. |
|Description |String |this is a param description |Variable notes |


<span id="pipelinecache"></span>
### PipelineCache


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Key |String |m2 |Cache directory name |
|Path |String |$(CP_WORKSPACE)/.m2 |Cache path. |
|Description |String |this is a param description |Cache directory remarks. |


<span id="pipelinenotification"></span>
### PipelineNotification


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Events |Array of String |["EventPipelineStarted"] |List of events that trigger notification messages.<br><br><br>* EventPipelineStarted: Start running<br><br>* EventPipelineSucceeded: Pipeline succeeded<br><br>* EventPipelineFailed: Operation failed<br><br>* EventPipelineCanceled: Execution canceled |
|EnableSiteLetter |Boolean |true/false |Enable in\-site message notifications?<br><br><br>* Enable site message notifications<br><br>* false: Do not turn on site message notification |
|Sms |Object of [NotificationTarget](https://docs.byteplus.com/en/docs/292/73448#notificationtarget) |\- |SMS notification configuration. |
|Email |Object of [NotificationTarget](https://docs.byteplus.com/en/docs/292/73448#notificationtarget) |\- |Email message notification configuration |
|Webhook |Object of [WebhookNotification](https://docs.byteplus.com/en/docs/292/73448#webhooknotification) |\- |Webhook notification configuration |
|CustomContent |String |A custom message |Custom notification messages |


<span id="notificationtarget"></span>
### NotificationTarget


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Enable |Boolean |true/false |Enable notifications?<br><br><br>* Turn on notifications<br><br>* Do not turn on notification |
|Targets |Array of String |["TriggerBy","CreateBy"] |Notification target.<br><br><br>* Triggerer: Pipeline runner<br><br>* Pipeline creator |


<span id="webhooknotification"></span>
### WebhookNotification


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Enable |Boolean |true/false |Turn on notification.<br><br><br>* true: Turn on notification<br><br>* Notifications off |
|Type |String |Lark |Webhook type.<br><br><br>* Lark: Feishu webhook<br><br>* Common webhooks |
|Url |String |https://open.feishu.cn/open\-apis/bot/v2/hook/2e5c3202\-aa81\-4b14\-\*\*\*\* |WebhookURL。 |
|Token |String |foo |Call a token. |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |account (main account) ID. |
|UserId |Long |28\*\*\*\* |Sub\-user (IAM user) ID |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404031138595E5D8BD124299EB9****",
        "Action": "ListPipelines",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1",
    },
    "Result": {
        "Items": [
            {
                "Id": "67d0485e1efb44128f0d990cdad6****",
                "Name": "test-v2-pipeline_1683717039073",
                "WorkspaceId": "9d3f01e4f7ee4293a7cfc0c2d4d6****",
                "Description": "",
                "Spec": "version: 1.0.0\nstages:\n  - stage: stage-1\n    displayName: 阶段-1\n    tasks:\n      - dependsOn: []\n        task: task1\n        displayName: 任务-1\n        steps:\n          - step: exec-cmd\n            displayName: 命令执行\n            inputs:\n              shell: BASH\n              cmd: |-\n                sleep 200\n\n                echo 'aa'\n            component: execCmd@1.0.0/shell\n        plugins: []\n        outputs: []\n        timeout:\n          time: '2'\n          unit: h\n        workspace:\n          resources:\n            - ref: test111\n              directory: $(CP_WORKSPACE)\n          caches:\n            - cacheKey: m2\n              directory: $(CP_WORKSPACE)/m2\n              cachePolicy: pull-push\n            - cacheKey: gradle\n              directory: $(CP_WORKSPACE)/gradle\n              cachePolicy: pull-push\n            - cacheKey: npm\n              directory: $(CP_WORKSPACE)/npm\n              cachePolicy: pull-push\nagentPool: public/sit-v2-public\n",
                "Resources": [
                    {
                        "Id": "669631b1495540a49915ede9893d****",
                        "Configuration": {
                            "Git": {
                                "DefaultBranch": "demo"
                            }
                        }
                    }
                ],
                "CreateTime": "2023-05-10T19:10:39Z",
                "UpdateTime": "2023-05-10T21:33:20Z",
                "Creator": {
                    "AccountId": 140000****,
                    "UserId": 0
                },
                "Draft": false
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

This API does not currently provide independent error codes. If an error occurs during the API call, please refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
