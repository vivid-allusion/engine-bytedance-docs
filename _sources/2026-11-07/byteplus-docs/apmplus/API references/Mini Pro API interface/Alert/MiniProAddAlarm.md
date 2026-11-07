---
title: "MiniProAddAlarm"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAddAlarm"
---

Add a new alert task.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAddAlarm&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAddAlarm |The API name. The current API name is `MiniProAddAlarm`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68018#common) |Yes |\- |Common parameters. |
|alarm_param_list |Array of [AlarmParamList](https://docs.byteplus.com/en/docs/299/68018#alarmparamlist) |Yes |\- |Alert task parameter list. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. Supported values: **app**, **webpro**, **minipro**. |

### AlarmParamList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|name |String |Yes |test |Alert name. |
|desc |String |Yes |\- |Alert description. |
|is_close |Integer |No |0 |Whether to disable the alert.<br><br><br>* status_open: Enable<br><br>* status_close: Disable |
|category |String |Yes |pageview |Alert type. Call the `GetAlarmMeta` API to view available values. |
|alarm_level |String |Yes |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/68018#strategylist) |No |\- |Alert policy list. |
|strategy_op |String |No |and |Multi\-policy relationship.<br><br><br>* and: Satisfy all policies simultaneously<br><br>* or: Satisfy any policy |
|interval_seconds |Integer |No |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/68018#alarmperiod) |No |\- |Time period during which alerts are active. <br><br>Alerts outside the time range will not trigger notifications. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/68018#notifyconfig) |No |\- |Alert task notification configuration. |
|is_avoid_spike |Boolean |No |false |Alert optimization: Whether to filter spike alerts. |
|pct_avoid_spike |Object of [PctAvoidSpike](https://docs.byteplus.com/en/docs/299/68018#pctavoidspike) |No |\- |Alert parameter. This parameter is required when PCT alert suppression is enabled. |

### StrategyList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/68018#measure) |No |\- |The metric set of the current policy. It includes simple metrics and composite metrics. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/68018#filterlist) |No |\- |Filtering conditions of alert policies. |
|alarm_strategy_type |String |No |threshold |Threshold / Period\-over\-period / cycle\-on\-cycle. For enumerated values, see const_def.thrift. |
|daily_compare_count |Integer |No |5 |The offset in days for period\-over\-period comparison.<br><br>For example, 1 indicates yesterday, and 7 indicates the same day last week. |
|alarm_threshold |Double |No |10 |Alert threshold. |
|threshold_cmp_op |String |No |gt |Policy operator.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |No |1 |User count threshold. |
|alarm_sample_threshold |Double |No |1 |Sample count threshold. |
|alarm_window_size |Long |No |180 |Time window for alert task query. It represents the last X minutes. The unit is minutes. |
|group_bys |Array of [GroupBys](https://docs.byteplus.com/en/docs/299/68018#groupbys) |No |\- |Alert grouping dimension. |
|attribution_dimensions |Array of [AttributionDimensions](https://docs.byteplus.com/en/docs/299/68018#attributiondimensions) |No |\- |Alert attribution dimension. |

### AlarmPeriod

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |No |0 |Alert start time.<br><br>The value is the number of seconds from 00:00 of the current day to the start time. For example, if the start time is 2:00 on the current day, the value is 7200. |
|end_time |Integer |No |866399 |Alert end time.<br><br>The value is the number of seconds from 00:00 of the current day to the end time. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|notify_types |Array of String |No |["mail"] |Notification method for the alert task.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_lark_webhooks |Array of String |No |[] |List of Feishu notification webhooks. Required when the alert notification method includes Feishu. |
|notify_groups |Array of Long |No |[ 291 ] |List of email group IDs used for alert notifications.<br><br>This parameter is required when the alert notification methods include email. |
|notify_wechat_webhooks |Array of String |No |[] |List of WeCom notification webhooks. Required when the alert notification method includes WeCom. |
|notify_dingding_webhooks |Array of String |No |[] |List of DingTalk notification webhooks. Required when the alert notification method includes DingTalk. |

### PctAvoidSpike

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|pct |Integer |No |1 |Alert sub\-window value. Available values are 1~9.<br><br>The alert is triggered only when the alert metric values of X or more sub\-windows exceed the configured alert threshold. |

### Measure

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/68018#rawmeasurelist) |No |\- |The set of all metrics. |
|formula |String |No |\- |Metric arithmetic formula. Optional when the metric type is the composite metric polynomial. |
|name |String |No |PV |The metric name. When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Condition operators.<br><br><br>* in<br><br>* not_in<br><br>* Regex<br><br>* not_regex |
|filter_name |String |No |browser_brand |Filter criterion key. Call the `GetAlarmMetricRelatedMeta` API to view the values. |
|values |Array of String |No |["Chrome"] |Filter criterion values. Call the `GetAlarmMeticCandidate` API to view available values. |

### GroupBys

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|group_by_name |String |No |pid |Grouping dimension key. Call the `GetAlarmMetricRelatedMeta` API to view the values. |
|label |String |No |pid |Grouping metric. |

### AttributionDimensions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|group_by_name |String |No |pid |Attribution dimension key. Call the `GetAlarmMetricRelatedMeta` API to view the values. |
|label |String |No |pid |Attribution metric. |

### RawMeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_name |String |No |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view available values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/68018#filterlist) |No |\- |The filter condition. Optional when a single simple metric carries criteria and the metric type is composite. |
|event_name |String |No |\- |The frontend passed this parameter, but the backend did not use it. However, when restoring the chart, the event name is read from this field. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAddAlarm&Version=2024-03-12
{
    "alarm_param_list": [
        {
            "name": "test",
            "alarm_level": "warning",
            "desc": "",
            "category": "pageview",
            "interval_seconds": 300,
            "strategy_op": "and",
            "strategy_list": [
                {
                    "alarm_window_size": 180,
                    "measure": {
                        "type": "monomial",
                        "raw_measure_list": [
                            {
                                "measure_name": "pv_uv.count",
                                "event_name": "",
                                "filter_list": [
                                    {
                                        "filter_name": "browser_brand",
                                        "values": [
                                            "Chrome"
                                        ],
                                        "op": "in"
                                    }
                                ]
                            }
                        ],
                        "formula": "",
                        "name": "PV",
                        "unit": {
                            "unit_type": "",
                            "unit": ""
                        }
                    },
                    "alarm_strategy_type": "threshold",
                    "daily_compare_count": 5,
                    "threshold_cmp_op": "gt",
                    "alarm_threshold": 10,
                    "group_bys": [
                        {
                            "label": "pid",
                            "group_by_name": "pid"
                        }
                    ],
                    "attribution_dimensions": [
                        {
                            "label": "pid",
                            "group_by_name": "pid"
                        }
                    ],
                    "filter_list": [
                        {
                            "filter_name": "pid",
                            "op": "in",
                            "values": [
                                "dashboard"
                            ]
                        }
                    ],
                    "alarm_user_threshold": 1,
                    "alarm_sample_threshold": 1
                }
            ],
            "alarm_period": {
                "start_time": 0,
                "end_time": 86399
            },
            "notify_config": {
                "notify_types": [
                    "mail"
                ],
                "notify_groups": [
                    291
                ],
                "notify_lark_webhooks": [
                ],
                "notify_wechat_webhooks": [
                ],
                "notify_dingding_webhooks": [
                ]
            },
            "is_avoid_spike": false,
            "is_close": 0,
            "pct_avoid_spike": {
                "pct": 1
            }
        }
    ],
    "common": {
        "aid": 12345,
        "os": "minipro"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68018#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ids |Array of Long |[ 303 ] |Returned data. |

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
