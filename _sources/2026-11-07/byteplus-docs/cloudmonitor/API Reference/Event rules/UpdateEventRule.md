---
title: "UpdateEventRule"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/UpdateEventRule"
---

Update an event rule.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=UpdateEventRule&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateEventRule&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateEventRule |The name of the API. The API name is `UpdateEventRule`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|RuleId |String |Yes |15847\*\*\*\*\*\*\*\*688768 |Event rule ID. |
|RuleName |String |No |rule\-01 |Event rule name.<br><br><br>* The name must be 1 to 128 characters in length.<br><br>* It cannot start with a digit or hyphen (`-`). |
|Descriptions |String |No |This is test rule 01 after updating |Event rule description.<br><br><br>* It cannot start with a digit, hyphen (`-`), or Chinese character.<br><br>* It can contain only Chinese characters, letters, digits, underscore (`_`), hyphen (`-`), and Chinese characters.<br><br>* It must be 0 to 255 characters in length. |
|EventBusName |String |Yes |default |Event bus name. Only `default` is supported. |
|EventSource |String |Yes |ecs |Event source. |
|EventType |Array of String |Yes |[ "ecs:Disk:DiskError.Redeploy.Executing", "ecs:Disk:DiskError.Redeploy.Inquiring", "ecs:Disk:DiskError.Redeploy.Succeeded" ] |Event type. |
|Status |String |No |enable |Rule status.<br><br><br>* **enable**: The rule is enabled.<br><br>* **disable**: The rule is disabled. |
|Level |String |Yes |notice |Severity level of the alert.<br><br><br>* **notice**<br><br>* **warning**<br><br>* **critical** |
|FilterPattern |JSON Map |No |\- |Filter pattern, also known as event matching rules.<br><br>Custom matching rules are not supported. |
|EffectiveTime |Object of [EffectiveTime](https://docs.byteplus.com/en/docs/39/16304#effectivetime) |Yes |\- |The period of time during which the rule is active. |
|ContactMethods |Array of String |Yes |[ "Webhook", "Email", "SMS" ] |Alert notification method.<br><br><br>* **Phone**: Phone<br><br>* **Email**: Email<br><br>* **SMS**: SMS<br><br>* **Webhook**: Alert callback<br><br>* **TLS**: TLS<br><br>* **MQ**: Message Queue for Kafka |
|ContactGroupIds |Array of String |No |[ "157284\*\*\*\*\*\*\*\*69152" ] |A list of alert contact group IDs. When the `ContactMethods` parameter is `Email`, `Phone`, or `SMS`, this parameter cannot be empty. |
|Endpoint |String |No |http://example.com/alert |Callback address to be triggered. This parameter is configurable when `ContactMethods` options include `webhook`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><code>WebhookIds</code> and <code>Endpoint</code> parameters are mutually exclusive. Only one can be configured per call.</div><br> |
|TLSTarget |Array of [TLSTarget](https://docs.byteplus.com/en/docs/39/16304#tlstarget) |No |\- |TLS configuration when `ContactMethods` options include `TLS`. |
|MessageQueue |Array of [MQTarget](https://docs.byteplus.com/en/docs/39/16304#mqtarget) |No |\- |Message queue when `ContactMethods` options include `MQ`. |
|WebhookIds |Array of String |No |\- |A list of alert callback IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><code>WebhookIds</code> and <code>Endpoint</code> parameters are mutually exclusive. Only one can be configured per call.</div><br> |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/16304#notifytemplatebasic) |No |\- |Notification template configuration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Events follow a subscription model. A single event can match multiple event rules, with each event rule configurable with different delivery channels. When contact duplicates exist across rules, event rules are sorted by <strong>severity level (descending) + update time (descending)</strong>. The <strong>severity level and notification template</strong> of the highest\-priority rule are used for event delivery.</div><br> |


<span id="filterpattern"></span>
### FilterPattern


|**Parameters** |**Types** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|key |String |Yes |Source |Key for pattern matching. |
|value |Any |Yes |ecs |Key value for pattern matching. |


<span id="effectivetime"></span>
### EffectiveTime


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|StartTime |String |No |09:00 |The start of the time period during which the rule is active. |
|EndTime |String |No |20:59 |The end of the time period during which the rule is active. |


<span id="tlstarget"></span>
### TLSTarget


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|TopicId |String |No |6a6\*\*\*\*67c7 |Topic ID. |
|ProjectId |String |No |79fe\*\*\*\*122f |Project ID. |
|ProjectName |String |No |default |The project name. |
|RegionNameCN |String |No |Beijing |Chinese name of the region. |
|RegionNameEN |String |No |cn\-beijing |English name of the region. |


<span id="mqtarget"></span>
### MQTarget


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |No |kafka |Alert notification method. |
|Topic |String |No |testkafka |Topic of the message queue. |
|VpcId |String |No |vpc\-2bzq\*\*\*\*\*pm22 |VPC ID. |
|Region |String |No |cn\-beijing |Region where the MQ instance is located. |
|Password |String |No |\- |Password of the MQ instance. |
|Endpoints |String |No |\- |Cluster address, which is only returned for rule_engine. |
|InstanceId |String |No |kafka\-cno\*\*\*\*\*5hc |MQ instance ID. |
|AuthEncrypt |Array of Integer |No |\- |Encrypted account password, which is only returned for rule_engine. |


<span id="notifytemplatebasic"></span>
### NotifyTemplateBasic


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Channel |String |No |email |Notification channel. Valid values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**：Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |No |189828\*\*\*00 |Notification template ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one notification template ID can be specified for each notification channel.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=UpdateEventRule&Version=2018-01-01
Content-Type: application/json
{
    "RuleId": "15847********688768",
    "RuleName": "rule-01",
    "Status": "enable",
    "ContactGroupIds": [
        "157284********69152"
    ],
    "ContactMethods": [
        "Webhook",
        "Email",
        "SMS"
    ],
    "Description": "This is test rule 01 after updating",
    "EffectiveTime": {
        "EndTime": "20:59",
        "StartTime": "09:00"
    },
    "Endpoint": "http://example.com/alert",
    "EventBusName": "default",
    "EventSource": "ecs",
    "EventType": [
        "ecs:Disk:DiskError.Redeploy.Executing",
        "ecs:Disk:DiskError.Redeploy.Inquiring",
        "ecs:Disk:DiskError.Redeploy.Succeeded"
    ],
    "FilterPattern": {},
    "Level": "notice",
    "MessageQueue": [
        {
            "Type": "kafka",
            "Topic": "testkafka",
            "VpcId": "vpc-2bzq*****pm22",
            "Region": "cn-guilin-boe",
            "Password": "-",
            "Endpoints": "-",
            "InstanceId": "kafka-cno*****5hc",
            "AuthEncrypt": [
                null
            ]
        }
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
        {
            "Channel": "email",
            "NotifyTemplateId": "189828***00"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Types** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Object of [RuleIDVo](https://docs.byteplus.com/en/docs/39/16304#ruleidvo) |\- |Event rule content. |


<span id="ruleidvo"></span>
### RuleIDVo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|RuleId |String |157284163494346\*\*\*\* |Event rule ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateEventRule",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "RuleId": "157284163494346****"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
