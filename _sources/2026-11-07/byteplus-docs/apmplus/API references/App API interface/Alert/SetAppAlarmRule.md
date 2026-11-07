---
title: "SetAppAlarmRule"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SetAppAlarmRule"
---

Create or update an app alert task.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=SetAppAlarmRule&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |SetAppAlarmRule |The API name. The current API name is `SetAppAlarmRule`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|id |Long |No |1 |Alert rule ID. It can be omitted if you are creating a new rule. |
|name |String |Yes |task_test |Rule name. |
|description |String |No |alarm for xxx |Rule description. |
|monitor_type |String |Yes |crash |Monitoring type.<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* app_page_js_err: Page monitoring / JS error<br><br>* app_page_ajax_err: Page monitoring / Request error<br><br>* app_page_perf: Page monitoring / Performance<br><br>* app_event: Event alert<br><br>* net_err: Network error<br><br>* custom_exception: Custom error<br><br>* traffic_exception: Traffic<br><br>* disk_exception: Disk<br><br>* battery_trace: Battery<br><br>* cpu_exception：CPU |
|alarm_level |String |Yes |warning |Alert level.<br><br><br>* warning<br><br>* fatal |
|check_cycle |Long |Yes |5 |Monitoring period, in minutes. Enter 0 for instant alerts. |
|activations |Array of [Activation](https://docs.byteplus.com/en/docs/299/67878#activation) |No |\- |Multiple time periods. |
|filter |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67878#filtercondition) |No |\- |Alert metric filter criteria. |
|group_bys |Array of [GroupBy](https://docs.byteplus.com/en/docs/299/67878#groupby) |No |\- |Alert grouping condition. |
|hit_rule |Object of [AlarmHitRule](https://docs.byteplus.com/en/docs/299/67878#alarmhitrule) |Yes |\- |Alert trigger condition. |
|notice_conf |Object of [AlarmNoticeConf](https://docs.byteplus.com/en/docs/299/67878#alarmnoticeconf) |Yes |\- |Notification configuration information. |


<span id="activation"></span>
### Activation


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|activation_start |String |No |08:00 |Start of all\-day effective time. 24\-hour format, accurate to the minute. For example, 9:00 AM is "09:00". |
|activation_end |String |No |23:00 |End of all\-day effective time. 24\-hour format, accurate to the minute. For example, 9:00 PM is "21:00". |


<span id="filtercondition"></span>
### FilterCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |and |Condition type.<br><br><br>* expression: Expression<br><br>* and: AND operator<br><br>* or: OR operator |
|dimension |String |No |aid |The name of the condition. |
|op |String |No |in |The operator.<br><br><br>* in: contains |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|sub_conditions |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67878#filtercondition) |No |\- |The sub\-condition. |


<span id="groupby"></span>
### GroupBy


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|dimension |String |No |path |Group name. |


<span id="alarmhitrule"></span>
### AlarmHitRule


|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Condition type.<br><br><br>* expression: Expression<br><br>* and: AND operator<br><br>* or: OR operator |
|hit_rule_type |String |Yes |threshold |Rule type.<br><br><br>* threshold: Threshold<br><br>* compare: Year\-over\-year and period\-over\-period comparison |
|threshold_calculate_type |String |Yes |\- |Threshold calculation method. It can be addition, subtraction, or percentage. |
|threshold_value |Double |Yes |10,000 |Alert threshold. |
|op |String |Yes |gt |The comparator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to |
|indicator |Object of [Indicator](https://docs.byteplus.com/en/docs/299/67878#indicator) |No |\- |Threshold type parameter configuration. |
|indicators |Array of [Indicator](https://docs.byteplus.com/en/docs/299/67878#indicator) |No |\- |Year\-over\-year and period\-over\-period parameter configuration. |
|sub_hit_rules |Array of [AlarmHitRule](https://docs.byteplus.com/en/docs/299/67878#alarmhitrule) |No |\- |Sub\-rule. |


<span id="alarmnoticeconf"></span>
### AlarmNoticeConf


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |Array of String |No |mail |Notification type.<br><br><br>* lark: Feishu<br><br>* mail: Email<br><br>* dingding: DingTalk<br><br>* wechat: WeCom |
|lark_web_hooks |Array of String |No |\- |The configuration for adding the Feishu webhook link. |
|dingding_web_hooks |Array of String |No |\- |DingTalk webhook. |
|wechat_web_hooks |Array of String |No |\- |WeChat webhook. |
|alarm_receives |Array of [Candidate](https://docs.byteplus.com/en/docs/299/67878#candidate) |No |\- |Receiver group. |


<span id="indicator"></span>
### Indicator


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|name |String |Yes |crash_count |Metric definition name, obtained via the `GetAppAlarmMetricsConf` API. |
|value |Double |No |10 |The metric value. |
|recently |Long |Yes |180 |Metric query time range, for example, 180min. |
|compare_time |Long |Yes |0 |Comparison time.<br><br><br>* 5: Previous five minutes<br><br>* 0: Current |
|start_time |Long |No |\- |Statistics start time. |
|end_time |Long |No |\- |Statistics end time. |


<span id="candidate"></span>
### Candidate


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|is_group |Boolean |No |true |Whether it is a receiver group. |
|user_name |String |No |\- |Single user. |
|email |String |No |\- |Group. |
|group_name |String |No |\- |Group name. |
|group_id |Integer |No |123 |Receiver group ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=SetAppAlarmRule&Version=2022-10-12
{
    "name": "test_alarm_0401",
    "description": "",
    "alarm_level": "fatal",
    "filter": {
        "type": "and",
        "sub_conditions": [
            {
                "dimension": "aid",
                "type": "expression",
                "op": "in",
                "values": [
                    "123456"
                ]
            }
        ]
    },
    "hit_rule": {
        "type": "and",
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
                "op": "gte"
            }
        ]
    },
    "check_cycle": 5,
    "activations": [
        {
            "activation_start": "00:00",
            "activation_end": "23:59"
        }
    ],
    "group_bys": [
        {
            "dimension": "os"
        }
    ],
    "notice_conf": {
        "type": [
            "lark"
        ],
        "lark_web_hooks": [
            "https://open.feishu.cn/open-apis/bot/v2/hook/f135"
        ]
    },
    "monitor_type": [
        "crash"
    ],
    "id": 12345
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |\- |Error message. If the request was successful, this field is empty. |
|error_no |Long |0 |Error code. If the request was successful, its value is 0. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
