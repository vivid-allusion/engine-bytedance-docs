---
title: "DescribeLiveISPData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata-zh-CN"
---

调用 `DescribeLiveISPData` API，以获取为 BytePlus MediaLive 提供网络接入服务的互联网服务提供商（ISP）标识符。获得 ISP 标识符后，可在支持基于 ISP 查询的 API 中，使用这些标识符查询特定 ISP 的维度数据。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多 30 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveISPData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveISPData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ISPList |[ISPList](https://docs.byteplus.com/en/docs/24/107026#isplist) 数组 |`-` |用于表示互联网服务提供商（ISP）标识符的数组。 |


<span id="isplist"></span>
### ISPList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |String |`unicom` |互联网服务提供商（ISP）标识符。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|Name |String |`unicom` |互联网服务提供商（ISP）名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202309042019116E825EC4FC63CD166C91",
        "Action": "DescribeLiveISPData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "ISPList": [
            {
                "Code": "unicom",
                "Name": "unicom"
            },
            {
                "Code": "railcom",
                "Name": "railcom"
            },
            {
                "Code": "telecom",
                "Name": "telecom"
            },
            {
                "Code": "mobile",
                "Name": "mobile"
            },
            {
                "Code": "cernet",
                "Name": "cernet"
            },
            {
                "Code": "tianwei",
                "Name": "tianwei"
            },
            {
                "Code": "alibaba",
                "Name": "alibaba"
            },
            {
                "Code": "tencent",
                "Name": "tencent"
            },
            {
                "Code": "drpeng",
                "Name": "drpeng"
            },
            {
                "Code": "btvn",
                "Name": "btvn"
            },
            {
                "Code": "huashu",
                "Name": "huashu"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参阅 [请求参数](https://docs.byteplus.com/en/docs/24/107026#request-parameters)说明进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
