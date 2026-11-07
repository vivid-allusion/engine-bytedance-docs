---
title: "ListRulesByIds"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListRulesByIds"
---

Query alert policies based on alert policy IDs.

## Request descriptions

* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListRulesByIds&Version=2018\-01\-01

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListRulesByIds&serviceCode=Volc_Observe&version=2018-01-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListRulesByIds |The name of the API action. The API name is `ListRulesByIds`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Ids |Array of String |Yes |["1502121719593\*\*\*\*\*\*"] |Alert policy ID. |
|ProjectName |String |No |project_1 |Name of the project to which the alert policy belongs. If no project is specified, it defaults to the "default" project. |

## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListRulesByIds&Version=2018-01-01
Content-Type: application/json
{
    "ProjectName": "project_1",
    "Ids": [
        "1502121719593******"
    ]
}
```

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [RuleVO](https://docs.byteplus.com/en/docs/39/16293#rulevo) |\- |Details of the alert policy. |

### RuleVO

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |1502121719593\*\*\*\*\*\* |Alert policy ID. |
|RuleName |String |alarm_rule_demo |Alert policy name. |
|Descriptions |String |this is a alerm rule demo |Description of the alert policy. |
|Namespace |String |VCM_VKE |The cloud product to which the metric belongs. For details, see the **Namespace** field in the [Cloud product metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics). |
|SubNamespace |String |Cluster |The dimension to which the metric belongs. For details, see the **SubNamespace** field for each product on the [Cloud Monitor metric queries](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page. |
|CreatedAt |String |1659421463 |Alert policy creation time as a timestamp. |
|UpdatedAt |String |1659529768 |Last update time of the alert policy as a timestamp. |
|ContactGroupIds |Array of String |["148357472501\*\*\*\*\*\*"] |IDs of contact groups associated with the alert policy. |
|AlertMethods |Array of String |["Email"] |Alert notification method.<br><br><br>* **Email**: Email<br><br>* **Phone**: Phone<br><br>* **SMS**: SMS<br><br>* **Webhook**: Alert callback |
|WebHook |String |http://alert.volc.com/callback |The alert callback URL associated with the alert policy. |
|AlertState |String |normal |Alert status.<br><br><br>* **alerting**: Alerting<br><br>* **normal**: Normal |
|Level |String |critical |The alert level. Valid values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/16293#rulecondition) |\- |Alerting condition. It is an array. You can specify up to 10 metric evaluation statements. |
|OriginalDimensions |JSON Map |\- |Resource ID detected by the alert policy. |
|EffectStartAt |String |00:00 |The time when the policy starts taking effect. The time is in the format `HH:MM`. |
|EffectEndAt |String |23:59 |The time when the policy stops being in effect. The time is in the format `HH:MM`. |
|EnableState |String |enable |Alert policy status.<br><br><br>* **enable**: Enabled<br><br>* **disable**: Disabled |
|Regions |Array of String |["cn\-beijing"] |IDs of the availability zones where the cloud product is used. |
|EvaluationCount |Integer |5 |The duration required to trigger an alert. Unit: minutes. |
|SilenceTime |Integer |5 |Notification intervals. Unit: minutes. Valid values include 5, 30, 60, 180, 360, 720, and 1440. |
|MultipleConditions |Boolean |false |Whether the alert policy uses multiple metrics.<br><br><br>* **true**: Multiple metrics<br><br>* **false**: Single metric (default) |
|ConditionOperator |String |&& |Multi\-metric judgment logic.<br><br><br>*  **&&** : The alert is triggered only when all metrics are satisfied.<br><br>*  **\|\|** : The alert is triggered when any metric meets the condition. |
|RecoveryNotify |Object of [RecoveryNotify](https://docs.byteplus.com/en/docs/39/16293#recoverynotify) |\- |Alert recovery notification. |
|NotifyMode |String |rule |Alert notification aggregation policy.<br><br><br>* **rule** (Default): Rule<br><br>* **Resource**: Rule and resource |
|NoData |Object of [NoData](https://docs.byteplus.com/en/docs/39/16293#nodata) |\- |NoData alert. |
|WebhookIds |Array of String |\- |A list of alert callback IDs when alerts occur. |
|Tags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/39/16293#resourcetag) |\- |Tags associated with the alert policy. |
|Webhook |String |http://alert.volc.com/callback |The alert callback URL associated with the alert policy.<br><br>> **tip**<br><br><br>> You can use `WebHook`, `Webhook`, or `webhook`. For details, see the [official documentation](https://pkg.go.dev/encoding/json#Unmarshal).<br> |
|ProjectName |String |default |Project to which the alert policy belongs. |
|ObjectGroupId |String |group1 |Object group associated with the alert policy. |
|NotificationId |String |189465\*\*\* |Notification policy ID. |
|LevelConditions |Array of [LevelCondition](https://docs.byteplus.com/en/docs/39/16293#levelcondition) |\- |Alert level configuration. |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/16293#notifytemplatebasic) |\- |Notification template configuration. |
|AlertTemplateName |String |template |Name of the alert template associated with the alert policy. |
|DimensionConditions |Object of [DimensionConditions](https://docs.byteplus.com/en/docs/39/16293#dimensionconditions) |\- |Dimension configuration. |

### RuleCondition

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|MetricName |String |Instance_CpuBusy |Name of the metric. For details, see the ** MetricName** field of each cloud product on the [Cloud Monitor metric queries](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|Statistics |String |avg |Statistical method. Values:<br><br><br>* **avg**: Average value.<br><br>* **max**: Maximum value.<br><br>* **min**: Minimum value.<br><br><br>> **tip**<br><br><br>> The statistical method is applied to the data within the detection period. For example, by default, the time span for each data detection is 1 minute. If the statistical method is avg, then the average value of the data within 1 minute is taken.<br> |
|ComparisonOperator |String |\> |Comparison operator. It supports common threshold alerts: \>, \>=, <, <=, !=, =, as well as the following cycle\-over\-cycle and period\-over\-period alerts:<br><br><br>* last_period_increase_pct: Cycle\-over\-cycle increase over the previous period.<br><br>* last_period_decrease_pct: Cycle\-over\-cycle decrease over the previous period.<br><br>* last_period_abs_pct: Cycle\-over\-cycle increase or decrease over the previous period.<br><br>* last_day_increase_pct: Period\-over\-period increase compared to the same period yesterday.<br><br>* last_day_decrease_pct: Period\-over\-period decrease compared to the same period yesterday.<br><br>* last_day_abs_pct: Period\-over\-period increase or decrease compared to the same period yesterday.<br><br>* last_week_increase_pct: Period\-over\-period increase compared to the same period last week.<br><br>* last_week_decrease_pct: Period\-over\-period decrease compared to the same period last week.<br><br>* last_week_abs_pct: Period\-over\-period increase or decrease compared to the same period last week. |
|Threshold |String |100 |Metric threshold.<br><br><br>* It can be a positive number or 0.<br><br>* It supports up to three decimal places. |
|MetricUnit |String |Percent |Metric unit. For details, see the **MetricUnit** field for each cloud product on the [Cloud Monitor metric queries](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page.<br><br>> **tip**<br><br><br><br>* > For cycle\-over\-cycle and period\-over\-period comparison alerts, MetricUnit must be set to "Percent".<br><br><br>* > The presence of "IEC" in MetricUnit indicates different scaling bases:<br><br><br>   * > With IEC: Base\-1024 scaling<br><br><br>   * > Without IEC: Base\-1000 scaling<br> |

### OriginalDimensions

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |ResourceID |Metric dimension name, for example, ResourceID or NodeName. |
|value |Array of String |["i\-123oiuoiu23uiow\*\*\*\*\*","i\-123oiuoiu23uiow\*\*\*\*\*"] |Metric dimension value. |

### RecoveryNotify

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Enable |Boolean |true |Whether to turn on alert recovery notifications. Available types:<br><br><br>* **true**: (Default) Turn on alert recovery notifications.<br><br>* **false**: Turn off alert recovery notifications. |

### NoData

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Enable |Boolean |true |Whether to enable the NoData alert. Available types:<br><br><br>* **true**: Enable the NoData alert.<br><br>* **false**: (Default) Disable the NoData alert. |
|EvaluationCount |Integer |10 |Threshold for triggering the NoData alert. If no data is reported within the configured cycle threshold, a NoData alert will be triggered.<br><br><br>* This field is required if `Enable` is set to `true`.<br><br>* The value is an integer from 3 to 20. |
|Level |String |notice |Level of NoData alert. Available types:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |

### ResourceTag

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |doc |Tag key. |
|Value |String |demo |Tag value. |

### LevelCondition

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Level |String |warning |Alert notification level. Valid values:<br><br><br>* **notice**<br><br>* **warning**<br><br>* **critical**<br><br>* **recovery** |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/16293#rulecondition) |\- |Alert level configuration. |

### NotifyTemplateBasic

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Channel |String |email |Notification channel. Valid values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |189828\*\*\*00 |Notification template ID.<br><br>> **warning**<br><br><br>> Only one notification template ID can be specified for each notification channel.<br> |

### DimensionConditions

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |meta |Dimensions type. Available types:<br><br><br>* **project**: Select alert objects by project.<br><br>* **tag**: Select alert objects by tag.<br><br>* **meta**: Select alert objects by resource name. |
|TagCondition |Object of [TagCondition](https://docs.byteplus.com/en/docs/39/16293#tagcondition) |\- |Tag condition for selecting alert objects. This field is required if `Type` is `tag`. |
|MetaCondition |Object of [MetaCondition](https://docs.byteplus.com/en/docs/39/16293#metacondition) |\- |Resource name condition for selecting alert objects. This field is required if `Type` is `meta`. |
|ProjectCondition |Object of [ProjectCondition](https://docs.byteplus.com/en/docs/39/16293#projectcondition) |\- |Project condition for selecting alert objects. This field is required if `Type` is set to `project`. |

### TagCondition

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Tags |Array of [KVComparator](https://docs.byteplus.com/en/docs/39/16293#kvcomparator) |\- |A list of tags.<br><br><br>* You can specify up to 10 tags.<br><br>* The label value can be up to 50 characters in length. |
|Condition |String |and |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |

### MetaCondition

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Metas |Array of [MetaKVComparator](https://docs.byteplus.com/en/docs/39/16293#metakvcomparator) |\- |A list of resources.<br><br><br>* You can configure up to 10 resource names.<br><br>* When `Comparator` is set to `equal` or `not_equal`, the character length is unlimited.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, the resource name cannot exceed 100 characters in length. |
|Condition |String |or |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |
|AllDimensions |Boolean |true |Whether all resources are included.<br><br><br>* **true**: All resources.<br><br>* **false**: Partial resources. |

### ProjectCondition

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Projects |Array of String |["testDefault1", "testDefault2"] |A list of project names. The data type is array. Separate multiple elements with commas (`,`). |

### KVComparator

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |testKey |Tag key. |
|Values |Array of String |["testValues", "testValues2"] |Tag value.<br><br><br>* When `Comparator` is set to `exist`, all values corresponding to the key are included. You cannot provide a specific value.<br><br>* When `Comparator` is set to `equal` or `not_equal`, you can enter multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, you can enter only one value. |
|Comparator |String |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to<br><br>* **exist**: Exists |

### MetaKVComparator

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |ResourceName |The resource name. Only `ResourceName` is supported. |
|Values |Array of String |["testResource1", "testResource2"] |Resource values.<br><br><br>* When `Comparator` is set to `equal` or `not_equal`, you can configure multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, only one value can be configured. |
|Comparator |String |equal |Comparator for resource matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |

## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListRulesByIds",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "1502121719593******",
                "Tags": [
                    {
                        "Key": "doc",
                        "Value": "demo"
                    }
                ],
                "Level": "critical",
                "NoData": {
                    "Level": "",
                    "Enable": true,
                    "EvaluationCount": 10
                },
                "Regions": [
                    "cn-beijing"
                ],
                "WebHook": "http://alert.volc.com/callback",
                "RuleName": "alarm_rule_demo",
                "CreatedAt": "1659421463",
                "Namespace": "VCM_VKE",
                "UpdatedAt": "1659529768",
                "AlertState": "normal",
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
                "Description": "this is a alerm rule demo",
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
                "NotificationId": "189465***",
                "RecoveryNotify": {
                    "Enable": true
                },
                "ContactGroupIds": [
                    "148357472501******"
                ],
                "EvaluationCount": 5,
                "LevelConditions": [
                    {
                        "Level": "warning",
                        "Conditions": []
                    }
                ],
                "NotifyTemplates": [
                    "Channel": "email",
                    "NotifyTemplateId": "189828***00"
                ],
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
        ]
    }
}
```

## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
