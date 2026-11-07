---
title: "GetWebProNewErrorAlertRuleDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetWebProNewErrorAlertRuleDetail"
---

Get details of a new error alert rule.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetWebProNewErrorAlertRuleDetail&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetWebProNewErrorAlertRuleDetail |The API name. The current API name is `GetWebProNewErrorAlertRuleDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67989#commonparams) |Yes |\- |Common parameters. |
|id |Long |Yes |1 |Alert ID. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, **minipro**. |
|user |String |No |test_user |Username. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetWebProNewErrorAlertRuleDetail&Version=2022-10-12
{
  "id": 1,
  "common": {
    "aid": 1,
    "os": "webpro"
  }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [AlertDetail](https://docs.byteplus.com/en/docs/299/67989#alertdetail) |\- |Response data. |
|errmsg |String |"" |Error message. An empty string `""` indicates success. |
|errno |Integer |0 |Error code. 0 indicates success. |

### AlertDetail

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|created_by |String |leeac |Alert task creator. |
|updated_by |String |leeac |Last modifier of the alert task. |
|alert_param |Object of [AlertParam](https://docs.byteplus.com/en/docs/299/67989#alertparam) |\- |Alert parameters. |
|created_time |Long |1665409567 |Alert task creation time. |
|updated_time |Long |1665409567 |The latest modification time of the alert task. |
|last_month_alert_count |Integer |0 |The number of alerts triggered by the alert task in the last month. |

### AlertParam

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1 |Alert task ID. |
|name |String |test |Alert task name. |
|chats |Array of String |[1234] |Alert notification group. |
|methods |Array of String |lark_webhook |Alert notification methods.<br><br><br>* mail: Email<br><br>* lark_webhook: Feishu<br><br>* wechat_webhook: WeCom<br><br>* dingding_webhook: DingTalk<br><br>* webhook: Alert callback |
|is_close |Boolean |0 |Whether to enable alerts.<br><br><br>* 0: Enable<br><br>* 1: Disable |
|receivers |Array of String |[] |Recipients. Required when the alert notification method is "lark". |
|alert_level |String |warning |Alert level.<br><br><br>* warning: Info<br><br>* fatal: Critical |
|mail_groups |Array of String |[123] |Email notification group. |
|lark_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67989#atconf) |Jack |Users to be @mentioned in Feishu. |
|callback_urls |Array of String |[] |Alert callback webhook. |
|lark_webhooks |Array of String |[] |Feishu webhook. |
|alert_language |String |zh |Alert language.<br><br><br>* en: Overseas<br><br>* zh: Domestic |
|alert_strategy |Object of [AlertStrategy](https://docs.byteplus.com/en/docs/299/67989#alertstrategy) |all |Alert policy. Multiple policies can only be joined by the OR operator.<br><br><br>* latest: Latest version<br><br>* specify: Specified version<br><br>* all: All versions |
|wechat_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67989#atconf) |Rose |Users to be @mentioned in WeCom. |
|dingding_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67989#atconf) |Carl |People to be @mentioned in DingTalk. |
|we_chat_webhooks |Array of String |[] |WeCom webhook. |
|dingding_webhooks |Array of String |[] |DingTalk webhook. |

### AtConf

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id_type |String |userid |Type. |
|id_values |Array of String |[] |Value corresponding to the type. |

### AlertStrategy

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|evType |String |js_error |Enumeration type.<br><br><br>* js_error: JS error<br><br>* http: Request error<br><br>* resource_error: Static resource error |
|releases |Array of String |2.0.0 |If you want to monitor new errors in specific versions, specify the list of versions to monitor. |
|disappear_time |Integer |30 |An error will be treated as a new error if it does not recur within this number of days. |
|user_threshold |Integer |100 |User count threshold. |
|filter_condition |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/67989#filterconditions) |\- |The filter condition. |
|sample_threshold |Integer |100 |Sample count threshold. |
|isReleaseNewError |Boolean |true |Whether to focus on new errors in versions.<br><br><br>* true: Yes<br><br>* false: No |

### FilterConditions

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |and |Filter criterion key. |
|sub_conditions |Array of [SubCondition](https://docs.byteplus.com/en/docs/299/67989#subcondition) |[] |Filter criterion values. |

### SubCondition

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |String |in |Condition operator.<br><br><br>* in: contains<br><br>* not_in: does not contain<br><br>* Regex: Regex match<br><br>* not_regex: Regex mismatch |
|value |String |\- |The filter value. It indicates an exact match. |
|values |Array of String |\- |The filter value. It indicates a range. |
|groupKey |String |\- |Alert grouping dimension. |
|dimension |String |\- |Alert attribution dimension. |

## Sample response

```JSON
{
  "err_detail": "",
  "data": {
    "alert_param": {
      "id": 1,
      "name": "newRule",
      "is_close": false,
      "methods": [
        "lark_webhook"
      ],
      "feedback_duty_name": "",
      "note": "",
      "alert_language": "zh",
      "alert_level": "warning",
      "lark_webhooks": [
        "your webhook"
      ],
      "lark_at_conf": {
        "id_type": "userid",
        "id_values": []
      },
      "alert_strategy": {
        "evType": "js_error",
        "isReleaseNewError": true,
        "disappear_time": 30,
        "filter_condition": {
          "type": "and",
          "sub_conditions": []
        },
        "user_threshold": 200,
        "sample_threshold": 100,
        "strategy_update_time": 1720067406
      }
    },
    "created_by": "your@email.com",
    "updated_by": "your@email.com",
    "created_time": 1720067407,
    "updated_time": 1720072327,
    "last_month_alert_count": 0
  },
  "error_msg": "",
  "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
