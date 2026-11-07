---
title: "GetAppAlarmRuleList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmRuleList"
---

Get app alert task list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppAlarmRuleList&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppAlarmRuleList |The API name. The current API name is `GetAppAlarmRuleList`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|Aid |Long |No |123456 |The app ID. |
|RuleId |Long |No |1 |Alert task ID. |
|MonitorType |String |No |["crash"] |The exception type. Values:<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* flutter_crash: Flutter monitoring<br><br>* app_page_js_err: Page monitoring / JS error<br><br>* app_page_ajax_err: Page monitoring / Request error<br><br>* app_page_perf: Page monitoring / Performance<br><br>* app_event: Event alert<br><br>* net_err: Network error<br><br>* custom_exception: Custom error |
|MonitorTypes |Array of String |No |["crash","lag"] |Exception type list. Values:<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* flutter_crash: Flutter monitoring<br><br>* app_page_js_err: Page monitoring / JS error<br><br>* app_page_ajax_err: Page monitoring / Request error<br><br>* app_page_perf: Page monitoring / Performance<br><br>* app_event: Event alert<br><br>* net_err: Network error<br><br>* custom_exception: Custom error |
|Status |Array of Integer |Yes |[1,2] |Task status list. Values:<br><br><br>* 1: Enable<br><br>* 2: Disable |
|QueryKey |String |Yes |test |Search keyword. You can search by configuration or receiver group keyword. |
|PageSize |Long |Yes |2 |Number of items per page. Defaults to 10 if not specified. |
|PageNo |Long |Yes |1 |Start page number, which starts from 1. |
|Self |Integer |Yes |0 |Whether to only view rules created by yourself. Values:<br><br><br>* 1: Only view your own<br><br>* 0: View all |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppAlarmRuleList&Version=2025-12-01
{
    "Aid": 123456,
    "RuleId": 1,
    "MonitorType": "crash",
    "MonitorTypes": [
        "crash",
        "lag"
    ],
    "Status": [
        1,
        2
    ],
    "QueryKey": "test",
    "PageSize": 2,
    "PageNo": 1,
    "Self": 0
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [AlarmRule](https://docs.byteplus.com/en/docs/299/67880#alarmrule) |\- |Alert task list. |
|CurrPage |Long |1 |Current page number. |
|TotalCnt |Long |1 |The total number of items. |
|TotalPage |Long |1 |Total page count. |


<span id="alarmrule"></span>
### AlarmRule


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |1 |Alert rule ID. It can be omitted when creating a new rule. |
|Os |String |iOS |The operating system. |
|Name |String |task_test |Rule name. |
|Brief |String |\- |Rule overview information. |
|Count |Long |1 |Alert count. |
|Filter |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67880#filtercondition) |\- |Alert metric filter criteria. |
|Status |Integer |0 |Alert status. Values:<br><br><br>* 1: Enable<br><br>* 2: Disable<br><br>* 0: Delete |
|AckTime |String |2006\-01\-02 15:04:05 |Ack time. |
|HitRule |Object of [AlarmHitRule](https://docs.byteplus.com/en/docs/299/67880#alarmhitrule) |\- |Alert trigger condition. |
|OwnerId |Long |123456 |Rule owner ID. |
|GroupBys |Array of [GroupBy](https://docs.byteplus.com/en/docs/299/67880#groupby) |\- |Alert grouping condition. |
|UpdateAt |String |2006\-01\-02 15:04:05 |The time when the event was updated, in the format "yyyy\-MM\-dd HH:mm:ss". |
|AckStatus |Integer |0 |ACK status. Values:<br><br><br>* 0: Not ACKed<br><br>* 1：ACK |
|OwnerInfo |Object of [UserProfile](https://docs.byteplus.com/en/docs/299/67880#userprofile) |\- |Rule owner information. |
|AlarmLevel |String |warning |Alert level, with enumerated values: "warning" and "fatal" |
|CheckCycle |Long |5 |Monitoring period. 0 for instant alerts, in minutes. |
|NoticeConf |Object of [AlarmNoticeConf](https://docs.byteplus.com/en/docs/299/67880#alarmnoticeconf) |\- |Notification configuration information. |
|Activations |Array of [Activation](https://docs.byteplus.com/en/docs/299/67880#activation) |\- |Multiple effective time periods. |
|CallbackUrl |String |https://www.baidu.com |Callback URL. |
|Description |String |alarm for xxx |Rule description. |
|MonitorType |String |crash |The exception type. Values:<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* flutter_crash: Flutter monitoring<br><br>* app_page_js_err: Page monitoring / JS error<br><br>* app_page_ajax_err: Page monitoring / Request error<br><br>* app_page_perf: Page monitoring / Performance<br><br>* app_event: Event alert<br><br>* net_err: Network error<br><br>* custom_exception: Custom error |
|ActivationEnd |String |23:00 |Start of all\-day effective time, 24\-hour format, accurate to the minute. For example, 9 AM is "09:00". |
|ActivationStart |String |08:00 |End of all\-day effective time, 24\-hour format, accurate to the minute. For example, 9:00 PM is "21:00". |
|RecentlyOccurTime |String |\- |The latest occurrence time. Empty string if not occurred. |


<span id="filtercondition"></span>
### FilterCondition


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Op |String |in |The operator. Values:<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|Type |String |and |Condition type. Sample value:<br><br><br>* expression: The current condition is a single expression.<br><br>* and: The current condition is a compound expression, and the sub\-conditions in SubConditions are in a logical AND relationship.<br><br>* or: The current condition is a compound expression, and the sub\-conditions in SubConditions are in a logical OR relationship. |
|Value |String |123456 |Single operand. |
|Values |Array of String |[123456] |Operand list. |
|Dimension |String |aid |Condition dimension name. |
|SubCondition |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67880#filtercondition) |\- |The sub\-condition. |
|SubConditions |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67880#filtercondition) |\- |Sub\-condition list. |


<span id="alarmhitrule"></span>
### AlarmHitRule


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Op |String |gt |The comparator. Values:<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to |
|Type |String |and |The type of the filter condition. Sample value:<br><br><br>* expression: The current condition is a single expression.<br><br>* and: The current condition is a compound expression, and the sub\-conditions in SubConditions are in a logical AND relationship.<br><br>* or: The current condition is a compound expression, and the sub\-conditions in SubConditions are in a logical OR relationship. |
|Indicator |Object of [Indicator](https://docs.byteplus.com/en/docs/299/67880#indicator) |\- |Threshold\-type metric configuration. |
|Indicators |Array of [Indicator](https://docs.byteplus.com/en/docs/299/67880#indicator) |\- |Year\-over\-year and period\-over\-period metric configuration. |
|SubHitRule |Object of [AlarmHitRule](https://docs.byteplus.com/en/docs/299/67880#alarmhitrule) |\- |Sub\-rule. |
|HitRuleType |String |threshold |Matched rule type. Values:<br><br><br>* threshold: Threshold<br><br>* compare: Year\-over\-year and period\-over\-period comparison |
|SubHitRules |Array of [AlarmHitRule](https://docs.byteplus.com/en/docs/299/67880#alarmhitrule) |\- |Sub\-rule list. |
|ThresholdValue |Double |10,000 |Alert threshold. |
|ThresholdCalculateType |String |\- |Threshold calculation method, supporting addition/subtraction or percentage. |


<span id="groupby"></span>
### GroupBy


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Dimension |String |path |Group name. |


<span id="userprofile"></span>
### UserProfile


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |1 |The user ID. |
|Email |String |test@test.com |User email |
|Username |String |test_name |User name. |
|SsoUserId |String |123456 |SSO user ID. |


<span id="alarmnoticeconf"></span>
### AlarmNoticeConf


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |Array of String |mail |Notification type.<br><br><br>* lark: Feishu<br><br>* mail: Email<br><br>* dingding: DingTalk<br><br>* wechat: WeCom |
|LarkAtConf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67880#atconf) |\- |Feishu @ configuration |
|LarkWebHooks |Array of String |\- |Feishu Webhook address list |
|WechatAtConf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67880#atconf) |\- |WeCom @ configuration. |
|AlarmReceives |Array of [Candidate](https://docs.byteplus.com/en/docs/299/67880#candidate) |\- |Alert recipient/receiver group. |
|TitleTemplate |String |\- |Alert title template, which may contain special characters. |
|DingdingAtConf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67880#atconf) |\- |DingTalk @ configuration. |
|WechatWebHooks |Array of String |\- |WeCom webhook address list. |
|ContentTemplate |String |\- |Alert content template, which may contain special characters. |
|DingdingWebHooks |Array of String |\- |DingTalk webhook address list. |


<span id="activation"></span>
### Activation


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ActivationEnd |String |23:00 |End of effective time, 24\-hour format, accurate to the minute. For example, 9:00 PM is "21:00". |
|ActivationStart |String |08:00 |Start of effective time, 24\-hour format, accurate to the minute. For example, 9 AM is "09:00". |
|ActivationEndStamp |Long |1665417900 |Effective period end timestamp. |
|ActivationStartStamp |Long |1665417600 |Effective period start timestamp. |


<span id="indicator"></span>
### Indicator


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |crash_count |Metric definition name, obtained via the `GetAppAlarmMetricsConf` API. |
|Value |Double |10 |The metric value. |
|EndTime |Long |1665417900 |Statistics end time. |
|Recently |Long |180 |Metric query time range, in minutes. |
|StartTime |Long |1665417600 |Timestamp of the statistics start time. |
|CompareTime |Long |0 |Comparison time. Values:<br><br><br>* 5: Previous five minutes<br><br>* 0: Current |


<span id="atconf"></span>
### AtConf


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|IdType |String |mobile |ID type. Values:<br><br><br>* mobile<br><br>* userid<br><br>* openid |
|IdValues |Array of String |["123"] |List of IDs to be @mentioned. |


<span id="candidate"></span>
### Candidate


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Email |String |test@test.com |User email |
|GroupId |Integer |123 |Receiver group ID. |
|IsGroup |Boolean |true |Whether it is a receiver group. Values:<br><br><br>* true: It is a receiver group.<br><br>* false: It is not a receiver group. |
|UserName |String |test |User name. |
|GroupName |String |test |Receiver group name. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAppAlarmRuleList",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": 1,
                "Os": "iOS",
                "Name": "task_test",
                "Brief": "-",
                "Count": 1,
                "Filter": {
                    "Op": "in",
                    "Type": "and",
                    "Value": "123456",
                    "Values": [
                        123456
                    ],
                    "Dimension": "aid",
                    "SubCondition": {
                        "Op": "in",
                        "Type": "and",
                        "Value": "123456",
                        "Values": [
                            123456
                        ],
                        "Dimension": "aid",
                        "SubCondition": {
                            "Op": "in",
                            "Type": "and",
                            "Value": "123456",
                            "Values": [
                                123456
                            ],
                            "Dimension": "aid",
                            "SubCondition": {
                                "description": "sub-condition",
                                "title": "sub-condition。"
                            },
                            "SubConditions": []
                        },
                        "SubConditions": []
                    },
                    "SubConditions": [
                        {
                            "Op": "in",
                            "Type": "and",
                            "Value": "123456",
                            "Values": [
                                123456
                            ],
                            "Dimension": "aid",
                            "SubCondition": {
                                "description": "sub-condition",
                                "title": "sub-condition。"
                            },
                            "SubConditions": []
                        }
                    ]
                },
                "Status": 0,
                "AckTime": "2006-01-02 15:04:05",
                "HitRule": {
                    "Op": "gt",
                    "Type": "and",
                    "Indicator": {
                        "Name": "crash_count",
                        "Value": 10,
                        "EndTime": 1665417900,
                        "Recently": 180,
                        "StartTime": 1665417600,
                        "CompareTime": 0
                    },
                    "Indicators": [
                        {
                            "Name": "crash_count",
                            "Value": 10,
                            "EndTime": 1665417900,
                            "Recently": 180,
                            "StartTime": 1665417600,
                            "CompareTime": 0
                        }
                    ],
                    "SubHitRule": {
                        "Op": "gt",
                        "Type": "and",
                        "Indicator": {
                            "Name": "crash_count",
                            "Value": 10,
                            "EndTime": 1665417900,
                            "Recently": 180,
                            "StartTime": 1665417600,
                            "CompareTime": 0
                        },
                        "Indicators": [],
                        "SubHitRule": {
                            "Op": "gt",
                            "Type": "and",
                            "Indicator": {
                                "description": "Threshold-based Metric configuration",
                                "title": "Thresh-based Metric Configuration。"
                            },
                            "Indicators": [],
                            "SubHitRule": {
                                "description": "Sub-condition",
                                "title": "Sub-condition。"
                            },
                            "HitRuleType": "threshold",
                            "SubHitRules": [],
                            "ThresholdValue": 10000,
                            "ThresholdCalculateType": "-"
                        },
                        "HitRuleType": "threshold",
                        "SubHitRules": [],
                        "ThresholdValue": 10000,
                        "ThresholdCalculateType": "-"
                    },
                    "HitRuleType": "threshold",
                    "SubHitRules": [],
                    "ThresholdValue": 10000,
                    "ThresholdCalculateType": "-"
                },
                "OwnerId": 123456,
                "GroupBys": [
                    {
                        "Dimension": "path"
                    }
                ],
                "UpdateAt": "2006-01-02 15:04:05",
                "AckStatus": 0,
                "OwnerInfo": {
                    "Id": 1,
                    "Email": "test@test.com",
                    "Username": "test_name",
                    "SsoUserId": "123456"
                },
                "AlarmLevel": "warning",
                "CheckCycle": 5,
                "NoticeConf": {
                    "Type": [
                        ""
                    ],
                    "LarkAtConf": {
                        "IdType": "mobile",
                        "IdValues": [
                            "123"
                        ]
                    },
                    "LarkWebHooks": [
                        ""
                    ],
                    "WechatAtConf": {
                        "IdType": "mobile",
                        "IdValues": [
                            "123"
                        ]
                    },
                    "AlarmReceives": [
                        {
                            "Email": "test@test.com",
                            "GroupId": 123,
                            "IsGroup": true,
                            "UserName": "test",
                            "GroupName": "test"
                        }
                    ],
                    "TitleTemplate": "-",
                    "DingdingAtConf": {
                        "IdType": "mobile",
                        "IdValues": [
                            "123"
                        ]
                    },
                    "WechatWebHooks": [
                        ""
                    ],
                    "ContentTemplate": "-",
                    "DingdingWebHooks": [
                        ""
                    ]
                },
                "Activations": [
                    {
                        "ActivationEnd": "23:00",
                        "ActivationStart": "08:00",
                        "ActivationEndStamp": 1665417900,
                        "ActivationStartStamp": 1665417600
                    }
                ],
                "CallbackUrl": "https://www.baidu.com",
                "Description": "alarm for xxx",
                "MonitorType": "crash",
                "ActivationEnd": "23:00",
                "ActivationStart": "08:00",
                "RecentlyOccurTime": "-"
            }
        ],
        "CurrPage": 1,
        "TotalCnt": 1,
        "TotalPage": 1
    },
    "-": {
        "Data": [
            {
                "Id": 1,
                "Os": "iOS",
                "Name": "task_test",
                "Brief": "-",
                "Count": 1,
                "Filter": {
                    "description": "Alert Metric Filter Configuration",
                    "title": "Alert Metric Filter Configuration。"
                },
                "Status": 0,
                "AckTime": "2006-01-02 15:04:05",
                "HitRule": {
                    "description": "Alert Trigger Conditions",
                    "title": "Alert Trigger Conditions。"
                },
                "OwnerId": 123456,
                "GroupBys": [],
                "UpdateAt": "2006-01-02 15:04:05",
                "AckStatus": 0,
                "OwnerInfo": {
                    "Id": 1,
                    "Email": "test@test.com",
                    "Username": "test_name",
                    "SsoUserId": "123456"
                },
                "AlarmLevel": "warning",
                "CheckCycle": 5,
                "NoticeConf": {
                    "Type": [
                        ""
                    ],
                    "LarkAtConf": {
                        "description": "Lark @ Configuration"
                    },
                    "LarkWebHooks": [
                        ""
                    ],
                    "WechatAtConf": {
                        "description": "WeCom @ Configuration",
                        "title": "WeCom @ Configuration。"
                    },
                    "AlarmReceives": [
                        {
                            "Email": "test@test.com",
                            "GroupId": 123,
                            "IsGroup": true,
                            "UserName": "test",
                            "GroupName": "test"
                        }
                    ],
                    "TitleTemplate": "-",
                    "DingdingAtConf": {
                        "description": "Ding Talk @ Configuration",
                        "title": "Ding Talk @ Configuration。"
                    },
                    "WechatWebHooks": [
                        ""
                    ],
                    "ContentTemplate": "-",
                    "DingdingWebHooks": [
                        ""
                    ]
                },
                "Activations": [
                    {
                        "ActivationEnd": "23:00",
                        "ActivationStart": "08:00",
                        "ActivationEndStamp": 1665417900,
                        "ActivationStartStamp": 1665417600
                    }
                ],
                "CallbackUrl": "https://www.baidu.com",
                "Description": "alarm for xxx",
                "MonitorType": "crash",
                "ActivationEnd": "23:00",
                "ActivationStart": "08:00",
                "RecentlyOccurTime": "-"
            }
        ],
        "CurrPage": 1,
        "TotalCnt": 1,
        "TotalPage": 1
    }
}
```


<span id="0diklvce"></span>
## 

<span id="ExPyEUdz"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
