---
title: "CreateWebProNewErrorAlertRule"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/CreateWebProNewErrorAlertRule"
---

Create an alert rule for new errors.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=CreateWebProNewErrorAlertRule&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateWebProNewErrorAlertRule |The API name. The API name is `CreateWebProNewErrorAlertRule`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|alert_param |Object of [AlertParam](https://docs.byteplus.com/en/docs/299/67994#alertparam) |No |\- |Alert parameters. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67994#commonparams) |Yes |\- |Common parameters. |

### AlertParam

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|id |Long |No |1 |Alert task ID. |
|name |String |No |test |Alert task name. |
|chats |Array of String |No |[1234] |Alert notification groups. |
|methods |Array of String |No |lark_webhook |Alert notification methods.<br><br><br>* mail: Email<br><br>* lark_webhook: Feishu<br><br>* wechat_webhook: WeCom<br><br>* dingding_webhook: DingTalk<br><br>* webhook: Alert callback |
|is_close |Boolean |No |0 |Whether to enable alerting.<br><br><br>* 0: Enabled<br><br>* 1: Disabled |
|receivers |Array of String |No |[] |Receiver. This parameter is required when the alert notification method is "lark". |
|alert_level |String |No |warning |The alert level.<br><br><br>* warning: Warning<br><br>* fatal: Critical |
|mail_groups |Array of String |No |[123] |Email notification groups. |
|lark_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67994#atconf) |No |Jack |People to be @mentioned in Feishu. |
|callback_urls |Array of String |No |[] |Alert callback webhook. |
|lark_webhooks |Array of String |No |[] |Feishu webhook. |
|alert_language |String |No |zh |Alert language.<br><br><br>* en: Overseas<br><br>* zh: Domestic |
|alert_strategy |Object of [AlertStrategy](https://docs.byteplus.com/en/docs/299/67994#alertstrategy) |No |all |Alert policy. The relationship between multiple policies can only be OR.<br><br><br>* latest: Latest version<br><br>* specify: Specified version<br><br>* all: All versions |
|wechat_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67994#atconf) |No |Rose |People to be @mentioned in WeCom. |
|dingding_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67994#atconf) |No |Carl |People to be @mentioned in DingTalk. |
|we_chat_webhooks |Array of String |No |[] |WeCom webhook. |
|dingding_webhooks |Array of String |No |[] |DingTalk webhook. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### AtConf

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|id_type |String |No |userid |Type. |
|id_values |Array of String |No |[] |Value corresponding to the type. |

### AlertStrategy

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|evType |String |No |js_error |Enumeration type<br><br><br>* js_error: JavaScript error<br><br>* http: Request error<br><br>* resource_error: Static resource error |
|releases |Array of String |No |2.0.0 |If you monitor new errors in versions, pass the list of versions to monitor. |
|disappear_time |Integer |No |30 |The number of days after which an error that has not recurred is considered a new error. |
|user_threshold |Integer |No |100 |User count threshold. |
|filter_condition |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/67994#filterconditions) |No |\- |The filter condition. |
|sample_threshold |Integer |No |100 |Sample count threshold. |
|isReleaseNewError |Boolean |No |true |Whether to monitor new errors in a version.<br><br><br>* true: Yes<br><br>* false: No |

### FilterConditions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |and |The key of the filtering condition. |
|sub_conditions |Array of [SubCondition](https://docs.byteplus.com/en/docs/299/67994#subcondition) |No |[] |Filtering condition values. |

### SubCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Condition operator.<br><br><br>* in: contains<br><br>* not_in: does not contain<br><br>* regex: Regular expression matching<br><br>* not_regex: Regular expression mismatch |
|value |String |No |\- |The filter value. It indicates an exact match. |
|values |Array of String |No |\- |Filter values, indicating a range. |
|groupKey |String |No |\- |Alert grouping dimension. |
|dimension |String |No |\- |Alert attribution dimension. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=CreateWebProNewErrorAlertRule&Version=2022-10-12
{
  "common": {
    "aid": 1,
    "os": "webpro"
  },
  "alert_param": {
    "name": "newRule",
    "is_close": false,
    "methods": [
      "lark_webhook"
    ],
    "alert_language": "zh",
    "alert_level": "warning",
    "note": "",
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
      "user_threshold": 100,
      "sample_threshold": 100,
      "filter_condition": {
        "type": "and",
        "sub_conditions": []
      }
    }
  }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [AddAlertResponseData](https://docs.byteplus.com/en/docs/299/67994#addalertresponsedata) |\- |Response data. |
|errmsg |String |"" |Error message. An empty string `""` indicates success. |
|errno |Integer |0 |Error code. 0 indicates success. |

### AddAlertResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |123\*\*\*\*456 |New error alert task ID. |

## Sample response

```JSON
{
  "err_detail": "",
  "data": {
    "id": 1
  },
  "error_msg": "",
  "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
