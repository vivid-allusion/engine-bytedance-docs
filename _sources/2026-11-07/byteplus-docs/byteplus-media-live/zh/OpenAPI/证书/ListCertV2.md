---
title: "ListCertV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2-zh-CN"
---

调用 `ListCertV2` API 查看当前账号下的证书列表。

## 要求

速率限制：每个账号每秒 10 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=ListCertV2&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特有参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`ListCertV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Available |Boolean |否 |`true` |是否获取已启用或已禁用的证书。<br><br><br>* `true`：（默认）获取已启用的证书。<br><br>* `false`：获取已禁用的证书。 |
|Domain |String |否 |`push.example.com` |证书保护的域名。支持精确搜索。 |
|Expiring |Boolean |否 |`false` |是否获取有效或已过期的证书。<br><br><br>* `false`：（默认）获取仍然有效的证书。<br><br>* `true`：获取已过期的证书。<br><br><br>> **说明**<br><br><br>> 仅当 `Available` 已指定时，此参数才生效。<br> |
|CertName |String |否 |`domaincert` |证书名称。支持模糊搜索。 |
|PageSize |Integer |否 |`10` |每页查询结果数量。有效值：[1,1000]。<br><br>> **说明**<br><br><br>> `PageNum` 和 `PageSize` 必须同时指定。如果未指定其中任一参数，则返回所有结果。<br> |
|PageNum |Integer |否 |`1` |页码。有效值：[1,1000]。<br><br>> **说明**<br><br><br>> `PageNum` 和 `PageSize` 必须同时指定。如果未指定其中任一参数，则返回所有结果。<br> |
|ProjectName |String |否 |`MyProject` |与证书关联的项目名称。此字段为可选字段，可用于按项目名称筛选证书。 |

## 响应参数

API 特有的响应参数见下表。更多详细信息，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|CertList |[CertList](https://docs.byteplus.com/en/docs/24/106959#certlist) 数组 |`-` |证书列表。 |
|Total |Integer |`20` |当前查询结果中的证书总数。 |
|ExpirationInfo |[ExpirationInfo](https://docs.byteplus.com/en/docs/24/106959#expirationinfo) 对象 |`-` |当前查询中所有证书的过期信息。 |

### CertList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|ProjectName |String |`default` |证书所属项目。 |
|CertDomainList |String 数组 |`["push.example.com"]` |证书保护的域名列表。 |
|CertName |String |`push.example.com` |证书名称。 |
|ChainID |String |`4060e26538a149e2a87b42*******11` |证书链 ID。 |
|CertID |String |`812******1` |证书 ID。 |
|NotAfter |String |`2024-08-18T07:19:00Z` |证书的生效时间（UTC 时间，采用 RFC 3339 格式，时间戳精度为秒）。 |
|NotBefore |String |`2020-08-19T07:19:00Z` |证书的过期时间（UTC 时间，采用 RFC 3339 格式，时间戳精度为秒）。 |
|Status |String |`OK` |证书状态。有效值包括：<br><br><br>* `OK`：正常。<br><br>* `Expire`：已过期。<br><br>* `30days`：30 天后过期。<br><br>* `15days`：15 天后过期。<br><br>* `7days`：7 天后过期。<br><br>* `1days`：1 天后过期。 |
|CreateTime |String |`2020-08-19T07:19:00Z` |证书创建时的时间戳，采用 RFC3339 格式，UTC 时区，精度为秒。 |

### ExpirationInfo

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|ActiveNum |Integer |`10` |当前有效且未过期的证书数量。 |
|ExpireNum |Integer |`5` |当前查询结果中已过期的证书数量。 |
|ClosingExpireNum |Integer |`5` |一个月内即将过期的证书数量。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListCertV2&Version=2023-01-01
{
    "AccountID": "1000000001"
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestID":  "2020091618453101022706705762997",
        "Action": "ListCert",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertList": [
            {
                "CertID": "cert-94552b4a4b0a4b8fbe3d*****",
                "CertName": "*.example.com",
                "CertDomainList": ["*.example.com"],
                "ChainID": "4060e26538a149e2a87b42deba979011",
                "NotBefore": "2020-08-19T07:19:00Z",
                "NotAfter": "2024-08-18T07:19:00Z",
                "Status": "OK"
            }
            {
                "CertID": "cert-94552b4a4b0a4b8******e5152",
                "CertName": "*.test.com.cn",
                "CertDomainList": ["*.test.com.cn"],
                "ChainID": "d7134cbff1dd4425847f329cba0245e4",
                "NotBefore": "2020-08-11T05:42:54Z",
                "NotAfter": "2020-09-18T05:42:54Z",
                "Status": "Expire"
            }
        ]
    }
}
```

## 错误码

以下是与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106959#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数验证失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝。当前账号下没有请求的资源（域名空间、域名、应用、配置模板、证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |请求被拒绝。当前账号下没有请求的资源（域名空间、域名、应用、配置模板、证书）或接口权限。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://docs.byteplus.com/en/docs/24/%5B++https://console.byteplus.com/workorder/create++%5D(https://console.byteplus.com/workorder/create))。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
