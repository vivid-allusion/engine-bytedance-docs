---
title: "GetAlarmAllHistory"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmAllHistory"
---

Get all alert histories.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmAllHistory&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmAllHistory |The API name. The API name is `GetAlarmAllHistory`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67929#common) |No |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67929#timefilter) |No |\- |Time range. |
|category_list |Array of String |No |pageview |Alert task type. If this parameter is not specified, the history alerts of all types are returned. Call the `GetAlarmMeta` API to view values. |
|name_list |Array of String |No |111111 |A list of alert task names. All alert histories are returned if this parameter is left empty. Call the `GetAlarmRuleList` API to view available values. |
|level_list |Array of String |No |warning |A list of alert levels. All alert types are returned if this field is left empty.<br><br><br>* warning<br><br>* fatal |
|page_size |Integer |No |10 |Number of items returned in the alert history list. |
|page_num |Integer |No |1 |Page number of the alert history list. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |No |1665849600 |Start time. |
|granularity |Integer |No |60 |Aggregation time granularity. Unit: s. |
|end_time |Integer |No |1666011403 |The end time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmAllHistory&Version=2022-10-12
{
    "common":{
        "aid":312541,
        "os":"webpro"
    },
    "time_filter":{
        "start_time":1665849600,
        "end_time":1666011403,
        "granularity":3600
    },
    "page_size":10,
    "page_num":1,
    "category_list":[
        "pageview"
    ],
    "name_list":[
        "111111111"
    ],
    "level_list":[
        "warning"
    ]
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67929#data) |\- |Response data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_all_histories |Array of [AlarmAllHistories](https://docs.byteplus.com/en/docs/299/67929#alarmallhistories) |\- |Alert trend. |

### AlarmAllHistories

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |160570 |Alert history ID. |
|alarm_param |Object of [AlarmParam](https://docs.byteplus.com/en/docs/299/67929#alarmparam) |\- |Alert parameters. |
|alarm_time |Long |1666011480 |Alert occurrence time. |
|alarm_result |Object of [AlarmResult](https://docs.byteplus.com/en/docs/299/67929#alarmresult) |\- |Alert result. |
|ack_status |Integer |1 |ACK status during alerting.<br><br><br>* 0: ACK<br><br>* 1: ACK canceled |
|ack_until_time |Long |1659611486 |ACK expiration time. The current ACK state, displayed when an ACK operation is performed in alert statistics.. |
|operator |String |bytedance\-apm |Last updater of the alert task. |
|detail_link |String |/apmplus/webpro/data_search?aid=12345&end_time=1666011480&ev_type=view&start_time=1666000680 |Link to the alert details page. |

### AlarmParam

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |302 |Alert task ID. |
|name |String |test |Alert task name. |
|desc |String |\- |Alert description. |
|is_close |Integer |0 |Whether to disable alerts.<br><br><br>* 0: Enabled<br><br>* 1: Disabled |
|category |String |performance |Alert type. |
|category_label |String |\- |Alert type filter.<br><br>If this parameter is not specified, alert tasks of all alert types are returned. If this parameter is specified, alert tasks of the specified alert type are returned. Call the `GetAlarmMeta` API to view available values. |
|alarm_level |String |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/67929#strategylist) |\- |A list of alert policies. |
|strategy_op |String |and |Relationship between multiple policies.<br><br><br>* and: All policies must be satisfied simultaneously.<br><br>* or: Any policy is satisfied. |
|interval_seconds |Integer |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/67929#alarmperiod) |\- |The time period during which an alert notification can be triggered. Alerts outside the time period will not trigger notifications. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/67929#notifyconfig) |\- |Notification configuration. |
|is_avoid_spike |Boolean |false |Whether to silence spike alerts. |

### AlarmResult

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether an alert is triggered. |
|strategy_result_list |Array of [StrategyResultList](https://docs.byteplus.com/en/docs/299/67929#strategyresultlist) |\- |Alert results by policy. |

### StrategyList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |123\-456 |Alert ID. |
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/67929#measure) |\- |Metrics of the current policy, including simple metrics and composite metrics. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67929#filterlist) |[] |Filtering conditions of alert policies. |
|alarm_strategy_type |String |threshold |Alert policy type.<br><br><br>* threshold: Threshold\-based alert<br><br>* cmp_last_n_day: Difference\-based alert |
|daily_compare_count |Integer |5 |Time interval between the previous period and the current period.<br><br>This parameter is required when the alert policy is difference\-based. The unit is minutes. For example, 1440 sets the comparison offset to 1 day ago. |
|alarm_threshold |Double |0 |The alert threshold. |
|threshold_cmp_op |String |gte |Comparison operator.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |0 |User count threshold. |
|alarm_sample_threshold |Double |0 |Sample size threshold. |
|alarm_window_size |Long |180 |Time window for querying alert tasks. It represents the last X minutes. The unit is minutes. |

### AlarmPeriod

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|start_time |Integer |0 |The start of the time period during which an alert notification can be triggered.<br><br>The value is the number of seconds from 00:00 to the start time on the current day. For example, if the start time is 2:00 on the current day, the value is 7200. |
|end_time |Integer |86399 |End of the time period during which alert notifications can be triggered.<br><br>The value is the number of seconds from 00:00 to the end time on the current day. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|notify_types |Array of String |[ "mail" ] |Notification methods for the alert task.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_groups |Array of Long |287 |A list of IDs of alert notification email groups.<br><br>This parameter is required when the alert notification methods include email. |

### StrategyResultList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether the policy conditions are met. |
|title |String |Threshold\-based alert for slow\-pageload count |Title of the query result. |
|is_attributable |Boolean |false |Whether attribution is enabled. |
|group_result_list |Array of [GroupResultList](https://docs.byteplus.com/en/docs/299/67929#groupresultlist) |\- |Grouped alert results. |

### Measure

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67929#rawmeasurelist) |\- |A list of alert metrics. |
|formula |String |\- |The arithmetic formula for the metric.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |Slow\-pageload count |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |String |\- |Relationship between filter conditions and filter values. |
|filter_name |String |\- |Filter dimension. |
|values |Array of String |\- |Filtering values. |

### GroupResultList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether an alert is triggered. |
|group_value |String |\- |Group value. For example, this field returns China for grouping by country. This field is not returned if alerts are not grouped. |
|alarm_tag_list |Array of [AlarmTagList](https://docs.byteplus.com/en/docs/299/67929#alarmtaglist) |\- |A list of alert tags. |

### RawMeasureList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_name |String |slow_load_count |Simple metric key. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67929#filterlist) |[] |The filter condition. This parameter is optional when a simple metric in a composite metric has filtering conditions. |

### AlarmTagList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1174 |Current value of the metric. |
|format_value |String |1174 |Formatted value. Currently, special formatting applies only to time\-window values, which include a time unit. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "alarm_all_histories":[
            {
                "id":160570,
                "alarm_param":{
                    "id":302,
                    "name":"jiyi-test",
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
                    "os":"webpro"
                },
                "alarm_time":1666011480,
                "alarm_content":"\nSlow page count threshold in the last 180 minutes >= 0    \n    Current value: 1174, Threshold: 0, Sample size: 10745, Number of users: 458, Time window: 180 minutes",
                "alarm_result":{
                    "is_alarm":true,
                    "strategy_result_list":[
                        {
                            "is_alarm":true,
                            "title":"Alarm for slow page count threshold",
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
                "ack_status":1,
                "ack_until_time":1659611486,
                "operator":"bytedance-apm",
                "detail_link":"/apmplus/webpro/data_search?aid=123456&end_time=1666011480&ev_type=view&start_time=1666000680"
            }
        ],
        "count":1265
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
