---
title: "ListTimeShiftPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023-zh-CN"
---

调用 `ListTimeShiftPresetV2` API，查询指定域名空间下所有应用的时移配置。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多查询 1 次。

* 生效接口行为：新增、更新、删除时移配置后，需在操作完成后（3\-5 分钟）重新推流和拉流，才能使用变更后的配置。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListTimeShiftPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除接口专属参数外，还需携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListTimeShiftPresetV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空间。如未指定，则表示查询所有域名空间下的全部配置。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名所属的域名空间。 |
|Type |String |是 |`tos` |存储类型。请始终设置为 `tos`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

接口专属返回调用结果参数详见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|List |[List](https://docs.byteplus.com/en/docs/24/106965#list) 数组 |`-` |时移模版列表。 |


<span id="list"></span>
### 列表


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|App |String |`live` |应用名称字段。 |
|MaxShiftTime |Integer |`25920` |时移时长，即将直播流的可用时间延后指定秒数。单位：秒。 |
|Domain |String |`pull.example.com` |拉流域名。 |
|Name |String |`livedemo` |时移配置名称。 |
|Bucket |String |`5cd18a3563**********cbe0aaf694` |BytePlus TOS 的 bucket。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListTimeShiftPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListTimeShiftPresetV2",
    "Version": "2023-01-01",
    "Service": "live",
    "Region": "ap-singapore-1",
  }
  "Result": {
      "List": [
        {
          "Vhost": "push.example.com",
          "App": "live",
          "Bucket": "5cd18********f694",
          "Domain": "pull.example.com",
          "MaxShiftTime": 259200,
          "Name": "livedemo",
          "Type": "tos"

        }
      ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106965#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 未开通计费情况，请激活服务或充值。 |视频直播服务未开启或账号欠费，导致计费情况不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
