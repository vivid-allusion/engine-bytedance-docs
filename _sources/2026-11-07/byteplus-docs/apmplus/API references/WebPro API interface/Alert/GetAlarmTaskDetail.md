---
title: "GetAlarmTaskDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmTaskDetail"
---

Get the details of the specified alert task.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmTaskDetail&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmTaskDetail |The API name. The current API name is `GetAlarmTaskDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67924#common) |No |\- |Common parameter. |
|id |Long |No |302 |Alert task ID list. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmTaskDetail&Version=2022-10-12
{
    "common":{
        "aid":312541,
        "os":"webpro"
    },
    "id":302
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67924#data) |\- |Response data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_param |Object of [AlarmParam](https://docs.byteplus.com/en/docs/299/67924#alarmparam) |\- |All alert parameters. |
|created_by |String |leeac |Alert task creator. |
|updated_by |String |leeac |Last modifier of the alert task. |
|created_time |Long |1665409567 |Alert task creation time. |
|updated_time |Long |1665409567 |The latest modification time of the alert task. |
|next_trigger_time |Long |1665409867 |Next trigger time of the alert task. |
|last_execute_time |Long |0 |Last execution time of the alert task. |
|ack_until_time |Long |0 |ACK expiration time of the alert task. |
|num_of_alarm_in_last_one_month |Integer |0 |Number of alerts triggered by the alert task in the last month. |

### AlarmParam

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1 |Alert task ID. |
|name |String |test |Alert task name. |
|desc |String |\- |Alert description. |
|is_close |Integer |0 |Whether to disable alerts.<br><br><br>* 0: Enable<br><br>* 1: Disable |
|category |String |pageview |Alert type key. Call the `GetAlarmMeta` API to view available values. |
|alarm_level |String |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/67924#strategylist) |\- |Alert policy list. |
|strategy_op |String |and |Relationship between multiple alert policies.<br><br><br>* and: Satisfy all policies simultaneously<br><br>* or: Satisfy any policy |
|interval_seconds |Integer |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/67924#alarmperiod) |\- |Effective period of the alert. Alerts outside the time range will not trigger notifications. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/67924#notifyconfig) |\- |Alert task notification configuration. |
|is_avoid_spike |Boolean |false |Whether to silence spike alerts. |
|pct_avoid_spike |Object of [PctAvoidSpike](https://docs.byteplus.com/en/docs/299/67924#pctavoidspike) |\- |PCT alert parameter. This parameter is required when PCT alert suppression is enabled. |

### StrategyList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/67924#measure) |\- |Metric set. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67924#filterlist) |\- |Alert policy filter criteria. |
|alarm_strategy_type |String |threshold |Alert policy type.<br><br><br>* threshold: Threshold\-based alert<br><br>* cmp_last_n_day: Difference\-based alert |
|daily_compare_count |Integer |5 |Time interval between the previous period and the current period.<br><br>This parameter is required when the alert policy is difference\-based. The unit is minutes. For example, 1440 sets the comparison offset to 1 day ago. |
|alarm_threshold |Double |10 |Alert threshold. |
|threshold_cmp_op |String |gt |Policy operator.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |1 |User count threshold. |
|alarm_sample_threshold |Double |1 |Sample size threshold. |
|alarm_window_size |Long |180 |Time window for alert task query. It represents the last X minutes. The unit is minutes. |
|group_bys |Array of [GroupBys](https://docs.byteplus.com/en/docs/299/67924#groupbys) |\- |Alert grouping dimensions. |
|attribution_dimensions |Array of [AttributionDimensions](https://docs.byteplus.com/en/docs/299/67924#attributiondimensions) |\- |Alert attribution dimensions. |

### AlarmPeriod

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|start_time |Integer |0 |Alert start time.<br><br>The value is the start timestamp in seconds relative to 0:00 of the current day. For example, if the start time is 2:00 on the current day, the value is 7200. |
|end_time |Integer |86399 |Alert end time.<br><br>The value is the end timestamp in seconds relative to 0:00 of the current day. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|notify_types |Array of String |["mail"] |Alert task notification method.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_lark_webhooks |Array of String |[] |List of Feishu notification webhooks.<br><br>Required when the alert notification method includes Feishu. |
|notify_groups |Array of Long |[ 291 ] |List of alert notification email group IDs.<br><br>Required when the alert notification method includes email. |
|notify_wechat_webhooks |Array of String |[] |List of WeCom notification webhooks.<br><br>Required when the alert notification method includes WeCom. |
|notify_dingding_webhooks |Array of String |[] |A list of DingTalk notification webhooks.<br><br>Required when the alert notification method includes DingTalk. |

### PctAvoidSpike

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pct |Integer |1 |Alert sub\-window value. Available values: 1 to 9.<br><br>The alert is triggered only when the alert metric values of X or more sub\-windows exceed the configured alert threshold. |

### Measure

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67924#rawmeasurelist) |\- |Alert metric list. |
|formula |String |\- |Metric arithmetic formula.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |PV |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |String |in |Condition operator.<br><br><br>* in: contains<br><br>* not_in: does not contain<br><br>* Regex: Regex match<br><br>* not_regex: Regex mismatch |
|filter_name |String |browser_brand |Filter criterion key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|values |Array of String |["Chrome"] |Filter criterion values. Call the `GetAlarmMetricCandidate` API to view available values. |

### GroupBys

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|group_by_name |String |pid |Grouping dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|label |String |pid |Grouping metric. |

### AttributionDimensions

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|group_by_name |String |pid |Attribution dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|label |String |pid |Attribution metric. |

### RawMeasureList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_name |String |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view available values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67924#filterlist) |\- |The filter condition. This parameter is optional when a simple metric in a composite metric has filtering conditions. |
|event_name |String |\- |Custom event key. Required when the metric is a custom event metric. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "alarm_rule_list":[
            {
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
                "created_time":1665409567,
                "updated_time":1665409567,
                "next_trigger_time":1665409867,
                "last_execute_time":0,
                "ack_until_time":0,
                "num_of_alarm_in_last_one_month":0
            }
        ],
        "count":1
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
