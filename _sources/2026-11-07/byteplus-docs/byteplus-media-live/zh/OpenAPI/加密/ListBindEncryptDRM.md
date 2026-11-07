---
title: "ListBindEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listbindencryptdrm-zh-CN"
---

调用`ListBindEncryptDRM`接口，查询指定域名空间和应用名称的加密配置，或查看指定域名空间下的所有加密配置。

## HTTP请求

* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListBindEncryptDRM&Version=2023\-01\-01

## 请求参数

### 通用参数

所有API调用时，除接口专属参数外，还需携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListBindEncryptDRM` |API操作。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |

### Body参数

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)接口或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名所属的域名空间。 |
|应用 |String |否 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。如未指定，则表示查询所有域名空间下的全部配置。 |

## 返回调用结果

接口专属返回调用结果请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DRMBindingList |[DRMBindingList](https://docs.byteplus.com/en/docs/24/124024#drmbindinglist)数组 |`-` |DRM加密配置列表。 |

### DRMBindingList

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|应用 |String |`live` |AppName字段。 |
|DRMSystems |String数组 |`["FairPlay","Widevine"]` |加密类型，支持的取值及含义如下。<br><br><br>* `FairPlay`：使用FairPlay技术的商业DRM加密；<br><br>* `Widevine`：使用Widevine技术的商业DRM加密；<br><br>* `PlayReady`：使用PlayReady技术的商业DRM加密；<br><br>* `ClearKey`：HLS标准加密。<br><br><br>> **说明**<br><br><br>> DRM加密与HLS标准加密不可同时配置。<br> |
|EncryptOriginStream |Boolean |`true` |是否开启源流加密，取值及含义如下。<br><br><br>* `true`：已开启；<br><br>* `false`：未开启。 |
|EncryptTranscodeStream |Boolean |`true` |是否开启转码流加密，取值及含义如下。<br><br><br>* `true`：已开启；<br><br>* `false`：未开启。 |
|EncryptTranscodeSuffix |String数组 |`["_hd"]` |开启转码流加密时，配置需加密的转码流后缀。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListBindEncryptDRM&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```

### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "ListBindEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DRMBindingList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "AccountID": "1000000002",
                "Enable": true,
                "EncryptTranscodeSuffix": [
                    "_hd"
                ]
            }
        ]
    }
}
```

## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/124024#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的计费情况不可用，请激活服务或充值。 |视频直播服务尚未开启或账号处于欠费状态，导致账单不可用。请检查服务激活状态和账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
