---
title: "DescribeAuth"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023-zh-CN"
---

调用 `DescribeAuth` API，查询满足条件的 URL 鉴权配置。

## 使用限制

频率限制：每个账号每秒 1 次查询。

## HTTP 请求

* 方法：POST

* 接入地址：https://open.byteplusapi.com/?Action=DescribeAuth&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeAuth` |API 操作。 |
|Version |String |是 |`2023-01-01` |API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |否 |`pull.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名管理](https://console.byteplus.com/live/main/domain/list)页面，获取域名空间。<br><br>> **说明**<br><br><br>> 必须提供 `Vhost` 或 `Domain`，且不能同时提供。<br> |
|Domain |String |否 |`pull.example.com` |域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名管理](https://console.byteplus.com/live/main/domain/list)页面，获取域名。<br><br>> **说明**<br><br><br>> 必须提供 `Vhost` 或 `Domain`，且不能同时提供。<br> |
|App |String |否 |`live` |直播流 URL 中的 AppName 字段。默认值为空，表示查询所有 AppName。支持大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和句点（.），长度为 1 到 30 个字符。 |
|SceneType |String |是 |`push` |鉴权场景类型，取值及含义如下。<br><br><br>* `push`：推流鉴权。<br><br>* `pull`：拉流鉴权。 |

## 响应参数

API 特有的响应参数见下表。更多信息，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|AuthList |[AuthList](https://docs.byteplus.com/en/docs/24/106891#authlist) 数组 |`-` |查询结果列表。 |

### AuthList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Vhost |String |`pull.example.com` |域名空间。 |
|Domain |String |`pull.example.com` |域名。 |
|App |String |`live` |AppName 字段。 |
|SceneType |String |`push` |鉴权场景类型，取值及含义如下。<br><br><br>* `push`：推流鉴权。<br><br>* `pull`：拉流鉴权。 |
|AuthDetailList |[AuthDetailList](https://docs.byteplus.com/en/docs/24/106891#authdetaillist) 数组 |`-` |鉴权信息列表。 |
|ValidDuration |Integer |`604800` |有效时长，单位为秒。 |
|AuthStatus |Boolean |`false` |鉴权状态。有效取值包括：<br><br><br>* `false`：鉴权设置已禁用。<br><br>* `true`：鉴权设置已启用。 |
|TimeStampBase |Integer |`10` |时间戳的时间格式。有效取值：<br><br><br>* `2`：二进制。<br><br>* `8`：八进制。<br><br>* `10`：十进制。<br><br>* `16`：十六进制。<br><br><br>> **说明**<br><br><br>> 当 `SceneType` 的值为 `push` 时，此参数的值固定为 `10`。<br> |

### AuthDetailList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|SecretKey |String |`1asd111` |用于鉴权的密钥。 |
|EncryptionAlgorithm |String |`md5` |加密算法。 |
|AuthField |JSON Map |`{"volcSecret":"sign","volcTime":"expire"}` |推/拉流地址中鉴权信息的自定义参数名称。 |
|EncryptField |String 数组 |`["key","volcTime","Domain"]` |用于鉴权的信息。 |
|AuthType |String |`TypeB` |URL 鉴权类型。有效取值：<br><br><br>* `TypeA`：A 类型。<br><br>* `TypeB`：B 类型。<br><br>* `TypeC`：C 类型。<br><br>* `TypeCustom`：自定义类型。<br><br><br>> **说明**<br><br><br>> 关于 A、B 或 C 类型的更多信息，请参见[配置 URL 鉴权](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication)。<br> |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeAuth&Version=2023-01-01
{
    "Vhost": "pull.example.com",
    "SceneType": "push"
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "Action": "DescribeAuth",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "AuthList": [
            {
                "App": "live",
                "AuthDetailList": [
                    {
                        "SecretKey": "1asd111",
                        "EncryptionAlgorithm": "md5",
                        "AuthField": {},
                        "EncryptField": [],
                        "AuthType": "TypeB"
                    }
                ],
                "AuthStatus": false,
                "Domain": "pull.example.com",
                "SceneType": "push",
                "ValidDuration": 604800,
                "Vhost": "pull.example.com",
                "TimeStampBase": 10
            }
        ]
    }
}
```

## 错误码

以下为当前操作相关的错误码。其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106891#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |vhost not found |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
