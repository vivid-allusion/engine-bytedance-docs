---
title: "UpdateRule"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/UpdateRule"
---

Update an alert policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is the most optimal for the region of your services.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=UpdateRule&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateRule&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateRule |The name of the API. The API name is `UpdateRule`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Id |String |Yes |1572416252557\*\*\*\*\*\* |Alert policy ID.<br><br>You can call the [ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) API to obtain alert policy IDs. |
|RuleName |String |Yes |alarm_rule_demo |Alert policy name.<br><br><br>* The name must be 1 to 128 characters in length.<br><br>* It cannot start with a digit or hyphen (`-`). |
|Descriptions |String |No |This is an example of an alert rule |Description of the alert policy.<br><br><br>* It cannot start with a digit, hyphen (\-), or Chinese character.<br><br>* It can contain only Chinese characters, letters, digits, underscore (`_`), hyphen (`-`), and Chinese characters.<br><br>* It must be 0 to 255 characters in length. |
|RuleType |String |Yes |static |The type of selecting alert objects.<br><br><br>* **static**: Static selection.<br><br>* **dynamic**: Dynamic select by resource name, project, and tag. |
|Namespace |String |Yes |VCM_ECS |The cloud product to which the policy is applicable. For details, see the **Namespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|SubNamespace |String |Yes |Instance |The dimension of the metric referenced by this policy. For details, see the **SubNamespace** field for each product on the [Cloud Monitor metric query](https://docs.byteplus.com/docs/cloudmonitor/Cloud-service-metrics) page. |
|Level |String |Yes |critical |The alarm level. Valid values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |
|OriginalDimensions |JSON Map |Yes |\- |Resource ID detected by the policy. |
|EvaluationCount |Integer |Yes |5 |The duration required to trigger an alert. The unit is minutes. Supported values include 1, 3, 5, 10, 15, 30, 60, and 120. |
|EnableState |String |Yes |enable |Alert policy status.<br><br><br>* **enable**: Enabled<br><br>* **disable**: Disabled |
|Regions |Array of String |Yes |["cn\-beijing,cn\-shanghai"] |IDs of the availability zones where the cloud product is used.<br><br><br>* When `RuleType` is `static`, only one region ID can be specified.<br><br>* When `RuleType` is `dynamic`, multiple Region IDs can be specified. Separate multiple region IDs with commas (`,`). |
|SilenceTime |Integer |Yes |5 |Notification intervals. The unit is minutes. Valid values include 5, 30, 60, 180, 360, 720, and 1440. |
|NotificationId |String |No |1894657089\*\*\* |Notification policy ID.<br><br>You can call the [ListNotifications](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifications) API to query notification policy IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter has higher priority than <code>AlertMethods</code>. Therefore, when you use this parameter to specify alert notification policy IDs, other alert notification configurations (including <code>AlertMethods</code>, <code>ContactGroupIds</code>, <code>WebhookIds</code>, <code>EffectStartAt</code>, and <code>EffectEndAt</code>) will become invalid.</div><br> |
|AlertMethods |Array of String |Yes |Phone |Notification methods for the alert policy.<br><br><br>* **Email**: Email<br><br>* **Phone**: Phone<br><br>* **SMS**: SMS<br><br>* **Webhook**: Alert callback |
|Webhook |String |No |http://alert.volc.com/callback |When `AlertMethods` is `Webhook`, specify a Webhook callback address. For restrictions, see [Alert callback usage](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one of the <code>WebhookIds</code> or <code>Webhook</code> parameters can be configured simultaneously.</div><br> |
|WebhookIds |Array of String |No |["1894350011\*\*\*"] |When `AlertMethods` is `Webhook`, specify the ID of the alert Webhook callback.<br><br>You can call the [ListWebhooks](https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooks) API to obtain Webhook callback IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one of the <code>WebhookIds</code> and <code>Webhook</code> parameters can be configured simultaneously.</div><br> |
|ContactGroupIds |Array of String |No |1526538875\*\*\* |When `AlertMethods` is `Email`, `Phone`, or `SMS`, specify alert contact group IDs.<br><br>You can call the [ListContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups) API to query contact group IDs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can specify up to 5 contact groups.</div><br> |
|EffectStartAt |String |Yes |00:00 |The time when the policy starts taking effect. The time is in the format `HH:MM` (example: 00:00). |
|EffectEndAt |String |Yes |23:59 |The time when the alert policy stops being in effect. The time is in the format `HH:MM` (example: 23:59).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>EffectEndAt</code> time must be later than the <code>EffectStartAt</code> time.</div><br> |
|ConditionOperator |String |No |&& |Multi\-metric judgment logic.<br><br><br>*  **&&** : The alert is triggered only when all metrics are satisfied.<br><br><br><br>---<br><br> |
|RecoveryNotify |Object of [RecoveryNotify](https://docs.byteplus.com/en/docs/39/16292#recoverynotify) |No |\- |Alert recovery notification. |
|MultipleConditions |Boolean |No |false |Whether the alert policy uses multiple metrics.<br><br><br>* **true**: Multiple metrics<br><br>* **false**: Use a single metric (default). |
|NoData |Object of [NoData](https://docs.byteplus.com/en/docs/39/16292#nodata) |No |\- |NoData alert. |
|DimensionConditions |Object of [DimensionConditions](https://docs.byteplus.com/en/docs/39/16292#dimensionconditions) |No |\- |Dimension configuration. This parameter is valid only when `RuleType` is set to `dynamic`. It supports matching by project, tag, and meta. |
|LevelConditions |Array of [LevelCondition](https://docs.byteplus.com/en/docs/39/16292#levelcondition) |No |\- |Alert levels. |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/16292#rulecondition) |Yes |\- |Alerting condition. It is an array. You can specify up to 10 metric evaluation statements. |
|NotifyMode |String |No |rule |Alert notification aggregation policy.<br><br><br>* **rule**: (Default) Aggregate alerts by rule.<br><br>* **Resource**: Aggregate alerts by rule and resource. |
|ProjectName |String |No |default |Name of the project to which the alert policy belongs. If no project is specified, it defaults to the "default" project. |
|Tags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/39/16292#resourcetag) |No |\- |Tags associated with the alert policy. |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/16292#notifytemplatebasic) |No |\- |Notification template configuration. |
|EvaluationInterval |Integer |No |1 |The check interval is used to trigger N alerts within M intervals. EvaluationInterval indicates M, and EvaluationCount indicates N.<br><br>EvaluationInterval is equal to CheckInterval multiplied by EvaluationCount. If EvaluationInterval is left empty, the value of EvaluationCount is used by default. |


<span id="originaldimensions"></span>
### OriginalDimensions


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|key |String |Yes |ResourceID |Dimension key, such as `ResourceID` or `NodeName`.<br><br><br>* Supported Dimension keys of different cloud products vary. For details, see [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/docs).<br><br>* `ResourceID` is required, and the capitalization case must be consistent with the one displayed on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/docs) page.<br><br>* You can specify multiple dimension keys, based on which grouping is performed. Sample code:<br><br>   * When only `ResourceID` is specified, the system will group alerts by `ResourceID`.<br><br>   * When both `ResourceID` and `NodeName` are specified, the system will group alerts first by `ResourceID`. Then, within each group, further grouping is performed by `NodeName`. |
|value |Array of String |Yes |["i\-123oiuoiu23uiow\*\*\*\*\*","i\-123oiuoiu23uiow\*\*\*\*\*"] |Metric Dimension value. The data type is array. Separate multiple values with commas (`,`). You can use the wildcard character `*` to select the values of all instances. For example, you can set it to ["\*"]. |


<span id="recoverynotify"></span>
### RecoveryNotify


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |true |Whether to turn on alert recovery notifications. Available types:<br><br><br>* **true**: (Default) Turn on alert recovery notifications.<br><br>* **false**: Turn off alert recovery notifications. |


<span id="nodata"></span>
### NoData


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |true |Whether to enable the NoData alert. Available types:<br><br><br>* **true**: Enable the NoData alert.<br><br>* **false**: (Default) Disable the NoData alert. |
|EvaluationCount |Integer |No |10 |Threshold for triggering the NoData alert. If no data is reported within the configured cycle threshold, a NoData alert will be triggered.<br><br><br>* This field is required if `Enable` is set to `true`.<br><br>* The value is an integer from 3 to 20. |
|Level |String |No |notice |NoData alert level. Available types:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |


<span id="dimensionconditions"></span>
### DimensionConditions


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |No |meta |Dimensions type. Available types:<br><br><br>* **project**: Select alert object by project.<br><br>* **tag**: Select alert objects by tag.<br><br>* **meta**: Select alert objects by resource name. |
|TagCondition |Object of [TagCondition](https://docs.byteplus.com/en/docs/39/16292#tagcondition) |No |\- |Tag condition for selecting alert objects. This field is required if `Type` is `tag`. |
|MetaCondition |Object of [MetaCondition](https://docs.byteplus.com/en/docs/39/16292#metacondition) |No |\- |Resource name condition for selecting alert objects. This field is required if `Type` is `meta`. |
|ProjectCondition |Object of [ProjectCondition](https://docs.byteplus.com/en/docs/39/16292#projectcondition) |No |\- |Project condition for selecting alert objects. This field is required if `Type` is set to `project`. |


<span id="levelcondition"></span>
### LevelCondition


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Level |String |No |warning |Alert notification level. Valid values:<br><br><br>* **notice**<br><br>* **warning**<br><br>* **critical**<br><br>* **recovery** |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/16292#rulecondition) |No |\- |Alert level configuration. |


<span id="rulecondition"></span>
### RuleCondition


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|MetricName |String |No |Instance_CpuBusy |Name of the metric. For details, see the **MetricName** field for each cloud product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|Statistics |String |No |avg |Statistical method. Values:<br><br><br>* **avg**: Average value.<br><br>* **max**: Maximum value.<br><br>* **min**: Minimum value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The statistical method is applied to the data within the detection period. For example, by default, the time span for each data detection is 1 minute. If the statistical method is avg, then the average value of the data within 1 minute is taken.</div><br> |
|ComparisonOperator |String |No |\> |Comparison operator. It supports common threshold alerts: \>, \>=, <, <=, !=, =, as well as the following cycle\-over\-cycle and period\-over\-period alerts:<br><br><br>* last_period_increase_pct: Cycle\-over\-cycle increase over the previous period.<br><br>* last_period_decrease_pct: Cycle\-over\-cycle decrease over the previous period.<br><br>* last_period_abs_pct: Cycle\-over\-cycle increase or decrease over the previous period.<br><br>* last_day_increase_pct: Period\-over\-period increase compared to the same period yesterday.<br><br>* last_day_decrease_pct: Period\-over\-period decrease compared to the same period yesterday.<br><br>* last_day_abs_pct: Period\-over\-period increase or decrease compared to the same period yesterday.<br><br>* last_week_increase_pct: Period\-over\-period increase compared to the same period last week.<br><br>* last_week_decrease_pct: Period\-over\-period decrease compared to the same period last week.<br><br>* last_week_abs_pct: Period\-over\-period increase or decrease compared to the same period last week. |
|Threshold |String |No |100 |Metric threshold.<br><br><br>* It can be a positive number or 0.<br><br>* It supports up to three decimal places. |
|MetricUnit |String |No |Percent |Metric unit. For details, see the **MetricUnit** field on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page for the corresponding cloud product.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For cycle\-over\-cycle and period\-over\-period comparison alerts, MetricUnit must be set to "Percent".</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The presence of "IEC" in MetricUnit indicates different scaling bases:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">With IEC: The unit base is 1024.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Without IEC: Base\-1000 scaling</div><br> |
|EvaluationWindow |Integer |No |1 |The time window for statistics is the time period over which alert statistics are collected. |


<span id="resourcetag"></span>
### ResourceTag


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |No |doc |Tag key.<br><br><br>* It can contain Chinese characters, uppercase and lowercase letters, digits, and spaces.<br><br>* The following special characters are supported: `_.:/=+-@`.<br><br>* It cannot start or end with a space.<br><br>* `volc:` and `/sys:` are tag keys reserved by the system. You cannot add a tag key that starts with `volc:` or `/sys:` in any case variation.<br><br>* A tag key must be from 1 to 128 characters in length. |
|Value |String |No |demo |Tag value.<br><br><br>* It can contain Chinese characters, uppercase and lowercase letters, digits, and spaces.<br><br>* The following special characters are supported: `_.:/=+-@`.<br><br>* It cannot start or end with a space.<br><br>* The length of a tag key must be 0 to 255 characters. |


<span id="notifytemplatebasic"></span>
### NotifyTemplateBasic


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Channel |String |No |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |No |189828\*\*\*00 |Notification template ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one notification template ID can be specified for each notification channel.</div><br> |


<span id="tagcondition"></span>
### TagCondition


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Tags |Array of [KVComparator](https://docs.byteplus.com/en/docs/39/16292#kvcomparator) |No |\- |A list of tags.<br><br><br>* You can specify up to 10 tags.<br><br>* The label value can be up to 50 characters in length. |
|Condition |String |No |and |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition can be met. |


<span id="metacondition"></span>
### MetaCondition


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Metas |Array of [MetaKVComparator](https://docs.byteplus.com/en/docs/39/16292#metakvcomparator) |No |\- |A list of resources.<br><br><br>* You can configure up to 10 resource names.<br><br>* When `Comparator` is set to `equal` or `not_equal`, the character length is unlimited.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, the resource name cannot exceed 100 characters in length. |
|Condition |String |No |or |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition can be met. |
|AllDimensions |Boolean |No |true |Whether all resources are included.<br><br><br>* **true**: All resources.<br><br>* **false**: Partial resources. |


<span id="projectcondition"></span>
### ProjectCondition


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Projects |Array of String |No |["testDefault1", "testDefault2"] |A list of project names. The data type is array. Separate multiple elements with commas (`,`). |


<span id="kvcomparator"></span>
### KVComparator


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |No |testKey |Tag key. |
|Values |Array of String |No |["testValues", "testValues2"] |Tag value.<br><br><br>* When `Comparator` is set to `exist`, all values corresponding to the key are included. You cannot provide a specific value.<br><br>* When `Comparator` is `equal` or `not_equal`, you can enter multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, you can enter only one value. |
|Comparator |String |No |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to<br><br>* **exist**: exists |


<span id="metakvcomparator"></span>
### MetaKVComparator


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |No |ResourceName |The resource name. Only `ResourceName` is supported. |
|Values |Array of String |No |["testResource1", "testResource2"] |Resource values.<br><br><br>* When `Comparator` is `equal` or `not_equal`, multiple Values can be configured.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, only one value can be configured. |
|Comparator |String |No |equal |Comparator for resource matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=UpdateRule&Version=2018-01-01
Content-Type: application/json
{
    "AlertMethods": [
        ""
    ],
    "ConditionOperator": "&&",
    "Conditions": [
        {
            "Threshold": "100",
            "MetricName": "Instance_CpuBusy",
            "MetricUnit": "Percent",
            "Statistics": "avg",
            "EvaluationWindow": 1,
            "ComparisonOperator": "\\>"
        }
    ],
    "ContactGroupIds": [
        ""
    ],
    "Description": "This is an example of an alert rule",
    "DimensionConditions": {
        "Type": "meta",
        "TagCondition": {
            "Tags": [
                {
                    "Key": "testKey",
                    "Values": [
                        "testValues",
                        "testValues2"
                    ],
                    "Comparator": "equal"
                }
            ],
            "Condition": "and"
        },
        "MetaCondition": {
            "Metas": [
                {
                    "Key": "ResourceName",
                    "Values": [
                        "testResource1",
                        "testResource2"
                    ],
                    "Comparator": "equal"
                }
            ],
            "Condition": "or",
            "AllDimensions": true
        },
        "ProjectCondition": {
            "Projects": [
                "testDefault1",
                "testDefault2"
            ]
        }
    },
    "EffectEndAt": "23:59",
    "EffectStartAt": "00:00",
    "EnableState": "enable",
    "EvaluationCount": 5,
    "EvaluationInterval": 1,
    "Id": "1572416252557******",
    "Level": "critical",
    "LevelConditions": [
        {
            "Level": "warning",
            "Conditions": []
        }
    ],
    "MultipleConditions": true,
    "Namespace": "VCM_ECS",
    "NoData": {
        "Level": "notice",
        "Enable": true,
        "EvaluationCount": 10
    },
    "NotificationId": "1894657089***",
    "NotifyMode": "rule",
    "NotifyTemplates": [
        {
            "Channel": "email",
            "NotifyTemplateId": "189828***00"
        }
    ],
    "OriginalDimensions": {},
    "ProjectName": "default",
    "RecoveryNotify": {
        "Enable": true
    },
    "Regions": [
        "cn-beijing,cn-shanghai"
    ],
    "RuleName": "alarm_rule_demo",
    "RuleType": "static",
    "SilenceTime": 5,
    "SubNamespace": "Instance",
    "Tags": [
        {
            "Key": "doc",
            "Value": "demo"
        }
    ],
    "Webhook": "http://alert.volc.com/callback",
    "WebhookIds": [
        "1894350011***"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |[] |Response data. It is an empty placeholder. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "Result": {
        "Data": [
            ""
        ]
    },
    "ResponseMetadata": {
        "Action": "UpdateRule",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
