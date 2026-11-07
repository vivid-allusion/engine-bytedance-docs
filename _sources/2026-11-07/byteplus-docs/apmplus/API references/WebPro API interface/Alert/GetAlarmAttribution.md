---
title: "GetAlarmAttribution"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmAttribution"
---

Get attribution information.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmAttribution&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmAttribution |The API name. The current API name is `GetAlarmAttribution`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67925#common) |No |\- |Common parameter. |
|alarm_param |Object of [AlarmParam](https://docs.byteplus.com/en/docs/299/67925#alarmparam) |No |\- |Alert task parameter list. |
|group_by_value |String |No |Chrome Webview |Attribution dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|strategy_id |Integer |No |0 |Alert policy index. Indicates the index value of the attribution policy in alarm_param.strategy_list. |
|attribution_time |Long |No |1666012500 |Alert attribution end time. The attribution time range is [alarm_attribution_time\-alarm_window_size\*60, alarm_attribution_time]. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### AlarmParam

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|id |Long |No |1 |Alert task ID. |
|name |String |No |test |Alert task name. |
|desc |String |No |\- |Alert description. |
|is_close |Integer |No |0 |Whether to disable alerts.<br><br><br>* 0: Enable<br><br>* 1: Disable |
|category |String |No |pageview |Alert type key. Call the `GetAlarmMeta` API to view available values. |
|alarm_level |String |No |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|strategy_list |Array of [StrategyList](https://docs.byteplus.com/en/docs/299/67925#strategylist) |No |\- |Alert policy list. |
|strategy_op |String |No |and |Alert multi\-policy relationship.<br><br><br>* and: Satisfy all policies simultaneously<br><br>* or: Satisfy any policy |
|interval_seconds |Integer |No |300 |Alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|alarm_period |Object of [AlarmPeriod](https://docs.byteplus.com/en/docs/299/67925#alarmperiod) |No |\- |Alert effective time. Alerts outside the time range will not trigger notifications. |
|notify_config |Object of [NotifyConfig](https://docs.byteplus.com/en/docs/299/67925#notifyconfig) |No |\- |Notification configuration. |
|is_avoid_spike |Boolean |No |false |Whether to silence spike alerts. |
|pct_avoid_spike |Object of [PctAvoidSpike](https://docs.byteplus.com/en/docs/299/67925#pctavoidspike) |No |\- |pct alert. It is required when pct alert silence is enabled. |

### StrategyList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/67925#measure) |No |\- |Metric set. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67925#filterlist) |No |\- |Alert policy filter criteria. |
|alarm_strategy_type |String |No |threshold |Alert policy type.<br><br><br>* threshold: Threshold\-based alert<br><br>* cmp_last_n_day: Difference\-based alert |
|daily_compare_count |Integer |No |5 |Time interval between the previous period and the current period.<br><br>This parameter is required when the alert policy is difference\-based. The unit is minutes. For example, 1440 sets the comparison offset to 1 day ago. |
|alarm_threshold |Double |No |10 |Alert threshold. |
|threshold_cmp_op |String |No |gt |Policy operator.<br><br><br>* Valid values for difference\-based alerts: gt and lt<br><br>* Valid values for threshold\-based alerts: lt, lte, gt, and gte |
|alarm_user_threshold |Double |No |1 |User count threshold. |
|alarm_sample_threshold |Double |No |1 |Sample size threshold. |
|alarm_window_size |Long |No |180 |Time window for alert task query. It represents the last X minutes. The unit is minutes. |
|group_bys |Array of [GroupBys](https://docs.byteplus.com/en/docs/299/67925#groupbys) |No |\- |Alert grouping dimensions. |
|attribution_dimensions |Array of [AttributionDimensions](https://docs.byteplus.com/en/docs/299/67925#attributiondimensions) |No |\- |Alert attribution dimensions. |

### AlarmPeriod

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |No |0 |Alert start time.<br><br>The value is the start timestamp in seconds relative to 0:00 of the current day. For example, if the start time is 2:00 on the current day, the value is 7200. |
|end_time |Integer |No |86399 |Alert effective end time.<br><br>The value is the end timestamp in seconds relative to 0:00 of the current day. For example, if the end time is 23:59:59 on the current day, the value is 86399. |

### NotifyConfig

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|notify_types |Array of String |No |["mail"] |Alert task notification method.<br><br><br>* mail: Email<br><br>* lark: Feishu<br><br>* wechat: WeCom<br><br>* dingding: DingTalk |
|notify_lark_webhooks |Array of String |No |[] |A list of Feishu notification webhooks.<br><br>Required when the alert notification method includes Feishu. |
|notify_groups |Array of Long |No |[ 291 ] |List of alert notification email group IDs.<br><br>Required when the alert notification method includes email. |
|notify_wechat_webhooks |Array of String |No |[] |A list of WeCom notification webhooks.<br><br>Required when the alert notification method includes WeCom. |
|notify_dingding_webhooks |Array of String |No |[] |A list of DingTalk notification webhooks.<br><br>Required when the alert notification method includes DingTalk. |

### PctAvoidSpike

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|pct |Integer |No |1 |Alert sub\-window value. Available values: 1 to 9.<br><br>The alert is triggered only when the alert metric values of X or more sub\-windows exceed the configured alert threshold. |

### Measure

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67925#rawmeasurelist) |No |\- |List of metric sets. |
|formula |String |No |\- |Metric arithmetic formula.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |No |PV |The metric name.<br><br>When the metric is a simple metric, it is the metric name. When the metric is a composite metric, it is the custom metric name. |

### FilterList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Condition operator.<br><br><br>* in: contains<br><br>* not_in: does not contain<br><br>* Regex: Regex match<br><br>* not_regex: Regex mismatch |
|filter_name |String |No |browser_brand |Filter criterion key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|values |Array of String |No |["Chrome"] |Filter criterion values. Call the `GetAlarmMetricCandidate` API to view available values. |

### GroupBys

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|group_by_name |String |No |pid |Grouping dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|label |String |No |pid |Grouping metric. |

### AttributionDimensions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|group_by_name |String |No |pid |Attribution dimension key. Call the `GetAlarmMetricRelatedMeta` API to view available values. |
|label |String |No |pid |Attribution dimension. |

### RawMeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_name |String |No |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view available values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67925#filterlist) |No |\- |The filter condition. Optional when a single simple metric carries criteria and the metric type is composite. |
|event_name |String |No |\- |Custom event key. Required when the metric is a custom event metric. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmAttribution&Version=2022-10-12
{
    "common":{
        "aid":12345,
        "os":"webpro"
    },
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
    "strategy_id":0,
    "attribution_time":1666012500,
    "group_by_value":"Chrome Webview"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [Data](https://docs.byteplus.com/en/docs/299/67925#data) |\- |Response data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_category |String |performance |Alert task type. |
|attribution_dimension |String |pid |Attribution dimension key. |
|attribution_dimension_label |String |TOP pid |Alert description. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":[
        {
            "alarm_category":"performance",
            "attribution_dimension":"pid",
            "attribution_dimension_label":"TOP pid",
            "detail_list":[
                {
                    "name":"JS Monitoring list",
                    "link":""
                }
            ]
        },
        {
            "alarm_category":"performance",
            "attribution_dimension":"pid",
            "attribution_dimension_label":"Top PID with the fastest growth compared to the same period in the previous cycle",
            "detail_list":[
                {
                    "name":"JS Monitoring list",
                    "link":""
                }
            ]
        }
    ],
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
