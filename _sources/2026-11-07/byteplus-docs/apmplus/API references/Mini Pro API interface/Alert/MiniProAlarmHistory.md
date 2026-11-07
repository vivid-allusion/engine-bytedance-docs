---
title: "MiniProAlarmHistory"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmHistory"
---

Get the alert history of the specified task.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAlarmHistory&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAlarmHistory |The API name. The current API name is `MiniProAlarmHistory`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68010#common) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68010#timefilter) |Yes |\- |Time range. |
|id |Long |No |302 |Alert task ID list. |
|page_size |Integer |No |10 |Number of items returned in the alert history list. |
|page_num |Integer |No |1 |Page count for alert history list. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. Supported values: **app**, **webpro**, **minipro**. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665849600 |Start time. |
|granularity |Integer |No |60 |Aggregation time granularity. |
|end_time |Integer |Yes |1666011403 |End time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAlarmHistory&Version=2024-03-12
{
    "common": {
        "aid": 12345,
        "os": "minipro"
    },
    "id": 302,
    "time_filter": {
        "start_time": 1665849600,
        "end_time": 1666011403,
        "granularity": 3600
    },
    "page_size": 10,
    "page_num": 1
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68010#data) |\- |Returned data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_histories |Array of [AlarmHistories](https://docs.byteplus.com/en/docs/299/68010#alarmhistories) |\- |Alert history details. |

### AlarmHistories

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |160570 |Alert history ID. |
|alarm_param |Object of [AlarmParam](https://docs.byteplus.com/en/docs/299/68010#alarmparam) |\- |Alert parameters. |
|alarm_time |Long |1666011480 |Alert occurrence time. |
|alarm_content |String |\- |Alert content. |
|alarm_result |Object of [AlarmResult](https://docs.byteplus.com/en/docs/299/68010#alarmresult) |\- |Alert result. |

### AlarmParam

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |302 |Alert task ID. |
|name |String |test |Alert task name. |
|desc |String |\- |Alert description. |
|is_close |Integer |0 |Whether to disable alerts.<br><br><br>* 0: Enable<br><br>* 1: Disable |
|category |String |performance |Alert type. |
|category_label |String |\- |Alert type name.<br><br>If not specified, alert tasks of all alert types are returned. If specified, alert tasks of the specified alert type are returned. Call the `GetAlarmMeta` API to view available values. |
|alarm_level |String |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/68010#strategylist) |\- |Alert policy list. |
|strategy_op |String |and |Alert multi\-policy relationship.<br><br><br>* and: Satisfy all policies simultaneously<br><br>* or: Satisfy any one policy |
|interval_seconds |Integer |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/68010#alarmperiod) |\- |Alert effective time. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/68010#notifyconfig) |\- |Alert task notification configuration. |
|is_avoid_spike |Boolean |false |Whether to silence spike alerts. |

### AlarmResult

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether an alert is triggered. |
|strategy_result_list |Array of [StrategyResultList](https://docs.byteplus.com/en/docs/299/68010#strategyresultlist) |\- |Alert results by policy. |

### StrategyList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |123\-456 |Alert ID. |
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/68010#measure) |\- |The metric set of the current policy. It includes simple metrics and composite metrics. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/68010#filterlist) |[] |Alert policy filter criteria. |
|alarm_strategy_type |String |threshold |Alert policy type.<br><br><br>* threshold: Threshold\-based alert<br><br>* cmp_last_n_day: Ratio\-based alert |
|daily_compare_count |Integer |5 |Time interval between the previous period and the current period.<br><br>This parameter is required when the alert policy is difference\-based. The unit is minutes. For example, 1440 sets the comparison offset to 1 day ago. |
|alarm_threshold |Double |0 |Alert threshold. |
|threshold_cmp_op |String |gte |Policy operator.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |0 |User count threshold. |
|alarm_sample_threshold |Double |0 |Sample count threshold. |
|alarm_window_size |Long |180 |Time window for alert task query. It represents the most recent X minutes. The unit is minutes. |

### AlarmPeriod

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|start_time |Integer |0 |Alert start time.<br><br>The value is the number of seconds from 00:00 of the current day to the start time. For example, if the start time is 02:00 on the current day, the value is 7200. |
|end_time |Integer |86399 |Alert end time.<br><br>The value is the number of seconds from 00:00 of the current day to the end time. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|notify_types |Array of String |[ "mail" ] |Notification method for the alert task.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_lark_webhooks |Array of String |[] |A list of Feishu notification webhooks. |
|notify_groups |Array of Long |287 |A list of mail receiver group IDs. |
|notify_wechat_webhooks |Array of String |[] |A list of WeCom notification webhooks. |
|notify_dingding_webhooks |Array of String |[] |A list of DingTalk notification webhooks. |

### StrategyResultList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether the policy conditions are met. |
|title |String |Threshold\-based alert for slow page count |Title of the query result. |
|is_attributable |Boolean |false |Whether attribution is enabled. |
|group_result_list |Array of [GroupResultList](https://docs.byteplus.com/en/docs/299/68010#groupresultlist) |\- |Grouped alert results. |

### Measure

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/68010#rawmeasurelist) |\- |Alert metric list. |
|formula |String |\- |Metric arithmetic formula.<br><br>Optional when the metric type is the composite metric polynomial. |
|name |String |Slow page count |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |String |in |Condition operator.<br><br><br>* in<br><br>* not_in<br><br>* Regex<br><br>* not_regex |
|filter_name |String |browser_brand |Filter criterion key. Call the `GetAlarmMetricRelatedMeta` API to view available values. Indicates the dimension of the filter. |
|values |Array of String |["Chrome"] |Filter criterion values. Call the `GetAlarmMetricCandidate` API to view available values. |

### GroupResultList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether an alert is triggered. |
|group_value |String |\- |Grouped alert value, e.g., "China" for the country grouping. It is not returned if it is not a grouped alert. |
|alarm_tag_list |Array of [AlarmTagList](https://docs.byteplus.com/en/docs/299/68010#alarmtaglist) |\- |Alert list tag. |
|is_spike |Boolean |false |Whether to filter spikes. |

### RawMeasureList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_name |String |slow_load_count |Simple metric key. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/68010#filterlist) |[] |The filter condition. Optional when a single simple metric carries criteria and the metric type is composite. |
|event_name |String |\- |Custom event key. Required when the metric is a custom event metric. |

### AlarmTagList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1174 |Available values of the metric. |
|format_value |String |1174 |Formatted value. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "alarm_histories":[
            {
                "id":160570,
                "alarm_param":{
                    "id":302,
                    "name":"test",
                    "desc":"",
                    "is_close":0,
                    "category":"performance",
                    "category_label":"",
                    "alarm_level":"warning",
                    "strategy_list":[
                        {
                            "id":"123-456",
                            "measure":{
                                "type":"monomial",
                                "raw_measure_list":[
                                    {
                                        "measure_name":"slow_load_count",
                                        "filter_list":[
                                        ],
                                        "event_name":""
                                    }
                                ],
                                "formula":"",
                                "name":"slow page count"
                            },
                            "filter_list":[
                            ],
                            "alarm_strategy_type":"threshold",
                            "daily_compare_count":5,
                            "alarm_threshold":0,
                            "threshold_cmp_op":"gte",
                            "alarm_user_threshold":0,
                            "alarm_sample_threshold":0,
                            "alarm_window_size":180,
                            "sample_metric":{
                                "type":"monomial",
                                "raw_measure_list":[
                                    {
                                        "measure_name":"browser_perf.count",
                                        "filter_list":[
                                        ]
                                    }
                                ],
                                "formula":"",
                                "name":"count"
                            },
                            "user_metric":{
                                "type":"monomial",
                                "raw_measure_list":[
                                    {
                                        "measure_name":"browser_perf.user",
                                        "filter_list":[
                                        ]
                                    }
                                ],
                                "formula":"",
                                "name":"user"
                            }
                        }
                    ],
                    "strategy_op":"and",
                    "interval_seconds":300,
                    "alarm_period":{
                        "start_time":0,
                        "end_time":86399
                    },
                    "notify_config":{
                        "notify_types":[
                            "mail"
                        ],
                        "notify_groups":[
                            287
                        ]
                    },
                    "is_avoid_spike":false,
                    "aid":123456,
                    "os":"minipro"
                },
                "alarm_time":1666011480,
                "alarm_content":"\nIn the past 180 minutes, the threshold for the number of slow pages >= 0\n Current value: 1174, Threshold: 0, Sample size: 10745, Number of users: 458, Time window: 180 minutes\n",
                "alarm_result":{
                    "is_alarm":true,
                    "strategy_result_list":[
                        {
                            "is_alarm":true,
                            "title":"Alarm for the threshold of the number of slow pages",
                            "is_attributable":false,
                            "group_result_list":[
                                {
                                    "is_alarm":true,
                                    "group_value":"",
                                    "alarm_tag_list":[
                                        {
                                            "label":"Current value",
                                            "value":1174,
                                            "format_value":"1174"
                                        },
                                        {
                                            "label":"Threshold",
                                            "value":0,
                                            "format_value":"0"
                                        },
                                        {
                                            "label":"Sample size",
                                            "value":10745,
                                            "format_value":"10745"
                                        },
                                        {
                                            "label":"Number of users",
                                            "value":458,
                                            "format_value":"458"
                                        },
                                        {
                                            "label":"Time window",
                                            "value":180,
                                            "format_value":"3 minutes"
                                        }
                                    ],
                                    "alarm_value":{
                                        "current_value":{
                                            "label":"Current value",
                                            "value":1174,
                                            "format_value":""
                                        },
                                        "alarm_threshold":{
                                            "label":"Threshold",
                                            "value":0,
                                            "format_value":"0"
                                        },
                                        "sample_count":{
                                            "label":"Sample size",
                                            "value":10745,
                                            "format_value":"10745"
                                        },
                                        "user_count":{
                                            "label":"Number of users",
                                            "value":458,
                                            "format_value":"458"
                                        },
                                        "window_size":{
                                            "label":"Time window",
                                            "value":180,
                                            "format_value":"3 minutes"
                                        }
                                    },
                                    "is_spike":false
                                }
                            ]
                        }
                    ]
                },
                "operator":"bytedance-apm",
                "detail_link":"/apmplus/minipro/data_search?aid=123456&end_time=1666011480&ev_type=view&start_time=1666000680"
            }
        ],
        "count":1265
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
