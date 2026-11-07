---
title: "FlatAlertHistoryList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/FlatAlertHistoryList"
---

Modifies the details of alert rules.

<span id="a170d0ad"></span>
## Request method

Use the POST method to send the request.

<span id="d0075e93"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a common parameter. |FlatAlertHistoryList |
|Version |Query |String |Yes |The API version, which is a public parameter. |2022\-07\-11 |
|StartTime |RequestBody |Int64 |Yes |Start time. |\- |
|EndTime |RequestBody |Int64 |Yes |End time. |\- |
|OrderBy |RequestBody |String |Yes |The order.<br><br><br>* asc<br><br>* desc |\- |
|AlertType |RequestBody |String |Yes |The alert type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric: This parameter can be left empty. |\- |
|Keyword |RequestBody |String |Yes |The search keyword. |\- |
|RuleIds |RequestBody |Array[Int64] |Yes |The alert policy IDs. |\- |
|PageNo |RequestBody |Int32 |Yes |The page number. |\- |
|PageSize |RequestBody |Int32 |Yes |The page size. |\- |


<span id="abb1a7a6"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Total |Int32 |The list length. |
|Data |Array[FlatAlertHistoryItem] |The alert details. |


**FlatAlertHistoryItem**


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert history ID. |
|RuleId |Int32 |The alert policy ID. |
|Name |Int32 |The alert policy name. |
|Level |Int32 |The alert level. |
|AlertTime |Int32 |The alert time. |
|AlertStrategy |AlertStrategy |The alert policy. |
|NotifyConfig |NotifyConfig |The alert notification configuration. |
|RuleCheckResult |RuleCheckResult |The alert query result. |
|Status |AlertRuleStatus |The alert status. |


**AlertRuleConfig**


|**Field** |**Type** |**Description** |
|---|---|---|
|Name |String |The alert name. |
|Desc |String |The alert description. |
|AlertStrategy |AlertStrategy |The alert policy. |
|NotifyConfig |NotifyConfig |The alert notification configuration. |


**NotifyConfig**


|**Field** |**Type** |**Description** |
|---|---|---|
|NotifyInterval |Int32 |The notification interval. |
|NotifyTypes |Array[String] |The alert type.<br><br><br>* email<br><br>* lark |
|NotifyLarkWebhooks |Array[String] |The Feishu webhooks. |
|NotifyWebhooks |Array[String] |The common webhooks. |
|NotifyGroup |Array[Int32] |The alert group ID. |


**AlertStrategy**


|**Field** |**Type** |**Description** |
|---|---|---|
|AlertType |String |The alert type. |
|AlertLevel |Array[String] |The alert level. |
|LogicOperator |String |Multiple\-policy logic<br><br><br>* and<br><br>* or |
|ExecuteInterval |Int32 |The alert execution interval. Unit: minutes. |
|MetricConfig |Array[AlertMetricConfig] |The metric policy. |


**AlertMetricConfig**


|**Field** |**Type** |**Description** |
|---|---|---|
|ScanWindow |Int32 |The detection time window. Unit: minutes. |
|RollupTimeframeByAggregator |String |Time window aggregation method.<br><br><br>* AVG<br><br>* SUM<br><br>* LAST<br><br>* COUNT<br><br>* MAX<br><br>* MIN |
|AlertMetric |AlertMetric |The alert execution interval. Unit: minutes. |
|CompareConfigList |Map[AlertCompareConfig] |The metric policy. |


**AlertMetric**


|**Field** |**Type** |**Description** |
|---|---|---|
|IsFormula |Boolean |Whether it is a composite alert. |
|SimpleMetric |AlertSimpleMetric |The simple alert metric. When IsFormula is set to true, leave this parameter empty. |
|FormulaMetric |AlertFormulaMetric |The composite alert metric. When IsFormula is set to false, leave this parameter empty. |


**AlertSimpleMetric**


|**Field** |**type** |**Description** |
|---|---|---|
|AlertSimpleMetric |Array[AlertSimpleMetric] |The simple alert metric. |
|FormulaQuery |FormulaQuery |The composite metric configuration. |


**FormulaQuery**


|**Field** |**Type** |**Description** |
|---|---|---|
|Formula |String |Composite metric calculation formula. |
|Alias |String |Displayed name. |
|Unit |String |Unit |
|Alphabet |String |Symbols used for calculation formulas. |


**RuleCheckResult**


|**Field** |**Type** |**Description** |
|---|---|---|
|IsAlert |Boolean |Composite metric calculation formula. |
|NoDataAlert |Boolean |The NoData alert. |
|Level |String |The alert level. |
|Alphabet |String |The symbol used in the calculation formula. |
|AlertStrategy |AlertStrategy |The alert policy. |
|RelatedAlertMetricResult |Array[MetricCheckResult] |The associated alert metrics. |


**MetricCheckResult**


