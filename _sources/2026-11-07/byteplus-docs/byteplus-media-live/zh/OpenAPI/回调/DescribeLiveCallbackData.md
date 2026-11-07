---
title: "DescribeLiveCallbackData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata-zh-CN"
---

该 API 用于查询与直播相关的回调记录，包括事件类型、状态、请求和响应数据。可帮助您排查回调异常，并验证回调是否成功送达。

## 要求

频率限制：每个账号每秒 30 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=DescribeLiveCallbackData&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveCallbackData` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|DomainList |String 数组 |否 |`["example.com", "example2.com"]` |要查询的域名列表。默认表示当前账号下的所有域名。 |
|App |String |否 |`example_app` |应用名称。必须与流 URL 中使用的应用名称一致。 |
|Stream |String |否 |`example_stream` |流名称，用于准确定位指定直播流。 |
|CallbackEventType |String 数组 |否 |`["push_start"]` |支持的回调事件类型：<br><br><br>* `push_start`：推流开始<br><br>* `push_end`：推流结束<br><br>* `snapshot_event`：截图回调<br><br>* `record_event`：录制回调 |
|CallbackStatus |String 数组 |否 |`["success"]` |回调状态。支持以下取值：<br><br><br>* `success`：成功。<br><br>* `fail`：失败。 |
|StartTime |String |是 |`2021-08-16T00:01:59Z` |查询的开始时间，UTC 时间，RFC3339 格式，精确到秒。<br><br>> **说明**<br><br><br>> 单次查询的最大时间跨度为 31 天，历史查询的最大时间范围为 366 天。<br> |
|EndTime |String |是 |`2021-08-16T00:01:59Z` |查询的结束时间，UTC 时间，RFC3339 格式，精确到秒。 |
|PageNum |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|PageSize |Integer |否 |`100` |每页查询结果数量。取值范围：[1,1000]。默认值：`100`。<br><br>> **说明**<br><br><br>> 如果将该参数设置为 `0`，则使用默认值。<br> |

## 响应参数

有关 API 特定的唯一响应参数，请参见下表。更多详情，请参阅[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|DomainList |String 数组 |`["example.com", "example2.com"]` |域名列表。 |
|App |String |`example_app` |应用名称。 |
|Stream |String |`example_stream` |流名称。 |
|CallbackEventType |String 数组 |`["push_start"]` |回调事件类型。 |
|CallbackStatus |String 数组 |`["success"]` |回调状态值。 |
|StartTime |String |`2021-08-16T00:01:59Z` |查询的开始时间，UTC 时间，RFC3339 格式，精确到秒。 |
|EndTime |String |`2022-11-11T00:00:00Z` |查询的结束时间，UTC 时间，RFC3339 格式，精确到秒。 |
|CallbackInfoList |[CallbackInfoList](https://docs.byteplus.com/en/docs/24/107044#callbackinfolist) 数组 |`-` |回调事件详情。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107044#pagination) 对象 |`-` |查询结果的分页信息。 |

### CallbackInfoList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Domain |String |`example.com` |域名。 |
|App |String |`example_app` |应用名称。 |
|Stream |String |`example_stream` |流名称。 |
|CallbackTime |String |`2022-11-11T00:00:00Z` |回调执行时间。 |
|CallbackEventType |String |`push_start` |回调事件类型。 |
|CallbackMethod |String |`post` |回调请求方法。 |
|CallbackAddress |String |`http://example.com/xxx` |回调目标 URL。 |
|CallbackStatus |String |`success` |回调状态。 |
|CallbackBody |String |`{}` |回调请求正文。 |
|CallbackResponseCode |String |`200` |响应的 HTTP 状态码。 |
|CallbackResponseHeader |String |`Content-Type: application/json; charset=utf-8\r\nContent-Length: 29` |HTTP 响应头。 |
|CallbackResponseBody |String |`{"error_code":200,"msg":"ok"}` |回调的响应正文。 |
|CallbackResponseTime |String |`2022-11-11T00:00:00Z` |回调响应时间。 |
|CallbackErrorMessage |String |`InternalServiceError` |错误信息，回调失败时返回。 |
|CallbackErrorCode |String |`The callback receiving service is unreachable. Please check whether the callback address is available.` |错误描述。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageNum |Integer |`1` |当前页的页码。 |
|PageSize |Integer |`100` |每页显示的数据条数。 |
|TotalCount |Integer |`100` |查询结果中的数据总数。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveCallbackData&Version=2023-01-01
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250410201942D5628AA78C98A0C818D0",
        "Action": "DescribeLiveCallbackData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CallbackEventType": [
            "push_end"
        ],
        "StartTime": "2025-03-18T00:00:00Z",
        "EndTime": "2025-03-19T00:00:00Z",
        "CallbackInfoList": [
            {
                "Domain": "example.com",
                "App": "app_test",
                "Stream": "stream-111",
                "CallbackTime": "2025-03-18T23:30:52Z",
                "CallbackEventType": "push_end",
                "CallbackMethod": "post",
                "CallbackAddress": "http://example.com/callback/record",
                "CallbackStatus": "success",
                "CallbackBody": "{}",
                "CallbackResponseCode": "200",
                "CallbackResponseHeader": "HTTP/1.1 200 OK",
                "CallbackResponseBody": "{\"error_code\":200,\"msg\":\"ok\"}",
                "CallbackResponseTime": "2025-03-18T23:30:53Z",
                "CallbackErrorCode": "",
                "CallbackErrorMessage": ""
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 100,
            "TotalCount": 1
        }
    }
}
```

## 错误码

以下是与当前操作相关的错误码。有关其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参照请求参数描述进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查参数类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝。当前账号下没有请求的资源（域名空间、域名、应用、配置模板、证书）。 |
|404 |ResourceNotFound |\- |未找到资源（域名空间、域名、应用、配置模板、证书）。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |服务之间发生错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |服务之间发生错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
