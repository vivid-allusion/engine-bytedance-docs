---
title: "UpdateAlertRule"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/UpdateAlertRule"
---

Modifies the details of an alert rule.

<span id="159ccab6"></span>
## Request method

Use the POST method to send the request.

<span id="d1c41a58"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a public parameter. |UpdateAlertRule |
|Version |Query |String |Yes |The API version, which is a public parameter. |2022\-07\-11 |
|Id |RequestBody |Int64 |Yes |The alert configuration ID. |\- |
|Config |RequsetBody |AlertRuleConfig |Yes |The alert configuration. |\- |


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
|CompareConfigList |Map[AlertCompareConfig] |The metric policy.<br><br><br>* Notice<br><br>* Warn<br><br>* Fatal |


**AlertCompareConfig**


|**Field** |**Type** |**Description** |
|---|---|---|
|CompareType |String |* thershold: Threshold<br><br>* window: Comparison |
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


**AlertFormulaMetric**


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
|Alphabet |String |Symbols used in composite metric formulas. |
|MetricCategory |String |Metric type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric |
|MetricSource |String |Metric type.<br><br><br>* prometheus<br><br>* influxdb |
|GroupByFields |Array[String] |Grouping. |
|Aggregator |String |Group aggregation function. |
|AddFunc |String |Post\-processing function.<br><br><br>* diff<br><br>* per_second_rate<br><br>* per_minute_rate<br><br>* per_second<br><br>* per_minute |
|Filters |Array[FilterCondition] |The filter criteria. |


**FilterCondition**


|**Field** |**Type** |**Description** |
|---|---|---|
|Key |String |The tag name for filtering. |
|Op |String |The operator for filtering.<br><br><br>* <<br><br>* \><br><br>* =<br><br>* <=<br><br>* \>= |
|Values |String |Unit. |


<span id="d1d2c5db"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert group ID. |


<span id="d668bafa"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=UpdateAlertRule&Version=2022-07-11
&<Common Request Parameters>
```


<span id="4f81b81b"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "UpdateAlertRule",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id":1
    }
}
```
