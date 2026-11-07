---
title: "Querying ArkClaw Enterprise metrics"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Querying_ArkClaw_Enterprise_metrics"
---

ArkClaw Enterprise supports comprehensive metric query capabilities through Server\-side Monitoring. In addition to the basic visual dashboards, Server\-side Monitoring provides a unified metric query API that allows you to customize metric queries based on your needs. In this topic, the preset metric `arkclaw_enterprise_total_token_usage_sum` is used as an example to describe how to query ArkClaw Enterprise metrics.

<span id="o0GnnUv9"></span>
## Background


* The Draw API provided by Server\-side Monitoring is available for querying ArkClaw Enterprise metrics.

   
   |**Item** |**The value of a label** |
   |---|---|
   |API name |Draw, for metric graph queries |
   |Action |Draw |
   |Version |2022\-11\-09 |
   |Document |Draw API help documentation |
   |Protocol |HTTPS POST. The request body is JSON. |
   

* The reference for the basic information about the preset metric `arkclaw_enterprise_total_token_usage_sum`.

   
   |Category |Description |
   |---|---|
   |Preset metric |arkclaw_enterprise_total_token_usage_sum |
   |Metric definition |Total token consumption of ArkClaw instances across input, output, and cache. |
   |Grouping dimensions |Configure grouping dimensions based on your needs. The available fields include:<br><br><br>* service: instance ID<br><br>* user_email: user email<br><br>* user_name: user name<br><br>* user_department: user department<br><br>* claw_space_id: Claw space ID<br><br>* openclaw_token: Token type<br><br>* openclaw_channel: channel<br><br>* openclaw_provider: service provider<br><br>* openclaw_model: model |
   


<span id="rN7CnIug"></span>
## Limits

Draw supports both preset metric queries and PromQL queries. However, because the user information in ArkClaw Enterprise metrics comes from external APIs or underlying instrumentation, PromQL queries are not supported. You can use preset metric queries only.

<span id="TUqM58bx"></span>
## Query examples

Because the API parameters are relatively complex, to reduce debugging costs, the preset metric `arkclaw_enterprise_total_token_usage_sum` is used as an example to describe several common query examples for preset metric queries.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To query other preset metrics, use the query template for this scenario and replace the key fields for each metric. For more information about metrics, see <a href="https://docs.byteplus.com/en/docs/Observability_Platform/ArkClaw_Enterprise_metric_descriptions">ArkClaw Enterprise metric descriptions</a>.</div>



<Tabs>
<Tab zoneid="qKPPeERBJI" title="Example 1: Single value query / instant query">
<TabTitle>Example 1: Single value query / instant query</TabTitle>

This example illustrates how to query the total token consumption.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In a single\-value query request, set the parameter <code>"instant": true</code>. The result is returned in Table format.</div>


* <div data-tips="true" data-tips-type="warning">Modify <code>metric</code> to query the specified metric. To query ArkClaw metrics, simply set <code>metric_category</code> to <code>claw</code>.</div>


* <div data-tips="true" data-tips-type="warning">To set filter conditions, modify<code> filters</code>. To specify grouping dimensions, use<code> group_by_fields</code>.</div>


* <div data-tips="true" data-tips-type="warning">To specify a query time range, modify <code>start_time</code> and <code>end_time</code>.</div>



<span id="SHnhh21d"></span>
### Sample request

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If custom tags are configured for an ArkClaw instance, you can use the tags in <code>filters</code> to filter data and in<code> group_by_fields</code> to query data by group. For details of ArkClaw instance custom tags, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Tag_management">Managing tags</a>.</div>


```JSON
{
    "graph": {
        "graph_type": "table",
        "table_conf": {
            "simple_queries": [
                {
                    "metric": "arkclaw_enterprise_total_token_usage_sum",
                    "metric_category": "claw",
                    "filters": [
                        {
                            "key": "claw_space_id",
                            "op": "in",
                            "values": [
                                "csi-xxxxx"
                            ]
                        },
                        {
                            "key": "user_name",
                            "op": "in",
                            "values": [
                                "userA"
                            ]
                        }
                    ],
                    "group_by_fields": [
                        "user_name",
                        "user_email"
                    ],
                    "instant": true
                }
            ]
        }
    },
    "start_time": 1779270789,
    "end_time": 1780480389
}
```


