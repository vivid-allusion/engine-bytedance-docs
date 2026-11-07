---
title: "ListEventRules"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListEventRules"
---

Query event rules.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

This API involves multiple downstream dependencies. Frequent calls will trigger rate limiting. We recommend keeping QPS not higher than 20 for this API.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListEventRules&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListEventRules&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListEventRules |The name of the API. The API name is `ListEventRules`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|RuleName |String |No |rule\-01 |Event rule name. Fuzzy search by name is applied.<br><br><br>* The name must be 1 to 128 characters in length.<br><br>* It cannot start with a digit or hyphen (`-`). |
|Source |Array of String |No |ecs |Event source. |
|Status |Array of String |No |enable |Rule status.<br><br><br>* **enable**: The rule is enabled.<br><br>* **disable**: The rule is disabled. |
|PageSize |Integer |No |30 |The number of rows per page for a pagination query. Default value: 30. |
|PageNumber |Integer |No |1 |The page number for a pagination query. Default value: 1.<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|OrderBy |String |No |UpdatedAt |Rule sorting field.<br><br><br>* **UpdatedAt**: (Default) Sorted by rule modification time.<br><br>* **RuleName**: Sorted by rule name.<br><br>* **CreatedAt**: Sorted by rule creation time. |
|Asc |Boolean |No |false |Rule sorting order.<br><br><br>* **true**: Ascending order<br><br>* **false**: Descending order |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListEventRules&Version=2018-01-01
Content-Type: application/json
{
    "RuleName": "rule-01",
    "Asc": false,
    "OrderBy": "UpdatedAt",
    "Source": [
        "ecs"
    ],
    "Status": [
        "enable"
    ],
    "PageNumber": 1,
    "PageSize": 30
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Asc |Boolean |false |Sorting order of the returned event rules. |
|Data |Array of [Rule](https://docs.byteplus.com/en/docs/39/16305#rule) |\- |Details about rules that meet the criteria. |
|OrderBy |String |HappenTime |The sorting condition. |
|TotalCount |Integer |2 |Total number of event rules that meet the criteria. |


<span id="rule"></span>
### Rule


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|RuleId |String |168\*\*\*\*\*4352 |Event rule ID. |
|Source |String |vke |Event source. |
|RuleName |String |test\-kafka |Rule name. |
|Description |String |This is test rule 01 |Rule description. |
|EventBusName |String |default |Event bus name. Only `default` is supported. |
|AccountId |String |210\*\*\*\*168 |BytePlus root user ID. |
|Region |String |cn\-beijign |The region. |
|Level |String |critical |Severity level of the alert. |
|EnableState |String |enable |Rule status.<br><br><br>* **enable**: The rule is enabled.<br><br>* **disable**: The rule is disabled. |
|EffectStartAt |String |12:00 |The start of the time period during which the rule is active. |
|EffectEndAt |String |20:00 |The end of the time period during which the rule is active. |
|EventType |Array of String |["vke:Addon:AddonStatus.Failed"] |Event type. |
|FilterPattern |JSON Map |\- |Filter pattern, also known as an event matching rule.<br><br>Custom matching rules are not supported. |
|ContactMethods |Array of String |[ "Webhook",<br><br>"Email",<br><br>"MQ",<br><br>"SMS" ] |Alert notification method.<br><br><br>* **Phone**: Phone<br><br>* **Email**: Email<br><br>* **SMS**: SMS<br><br>* **Webhook**: Alert callback<br><br>* **TLS**: TLS<br><br>* **MQ**: Message Queue for Kafka |
|Endpoint |String |http://example.com/alert |The callback address when the alert notification method is alert callback. |
|TLSTarget |Array of [TLSTarget](https://docs.byteplus.com/en/docs/39/16305#tlstarget) |\- |TLS configuration. This is triggered when TLS is the alert method. |
|ContactGroupIds |Array of String |["166\*\*\*\*\*7680"] |A list of alert contact group IDs. When the `ContactMethods` parameter is `Email`, `Phone`, or `SMS`, this parameter cannot be empty. |
|MessageQueue |Array of [MQTarget](https://docs.byteplus.com/en/docs/39/16305#mqtarget) |\- |The message queue used when the alert notification method is Message Queue for Kafka. |
|UpdatedAt |Integer |1666686791 |Update time of the event rule. |
|CreatedAt |Integer |1666668613 |Creation time of the event rule. |
|WebhookIds |Array of String |\- |A list of alert callback IDs. |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/16305#notifytemplatebasic) |\- |Notification template configuration. |


<span id="filterpattern"></span>
### FilterPattern


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |"Type": [ "vke:Addon:AddonStatus.Failed" ] |A list of event types for pattern matching. Any matching is supported. |
|value |Any |"Source": "vke" |Event source in pattern matching. |


<span id="tlstarget"></span>
### TLSTarget


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TopicId |String |6a6\*\*\*\*67c7 |Topic ID. |
|ProjectId |String |79fe\*\*\*\*122f |Project ID. |
|ProjectName |String |default |The project name. |
|RegionNameCN |String |Beijing |Chinese name of the region. |
|RegionNameEN |String |cn\-beijing |Region name in English. |


<span id="mqtarget"></span>
### MQTarget


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |kafka |Alert notification method. |
|Topic |String |testkafka |Topic of the message queue. |
|VpcId |String |vpc\-2bzq\*\*\*\*\*pm22 |VPC ID. |
|Region |String |cn\-beijing |Region where the MQ instance is located. |
|Password |String |\- |MQ instance password. |
|Endpoints |String |\- |Cluster address, which is only returned for rule_engine. |
|InstanceId |String |kafka\-cno\*\*\*\*\*5hc |MQ instance ID. |
|AuthEncrypt |Array of Integer |\- |Encrypted account password, which is only returned for rule_engine. |


<span id="notifytemplatebasic"></span>
### NotifyTemplateBasic


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Channel |String |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**：Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |189828\*\*\*00 |Notification template ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one notification template ID can be specified for each notification channel.</div><br> |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListEventRules",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Level": "critical",
                "Region": "cn-beijing",
                "RuleId": "168*****4352",
                "Source": "vke",
                "Endpoint": "http://example.com/alert",
                "RuleName": "test-kafka",
                "AccountId": "210****168",
                "CreatedAt": 1666668613,
                "UpdatedAt": 1666686791,
                "EventType": [
                    "vke:Addon:AddonStatus.Failed"
                ],
                "TLSTarget": [
                    {
                        "TopicId": "6a6****67c7",
                        "ProjectId": "79fe****122f",
                        "ProjectName": "default",
                        "RegionNameCN": "北京",
                        "RegionNameEN": "cn-beijing"
                    }
                ],
                "WebhookIds": [
                    ""
                ],
                "NotifyTemplates": [
                    "Channel": "email",
                    "NotifyTemplateId": "189828***00"
                ],
                "Description": "This is test rule 01",
                "EffectEndAt": "20:00",
                "EnableState": "enable",
                "EventBusName": "default",
                "MessageQueue": [
                    {
                        "Type": "kafka",
                        "Topic": "testkafka",
                        "VpcId": "vpc-2bzq*****pm22",
                        "Region": "cn-beijing",
                        "Password": "",
                        "Endpoints": "",
                        "InstanceId": "kafka-cno*****5hc",
                        "AuthEncrypt": [
                            null
                        ]
                    }
                ],
                "EffectStartAt": "12:00",
                "ContactMethods": [
                    "Webhook",
                    "Email",
                    "MQ",
                    "SMS"
                ],
                "ContactGroupIds": [
                    "166*****7680"
                ]
            }
        ],
        "PageSize": 30,
        "PageNumber": 1,
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
