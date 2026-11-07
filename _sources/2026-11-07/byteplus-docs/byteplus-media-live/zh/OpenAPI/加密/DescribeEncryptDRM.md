---
title: "DescribeEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencryptdrm-zh-CN"
---

调用 `DescribeEncryptDRM` API 查看已配置的DRM证书管理平台访问密钥及FairPlay证书信息。

## 要求

频率限制：每个账号每秒1次查询。

## HTTP请求

* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeEncryptDRM&Version=2023\-01\-01

## 请求参数

### 通用参数

所有API调用时，除API专属参数外，还需包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeEncryptDRM` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |

## 返回调用结果参数

有关唯一API专属返回调用结果参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DRMItem |[DRMItem](https://docs.byteplus.com/en/docs/24/124020#drmitem)对象 |`-` |DRM加密配置列表。 |

### DRMItem

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|APIKey |String |`desnjkfjsedlfndskfnsklnda` |DRM证书管理平台API访问密钥。 |
|CertificateName |String |`test` |自定义FairPlay证书名称。 |
|PrivateKeyFileName |String |`private.cer` |申请FairPlay证书时创建的私钥文件名。 |
|CertificateFileName |String |`fairplay.pem` |FairPlay证书文件名称。 |
|ApplicationSecretKey |String |`dandkandkadacdsknkmkmmknk` |申请FairPlay证书过程中，Apple会返回ASk（Application Secret Key）字符串。 |
|PrivateKey |String |`hufh29893rh2f384hfv82` |申请FairPlay证书时创建的私钥文件密钥。 |

## 示例

### 请求示例

### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104*****100232280022D30",
        "Action": "DescribeEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DRMItem": {
            "APIKey": "desnjkfjs*****dskfnsklnda",
            "CertificateName": "test",
            "PrivateKeyFileName": "private.cer",
            "CertificateFileName": "fairplay.pem",
            "ApplicationSecretKey": "dandkan*****sknkmkmmknk",
            "PrivateKey": "hufh298*****84hfv82"
        }
    }
}
```

## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/124020#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所请求资源（资源包括域名空间、域名、应用名称、配置、证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝。当前账号下无所请求资源（域名空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.BillingStatus |该AccountID计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|403 |AccessDenied |用户无权对资源：%s 执行操作：%s |请求被拒绝。当前账号下无所请求资源（域名空间、域名、应用、配置模版、证书）或接口权限。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置、证书）。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
