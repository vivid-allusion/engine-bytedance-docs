---
title: "DescribeRegionAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeregionaccessrule-zh-CN"
---

调用 `DescribeRegionAccessRule` API 查询指定域名的地域访问限制。

## 要求

速率限制：每个账号每秒 10 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=DescribeRegionAccessRule&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeRegionAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名空间。 |
|Domain |String |是 |`push.example.com` |拉流或推流域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |

## 响应参数

API 特有响应参数请参见下表。更多详情请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|AccessRuleLists |[AccessRuleLists](https://docs.byteplus.com/en/docs/24/106951#accessrulelists) 数组 |`-` |地域访问限制。 |

### AccessRuleLists

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|Domain |String |`pull.example.com` |拉流域名。 |
|RegionAccessRule |[RegionAccessRule](https://docs.byteplus.com/en/docs/24/106951#regionaccessrule) 对象 |`-` |地域访问限制。 |

### RegionAccessRule

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Type |String |`allow` |访问规则类型。<br><br><br>* `allow`：仅允许指定地域的请求访问您的域名。<br><br>* `deny`：禁止指定地域的请求访问您的域名。 |
|Enable |String |`true` |是否启用配置。<br><br><br>* `true`：配置已启用。<br><br>* `false`：配置已禁用。 |
|CountryList |Array of String |`CN` |允许名单或封禁名单中的国家和地区。使用 ISO 3166\-1 代码表示国家和地区，例如 CN、SG 或 US。 |
|ProvinceList |Array of String |`HK` |允许名单或封禁名单中的省份，目前仅支持中国香港、中国澳门和中国台湾地区。对应代码分别为 HK、MO 和 TW。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeRegionAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeRegionAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AccessRuleLists": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "RegionAccessRule": {
                    "Type": "deny",
                    "Enable": true,
                    "RegionList": [
                        "CN",
                        "region2"
                    ]
                }
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
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106951#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.DomainAndApp |domain and app exist can not exist at the same time |不能同时传入 Domain 和 App。请修改输入参数。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通，或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
