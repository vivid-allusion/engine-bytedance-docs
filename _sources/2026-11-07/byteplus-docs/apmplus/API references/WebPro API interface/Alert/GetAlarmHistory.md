---
title: "GetAlarmHistory"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmHistory"
---

Get the alert history of the specified task.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmHistory&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmHistory |The API name. The current API name is `GetAlarmHistory`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67933#common) |No |\- |Common parameter. |
|id |Long |No |302 |Alert task ID list. |
|page_size |Integer |No |30 |The number of items per page for a pagination query. Default value: 30. |
|page_num |Integer |No |1 |The page number for a pagination query. Default value: 1. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67933#timefilter) |No |\- |Time range. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |No |1665849600 |Start time. |
|granularity |Integer |No |60 |Aggregation time granularity. |
|end_time |Integer |No |1666011403 |The end time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmHistory&Version=2022-10-12
{
    "common":{
        "aid":12345,
        "os":"webpro"
    },
    "id":302,
    "time_filter":{
        "start_time":1665849600,
        "end_time":1666011403,
        "granularity":3600
    },
    "page_size":10,
    "page_num":1
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67933#data) |\- |Response data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_histories |Array of [AlarmHistories](https://docs.byteplus.com/en/docs/299/67933#alarmhistories) |\- |Alert trend. |
|count |Integer |1 |Alert count. |

### AlarmHistories

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |160570 |Alert history ID. |
|alarm_param |Object of [AlarmParam](https://docs.byteplus.com/en/docs/299/67933#alarmparam) |\- |Alert parameters. |
|alarm_time |Long |1666011480 |Alert occurrence time. |
|alarm_content |String |\- |Alert content. |
|alarm_result |Object of [AlarmResult](https://docs.byteplus.com/en/docs/299/67933#alarmresult) |\- |Alert result. |
|operator |String |bytedance\-apm |Alert task creator. |
|detail_link |String |/apmplus/webpro/data_search?aid=12345&end_time=1666011480&ev_type=view&start_time=1666000680 |Link to the alert details page. |

### AlarmParam

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |302 |Alert task ID. |
|name |String |jiyi\-test |Alert task name. |
|desc |String |\- |Alert description. |
|is_close |Integer |0 |Whether to disable alerts.<br><br><br>* 0: Enable<br><br>* 1: Disable |
|category |String |performance |Alert type. |
|category_label |String |\- |Alert type filter.<br><br> <br><br>If not specified, alert tasks of all alert types are returned. If specified, alert tasks of the specified alert type are returned. Call the `GetAlarmMeta` API to view available values. |
|alarm_level |String |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/67933#strategylist) |\- |Alert policy list. |
|strategy_op |String |and |Relationship between multiple alert policies.<br><br><br>* and: Satisfy all policies simultaneously<br><br>* or: Satisfy any policy |
|interval_seconds |Integer |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/67933#alarmperiod) |\- |Time period during which alerts are active. Alerts outside the time range will not trigger notifications. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/67933#notifyconfig) |\- |Notification configuration. |
|is_avoid_spike |Boolean |false |Whether to silence spike alerts. |

### AlarmResult

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether an alert is triggered. |
|strategy_result_list |Array of [StrategyResultList](https://docs.byteplus.com/en/docs/299/67933#strategyresultlist) |\- |Alert results by policy. |

### StrategyList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |123\-456 |Alert ID. |
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/67933#measure) |\- |Metrics of the current policy, including simple metrics and compound metrics. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67933#filterlist) |[] |Alert policy filter criteria. |
|alarm_strategy_type |String |threshold |Alert policy type.<br><br><br>* threshold: Threshold\-based alert<br><br>* cmp_last_n_day: Difference\-based alert |
|daily_compare_count |Integer |5 |Time interval between the previous period and the current period.<br><br>This parameter is required when the alert policy is difference\-based. The unit is minutes. For example, 1440 sets the comparison offset to 1 day ago. |
|alarm_threshold |Double |5 |Alert threshold. |
|threshold_cmp_op |String |gt |Alert threshold policy operators.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |0 |User count threshold. |
|alarm_sample_threshold |Double |0 |Sample size threshold. |
|alarm_window_size |Long |180 |Time window for alert task query. It represents the last X minutes. The unit is minutes. |
|sample_metric |Object of [SampleMetric](https://docs.byteplus.com/en/docs/299/67933#samplemetric) |\- |Sample metric. |
|user_metric |Object of [UserMetric](https://docs.byteplus.com/en/docs/299/67933#usermetric) |\- |User metric. |

### AlarmPeriod

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|start_time |Integer |0 |Alert start time.<br><br>The value is the number of seconds from 00:00 of the current day to the start time. For example, if the start time is 2:00 on the current day, the value is 7200. |
|end_time |Integer |86399 |Alert end time.<br><br>The value is the end timestamp in seconds relative to 0:00 of the current day. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|notify_types |Array of String |[ "mail" ] |Notification methods for the alert task.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_groups |Array of Long |287 |List of email group IDs used for alert notifications.<br><br>Required when the alert notification method includes email. |

### StrategyResultList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether the policy conditions are met. |
|title |String |Alerts based on slow page count threshold. |Title of the query result. |
|is_attributable |Boolean |false |Whether attribution is enabled. |
|group_result_list |Array of [GroupResultList](https://docs.byteplus.com/en/docs/299/67933#groupresultlist) |\- |Alert grouping results. |

### Measure

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67933#rawmeasurelist) |\- |Alert metric list. |
|formula |String |\- |Metric arithmetic formula.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |Slow page count |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |String |\- |Relationship between filter conditions and filter values. |
|filter_name |String |\- |Filter metric name. |
|values |Array of String |\- |Available values of the filter metric. |

### SampleMetric

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67933#rawmeasurelist) |\- |A list of alert metrics. |
|formula |String |\- |Metric arithmetic formula.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |count |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### UserMetric

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67933#rawmeasurelist) |\- |Alert metric list. |
|formula |String |\- |Metric arithmetic formula.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |user |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### GroupResultList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_alarm |Boolean |true |Whether an alert is triggered. |
|group_value |String |\- |Value of the grouped alert. For example, this field returns China when grouping by country. This field is not returned if alerts are not grouped. |
|alarm_tag_list |Array of [AlarmTagList](https://docs.byteplus.com/en/docs/299/67933#alarmtaglist) |\- |A list of alert tags. |
|alarm_value |Object of [AlarmValue](https://docs.byteplus.com/en/docs/299/67933#alarmvalue) |\- |Alert value. |
|is_spike |Boolean |false |Whether spike alerts are silenced. |

### RawMeasureList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_name |String |slow_load_count |Simple metric key. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67933#filterlist) |[] |Filtering conditions. Optional when a single simple metric carries criteria and the metric type is composite. |
|event_name |String |\- |Custom event key. Required when the metric is a custom event metric. |

### AlarmTagList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1172 |Current value of the metric. |
|format_value |String |1172 |Formatted value. Currently, special formatting applies only to time\-window values, which include a time unit. |

### AlarmValue

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|current_value |Object of [CurrentValue](https://docs.byteplus.com/en/docs/299/67933#currentvalue) |\- |Current value. |
|alarm_threshold |Object of [AlarmThreshold](https://docs.byteplus.com/en/docs/299/67933#alarmthreshold) |\- |Alert threshold. |
|sample_count |Object of [SampleCount](https://docs.byteplus.com/en/docs/299/67933#samplecount) |\- |Sample size. |
|user_count |Object of [UserCount](https://docs.byteplus.com/en/docs/299/67933#usercount) |\- |User count. |
|window_size |Object of [WindowSize](https://docs.byteplus.com/en/docs/299/67933#windowsize) |\- |Time window. |

### CurrentValue

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1174 |Current value of the metric. |
|format_value |String |\- |Formatted value. Currently, special formatting applies only to time\-window values, which include a time unit. |

### AlarmThreshold

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1174 |Current value of the metric. |
|format_value |String |\- |Formatted value. Currently, special formatting applies only to time\-window values, which include a time unit. |

### SampleCount

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1174 |Current value of the metric. |
|format_value |String |\- |Formatted value. Currently, special formatting applies only to time\-window values, which include a time unit. |

### UserCount

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1174 |Current value of the metric. |
|format_value |String |\- |Formatted value. Currently, special formatting applies only to time\-window values, which include a time unit. |

### WindowSize

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Current value |Metric. |
|value |Double |1174 |Current value of the metric. |
|format_value |String |\- |Formatted value. Currently, special formatting applies only to time\-window values, which include a time unit. |

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
                "alarm_content":"\nSlow page count threshold in the last 180 minutes >= 0    \n    Current value: 1174, Threshold: 0, Sample size: 10745, Number of users: 458, Time window: 180 minutes\n",
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
