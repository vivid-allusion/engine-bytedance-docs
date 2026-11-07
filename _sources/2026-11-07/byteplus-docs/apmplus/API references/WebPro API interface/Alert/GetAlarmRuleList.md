---
title: "GetAlarmRuleList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmRuleList"
---

Get the alert task list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmRuleList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmRuleList |The name of the API action. The API name is `GetAlarmRuleList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67920#common) |No |\- |Common parameters. |
|self |Integer |No |1 |Whether to return the list of tasks managed by me.<br><br><br>* 1: Returns the tasks managed by me.<br><br>* 0: Returns all. |
|category_list |Array of String |No |["pageview"] |Alert type filtering.<br><br>If not specified, alert tasks of all alert types are returned. If specified, alert tasks of the specified alert type are returned. Call the `GetAlarmMeta` API to view available values. |
|keyword |String |No |test |Fuzzy search by alert task name.<br><br>If not specified, all alert tasks are returned. If specified, alert tasks whose task names meet the condition are returned. |
|page_num |Long |No |1 |The page number for a pagination query. Default value: 1. |
|page_size |Long |No |30 |The number of items per page for a pagination query. Default value: 30. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |The service type. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmRuleList&Version=2022-10-12
{
    "common":{
        "aid":12345,
        "os":"webpro"
    },
    "category_list":[
        "pageview"
    ],
    "keyword":"test",
    "self":1,
    "page_num":1,
    "page_size":10
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67920#data) |\- |Returned data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_rule_list |Array of [AlarmRuleList](https://docs.byteplus.com/en/docs/299/67920#alarmrulelist) |\- |Alert task list. |
|count |Integer |1 |Alert task count. |

### AlarmRuleList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_param |Object of [AlarmParam](https://docs.byteplus.com/en/docs/299/67920#alarmparam) |\- |Alert parameter set. |
|created_by |String |leeac |Alert task creator. |
|updated_by |String |leeac |Last modifier of the alert task. |
|created_time |Long |1665409567 |Alert task creation time. |
|updated_time |Long |1665409567 |The latest modification time of the alert task. |
|next_trigger_time |Long |1665409867 |Next trigger time of the alert task. |
|last_execute_time |Long |0 |Last execution time of the alert task. |
|ack_until_time |Long |0 |ACK expiration time of alert task. |
|num_of_alarm_in_last_one_month |Integer |0 |Alert task alert count in the last month. |

### AlarmParam

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1 |Alert task ID. |
|name |String |test |Alert task name. |
|desc |String |\- |Alert description. |
|category |String |pageview |Alert type. Call `GetAlarmMeta` API to view available values. |
|alarm_level |String |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/67920#strategylist) |\- |A list of alert policies. |
|strategy_op |String |and |Multi\-policy relationship.<br><br><br>* and: All policies must be satisfied simultaneously.<br><br>* or: Any policy is satisfied. |
|interval_seconds |Integer |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/67920#alarmperiod) |\- |The time period during which an alert notification can be triggered. Alerts outside the time period will not trigger notifications. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/67920#notifyconfig) |\- |The alert notification configuration. |
|is_avoid_spike |Boolean |false |Whether to silence spike alerts. |
|pct_avoid_spike |Object of [PctAvoidSpike](https://docs.byteplus.com/en/docs/299/67920#pctavoidspike) |\- |pct alert parameter. This parameter is required when pct alert silence is enabled. |

### StrategyList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/67920#measure) |\- |The metric set for the current policy, including simple and composite metrics. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67920#filterlist) |\- |Filtering conditions of alert policies. |
|alarm_strategy_type |String |threshold |Alert policy type.<br><br><br>* threshold: Threshold\-based alert<br><br>* cmp_last_n_day: Difference\-based alert |
|daily_compare_count |Integer |5 |Time interval between the previous period and the current period.<br><br>This parameter is required when the alert policy is difference\-based. The unit is minutes. For example, 1440 sets the comparison offset to 1 day ago. |
|alarm_threshold |Double |10 |The alert threshold. |
|threshold_cmp_op |String |gt |The operator for the alert threshold, indicating the policy operator.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |1 |User count threshold. |
|alarm_sample_threshold |Double |1 |Sample size threshold. |
|alarm_window_size |Long |180 |Time window for querying alert tasks. It represents the last X minutes. The unit is minutes. |
|group_bys |Array of [GroupBys](https://docs.byteplus.com/en/docs/299/67920#groupbys) |\- |Alert grouping dimensions. |
|attribution_dimensions |Array of [AttributionDimensions](https://docs.byteplus.com/en/docs/299/67920#attributiondimensions) |\- |Alert attribution dimension. |

### AlarmPeriod

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|start_time |Integer |0 |The start of the time period during which an alert notification can be triggered.<br><br>The value is the start timestamp in seconds relative to 0:00 of the current day. For example, if the start time is 2:00 on the current day, the value is 7200. |
|end_time |Integer |86399 |Alert end time.<br><br>The value is the end timestamp in seconds relative to 0:00 of the current day. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|notify_types |Array of String |["mail"] |The alert notification method.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_lark_webhooks |Array of String |[] |A list of Feishu notification webhooks.<br><br>This parameter is required when the alert notification methods include Feishu. |
|notify_groups |Array of Long |[ 291 ] |A list of IDs of alert notification email groups.<br><br>This parameter is required when the alert notification methods include email. |
|notify_wechat_webhooks |Array of String |[] |A list of WeCom notification webhooks.<br><br>This parameter is required when the alert notification methods include WeCom. |
|notify_dingding_webhooks |Array of String |[] |A list of DingTalk notification webhooks.<br><br>This parameter is required when the alert notification methods include DingTalk. |

### PctAvoidSpike

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pct |Integer |1 |Alert sub\-window value. Available values are 1 to 9.<br><br>The alert is triggered only when the alert metric values of X or more sub\-windows exceed the configured alert threshold. |

### Measure

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67920#rawmeasurelist) |\- |A list of alert metrics. |
|formula |String |\- |The arithmetic formula for the metric.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |PV |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |String |in |Condition operator.<br><br><br>* in: contains<br><br>* not_in: does not contain<br><br>* regex: Regular expression matching<br><br>* not_regex: Regular expression mismatch |
|filter_name |String |browser_brand |The key of the filtering condition. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|values |Array of String |["Chrome"] |Filtering condition values. Call the `GetAlarmMetricCandidate` API to view available values. |

### GroupBys

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|group_by_name |String |pid |Grouping dimension key. Call the `GetAlarmMetricRelatedMeta` API to view the values. |
|label |String |pid |Grouping metric. |

### AttributionDimensions

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|group_by_name |String |pid |Attribution dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|label |String |pid |Attribution dimension. |

### RawMeasureList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_name |String |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view the values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67920#filterlist) |\- |The filter condition. This parameter is optional when a single simple metric carries conditions and the metric type is polynomial. |
|event_name |String |\- |Custom event key. This parameter is required when the metric is a custom event metric. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "alarm_param":{
            "id":1,
            "name":"test",
            "alarm_level":"warning",
            "desc":"",
            "category":"pageview",
            "interval_seconds":300,
            "strategy_op":"and",
            "strategy_list":[
                {
                    "alarm_window_size":180,
                    "measure":{
                        "type":"monomial",
                        "raw_measure_list":[
                            {
                                "measure_name":"pv_uv.count",
                                "event_name":"",
                                "filter_list":[
                                    {
                                        "filter_name":"browser_brand",
                                        "values":[
                                            "Chrome"
                                        ],
                                        "op":"in"
                                    }
                                ]
                            }
                        ],
                        "formula":"",
                        "name":"PV",
                        "unit":{
                            "unit_type":"",
                            "unit":""
                        }
                    },
                    "alarm_strategy_type":"threshold",
                    "daily_compare_count":5,
                    "threshold_cmp_op":"gt",
                    "alarm_threshold":10,
                    "group_bys":[
                        {
                            "label":"pid",
                            "group_by_name":"pid"
                        }
                    ],
                    "attribution_dimensions":[
                        {
                            "label":"pid",
                            "group_by_name":"pid"
                        }
                    ],
                    "filter_list":[
                        {
                            "filter_name":"pid",
                            "op":"in",
                            "values":[
                                "dashboard"
                            ]
                        }
                    ],
                    "alarm_user_threshold":1,
                    "alarm_sample_threshold":1
                }
            ],
            "alarm_period":{
                "start_time":0,
                "end_time":86399
            },
            "notify_config":{
                "notify_types":[
                    "mail"
                ],
                "notify_groups":[
                    291
                ],
                "notify_lark_webhooks":[
                ],
                "notify_wechat_webhooks":[
                ],
                "notify_dingding_webhooks":[
                ]
            },
            "is_avoid_spike":false,
            "is_close":0,
            "pct_avoid_spike":{
                "pct":1
            }
        },
        "created_by":"leeac",
        "updated_by":"leeac",
        "created_time":1666008398,
        "updated_time":1666008398,
        "next_trigger_time":1666008698,
        "last_execute_time":0,
        "ack_until_time":0
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
