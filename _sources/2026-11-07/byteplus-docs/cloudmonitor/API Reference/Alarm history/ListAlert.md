---
title: "ListAlert"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListAlert"
---

Obtain the details of alert records.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for your service region.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListAlert&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListAlert&serviceCode=cloudmonitor&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListAlert |The name of the API. The API name is `ListAlert`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|AlertGroupId |String |Yes |ag_20\*\*\*\*\*\*\*\*\*\*\*23\*\*\*\* |Alert group ID. You can obtain it by using the `ListAlertGroup` API. |
|EndTime |Integer |No |1749376800 |The end time of the query. You need to set the value to a UNIX timestamp in seconds. If you do not specify this parameter, the current time is used by default. |
|PageNumber |Integer |No |1 |The page number. Default value: 1. |
|PageSize |Integer |No |10 |The number of entries returned per page. Default value: 10. |
|StartTime |Integer |No |1749355200 |The start time of the query. You need to set the value to a UNIX timestamp in seconds. If you do not specify this parameter, data from the last 6 hours is obtained by default. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListAlert&Version=2018-01-01
Content-Type: application/json
{
    "AlertGroupId": "ag_20***********23****",
    "EndTime": 1749376800,
    "PageNumber": 1,
    "PageSize": 10,
    "StartTime": 1749355200
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [AlertVO](https://docs.byteplus.com/en/docs/39/110487#alertvo) |\- |The historical alert data. |
|PageSize |Integer |30 |The number of rows per page for a pagination query. Default value: 30. |
|PageNumber |Integer |1 |The page number for a pagination query. Default value: 1. |
|TotalCount |Integer |2 |The number of alert policies that meet the criteria. |


<span id="alertvo"></span>
### AlertVO


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |alert_20\*\*\*\*\*\*\*\*\*\*\*23\*\*\*\* |The alert ID for the current cycle. |
|Type |String |alert |The alert type. Valid values:<br><br><br>* alert: alert<br><br>* recovery<br><br>* nodata: No\-data alert |
|EndAt |String |2026\-06\-08T12:05:00 |The end time of the alert for the current cycle. |
|Level |String |warning |The alert level. Valid values:<br><br><br>* critical<br><br>* warning<br><br>* notice<br><br>* recovery |
|CreateAt |String |2026\-06\-08T12:00:00 |The start time of the alert for the current cycle. |
|EvaluationCount |Integer |3 |The number of consecutive times the alert condition must be triggered. It is used to trigger N alerts within M cycles. `EvaluationInterval` indicates M, and `EvaluationCount` indicates N. |
|SendAlertResult |Object of [SendAlertResult](https://docs.byteplus.com/en/docs/39/110487#sendalertresult) |\- |The alert sending results. |
|MetricConditions |Array of [MetricCondition](https://docs.byteplus.com/en/docs/39/110487#metriccondition) |\- |The alert metric conditions. |
|EvaluationInterval |Integer |5 |The check cycle is used to trigger N alerts within M cycles. `EvaluationInterval` indicates M, and `EvaluationCount` indicates N. |


<span id="sendalertresult"></span>
### SendAlertResult


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |sent |The alert sending status. Valid values:<br><br><br>* sent: The alert was sent.<br><br>* recovery_disabled: Alert recovery was disabled.<br><br>* silenced: The alert was suppressed.<br><br>* no_receiver: No receiver was configured.<br><br>* rule_send_interval: The alert was not sent because the cooldown period has not elapsed. |
|IsSendAlert |Boolean |true |Whether the alert was sent.<br><br><br>* true: The alert was sent.<br><br>* false: The alert was not sent. |
|SilencePolicyId |String |sp_20\*\*\*\*\*\*\*\*\*\*\*23\*\*\*\* |The ID of the alert suppression policy. If this ID exists, it indicates that the alert is suppressed. |
|SendAlertNotifications |Array of [SendAlertNotification](https://docs.byteplus.com/en/docs/39/110487#sendalertnotification) |\- |The information about alert notifications. |


<span id="metriccondition"></span>
### MetricCondition


|**Parameters** |**Types** |**Sample value** |**Description** |
|---|---|---|---|
|Metric |String |AVG(Instance/CPU utilization)[1m] |The semantic description of the metric. |
|Condition |String |alert |The metric status. Valid values:<br><br><br>* alert: alert<br><br>* nodata: No\-data alert<br><br>* normal: Normal |
|CurrentValue |String |86.4 |The current value of the metric. |
|TriggerCondition |String |The average value of instance/CPU utilization in the last cycle is \>= 90%, and the condition is met per cycle (1 cycle = 1 minute) |The semantic description of the metric trigger condition. |


<span id="sendalertnotification"></span>
### SendAlertNotification


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |alert |The alert type. Valid values:<br><br><br>* alert: alert<br><br>* nodata: No\-data alert<br><br>* alert_recovery: Alert recovery<br><br>* nodata_recovery: No\-data recovery |
|Level |String |warning |The alert level. Valid values:<br><br><br>* critical<br><br>* warning<br><br>* notice<br><br>* recovery |
|ErrMsg |String |{"body":"ok","code":200} |The description of the alert sending status. |
|SendAt |String |2026\-06\-08T12:01:00 |The time when the alert was sent. |
|Status |String |sent |The alert sending status. Valid values:<br><br><br>* sent: The alert was sent.<br><br>* recovery_disabled: Alert recovery was disabled.<br><br>* silenced: The alert was suppressed.<br><br>* no_receiver: No receiver was configured.<br><br>* rule_send_interval: The alert was not sent because the cooldown period has not elapsed. |
|SendAlertOOSs |Array of [SendAlertOOS](https://docs.byteplus.com/en/docs/39/110487#sendalertoos) |\- |The information about alert sending orchestration. |
|SilencePolicyId |String |sp_20\*\*\*\*\*\*\*\*\*\*\*23\*\*\*\* |The ID of the alert suppression policy. If this ID exists, it indicates that the alert is suppressed. |
|SendAlertContacts |Array of [SendAlertContact](https://docs.byteplus.com/en/docs/39/110487#sendalertcontact) |\- |The information about alert contacts. |
|SendAlertWebhooks |Array of [SendAlertWebhook](https://docs.byteplus.com/en/docs/39/110487#sendalertwebhook) |\- |The information about webhooks used for sending alerts. |


<span id="sendalertoos"></span>
### SendAlertOOS


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ErrMsg |String |{"body":"ok","code":200} |The description of the alert sending status. |
|Region |String |cn\-north\-1 |The region. |
|Status |String |sent |The alert sending status. Valid values:<br><br><br>* waiting: The alert is to be sent.<br><br>* sent: The alert was sent. |
|Success |Boolean |true |Whether the alert was sent. |
|OrchestrationPlanId |String |oop\-20\*\*\*\*\*\*\*\*\*\*\*23\*\*\*\* |The orchestration plan ID. |


<span id="sendalertcontact"></span>
### SendAlertContact


|**Parameters** |**Types** |**Sample value** |**Description** |
|---|---|---|---|
|ContactName |String |user_20\*\*\*\*\*\*\*\*\*\*\*23\*\*\*\* |The name of the alert contact. |
|DutyScheduleId |String |ds_20\*\*\*\*\*\*\*\*\*\*\*23\*\*\*\* |The on\-duty schedule ID. |
|ContactSendResults |Array of [SendAlertContactResult](https://docs.byteplus.com/en/docs/39/110487#sendalertcontactresult) |\- |The information about alert contacts. |


<span id="sendalertwebhook"></span>
### SendAlertWebhook


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Url |String |https://example.org/webhook |Webhook address. |
|Name |String |default_webhook |Webhook name. |
|Type |String |custom |Webhook type. |
|ErrMsg |String |{"body":"ok","code":200} |The description of the alert sending status. |
|Status |String |sent |The alert sending status. Valid values:<br><br><br>* waiting: The alert is to be sent.<br><br>* sent: The alert was sent. |
|Success |Boolean |true |Whether the alert was sent. |


<span id="sendalertcontactresult"></span>
### SendAlertContactResult


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ErrMsg |String |{"body":"ok","code":200} |The description of the alert sending status. |
|Status |String |sent |The alert sending status. Valid values:<br><br><br>* waiting: The alert is to be sent.<br><br>* sent: The alert was sent. |
|Success |Boolean |true |Whether the alert was sent. |
|AlertMethod |String |Email |The channel through which the alert is sent to the contact. Valid values: Phone, Email, and SMS. |
|AlertMethodVal |String |u\*\*\*@example.com |The contact information, such as email addresses and mobile numbers. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "Data": [
            {
                "Id": "alert_20***********23****",
                "Type": "alert",
                "EndAt": "2026-06-08T12:05:00",
                "Level": "warning",
                "CreateAt": "2026-06-08T12:00:00",
                "EvaluationCount": 3,
                "SendAlertResult": {
                    "Status": "sent",
                    "IsSendAlert": true,
                    "SilencePolicyId": "sp_20***********23****",
                    "SendAlertNotifications": [
                        {
                            "Type": "alert",
                            "Level": "warning",
                            "ErrMsg": "{"body":"ok","code":200}",
                            "SendAt": "2026-06-08T12:01:00",
                            "Status": "sent",
                            "SendAlertOOSs": [
                                {
                                    "ErrMsg": "{"body":"ok","code":200}",
                                    "Region": "cn-north-1",
                                    "Status": "sent",
                                    "Success": true,
                                    "OrchestrationPlanId": "oop-20***********23****"
                                }
                            ],
                            "SilencePolicyId": "sp_20***********23****",
                            "SendAlertContacts": [
                                {
                                    "ContactName": "user_20***********23****",
                                    "DutyScheduleId": "ds_20***********23****",
                                    "ContactSendResults": [
                                        {
                                            "ErrMsg": "{"body":"ok","code":200}",
                                            "Status": "sent",
                                            "Success": true,
                                            "AlertMethod": "Email",
                                            "AlertMethodVal": "u***@example.com"
                                        }
                                    ]
                                }
                            ],
                            "SendAlertWebhooks": [
                                {
                                    "Url": "https://example.org/webhook",
                                    "Name": "default_webhook",
                                    "Type": "custom",
                                    "ErrMsg": "{"body":"ok","code":200}",
                                    "Status": "sent",
                                    "Success": true
                                }
                            ]
                        }
                    ]
                },
                "MetricConditions": [
                    {
                        "Metric": "AVG(Instance/CPU Utilization)[1m]",
                        "Condition": "alert",
                        "CurrentValue": "86.4",
                        "TriggerCondition": "Instance/CPU Utilization Average value calculated over the latest single cycle >= 90%，and the threshold conditions is met once within one cycle（1 cycle=1 minute）"
                    }
                ],
                "EvaluationInterval": 5
            }
        ],
        "PageSize": 30,
        "PageNumber": 1,
        "TotalCount": 2
    },
    "ResponseMetadata": {
        "Env": "",
        "Action": "ListAlert",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
