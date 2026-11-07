---
title: "Draw"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Draw"
---

Queries metric details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## **Request parameters**

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|Action |Query |String |Yes |The action to be performed. Value: Draw. |
|Version |Query |String |Yes |API version. Value: 2022\-11\-09. |
|Graph |Body |Query |Yes |For details, see [Graph](https://docs.byteplus.com/en/docs/apmplus/Draw). |
|CurrentVaribaleValues |Body |Array[Varable] |Yes |Pass in an empty array. |
|StartTime |Body |Int64 |Yes |Start time. |
|EndTime |Body |Int64 |Yes |End time. |
|GranularityUnit |Body |String |Yes |Time interval. |
|Granularity |Body |Int64 |Yes |Interval. |


**Graph**


|**Parameters** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Id |String |Yes |An arbitrary value passed in from the frontend. |
|GraphType |String |Yes |Dashboard type.<br><br><br>* time_series: Time\-series graph<br><br>* table: Table<br><br>* single_value: Value |
|Name |String |Yes |An arbitrary value passed in from the frontend. |
|TimeSeriesConf |TimeSeriesGraphConfig |No |It can be used when the dashboard type is time_series. For details, see **TimeSeriesGraphConfig**. |
|TableConf |TableGraphConfig |No |It can be used when the dashboard type is table. For details, see **TableGraphConfig**. |
|SingleValueConf |SingleValueGraphConfig |No |It can be used when the dashboard type is single_value. For details, see **SingleValueGraphConfig**. |


**TimeSeriesGraphConfig**


|**Parameters** |**Type** |**Required** |**Description** |
|---|---|---|---|
|SimpleQueries |Array[TimeSeriesQuery] |Yes |Simple query. For details, see **TimeSeriesQuery**. |
|FormulaQueries |Array[FormulaQuery] |Yes |Formula query. For details, see **FormulaQuery**. |
|Precision |Int32 |Yes |Precision (number of decimal places). |
|Marker |Array[Marker] |Yes |Marker. You need to pass in an empty array. |
|ShowLegend |Boolean |Yes |Whether to show the legend. |
|Legend |Array[String] |Yes |Legend list. |


**TimeSeriesQuery**


|**Name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Id |String |Yes |The query name defined at the frontend. |
|Ispromql |Boolean |Yes |Whether it is a PromQL metric. |
|Promql |String |No |PromQL query. |
|Metric |String |Yes |The metric name. |
|Unit |String |Yes |Unit. |
|Alphabet |String |Yes |Symbols used in composite metric formulas. |
|Alias |String |Yes |Alias. |
|MetricCategory |String |Yes |Metric type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric |
|MetricSource |String |Yes |Metric type.<br><br><br>* prometheus<br><br>* influxdb |
|GroupByFields |Array[String] |Yes |Grouping.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the ArkClaw instance has custom tags, you can use these tags in <code>GroupByFields</code> for grouped querying.</div><br> |
|Aggregator |String |Yes |Group aggregation function. |
|AddFunc |String |Yes |Post\-processing function.<br><br><br>* diff<br><br>* per_second_rate<br><br>* per_minute_rate<br><br>* per_second<br><br>* per_minute |
|Filters |Array[FilterCondition] |Yes |Filter condition. For details, see **FilterCondition**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the ArkClaw instance has custom tags, you can use these tags in <code>Filters</code> for filtering.</div><br> |
|Hide |Boolean |Yes |Whether to hide. |
|CounterAs |String |No |Counter type.<br><br><br>* count<br><br>* rate |


**TableQuery**


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Id |String |Yes |The query name defined at the frontend. |
|Ispromql |Boolean |Yes |Whether it is a PromQL metric. |
|Promql |String |No |PromQL query. |
|Metric |String |Yes |The metric name. |
|Unit |String |Yes |Unit. |
|Alphabet |String |Yes |Symbols used in composite metric formulas. |
|Alias |String |Yes |Alias. |
|MetricCategory |String |Yes |Metric type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric |
|MetricSource |String |Yes |Metric type.<br><br><br>* prometheus<br><br>* influxdb |
|GroupByFields |Array[String] |Yes |Grouping.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the ArkClaw instance has custom tags, you can use these tags in <code>GroupByFields</code> for grouped querying.</div><br> |
|Aggregator |String |Yes |Group aggregation function. |
|AddFunc |String |Yes |Post\-processing function.<br><br><br>* diff<br><br>* per_second_rate<br><br>* per_minute_rate<br><br>* per_second<br><br>* per_minute |
|Filters |Array[FilterCondition] |Yes |Filter condition. For details, see **FilterCondition**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the ArkClaw instance has custom tags, you can use these tags in <code>Filters</code> for filtering.</div><br> |
|Hide |Boolean |Yes |Whether to show.  |
|CounterAs |String |No |Counter type.<br><br><br>* count<br><br>* rate |
|RollupTimeframeByAggregator |String |No |Time window aggregation method.<br><br><br>* AVG<br><br>* SUM<br><br>* LAST<br><br>* COUNT<br><br>* MAX<br><br>* MIN |


**SingleValueQuery**


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Id |String |Yes |The query name defined at the frontend. |
|Ispromql |Boolean |Yes |Whether it is a PromQL metric. |
|Promql |String |No |PromQL query. |
|Metric |String |Yes |The metric name. |
|Unit |String |Yes |Unit. |
|Alphabet |String |Yes |Symbols used in composite metric formulas. |
|Alias |String |Yes |Alias. |
|MetricCategory |String |Yes |Metric type.<br><br><br>* host<br><br>* process<br><br>* container<br><br>* custom_metric |
|MetricSource |String |Yes |Metric type.<br><br><br>* prometheus<br><br>* influxdb |
|GroupByFields |Array[String] |Yes |Grouping.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the ArkClaw instance has custom tags, you can use these tags in <code>GroupByFields</code> for grouped querying.</div><br> |
|Aggregator |String |Yes |Group aggregation function. |
|AddFunc |String |Yes |Post\-processing function.<br><br><br>* diff<br><br>* per_second_rate<br><br>* per_minute_rate<br><br>* per_second<br><br>* per_minute |
|Filters |Array[FilterCondition] |Yes |Filter condition. For details, see **FilterCondition**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the ArkClaw instance has custom tags, you can use these tags in <code>Filters</code> for filtering.</div><br> |
|Hide |Boolean |Yes |Whether to hide. |
|CounterAs |String |No |Counter type.<br><br><br>* count<br><br>* rate |
|RollupTimeframeByAggregator |String |Yes |Time window aggregation method.<br><br><br>* AVG<br><br>* SUM<br><br>* LAST<br><br>* COUNT<br><br>* MAX<br><br>* MIN |


**FormulaQuery**


|**Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Formula |String |Yes |Composite metric calculation formula. |
|Alias |String |No |Displayed name. |
|Unit |String |No |Unit. |
|Alphabet |String |No |Symbols used for calculation formulas. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## **Response parameters**

The Result parameter contains the following fields:


|**Field** |**type** |**Description** |
|---|---|---|
|SingleValue |SingleValueData |Numeric value dashboard. For details, see **SingleValueData**. |
|Table |TableData |Table dashboard. For details, see **TableData**. |
|TimeSeries |Array[TimeSeriesData] |Time\-series data dashboard. For details, see **TimeSeriesData**. |


**SingleValueData**


|**Field** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Value |String |100 |Numeric value. |
|Unit |String |s |Unit. |


**TableData**


|**Field** |**Type** |**Description** |
|---|---|---|
|Columns |Array[String] |Column name. |
|Units |Array[String] |Units that correspond to individual column names. |
|Rows |Array[Array[String]] |Numeric value. |


**TimeSeriesData**


|**Field** |**Type** |**Description** |
|---|---|---|
|QueryId |String |Request ID. It is consistent with the ID in the request. |
|Title |String |Title. It is consistent with the Alias field in the request. |
|Unit |String |Unit. |
|Legend |Legend |Legend. |
|Points |Array[SeriesPoint] |Time\-series data points. |
|Tagkvs |Array[Tagkv] |Label. |


**Legend**


|**Field** |**Type** |**Description** |
|---|---|---|
|Max |Float |Maximum value. |
|Min |Float |Minimum value. |
|Avg |Float |Average value. |
|Current |Float |Current value. |


**SeriesPoint**


|**Field** |**Type** |**Description** |
|---|---|---|
|Timestamp |String |Data timestamp. |
|Value |String |The value of the data point at this timestamp. |
|EndTimestamp |String |End timestamp. It is used for handling multi\-point merging. |


**TagKV**


|**Field** |**Type** |**Description** |
|---|---|---|
|Key |String |Marker. |
|Lable |String |Label. |
|Value |String |Marker value. |


<span id=".6K-35rGC56S65L6L"></span>
## **Sample request**

```json
POST https://open.volcengineapi.com?Action=Draw&Version=2022-11-09
&<Common Request Parameters>
```


<span id=".6L-U5Zue56S65L6L"></span>
## **Sample response**

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "Draw",
        "Version": "2022-11-09",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
        "SingleValue": {
            "Unit": "",
            "Value": ""
        },
        "Table": {
            "Columns": [],
            "Rows": [],
            "Units": []
        },
        "TimeSeries": [
            {
                "Legend": {
                    "Avg": 199291.5994444445,
                    "Current": 210846.96666666667,
                    "Max": 211086.86666666667,
                    "Min": 190502.8
                },
                "Points": [
                    {
                        "Timestamp": "1668135210",
                        "Value": 190875.13333333333
                    },
                    {
                        "Timestamp": "1668135240",
                        "Value": 190982.33333333334
                    },
                    {
                        "Timestamp": "1668135270",
                        "Value": 190502.8
                    },
                    {
                        "Timestamp": "1668135300",
                        "Value": 191046.43333333332
                    },
                    {
                        "Timestamp": "1668135330",
                        "Value": 190787.73333333334
                    },
                    {
                        "Timestamp": "1668135360",
                        "Value": 191358.9
                    },
                    {
                        "Timestamp": "1668135390",
                        "Value": 191692.96666666667
                    },
                    {
                        "Timestamp": "1668135420",
                        "Value": 191917.03333333333
                    },
                    {
                        "Timestamp": "1668135450",
                        "Value": 191739.16666666666
                    },
                    {
                        "Timestamp": "1668135480",
                        "Value": 191995.73333333334
                    },
                    {
                        "Timestamp": "1668135510",
                        "Value": 192374.5
                    },
                    {
                        "Timestamp": "1668135540",
                        "Value": 192149
                    },
                    {
                        "Timestamp": "1668135570",
                        "Value": 192211.73333333334
                    },
                    {
                        "Timestamp": "1668135600",
                        "Value": 193150.93333333332
                    },
                    {
                        "Timestamp": "1668135630",
                        "Value": 194578.9
                    },
                    {
                        "Timestamp": "1668135660",
                        "Value": 195246.33333333334
                    },
                    {
                        "Timestamp": "1668135690",
                        "Value": 195474.8
                    },
                    {
                        "Timestamp": "1668135720",
                        "Value": 194953.9
                    }
                ],
                "QueryId": "5387660146-1657110201438",
                "Tagkvs": [],
                "Title": "a : RTA_Product.call_user_interested",
                "Unit": ""
            }
        ]
    }
}
```
