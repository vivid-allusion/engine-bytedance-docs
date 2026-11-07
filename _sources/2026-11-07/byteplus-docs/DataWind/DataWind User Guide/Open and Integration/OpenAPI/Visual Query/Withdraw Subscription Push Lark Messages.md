---
title: "Withdraw Subscription Push Lark Messages"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Withdraw_Subscription_Push_Lark_Messages"
---

<span id="_1-概述"></span>
# 1. Overview

For certain special or important dashboards, to prevent subscription messages from being pushed when data has not been refreshed or there are other data anomalies, the product supports the capability to withdraw subscription messages. Currently, withdrawal is implemented by providing an API. Users can call the API with parameters when withdrawal is needed to retract the relevant Feishu messages. This capability is only available to dashboard administrators, subscription creators, and project administrators.

Caution: Before using the API described in this document, please familiarize yourself with the invocation method. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_2-订阅推送飞书消息撤回"></span>
# 2. Withdraw subscription push Feishu messages

<span id="4d38c533"></span>
## 2.1 Request description

Request URL: POST aeolus/api/v3/subscription/withdraw

<span id="333fe789"></span>
## 2.2 Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|subscription_id |int |Yes |27593 |Subscription ID |
|subscribers |array |Yes |【】 |When withdrawing push messages for specified users, specify the user list |
|after_push_time |string |Optional |07:01:01 |Set to withdraw messages sent after the specified time of the current day |


<span id="a294858e"></span>
## 2.3 Request example

```json
{
  "subscription_id":27593, // Subscription ID
  "subscribers": [], // When withdrawing push messages for specified users, specify the user list
  "after_push_time": "07:01:01" // Optional, set to withdraw messages sent after the specified time of the current day
}
```


<span id="97cbf12a"></span>
## 2.4 Response parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|code |string |Yes |aeolus/ok |Status code |
|data | |Yes | | |
|subscriptionId |int |Yes |27594 |Subscription ID |
|withdrawStatus |array |Yes |[] |Withdrawal status, example value |
|errCode | | | | |


<span id="e664a7e6"></span>
## 2.5 Response example

```json
// When execution is successful
{
    "code": "aeolus/ok",
    "data": {
        "subscriptionId": 27594,
        "withdrawStatus": [
            {
                "errCode": 0,
                "errMsg": null,
                "messageId": "{messageId}",
                "pushEndTime": "2023-10-13T03:38:38Z",
                "pushInstanceId": ******,
                "status": "success",
                "subscriber": "xiahaitao"
            },
            {
                "errCode": 0,
                "errMsg": null,
                "messageId": "{messageId}",
                "pushEndTime": "2023-10-13T03:38:39Z",
                "pushInstanceId": ******,
                "status": "success",
                "subscriber": "xiangbowen"
            }
        ]
    },
    "msg": "成功"
}
// When the request ID does not have permission
{
    "code": "aeolus/user/unauthorized",
    "detail": {
        "detail": null,
        "reasons": [
            "用户无权限"
        ],
        "suggestions": []
    },
    "extra_msg": "",
    "msg": "用户无权限",
    "queryHistoryId": 0
}
// When the request fails
{
    "code": "aeolus/subscribe/subscribeWithdrawError",
    "extra_msg": {
        "code": -1,
        "msg": "不支持该类型的订阅推送撤回"
    },
    "msg": "请求订阅服务错误：不支持该类型的订阅推送撤回",
    "queryHistoryId": 0
}
```
