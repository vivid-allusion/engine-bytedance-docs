---
title: "DescribeHTTPHeaderConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig-zh-CN"
---

调用 `DescribeHTTPHeaderConfig` API 查询指定域名的 HTTP 头部配置。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeHTTPHeaderConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeHTTPHeaderConfig` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名所属的域名空间。 |
|Domain |String |否 |`pull.example.com` |拉流域名。如未指定，查询结果将包含该域名空间下所有关联的拉流域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名。 |
|Phase |Integer |是 |`0` |要查询的 HTTP 头部配置类型：<br><br><br>* `0`：响应头。<br><br>* `1`：请求头。 |


<span id="Response parameters"></span>
## 返回参数

有关 API 专属返回参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|HeaderConfigList |[HeaderConfigList](https://docs.byteplus.com/en/docs/24/106907#headerconfiglist) 数组 |`无` |域名的头部配置列表。 |


<span id="headerconfiglist"></span>
### HeaderConfigList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`example` |域名空间。 |
|Domain |String |`example.com` |域名。 |
|HeaderDetailList |[HeaderDetailList](https://docs.byteplus.com/en/docs/24/106907#headerdetaillist) 数组 |`无` |要查询的 HTTP 头部列表。 |
|BlockOriginal |Integer |`0` |是否排除原始头部。<br><br><br>* `0`：包含。<br><br>* `1`：排除。 |
|Enable |Boolean |`true` |配置是否已开启。<br><br><br>* `true`：已开启。<br><br>* `false`：未开启。 |


<span id="headerdetaillist"></span>
### HeaderDetailList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|HeaderKey |String |`Content-Type` |头部名称。 |
|HeaderValue |String |`text/plain` |头部值。头部值可以为常量或以下变量之一：<br><br>对于响应头，头部值可为以下变量：<br><br><br>* `${domain}`：客户端请求中的域名。示例：`example.com`<br><br>* `${uri}`：客户端请求的路径（不含查询参数）。若客户端请求被重写，该变量表示重写后的路径。示例：`/dir/sample.php`<br><br>* `${args}`：客户端请求中的查询参数。若客户端请求被重写，该变量表示重写后的参数。示例：`color=red&n=10`<br><br>* `${remote_addr}`：发起请求的客户端 IP 地址。示例：`10.10.10.10`<br><br>* `${server_addr}`：响应客户端请求的边缘服务器 IP 地址。示例：`10.10.10.10`<br><br><br>对于请求头，头部值可为以下变量：<br><br><br>* `${upstream_host}`：回源请求中的域名。示例：`example.com`<br><br>* `${upstream_uri}`：回源请求的路径（不含查询参数）。若请求被重写，该变量表示重写后的路径。示例：`/dir/sample.php`<br><br>* `${upstream_args}`：回源请求中的查询参数。如果请求被重写，此变量表示重写后的参数。示例：`color=red&n=10`<br><br>* `${remote_addr}`：发送请求的客户端的 IP 地址。示例：`10.10.10.10` |
|HeaderFieldType |整数 |`0` |头部值的类型：<br><br><br>* `0`：常量<br><br>* `1`：变量 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeHTTPHeaderConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Phase": 0
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeHTTPHeaderConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "HeaderConfigList": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "BlockOriginal": 0,
                "Enable": false,
                "HeaderDetailList": [
                    {
                        "HeaderKey": "Content-Key",
                        "HeaderValue": "text/plain",
                        "HeaderFieldType": 0
                    }
                ]
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
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106907#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.DomainAndApp |域名和应用不能同时存在 |不能同时传入域名和应用。请修改输入参数。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |未开通视频直播服务或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到域名 |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