<span id="vR2YtlIL"></span>
### Sample response

The query response format is as follows. Focus on `Columns` and `Rows` in the response. When you query only one metric at a time, the last column in `Columns` is always the query result value, and the preceding columns contain the related attribute information. `ValueColumns` identifies which columns are metric value columns.


* Columns: The meaning of each column in the result.

* Rows: Each element represents a row in the result. The meaning of each column corresponds one\-to\-one with Columns.


```JSON
{
    "Result": {
        "Table": {
            "Columns": [
                "user_email",
                "user_name",
                "arkclaw_enterprise_total_token_usage_sum"
            ],
            "Rows": [
                [
                    "user_a@example.com",
                    "userA",
                    "1.000000"
                ]
            ],
            "Time": "1780480389",
            "Units": [
                "",
                "",
                ""
            ],
            "ValueColumns": [
                "arkclaw_enterprise_total_token_usage_sum"
            ]
        }
    }
}
```





</Tab>
<Tab zoneid="UeziVrpy6N" title="Example 2: Time series query">
<TabTitle>Example 2: Time series query</TabTitle>

This example illustrates how to query the total token consumption trend.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In a time series query request, set the<code> graph_type</code> parameter to <code>time_series</code>. The request returns data in time series format, where each time series contains data points aligned by time granularity along with the corresponding label information.</div>


* <div data-tips="true" data-tips-type="warning">Modify <code>metric</code> to query the specified metric. To query ArkClaw metrics, simply set <code>metric_category</code> to <code>claw</code>.</div>


* <div data-tips="true" data-tips-type="warning">To set filter conditions, modify<code> filters</code>. To specify grouping dimensions, use<code> group_by_fields</code>.</div>


* <div data-tips="true" data-tips-type="warning">To specify a query time range, modify <code>start_time</code> and <code>end_time</code>.</div>



<span id="HuDVD7lI"></span>
### Sample request

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If custom tags are configured for an ArkClaw instance, you can use the tags in <code>filters</code> to filter data and in<code> group_by_fields</code> to query data by group. For details of ArkClaw instance custom tags, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Tag_management">Managing tags</a>.</div>


```JSON
{
    "graph": {
        "graph_type": "time_series",
        "time_series_conf": {
            "simple_queries": [
                {
                    "metric": "arkclaw_enterprise_total_token_usage_sum",
                    "metric_category": "claw",
                    "filters": [
                        {
                            "key": "claw_space_id",
                            "op": "in",
                            "values": [
                                "csi-xxxxx"
                            ]
                        },
                        {
                            "key": "user_name",
                            "op": "in",
                            "values": [
                                "userA"
                            ]
                        }
                    ],
                    "aggregator": "GROUP_BY",
                    "group_by_fields": [
                        "user_name",
                        "user_email"
                    ]
                }
            ]
        }
    },
    "start_time": 1780477852,
    "end_time": 1780481452,
    "granularity": 30
}
```


<span id="iaCYrAhi"></span>
### Sample response

The query response format is as follows. Focus on `TimeSeries` in the response. In `TimeSeries`, each object is a single time series;` Points` contains the timestamp and corresponding value of each point in the time series; `TagKvs` contains all the attribute information of the time series.

```JSON
{
    "Result": {
        "TimeSeries": [
            {
                "Points": [
                    {
                        "Timestamp": 1780477830,
                        "Value": 1000800
                    },
                    {
                        "Timestamp": 1780477860,
                        "Value": 1992999
                    },
                    {
                        "Timestamp": 1780477890,
                        "Value": 1630000
                    }
                ],
                "Tagkvs": [
                    {
                        "Key": "user_name",
                        "Value": "userA"
                    },
                    {
                        "Key": "user_email",
                        "Value": "user_a@example.com"
                    }
                ]
            }
        ]
    }
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If custom tags are configured for an ArkClaw instance, you can use the tags in <code>filters</code> to filter data and in<code> group_by_fields</code> to query data by group.</div>



</Tab>
</Tabs>


<span id="J6ou9LVJ"></span>
###
