---
title: "ListRulesByInstanceId"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListRulesByInstanceId"
---

Query associated alert policies by resource instance ID.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListRulesByInstanceId&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListRulesByInstanceId&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListRulesByInstanceId |The name of the API. The API name is `ListRulesByInstanceId`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|InstanceId |String |Yes |i\-ydeqc\*\*\* |Resource instance ID. |
|Namespace |String |No |VCM_ECS |The cloud product to which the metric belongs. For details, see the **Namespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|PageNumber |Integer |No |1 |The page number for a pagination query. The default value is 1.<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|PageSize |Integer |No |10 |The number of rows per page for a pagination query. The default value is 30. |
|ProjectName |String |No |default |The project name. If no project is specified, it defaults to the "default" project. For more project introductions, refer to [Managing projects](https://docs.byteplus.com/en/docs/6649/94336). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListRulesByInstanceId&Version=2018-01-01
Content-Type: application/json
{
    "InstanceId": "i-ydeqcxxxxxxftuwzc",
    "Namespace": "VCM_ECS",
    "PageNumber": 1,
    "PageSize": 10,
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [RuleVO](https://docs.byteplus.com/en/docs/39/63272#rulevo) |\- |The details of the alarm strategy. |
|PageSize |Integer |30 |The number of rows per page for a pagination query. The default value is 30. |
|PageNumber |Integer |1 |The page number for a pagination query. The default value is 1. |
|TotalCount |Integer |2 |Total number of object groups that meet the criteria. |


<span id="rulevo"></span>
### RuleVO


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |1502121719593\*\*\*\*\*\* |Alert policy ID. |
|RuleName |String |alarm_rule_demo |Alert policy name. |
|Descriptions |String |This is a sample alert policy. |Description of the alert policy. |
|Namespace |String |VCM_VKE |The cloud product to which the metric belongs. For details, see the **Namespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|SubNamespace |String |Cluster |Category to which the metric belongs. For details, see the **SubNamespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|CreatedAt |String |1659421463 |Alert policy creation time as a timestamp. |
|UpdatedAt |String |1659529768 |Last update time of the alert policy as a timestamp. |
|ContactGroupIds |Array of String |["148357472501\*\*\*\*\*\*"] |IDs of contact groups associated with the alert policy.<br><br><br>* Up to 5 contact groups can be selected.<br><br>* This parameter is required if `AlertMethods` is `Email`, `Phone`, or `SMS`. |
|AlertMethods |Array of String |["Email"] |Alert notification method.<br><br><br>* **Email**: Email<br><br>* **Phone**: Phone<br><br>* **SMS**: SMS<br><br>* **Webhook**: Alert callback |
|WebHook |String |https://open.larkoffice.com/open\-apis/bot/v2/hook/8bf5d3b9\*\*\* |Webhook address of the alert callback. |
|AlertState |String |normal |Alert status.<br><br><br>* **alerting**: Alerting<br><br>* **normal**: Normal |
|Level |String |critical |The alarm level. Valid values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/63272#rulecondition) |\- |Alerting condition. The data type is array. You can specify up to 10 metric evaluation statements. |
|OriginalDimensions |JSON Map |\- |Resource ID detected by the alert policy. |
|EffectStartAt |String |00:00 |The time when the policy starts taking effect. The time is in the format `HH:MM` (for example, 00:00). |
|EffectEndAt |String |23:59 |The time when the alert policy stops being in effect. The time is in the format `HH:MM` (example: 23:59).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>EffectEndAt</code> time must be later than the <code>EffectStartAt</code> time.</div><br> |
|EnableState |String |enable |Alert policy status.<br><br><br>* **enable**: Enabled<br><br>* **disable**: Disabled |
|Regions |Array of String |["cn\-beijing,cn\-shanghai"] |IDs of the availability zones where the cloud product is used.<br><br><br>* When `RuleType` is `static`, only one region ID can be specified.<br><br>* When `RuleType` is `dynamic`, multiple Region IDs can be specified. Separate multiple region IDs with commas (`,`). |
|EvaluationCount |Integer |5 |The duration required to trigger an alert. Unit: minutes. |
|SilenceTime |Integer |5 |Notification intervals. Unit: minutes. Valid values include 5, 30, 60, 180, 360, 720, and 1440. |
|MultipleConditions |Boolean |false |Whether the alert policy uses multiple metrics.<br><br><br>* **true**: Use multiple metrics.<br><br>* **false**: (Default) Use a single metric. |
|ConditionOperator |String |&& |Multi\-metric judgment logic.<br><br><br>*  **&&** : The alert is triggered only when all metrics are satisfied.<br><br>*  **\|\|** : The alert is triggered when any metric meets the condition. |
|RecoveryNotify |Object of [RecoveryNotify](https://docs.byteplus.com/en/docs/39/63272#recoverynotify) |\- |Alert recovery notification. |
|NotifyMode |String |rule |Alert notification aggregation policy.<br><br><br>* **rule** (default): Aggregate alerts by rule.<br><br>* **Resource**: Aggregate alerts by rule and resource. |
|NoData |Object of [NoData](https://docs.byteplus.com/en/docs/39/63272#nodata) |\- |NoData alert. |
|WebhookIds |Array of String |["https://open.larkoffice.com/open\-apis/bot/v2/hook/8bf5d3b9\*\*\*","https://open.larkoffice.com/open\-apis/bot/v2/hook/a3d2af9\*\*\*"] |A list of alert callback IDs when alerts occur. |
|RuleType |String |static |The type of selecting alert objects.<br><br><br>* **static**: Static selection.<br><br>* **dynamic**: Dynamic select by resource name, project, and tag. |
|ObjectGroupId |String |group1 |Object group associated with the alert policy. |
|AlertTemplateName |String |template |Name of the alert template associated with the alert policy. |
|DimensionConditions |Object of [DimensionConditions](https://docs.byteplus.com/en/docs/39/63272#dimensionconditions) |\- |Dimension configuration. |
|ProjectName |String |default |Project to which the alert policy belongs. |
|NotificationId |String |189465\*\*\* |Notification policy ID. |
|LevelConditions |Array of [LevelCondition](https://docs.byteplus.com/en/docs/39/63272#levelcondition) |\- |Alert level configuration. |


<span id="rulecondition"></span>
### RuleCondition


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|MetricName |String |Instance_CpuBusy |Name of the metric. For details, see the **MetricName** field on the [Cloud Monitor metric query](https://docs.byteplus.com/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|Statistics |String |avg |Statistical method for the metric. Values:<br><br><br>* **avg**: Average value.<br><br>* **max**: Maximum value.<br><br>* **min**: Minimum value.<br><br>   The statistical method is applied to the data within the detection period. For example, if the detection period is 1 minute and the statistical method is avg, the system will calculate the average value of the data within 1 minute. |
|ComparisonOperator |String |\> |Comparator. It supports common threshold alerts: \>, \>=, <, <=, !=, =, as well as the following cycle\-over\-cycle and period\-over\-period alerts:<br><br><br>* last_period_increase_pct: Cycle\-over\-cycle increase over the previous period.<br><br>* last_period_decrease_pct: Cycle\-over\-cycle decrease over the previous period.<br><br>* last_period_abs_pct: Cycle\-over\-cycle increase or decrease over the previous period.<br><br>* last_day_increase_pct: Period\-over\-period increase compared to the same period yesterday.<br><br>* last_day_decrease_pct: Period\-over\-period decrease compared to the same period yesterday.<br><br>* last_day_abs_pct: Period\-over\-period increase or decrease compared to the same period yesterday.<br><br>* last_week_increase_pct: Period\-over\-period increase compared to the same period last week.<br><br>* last_week_decrease_pct: Period\-over\-period decrease compared to the same period last week.<br><br>* last_week_abs_pct: Period\-over\-period increase or decrease compared to the same period last week. |
|Threshold |String |80 |Metric threshold.<br><br><br>* It can be a positive number or 0.<br><br>* It supports up to three decimal places. |
|MetricUnit |String |Percent |Metric unit. For details, see the **MetricUnit** field on the [Cloud Monitor metric query](https://docs.byteplus.com/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For cycle\-over\-cycle and period\-over\-period comparison alerts, MetricUnit must be set to <code>Percent</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Whether IEC is included in MetricUnit indicates different unit bases.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">With IEC: The unit base is 1024.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Without IEC: The unit base is 1000.</div><br> |
|Level |String |critical |The alarm level. Valid values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field must be consistent with <code>LevelCondition.Level</code>.</div><br> |


<span id="originaldimensions"></span>
### OriginalDimensions


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|key |String |ResourceID |Dimension key, such as `ResourceID` or `NodeName`. |
|value |Array of String |["i\-ybw74rtkvd9z6f\*\*\*\*\*\*", "i\-ybvwojvnep9z6g\*\*\*\*\*\*"] |Metric Dimension value. The data type is array. You can use the wildcard character `*` to select all instances. For example, you can set it to ["\*"]. |


<span id="recoverynotify"></span>
### RecoveryNotify


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Enable |Boolean |true |Whether to turn on alert recovery notifications. Available types:<br><br><br>* **true**: (Default) Turn on alert recovery notifications.<br><br>* **false**: Turn off alert recovery notifications. |


<span id="nodata"></span>
### NoData


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Enable |Boolean |true |Whether to enable the NoData alert. Available types:<br><br><br>* **true**: Enable the NoData alert.<br><br>* **false**: (Default) Disable the NoData alert. |
|EvaluationCount |Integer |10 |Threshold for triggering the NoData alert. If no data is reported within the configured cycle threshold, a NoData alert will be triggered.<br><br><br>* This field is required if `Enable` is set to `true`.<br><br>* The value is an integer from 3 to 20. |
|Level |String |critical |Level of NoData alert.<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |


<span id="dimensionconditions"></span>
### DimensionConditions


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Type |String |meta |Dimensions type. Available types:<br><br><br>* **project**: Select alert object by project.<br><br>* **tag**: Select alert objects by tag.<br><br>* **meta**: Select alert objects by resource name. |
|TagCondition |Object of [TagCondition](https://docs.byteplus.com/en/docs/39/63272#tagcondition) |\- |Tag condition for selecting alert objects. This field is required if `Type` is `tag`. |
|MetaCondition |Object of [MetaCondition](https://docs.byteplus.com/en/docs/39/63272#metacondition) |\- |Resource name condition for selecting alert objects. This field is required if `Type` is `meta`. |
|ProjectCondition |Object of [ProjectCondition](https://docs.byteplus.com/en/docs/39/63272#projectcondition) |\- |Project condition for selecting alert objects. This field is required if `Type` is set to `project`. |


<span id="levelcondition"></span>
### LevelCondition


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Level |String |warning |The alarm level. Valid values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/63272#rulecondition) |\- |Alert rule details. |


<span id="tagcondition"></span>
### TagCondition


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Tags |Array of [KVComparator](https://docs.byteplus.com/en/docs/39/63272#kvcomparator) |\- |A list of tags.<br><br><br>* You can specify up to 10 tags.<br><br>* The label value can be up to 50 characters in length. |
|Condition |String |and |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |


<span id="metacondition"></span>
### MetaCondition


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Metas |Array of [MetaKVComparator](https://docs.byteplus.com/en/docs/39/63272#metakvcomparator) |\- |A list of resources.<br><br><br>* You can configure up to 10 resource names.<br><br>* When `Comparator` is set to `equal` or `not_equal`, no character length limit is applied to the resource name.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, the resource name cannot exceed 100 characters in length. |
|Condition |String |or |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |
|AllDimensions |Boolean |true |Whether all resources are included.<br><br><br>* **true**: All resources.<br><br>* **false**: Partial resources. |


<span id="projectcondition"></span>
### ProjectCondition


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Projects |Array of String |["testDefault1", "testDefault2"] |A list of project names. The data type is array. Separate multiple elements with commas (`,`). |


<span id="kvcomparator"></span>
### KVComparator


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Key |String |testKey |Tag key. |
|Values |Array of String |["testValues", "testValues2"] |Tag value.<br><br><br>* When `Comparator` is set to `exist`, all values corresponding to the key are included. You cannot provide a specific value.<br><br>* When `Comparator` is `equal` or `not_equal`, you can enter multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, you can enter only one value. |
|Comparator |String |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to<br><br>* **exist**: Exists |


<span id="metakvcomparator"></span>
### MetaKVComparator


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Key |String |ResourceName |The resource name. Only `ResourceName` is supported. |
|Values |Array of String |["testResource1", "testResource2"] |Resource values.<br><br><br>* When `Comparator` is set to `equal` or `not_equal`, you can configure multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, only one value can be configured. |
|Comparator |String |equal |Comparator for resource matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |
|TagKey |String |test |The actual key used for alert grouping. For example, in alert suppression, use this key to match with `tag.key` in alertGroup. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "ListRulesByInstanceId",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "RuleName": "alarm_rule_demo",
                "RuleType": "static",
                "CreatedAt": "1659421463",
                "Namespace": "VCM_VKE",
                "UpdatedAt": "1659529768",
                "AlertState": "normal",
                "Id": "1502121719593******",
                "Level": "critical",
                "NoData": {
                    "Enable": true,
                    "EvaluationCount": 10
                },
                "Regions": [
                    "cn-beijing,cn-shanghai"
                ],
                "WebHook": "http://alert.volc.com/callback",
                "Conditions": [
                    {
                        "Threshold": "100",
                        "MetricName": "Instance_CpuBusy",
                        "MetricUnit": "Percent",
                        "Statistics": "avg",
                        "ComparisonOperator": ">"
                    }
                ],
                "NotifyMode": "rule",
                "WebhookIds": [
                    ""
                ],
                "Description": "这是一个告警策略样例",
                "EffectEndAt": "23:59",
                "EnableState": "enable",
                "ProjectName": "default",
                "SilenceTime": 5,
                "AlertMethods": [
                    "Email"
                ],
                "SubNamespace": "Cluster",
                "EffectStartAt": "00:00",
                "ObjectGroupId": "group1",
                "RecoveryNotify": {
                    "Enable": true
                },
                "ContactGroupIds": [
                    "148357472501******"
                ],
                "EvaluationCount": 5,
                "AlertTemplateName": "template",
                "ConditionOperator": "&&",
                "MultipleConditions": true,
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
                                "TagKey": "test",
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
                }
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

&nbsp;