|**Field** |**Type** |**Description** |
|---|---|---|
|IsAlert |Boolean |Composite metric calculation formula. |
|Level |String |The alert level. |
|AlertMetric |AlertMetricConfig |The alert policy. |
|RelatedValues |Array[GroupValue] |The associated alert metrics. |


**GroupValue**


|**Field** |**Type** |**Description** |
|---|---|---|
|Tags |Array[Tags] |Label. |
|AlertValue |float64 |The alert value. |
|CurValue |float64 |Current value. |
|PreValue |float64 |The previous value. |
|DeltaRatio |float64 |The change value. |
|DeltaAbsolute |float64 |The change rate. |


**AlertSimpleMetric**


|**Field** |**Type** |**Description** |
|---|---|---|
|Ispromql |Boolean |Whether it is a PromQL metric. |
|Promql |String |PromQL query. |
|Metric |String |The metric name. |
|Unit |String |Unit. |
|Alphabet |String |Symbols used in composite metric formulas. |
|MetricCategory |String |The metric type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric |
|MetricSource |String |Metric type.<br><br><br>* prometheus<br><br>* influxdb |
|GroupByFields |Array[String] |Grouping. |
|Aggregator |String |Group aggregation function. |
|AddFunc |String |Post\-processing function.<br><br><br>* diff<br><br>* per_second_rate<br><br>* per_minute_rate<br><br>* per_second<br><br>* per_minute |
|Filters |Array[FilterCondition] |Filter condition. |


**FilterCondition**


|**Field** |**Type** |**Description** |
|---|---|---|
|Key |String |The tag name for filtering. |
|Op |String |The operator for filtering.<br><br><br>* <<br><br>* \><br><br>* =<br><br>* <=<br><br>* \>= |
|Values |String |Unit. |


**AlertRuleStatus**


|**Field** |**Type** |**Description** |
|---|---|---|
|CreateBy |User |The user who created the alert. |
|UpdateBy |User |The user who last modified the alert. |
|CreateAt |Int64 |Creation time. |
|UpdateAt |Int64 |The last update time. |
|AlertCount |Int64 |The alert count. |
|LastMonthAlertCount |Int64 |The alert count in the last month. |
|LastExecuteTime |Int64 |The last alert time. |
|NextTriggerTime |Int64 |The next execution time. |
|EnableStatus |Boolean |Whether the alert is enabled. |
|AlertStatus |Boolean |Whether it is deleted. |
|InAck |Boolean |Whether the alert is acknowledged. |
|AckUntilTime |int64 |The time until which the acknowledgement is valid. |


