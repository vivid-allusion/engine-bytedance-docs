---
title: "ListRules"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListRules"
---

Query alert policies based on specified conditions.

## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is the most optimal for the region of your services.

* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListRules&Version=2018\-01\-01

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListRules&serviceCode=Volc_Observe&version=2018-01-01&groupName=)

## Request parameters

> **tip**

> Multiple conditions in the request parameter are in a logical **AND** relationship.

|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListRules |The name of the API. The API name is `ListRules`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|RuleName |String |No |alarm_rule_demo |Name of the alert policy. The system will perform fuzzy matching based on this name.<br><br><br>* The name must be 1 to 128 characters in length.<br><br>* It cannot start with a digit or hyphen (`-`). |
|RuleIds |Array of String |No |['189436315\*\*\*'] |An array of alert policy IDs. Separate multiple values with commas (`,`). If an ID is specified, ID\-based querying is prioritized. |
|AlertState |Array of String |No |["normal"] |Alert policy status.<br><br><br>* **alerting**: Alerting<br><br>* **normal**: Normal<br><br><br>> **tip**<br><br><br>> You can specify multiple options. If you specify multiple options, separate them with comma (`,`), as in ["normal","alerting"].<br> |
|Namespace |Array of String |No |["VCM_ECS"] |The cloud product to which the metric belongs. For details, see the **Namespace** for each cloud product on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page.<br><br>> **tip**<br><br><br>> Multiple options can be selected. Separate multiple options with commas (,), for example, ["VCM_ECS","VCM_VKE"].<br> |
|Level |Array of String |No |["critical"] |Alert policy level.<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice**<br><br><br>> **tip**<br><br><br>> Multiple options can be selected. If you specify multiple options, separate them with commas (`,`), as in ["critical","warning"].<br> |
|EnableState |Array of String |No |["enable"] |Alert policy status.<br><br><br>* **enable**: Enabled<br><br>* **disable**: Disabled<br><br><br>> **tip**<br><br><br>> Multiple options can be selected. If you specify multiple options, separate them with commas (`,`), as in ["enable","disable"].<br> |
|PageSize |Integer |No |30 |The number of rows per page for a pagination query. The default value is 30. |
|PageNumber |Integer |No |1 |The page number for a pagination query. The default value is 1.<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|RuleType |String |No |static |The type of selecting alert objects.<br><br><br>* **static**: Static selection.<br><br>* **dynamic**: Dynamic select by resource name, project, and tag. |
|Dimensions |Array of JSON Map |No |\- |The Dimensions field of the cloud service is used to filter alert policies.<br><br>> **warning**<br><br><br><br>* > When this field is used to filter alert policies, the `Namespace` parameter must be specified. Otherwise, an error is reported.<br><br><br>* > The number of alert policies per dimension cannot exceed 30.<br> |
|NotificationId |String |No |18946\*\*\* |Alerting notify policy ID. |
|ProjectName |String |No |project_1 |Name of the project to which the alert policy belongs. If no project is specified, it defaults to the "default" project. |
|TagFilters |Array of [ListTagFilter](https://docs.byteplus.com/en/docs/39/16294#listtagfilter) |No |\- |Tags to be used as filters for alert policies. |
|AlertTemplateIds |Array of String |No |['1963447872315\*\*\*'] |Alert template ID. You can perform the query with alert template IDs as a filter. |
|ObjectGroupIds |Array of String |No |['196349165826\*\*\*'] |Object group IDs. You can perform the query with object group IDs as a filter. |

### Dimensions

|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|key |String |Yes |ResourceID |Dimensions fields supported by the cloud service. For example, `ResourceID` and `NodeName`. Dimensions supported by different cloud products vary. For details, see [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/docs). |
|value |String |Yes |i\-ydq828\*\*\* |The value corresponding to the Dimensions field key. For example, for ECS, when the key is ResourceID, the value is the ECS instance ID. |

### ListTagFilter

|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |No |doc |Tag key. |
|Values |Array of String |No |demo |Tag value. |

## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListRules&Version=2018-01-01
Content-Type: application/json
{
    "AlertState": [
        "normal"
    ],
    "AlertTemplateIds": [
        ""
    ],
    "Dimensions": [],
    "EnableState": [
        "enable"
    ],
    "Level": [
        "critical"
    ],
    "Namespace": [
        "VCM_ECS"
    ],
    "NotificationId": "18946***",
    "ObjectGroupIds": [
        ""
    ],
    "PageNumber": 1,
    "PageSize": 30,
    "ProjectName": "project_1",
    "RuleIds": [
        ""
    ],
    "RuleName": "alarm_rule_demo",
    "RuleType": "static",
    "TagFilters": [
        {
            "Key": "doc",
            "Values": [
                ""
            ]
        }
    ]
}
```

## Response parameters

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [RuleVO](https://docs.byteplus.com/en/docs/39/16294#rulevo) |\- |Details of the alert policy. |
|TotalCount |Integer |2 |The number of alert policies that meet the criteria. |

### RuleVO

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |1502121719593\*\*\*\*\*\* |Alert policy ID. |
|RuleName |String |alarm_rule_demo |Alert policy name. |
|Descriptions |String |this is a alerm rule demo |Description of the alert policy. |
|Namespace |String |VCM_VKE |The cloud product to which the metric belongs. For details, see the **Namespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|SubNamespace |String |Cluster |The dimension to which the metric belongs. For details, see the **SubNamespace** field for each product on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page. |
|CreatedAt |String |1659421463 |Alert policy creation time as a timestamp. |
|UpdatedAt |String |1659529768 |Last update time of the alert policy as a timestamp. |
|ContactGroupIds |Array of String |["148357472501\*\*\*\*\*\*"] |IDs of contact groups associated with the alert policy. |
|AlertMethods |Array of String |["Email"] |Alert notification method.<br><br><br>* **Email**: Email<br><br>* **Phone**: Phone<br><br>* **SMS**: SMS<br><br>* **Webhook**: Alert callback |
|WebHook |String |http://alert.volc.com/callback |The alert callback URL associated with the alert policy. |
|AlertState |String |normal |Alert status.<br><br><br>* **alerting**: Alerting<br><br>* **normal**: Normal |
|Level |String |critical |The alert level.<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/16294#rulecondition) |\- |Alerting condition. It is an array. You can specify up to 10 metric evaluation statements. |
|OriginalDimensions |JSON Map |\- |Resource ID monitored by the alert policy. |
|EffectStartAt |String |00:00 |The time when the policy starts taking effect. The time is in the format `HH:MM`. |
|EffectEndAt |String |23:59 |The time when the policy stops being in effect. The time is in the format `HH:MM`. |
|EnableState |String |enable |Alert policy status.<br><br><br>* **enable**: Enabled<br><br>* **disable**: Disabled |
|Regions |Array of String |["cn\-beijing"] |IDs of the availability zones where the cloud product is used. |
|EvaluationCount |Integer |5 |The duration required to trigger an alert. The unit is minutes. |
|SilenceTime |Integer |5 |Notification intervals. The unit is minutes. Valid values include 5, 30, 60, 180, 360, 720, and 1440. |
|MultipleConditions |Boolean |false |Whether the alert policy uses multiple metrics.<br><br><br>* **true**: Multiple metrics<br><br>* **false**: Use a single metric (default). |
|ConditionOperator |String |&& |Multi\-metric judgment logic.<br><br><br>*  **&&** : The alert is triggered only when all metrics are satisfied.<br><br>*  **\|\|** : The alert is triggered when any metric meets the condition. |
|RecoveryNotify |Object of [RecoveryNotify](https://docs.byteplus.com/en/docs/39/16294#recoverynotify) |\- |Alert recovery notification. |
|NotifyMode |String |rule |Alert notification aggregation policy.<br><br><br>* **rule** (Default): Rule<br><br>* **Resource**: Rule and resource |
|NoData |Object of [NoData](https://docs.byteplus.com/en/docs/39/16294#nodata) |\- |NoData alert. |
|WebhookIds |Array of String |\- |A list of alert callback IDs when alerts occur. |
|Tags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/39/16294#resourcetag) |\- |Tags associated with the alert policy. |
|Webhook |String |http://alert.volc.com/callback |The alert callback URL associated with the alert policy.<br><br>> **tip**<br><br><br>> You can use `WebHook`, `Webhook`, or `webhook`. For details, see the [official documentation](https://pkg.go.dev/encoding/json#Unmarshal).<br> |
|ProjectName |String |default |Project to which the alert policy belongs. |
|ObjectGroupId |String |group1 |Object group associated with the alert policy. |
|NotificationId |String |189465\*\*\* |Notification policy ID. |
|LevelConditions |Array of [LevelCondition](https://docs.byteplus.com/en/docs/39/16294#levelcondition) |\- |Alert level configuration. |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/16294#notifytemplatebasic) |\- |Notification template configuration. |
|AlertTemplateName |String |template |Name of the alert template associated with the alert policy. |
|EvaluationInterval |Integer |1 |The check interval is used to trigger N alerts within M intervals. EvaluationInterval indicates M, and EvaluationCount indicates N.<br><br>EvaluationInterval is equal to CheckInterval multiplied by EvaluationCount. If EvaluationInterval is left empty, the value of EvaluationCount is used by default. |
|DimensionConditions |Object of [DimensionConditions](https://docs.byteplus.com/en/docs/39/16294#dimensionconditions) |\- |Dimension configuration. |

### RuleCondition

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|MetricName |String |Instance_CpuBusy |Name of the metric. For details, see the **MetricName** field for each cloud product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|Statistics |String |avg |Statistical method. Values:<br><br><br>* **avg**: Average value.<br><br>* **max**: Maximum value.<br><br>* **min**: Minimum value.<br><br><br>> **tip**<br><br><br>> The statistical method is applied to the data within the detection period. For example, by default, the time span for each data detection is 1 minute. If the statistical method is avg, then the average value of the data within 1 minute is taken.<br> |
|ComparisonOperator |String |\> |Comparison operator. It supports common threshold alerts: \>, \>=, <, <=, !=, =, as well as the following cycle\-over\-cycle and period\-over\-period alerts:<br><br><br>* last_period_increase_pct: Cycle\-over\-cycle increase over the previous period.<br><br>* last_period_decrease_pct: Cycle\-over\-cycle decrease over the previous period.<br><br>* last_period_abs_pct: Cycle\-over\-cycle increase or decrease over the previous period.<br><br>* last_day_increase_pct: Period\-over\-period increase compared to the same period yesterday.<br><br>* last_day_decrease_pct: Period\-over\-period decrease compared to the same period yesterday.<br><br>* last_day_abs_pct: Period\-over\-period increase or decrease compared to the same period yesterday.<br><br>* last_week_increase_pct: Period\-over\-period increase compared to the same period last week.<br><br>* last_week_decrease_pct: Period\-over\-period decrease compared to the same period last week.<br><br>* last_week_abs_pct: Period\-over\-period increase or decrease compared to the same period last week. |
|Threshold |String |100 |Metric threshold.<br><br><br>* It can be a positive number or 0.<br><br>* It supports up to three decimal places. |
|MetricUnit |String |Percent |Metric unit. For details, see the **MetricUnit** field on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page for the corresponding cloud product.<br><br>> **tip**<br><br><br><br>* > For cycle\-over\-cycle and period\-over\-period comparison alerts, MetricUnit must be set to "Percent".<br><br><br>* > The presence of "IEC" in MetricUnit indicates different scaling bases:<br><br><br>   * > With IEC: The unit base is 1024.<br><br><br>   * > Without IEC: Base\-1000 scaling<br> |
|Period |String |60 |Statistics cycles. |
|EvaluationWindow |Integer |1 |The time window for statistics is the time period over which alert statistics are collected. |

### OriginalDimensions

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|key |String |ResourceID |Metric dimension name, for example, ResourceID or NodeName. |
|value |Array of String |["i\-123oiuoiu23uiow\*\*\*\*\*","i\-123oiuoiu23uiow\*\*\*\*\*"] |Metric Dimension value. |

### RecoveryNotify

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Enable |Boolean |true |Whether to turn on alert recovery notifications. Available types:<br><br><br>* **true**: (Default) Turn on alert recovery notifications.<br><br>* **false**: Turn off alert recovery notifications. |

### NoData

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Enable |Boolean |true |Whether to enable the NoData alert. Available types:<br><br><br>* **true**: Enable the NoData alert.<br><br>* **false**: (Default) Disable the NoData alert. |
|EvaluationCount |Integer |10 |Threshold for triggering the NoData alert. If no data is reported within the configured cycle threshold, a NoData alert will be triggered.<br><br><br>* This field is required if `Enable` is set to `true`.<br><br>* The value is an integer from 3 to 20. |
|Level |String |notice |NoData alert level. Available types:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |

### ResourceTag

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |doc |Tag key. |
|Value |String |demo |Tag value. |

### LevelCondition

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Level |String |warning |Alert notification level. Valid values:<br><br><br>* **notice**<br><br>* **warning**<br><br>* **critical**<br><br>* **recovery** |
|Conditions |Array of [RuleCondition](https://docs.byteplus.com/en/docs/39/16294#rulecondition) |\- |Alert level configuration. |

### NotifyTemplateBasic

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Channel |String |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |189828\*\*\*00 |Notification template ID.<br><br>> **warning**<br><br><br>> Only one notification template ID can be specified for each notification channel.<br> |

### DimensionConditions

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |meta |Dimensions type. Available types:<br><br><br>* **project**: Select alert object by project.<br><br>* **tag**: Select alert objects by tag.<br><br>* **meta**: Select alert objects by resource name. |
|TagCondition |Object of [TagCondition](https://docs.byteplus.com/en/docs/39/16294#tagcondition) |\- |Tag condition for selecting alert objects. This field is required if `Type` is `tag`. |
|MetaCondition |Object of [MetaCondition](https://docs.byteplus.com/en/docs/39/16294#metacondition) |\- |Resource name condition for selecting alert objects. This field is required if `Type` is `meta`. |
|ProjectCondition |Object of [ProjectCondition](https://docs.byteplus.com/en/docs/39/16294#projectcondition) |\- |Project condition for selecting alert objects. This field is required if `Type` is set to `project`. |

### TagCondition

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Tags |Array of [KVComparator](https://docs.byteplus.com/en/docs/39/16294#kvcomparator) |\- |A list of tags.<br><br><br>* You can specify up to 10 tags.<br><br>* The label value can be up to 50 characters in length. |
|Condition |String |and |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition can be met. |

### MetaCondition

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Metas |Array of [MetaKVComparator](https://docs.byteplus.com/en/docs/39/16294#metakvcomparator) |\- |A list of resources.<br><br><br>* You can configure up to 10 resource names.<br><br>* When `Comparator` is set to `equal` or `not_equal`, the character length is unlimited.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, the resource name cannot exceed 100 characters in length. |
|Condition |String |or |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition can be met. |
|AllDimensions |Boolean |true |Whether all resources are included.<br><br><br>* **true**: All resources.<br><br>* **false**: Partial resources. |

### ProjectCondition

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Projects |Array of String |["testDefault1", "testDefault2"] |A list of project names. The data type is array. Separate multiple elements with commas (`,`). |

### KVComparator

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |testKey |Tag key. |
|Values |Array of String |["testValues", "testValues2"] |Tag value.<br><br><br>* When `Comparator` is set to `exist`, all values corresponding to the key are included. You cannot provide a specific value.<br><br>* When `Comparator` is `equal` or `not_equal`, you can enter multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, you can enter only one value. |
|Comparator |String |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to<br><br>* **exist**: exists |

### MetaKVComparator

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |ResourceName |The resource name. Only `ResourceName` is supported. |
|Values |Array of String |["testResource1", "testResource2"] |Resource values.<br><br><br>* When `Comparator` is `equal` or `not_equal`, multiple Values can be configured.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, only one value can be configured. |
|Comparator |String |equal |Comparator for resource matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |

## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListRules",
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
                    "Level": "notice",
                    "Enable": true,
                    "EvaluationCount": 10
                },
                "Regions": [
                    "cn-beijing"
                ],
                "WebHook": "http://alert.volc.com/callback",
                "Webhook": "http://alert.volc.com/callback",
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
                        "EvaluationWindow": 1,
                        "ComparisonOperator": "\\>"
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
                    {
                        "Channel": "email",
                        "NotifyTemplateId": "189828***00"
                    }
                ],
                "AlertTemplateName": "template",
                "ConditionOperator": "&&",
                "EvaluationInterval": 1,
                "MultipleConditions": false,
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
                }
            }
        ]
    }
}
```

## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
