---
title: "GetAlertRuleDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlertRuleDetail"
---

Queries the details of an alert rule.

<span id="74e28235"></span>
## Request method

Use the POST method to send the request.

<span id="TNz08CZm"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a common parameter. |GetAlertRuleDetail |
|Version |Query |String |Yes |The API version, which is a public parameter. |2022\-07\-11 |
|Id |RequestBody |Int64 |Yes |The alert configuration ID. |\- |


<span id="b88fdd98"></span>
## Response parametersThe Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The API name, which is a common parameter. |
|Config |AlertRuleConfig |The alert configuration. |
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
|AlertType |String |The alert type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric |
|AlertLevel |Array[String] |The alert level. |
|LogicOperator |String |The multiple\-policy relationship.<br><br><br>* and<br><br>* or |
|ExecuteInterval |Int32 |The alert execution interval. Unit: minutes. |
|MetricConfig |Array[AlertMetricConfig] |The metric policy. |


**AlertMetricConfig**


|**Field** |**Type** |**Description** |
|---|---|---|
|ScanWindow |Int32 |The detection time window. Unit: minutes. |
|RollupTimeframeByAggregator |String |Time window aggregation method.<br><br><br>* AVG<br><br>* SUM<br><br>* LAST<br><br>* COUNT<br><br>* MAX<br><br>* MIN |
|AlertMetric |AlertMetric |The alert execution interval. Unit: minutes. |
|CompareConfigList |Map[AlertCompareConfig] |The metric policy. |


**AlertCompareConfig**


|**Field** |**Type** |**Description** |
|---|---|---|
|CompareType |String |* Threshold: thershold<br><br>* Comparison: window |
|CompareOp |String |Threshold:<br><br><br>* \><br><br>* <<br><br>* <=<br><br>* \>=<br><br>* =<br><br>   Comparison:<br><br>* increase<br><br>* increase_percent<br><br>* decrease<br><br>* decrease_percent<br><br>* abs<br><br>* abs_percent |
|Level |String |The alert level is the same as MapKey. |
|WindowSize |Int3 |The data sampling window size. Unit: seconds. |
|Value |Float64 |The threshold. |


**AlertMetric**


|**Field** |**Type** |**Description** |
|---|---|---|
|IsFormula |Boolean |Whether it is a composite alert. |
|SimpleMetric |AlertSimpleMetric |The simple alert metric. When IsFormula is set to true, leave this parameter empty. |
|FormulaMetric |AlertFormulaMetric |The composite alert metric. When IsFormula is set to false, leave this parameter empty. |


**AlertSimpleMetric**


|**Field** |**Type** |**Description** |
|---|---|---|
|AlertSimpleMetric |Array[AlertSimpleMetric] |The simple alert metric. |
|FormulaQuery |FormulaQuery |The composite metric configuration. |


**FormulaQuery**


|**Field** |**Type** |**Description** |
|---|---|---|
|Formula |String |Composite metric calculation formula. |
|Alias |String |Displayed name. |
|Unit |String |Unit. |
|Alphabet |String |Symbols used for calculation formulas. |


**AlertSimpleMetric**


|**Field** |**Type** |**Description** |
|---|---|---|
|Ispromql |Boolean |Whether it is a PromQL metric. |
|Promql |String |PromQL query. |
|Metric |String |The metric name. |
|Unit |String |Unit. |
|Alphabet |String |The symbol used in the composite metric formula. |
|MetricCategory |String |Metric type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric |
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


<span id="66e0188a"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=GetAlertRuleDetail&Version=2022-07-11
&<Common Request Parameters>
```


<span id="9a855b3c"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "GetAlertRuleDetail",
        "Region": "cn-beijing",
        "RequestId": "",
        "Service": "apmplus_server",
        "Version": "2022-07-11"
    },
    "Result": {
        "Config": {
            "AlertStrategy": {
                "AlertLevel": [
                    "Fatal"
                ],
                "AlertSphere": {
                    "IsAgg": false,
                    "ServiceApis": [],
                    "ServiceNames": [
                        "server_trace_error"
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
                                "CompareOp": "",
                                "CompareType": "threshold",
                                "Level": "Fatal",
                                "Value": 3,
                                "WindowSize": 60
                            },
                            "Notice": {
                                "CompareOp": "",
                                "CompareType": "threshold",
                                "Level": "Notice",
                                "Value": 0,
                                "WindowSize": 60
                            },
                            "Warn": {
                                "CompareOp": "",
                                "CompareType": "threshold",
                                "Level": "Warn",
                                "Value": 0,
                                "WindowSize": 60
                            }
                        },
                        "Id": "8979402427-1655877919010",
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
            "CreateFrom": "",
            "Desc": "",
            "Name": "gyf_test error_log1",
            "NotifyConfig": {
                "NotifyGroup": [
                    93
                ],
                "NotifyInterval": 86400,
                "NotifyTypes": [
                    "email"
                ]
            }
        },
        "Id": 241,
        "Status": {
            "AckUntilTime": "1655877953",
            "AlertCount": "12119",
            "AlertStatus": true,
            "CreateAt": "1655877953",
            "CreateBy": {
                "AvatarUrl": "",
                "Email": "",
                "Name": "bytedance-apm"
            },
            "EnableStatus": true,
            "InAck": false,
            "LastExecuteTime": "1657801440",
            "LastMonthAlertCount": "0",
            "LastTrigerTime": "0",
            "NextTriggerTime": "1657801560",
            "UpdateAt": "1657800066",
            "UpdateBy": {
                "AvatarUrl": "",
                "Email": "",
                "Name": "bytedance-apm"
            }
        }
    }
}
```
