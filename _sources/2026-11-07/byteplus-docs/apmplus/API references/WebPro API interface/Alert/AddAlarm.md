---
title: "AddAlarm"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/AddAlarm"
---

Create an alert task.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=AddAlarm&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |AddAlarm |The API name. The API name is `AddAlarm`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67923#common) |No |\- |Common parameters. |
|alarm_param_list |Array of [AlarmParamList](https://docs.byteplus.com/en/docs/299/67923#alarmparamlist) |No |\- |A list of alert task parameters. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### AlarmParamList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|name |String |No |test |Alert task name. |
|desc |String |No |\- |Alert description. |
|is_close |Integer |No |0 |Whether to disable alerts.<br><br><br>* 0: Enabled<br><br>* 1: Disabled |
|category |String |No |pageview |Alert type key. Call the `GetAlarmMeta` API to view available values. |
|alarm_level |String |No |warning |Alert level. Available values include warning and fatal. |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/67923#strategylist) |No |\- |A list of alert policies. |
|strategy_op |String |No |and |Multi\-policy relationship.<br><br><br>* and: All policies must be satisfied simultaneously.<br><br>* or: Any policy is satisfied. |
|interval_seconds |Integer |No |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/67923#alarmperiod) |No |\- |The time period during which an alert notification can be triggered. Alerts outside the time period will not trigger notifications. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/67923#notifyconfig) |No |\- |Alert task notification configuration. |
|is_avoid_spike |Boolean |No |false |Whether to filter out spike alerts for optimization. |
|pct_avoid_spike |Object of [PctAvoidSpike](https://docs.byteplus.com/en/docs/299/67923#pctavoidspike) |No |\- |PCT alert parameter. This parameter is required when PCT alert suppression is enabled. |

### StrategyList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/67923#measure) |No |\- |A list of metrics. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67923#filterlist) |No |\- |Filtering conditions of alert policies. |
|alarm_strategy_type |String |No |threshold |Alert policy type.<br><br><br>* threshold: Threshold\-based alert<br><br>* cmp_last_n_day: Difference\-based alert |
|daily_compare_count |Integer |No |5 |Time interval between the previous period and the current period.<br><br>This parameter is required when the alert policy is difference\-based. The unit is minutes. For example, 1440 sets the comparison offset to 1 day ago. |
|alarm_threshold |Double |No |10 |The alert threshold. |
|threshold_cmp_op |String |No |gt |Policy operator.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |No |1 |User count threshold. |
|alarm_sample_threshold |Double |No |1 |Sample size threshold. |
|alarm_window_size |Long |No |180 |Time window for querying alert tasks. It represents the last X minutes. The unit is minutes. |
|group_bys |Array of [GroupBys](https://docs.byteplus.com/en/docs/299/67923#groupbys) |No |\- |Alert grouping dimensions. |
|attribution_dimensions |Array of [AttributionDimensions](https://docs.byteplus.com/en/docs/299/67923#attributiondimensions) |No |\- |Alert attribution dimension. |

### AlarmPeriod

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |No |0 |The start of the time period during which an alert notification can be triggered.<br><br>The value is the start timestamp in seconds relative to 0:00 of the current day. For example, if the start time is 2:00 on the current day, the value is 7200. |
|end_time |Integer |No |86399 |Alert end time.<br><br>The value is the end timestamp in seconds relative to 0:00 of the current day. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|notify_types |Array of String |No |["mail"] |Notification methods for the alert task.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_lark_webhooks |Array of String |No |[] |A list of Feishu notification webhooks.<br><br>This parameter is required when the alert notification methods include Feishu. |
|notify_groups |Array of Long |No |[291] |A list of IDs of alert notification email groups.<br><br>This parameter is required when the alert notification methods include email. |
|notify_wechat_webhooks |Array of String |No |[] |A list of WeCom notification webhooks.<br><br>This parameter is required when the alert notification methods include WeCom. |
|notify_dingding_webhooks |Array of String |No |[] |A list of DingTalk notification webhooks.<br><br>This parameter is required when the alert notification methods include DingTalk. |

### PctAvoidSpike

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|pct |Integer |No |1 |Alert sub\-window value. Available values are 1 to 9.<br><br>The alert is triggered only when the alert metric values of X or more sub\-windows exceed the configured alert threshold. |

### Measure

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67923#rawmeasurelist) |No |\- |A list of all metrics. |
|formula |String |No |\- |The arithmetic formula for the metric.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |No |PV |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Condition operator. Supported values include in, not_in, Regex, and not_regex. |
|filter_name |String |No |browser_brand |The key of the filtering condition. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|values |Array of String |No |["Chrome"] |Filtering condition values. Call the `GetAlarmMeticCandidate` API to view available values. |

### GroupBys

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|group_by_name |String |No |pid |Grouping dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|label |String |No |pid |Grouping metric. |

### AttributionDimensions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|group_by_name |String |No |pid |Attribution dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|label |String |No |pid |Attribution metric. |

### RawMeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_name |String |No |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view the values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67923#filterlist) |No |\- |The filtering condition. This parameter is optional when a simple metric in a composite metric has filtering conditions. |
|event_name |String |No |\- |Custom event key. This parameter is required when the metric is a custom event metric. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=AddAlarm&Version=2022-10-12
{
    "alarm_param_list":[
        {
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
        }
    ],
    "common":{
        "aid":12345,
        "os":"webpro"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67923#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ids |Array of Long |[ 303 ] |Alert task IDs. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":[
        303
    ],
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
