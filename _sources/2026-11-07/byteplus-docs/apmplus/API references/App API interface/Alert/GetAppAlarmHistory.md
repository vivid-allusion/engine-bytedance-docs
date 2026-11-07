---
title: "GetAppAlarmHistory"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmHistory"
---

Get app alert history.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppAlarmHistory&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppAlarmHistory |The API name. The current API name is `GetAppAlarmHistory`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|aid |Long |Yes |123456 |Application ID. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67879#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|start_time |Long |Yes |1665417600 |Start time. |
|end_time |Long |Yes |1666417600 |The end time. |
|query_key |String |No |test |Fuzzy search by alert event name. It defaults to all events if not specified. |
|page_size |Long |No |2 |Number of items per page. Defaults to 10 if not specified. |
|page_no |Long |No |1 |The starting page number is 1. |
|monitor_types |Array of String |No |["crash"] |Monitoring type.<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* app_page_js_err: Page monitoring / JS error<br><br>* app_page_ajax_err: Page monitoring / Request error<br><br>* app_page_perf: Page monitoring / Performance<br><br>* app_event: Event alert<br><br>* net_err: Network error<br><br>* custom_exception: Custom error<br><br>* traffic_exception: Traffic<br><br>* disk_exception: Disk<br><br>* battery_trace: Battery<br><br>* cpu_exception：CPU |
|order_by |String |No |\- |Sorting method. It defaults to sorting by alert time in descending order. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67879#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppAlarmHistory&Version=2022-10-12
{
    "aid":123456,
    "start_time":1679155200,
    "end_time":1679295939,
    "filters":{
        "type":"and",
        "sub_conditions":[
            {
                "dimension":"rule_id",
                "type":"expression",
                "op":"in",
                "values":[
                    "717"
                ]
            }
        ]
    },
    "query_key":"",
    "monitor_types":[
        "crash"
    ],
    "page_no":1,
    "page_size":1
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [AlarmEventPage](https://docs.byteplus.com/en/docs/299/67879#alarmeventpage) |\- |Alert history list. |
|error_msg |String |\- |Error message. It is empty if the request succeeds. |
|error_no |Long |0 |Error code. If the request was successful, its value is 0. |


<span id="alarmeventpage"></span>
### AlarmEventPage


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [AlarmEvent](https://docs.byteplus.com/en/docs/299/67879#alarmevent) |\- |Alert history. |
|curr_page |Long |1 |Current page number. |
|total_cnt |Long |99 |The total number of items. |
|total_page |Long |10 |Total page count. |


<span id="alarmevent"></span>
### AlarmEvent


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1 |Alert ID. |
|rule_id |Long |1 |Alert task ID. |
|rule_name |String |test |Alert name. |
|occur_time |String |\- |Alert event occurrence time. |
|notify_content |String |\- |Alert content. |
|alarm_level |String |\- |Alert level.<br><br><br>* warning<br><br>* fatal |
|notify_types |Array of String |[mail] |Notification method. |
|handle_status |Long |\- |Processing state. |
|ack_status |Long |0 |ACK status.<br><br><br>* 0: Confirmable<br><br>* 1: Resettable |
|ack_time |String |\- |ACK time. |
|url |String |\- |URLs. |
|operators |Array of String |\- |List of alert creator IDs. |
|operators_info |Array of [UserProfile](https://docs.byteplus.com/en/docs/299/67879#userprofile) |\- |Information about the alert creator. |
|filter_info |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67879#filtercondition) |\- |Alert task condition. |
|monitor_type |String |crash |Monitoring type.<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* app_page_js_err: Page monitoring / JS error<br><br>* app_page_ajax_err: Page monitoring / Request error<br><br>* app_page_perf: Page monitoring / Performance<br><br>* app_event: Event alert<br><br>* net_err: Network error<br><br>* custom_exception: Custom exception type. |
|hit_rule |Object of [AlarmHitRule](https://docs.byteplus.com/en/docs/299/67879#alarmhitrule) |\- |Alert task rule configuration. |
|rule_brief |String |\- |Brief description of the rule corresponding to the alert event. |
|alarm_receives |Array of [Candidate](https://docs.byteplus.com/en/docs/299/67879#candidate) |\- |Alert email receiver group information. |


<span id="userprofile"></span>
### UserProfile


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1 |User ID. |
|username |String |test_name |Username. |
|email |String |test@test.com |User email. |


<span id="filtercondition"></span>
### FilterCondition


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |and |Condition type.<br><br><br>* expression: Expression<br><br>* and: AND operator<br><br>* or: OR operator |
|dimension |String |aid |The name of the condition. |
|op |String |in |The operator.<br><br><br>* in: contains |
|value |String |123456 |The filter value. |
|values |Array of String |[123456] |The filter value. Multiple filter values are supported. |
|sub_conditions |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67879#filtercondition) |\- |The sub\-condition. |


<span id="alarmhitrule"></span>
### AlarmHitRule


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |and |Condition type.<br><br><br>* expression: Expression<br><br>* and: AND operator<br><br>* or: OR operator |
|hit_rule_type |String |threshold |Rule type.<br><br><br>* threshold: Threshold<br><br>* compare: Year\-over\-year and period\-over\-period comparison |
|threshold_calculate_type |String |\- |Threshold calculation method. It can be addition, subtraction, or percentage. |
|threshold_value |Double |10,000 |Alert threshold. |
|op |String |gt |The comparator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to |
|indicator |Object of [Indicator](https://docs.byteplus.com/en/docs/299/67879#indicator) |\- |Threshold\-type parameter configuration. |
|indicators |Array of [Indicator](https://docs.byteplus.com/en/docs/299/67879#indicator) |\- |Year\-over\-year and period\-over\-period parameter configuration. |
|sub_hit_rules |Array of [AlarmHitRule](https://docs.byteplus.com/en/docs/299/67879#alarmhitrule) |\- |Sub\-rule. |


<span id="candidate"></span>
### Candidate


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|is_group |Boolean |true |Whether it is a receiver group. |
|user_name |String |test |A single username. |
|email |String |test@test.com |User email. |
|group_name |String |test |Receiver group name for the group. |
|group_id |Integer |1 |Receiver group ID. |


<span id="indicator"></span>
### Indicator


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |crash_count |Metric definition name, obtained via the `GetAppAlarmMetricsConf` API. |
|value |Double |10 |The metric value. |
|recently |Long |180 |Metric query time range, for example, 180min. |
|compare_time |Long |0 |Comparison time.<br><br><br>* 5: Previous five minutes<br><br>* 0: Current |
|start_time |Long |\- |Statistics start time. |
|end_time |Long |\- |Statistics end time. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "err_detail": "",
    "data": {
        "data": [
            {
                "id": 12345,
                "rule_id": 717,
                "rule_name": "test Alarm 0401",
                "occur_time": "2023-02-13 11:56:48",
                "notify_content": "Group 1: Operating System Name: Android\nNumber of crashes within the last 180 minutes >= 1, current value: 5\nTask interval: 5 minutes\nFiltering conditions:\n",
                "alarm_level": "fatal",
                "notify_types": [
                    "lark"
                ],
                "handle_status": 0,
                "ack_status": 0,
                "ack_time": "2022-04-27 23:57:13",
                "operators": [
                    "1"
                ],
                "operators_info": [
                    {
                        "id": 1,
                        "username": "admin-1",
                        "display_name": "admin-1",
                        "email": "",
                        "head_url": "",
                        "sso_user_id": "",
                        "auth_level": "admin",
                        "title": ""
                    }
                ],
                "filter_info": {
                    "type": "and",
                    "dimension": "",
                    "op": "",
                    "sub_conditions": [
                        {
                            "type": "expression",
                            "dimension": "aid",
                            "op": "in",
                            "values": [
                                "123456"
                            ]
                        }
                    ]
                },
                "rule_brief": "Task interval: 5 minutes\nFiltering conditions:\nAlarm group: Operating System Name\nThreshold for the number of crashes within the last 180 minutes >= 1",
                "monitor_type":"crash",
                "hit_rule": {
                    "type": "and",
                    "hit_rule_type": "",
                    "threshold_calculate_type": "",
                    "threshold_value": 0,
                    "op": "",
                    "sub_hit_rules": [
                        {
                            "type": "expression",
                            "hit_rule_type": "threshold",
                            "indicator": {
                                "name": "crash_count",
                                "recently": 180,
                                "compare_time": 0
                            },
                            "threshold_calculate_type": "",
                            "threshold_value": 1,
                            "op": "gte",
                            "hit_metric": []
                        }
                    ],
                    "hit_metric": []
                }
            }
        ],
        "total_cnt": 312,
        "total_page": 312,
        "curr_page": 1
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
