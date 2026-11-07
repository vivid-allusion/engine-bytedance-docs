---
title: "GetWebProNewErrorAlertHistory"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetWebProNewErrorAlertHistory"
---

Get historical trigger records for new error alerts.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetWebProNewErrorAlertHistory&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetWebProNewErrorAlertHistory |The API name. The current API name is `GetWebProNewErrorAlertHistory`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|id |Long |No |1 |Alert ID. |
|page_size |Integer |No |10 |The number of items per page for a pagination query. The default value is 10. |
|page_num |Integer |No |1 |The page number for a pagination query. Default value: 1. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67997#timefilter) |No |\- |Time range. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67997#commonparams) |Yes |\- |Common parameters. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity. Unit: s. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetWebProNewErrorAlertHistory&Version=2022-10-12
{
  "common": {
    "aid": 1,
    "os": "webpro"
  },
  "time_filter": {
    "start_time": 1719936000,
    "end_time": 1720072587
  },
  "id": 1,
  "page_size": 10,
  "page_num": 1
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [AlertHistoryList](https://docs.byteplus.com/en/docs/299/67997#alerthistorylist) |\- |Returned data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### AlertHistoryList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|count |Integer |10 |Number of alert trigger history records. |
|Alert_histories |Array of [AlertHistory](https://docs.byteplus.com/en/docs/299/67997#alerthistory) |\- |Alert history details. |

### AlertHistory

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|creator |String |leeac |Alert creator. |
|alert_time |Integer |1720605827 |Alert occurrence time. |
|alert_param |Object of [AlertParam](https://docs.byteplus.com/en/docs/299/67997#alertparam) |\- |Alert parameters. |
|detail_link |String |\- |Link to the alert details page. |
|alarm_content |String |\- |Alert content. |

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
|lark_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67997#atconf) |Jack |Users to be @mentioned in Feishu. |
|callback_urls |Array of String |[] |Alert callback webhook. |
|lark_webhooks |Array of String |[] |Feishu webhook. |
|alert_language |String |zh |Alert language.<br><br><br>* en: Overseas<br><br>* zh: Domestic |
|alert_strategy |Object of [AlertStrategy](https://docs.byteplus.com/en/docs/299/67997#alertstrategy) |all |Alert policy. Multiple policies can only be combined using the OR operator.<br><br><br>* latest: Latest version<br><br>* specify: Specified version<br><br>* all: All versions |
|wechat_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67997#atconf) |Rose |Users to be @mentioned in WeCom. |
|dingding_at_conf |Object of [AtConf](https://docs.byteplus.com/en/docs/299/67997#atconf) |Carl |Users to be @mentioned in DingTalk. |
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
|releases |Array of String |2.0.0 |If you monitor new errors in versions, pass the list of versions to monitor. |
|disappear_time |Integer |30 |An error will be treated as a new error if it does not recur within this number of days. |
|user_threshold |Integer |100 |User count threshold. |
|filter_condition |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/67997#filterconditions) |\- |The filter condition. |
|sample_threshold |Integer |100 |Sample count threshold. |
|isReleaseNewError |Boolean |true |Whether to focus on new errors in versions.<br><br><br>* true: Yes<br><br>* false: No |

### FilterConditions

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |and |Filter criterion key. |
|sub_conditions |Array of [SubCondition](https://docs.byteplus.com/en/docs/299/67997#subcondition) |[] |Filter criterion values. |

### SubCondition

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |String |in |Condition operator.<br><br><br>* in: contains<br><br>* not_in: does not contain<br><br>* Regex: Regex match<br><br>* not_regex: Regex mismatch |
|value |String |\- |The filter value. It indicates an exact match. |
|values |Array of String |\- |Filter values, indicating a range. |
|groupKey |String |\- |Alert grouping dimension. |
|dimension |String |\- |Alert attribution dimension. |

## Sample response

```JSON
{
  "err_detail": "",
  "data": {
    "Alert_histories": [],
    "count": 0
  },
  "error_msg": "",
  "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