<span id="a54b572e"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=FlatAlertHistoryList&Version=2022-07-11
&<Common Request Parameters>
```


<span id="a671c37e"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "FlatAlertHistoryList",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
        "Data": [
            {
                "AlertStrategy": {
                    "AlertLevel": [
                        "Fatal"
                    ],
                    "AlertSphere": {
                        "IsAgg": false,
                        "ServiceApis": [],
                        "ServiceNames": [
                            "server_trace_panic"
                        ],
                        "SphereType": "service"
                    },
                    "AlertType": "service",
                    "ExecuteInterval": 120,
                    "GroupAlert": false,
                    "LogicOperator": "and",
                    "MetricConfig": [
                        {
                            "AlertMetric": {
                                "FormulaMetric": {
                                    "AlertSimpleMetric": [
                                        {
                                            "Aggregator": "AVG",
                                            "Alphabet": "a",
                                            "Filters": [
                                                {
                                                    "Key": "",
                                                    "Op": "in",
                                                    "Values": []
                                                }
                                            ],
                                            "GroupByFields": [],
                                            "Ispromql": false,
                                            "Metric": "",
                                            "MetricCategory": "",
                                            "MetricLabel": "",
                                            "MetricSource": "",
                                            "MetricType": "",
                                            "Unit": ""
                                        }
                                    ],
                                    "FormulaQuery": {
                                        "Alias": "",
                                        "Alphabet": "",
                                        "Formula": "",
                                        "Hide": false,
                                        "Id": "",
                                        "Unit": ""
                                    }
                                },
                                "IsFormula": false,
                                "SimpleMetric": {
                                    "Aggregator": "AVG",
                                    "Alphabet": "a",
                                    "Filters": [
                                        {
                                            "Key": "",
                                            "Op": "in",
                                            "Values": []
                                        }
                                    ],
                                    "GroupByFields": [],
                                    "Ispromql": false,
                                    "Metric": "apminsight.service.log.error",
                                    "MetricCategory": "service",
                                    "MetricLabel": "Error Log Count",
                                    "MetricSource": "influxdb",
                                    "MetricType": "",
                                    "Unit": ""
                                }
                            },
                            "CompareConfigList": {
                                "Fatal": {
                                    "CompareOp": "\u003e",
                                    "CompareType": "threshold",
                                    "Level": "Fatal",
                                    "Value": 2,
                                    "WindowSize": 60
                                },
                                "Notice": {
                                    "CompareOp": "\u003e",
                                    "CompareType": "threshold",
                                    "Level": "Notice",
                                    "Value": 0,
                                    "WindowSize": 60
                                },
                                "Warn": {
                                    "CompareOp": "\u003e",
                                    "CompareType": "threshold",
                                    "Level": "Warn",
                                    "Value": 0,
                                    "WindowSize": 60
                                }
                            },
                            "Id": "8168465247-1658074826937",
                            "RollupTimeframeByAggregator": "SUM",
                            "ScanWindow": 5
                        }
                    ],
                    "NoDataNotify": false,
                    "NoDataNotifyThreshold": 10,
                    "ServiceNames": [
                        "server_trace_panic"
                    ],
                    "WatchdogEvents": [
                        {
                            "Category": "host",
                            "CategoryLabel": "Host Monitoring",
                            "EventName": "cpu_used_ratio_overtop",
                            "EventNameLabel": "High CPU Usage",
                            "Filters": []
                        }
                    ]
                },
                "AlertTime": "1658133720",
                "Id": "566776",
                "Level": "Fatal",
                "Name": "testwjx",
                "NotifyConfig": {
                    "NotifyGroup": [
                        137
                    ],
                    "NotifyInterval": 120,
                    "NotifyTypes": [
                        "email"
                    ]
                },
                "RuleCheckResult": {
                    "AlertStrategy": {
                        "AlertLevel": null,
                        "AlertType": "",
                        "ExecuteInterval": 0,
                        "GroupAlert": false,
                        "LogicOperator": "",
                        "MetricConfig": null,
                        "NoDataNotify": false,
                        "NoDataNotifyThreshold": 0,
                        "ServiceNames": null
                    },
                    "IsAlert": true,
                    "Level": "Fatal",
                    "NoDataAlert": false,
                    "RelatedAlertMetricResult": [
                        {
                            "AlertMetric": {
                                "AlertMetric": {
                                    "FormulaMetric": {
                                        "AlertSimpleMetric": [
                                            {
                                                "Aggregator": "AVG",
                                                "Alphabet": "a",
                                                "Filters": [
                                                    {
                                                        "Key": "",
                                                        "Op": "in",
                                                        "Values": []
                                                    }
                                                ],
                                                "GroupByFields": [],
                                                "Ispromql": false,
                                                "Metric": "",
                                                "MetricCategory": "",
                                                "MetricLabel": "",
                                                "MetricSource": "",
                                                "MetricType": "",
                                                "Unit": ""
                                            }
                                        ],
                                        "FormulaQuery": {
                                            "Alias": "",
                                            "Alphabet": "",
                                            "Formula": "",
                                            "Hide": false,
                                            "Id": "",
                                            "Unit": ""
                                        }
                                    },
                                    "IsFormula": false,
                                    "SimpleMetric": {
                                        "Aggregator": "AVG",
                                        "Alphabet": "a",
                                        "Filters": [
                                            {
                                                "Key": "",
                                                "Op": "in",
                                                "Values": []
                                            }
                                        ],
                                        "GroupByFields": [],
                                        "Ispromql": false,
                                        "Metric": "apminsight.service.log.error",
                                        "MetricCategory": "service",
                                        "MetricLabel": "Error Log Count",
                                        "MetricSource": "influxdb",
                                        "MetricType": "",
                                        "Unit": ""
                                    }
                                },
                                "CompareConfigList": {
                                    "Fatal": {
                                        "CompareOp": "\u003e",
                                        "CompareType": "threshold",
                                        "Level": "Fatal",
                                        "Value": 2,
                                        "WindowSize": 60
                                    },
                                    "Notice": {
                                        "CompareOp": "\u003e",
                                        "CompareType": "threshold",
                                        "Level": "Notice",
                                        "Value": 0,
                                        "WindowSize": 60
                                    },
                                    "Warn": {
                                        "CompareOp": "\u003e",
                                        "CompareType": "threshold",
                                        "Level": "Warn",
                                        "Value": 0,
                                        "WindowSize": 60
                                    }
                                },
                                "Id": "8168465247-1658074826937",
                                "RollupTimeframeByAggregator": "SUM",
                                "ScanWindow": 5
                            },
                            "IsAlert": true,
                            "Level": "Fatal",
                            "RelatedValues": [
                                {
                                    "AlertValue": 51,
                                    "CurValue": 51,
                                    "DeltaAbsolute": 51,
                                    "DeltaRatio": 1,
                                    "PreValue": 0,
                                    "Tags": null
                                }
                            ]
                        }
                    ],
                    "RelatedAlertWatchdogResult": null
                },
                "RuleId": 251,
                "Status": {
                    "AckUntilTime": "1658075004",
                    "InAck": false,
                    "IsNotified": true,
                    "IsUpgraded": false,
                    "NoNotifyReason": "",
                    "NoNotifyReasonDesc": ""
                }
            }
        ],
        "Total": 30
    }
}
```


&nbsp;
