---
title: "DescribeRelaySourceV3"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023-zh-CN"
---

调用`DescribeRelaySourceV3` API，以查询播放触发的回源配置。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多查询10次。

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeRelaySourceV3&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeRelaySourceV3` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取该域名所属的域名空间。 |
|应用 |String |否 |`live` |直播流URL中的AppName字段。如未指定，表示查询结果不对AppName字段进行过滤。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。 |
|Group |String |否 |`relay1` |回源配置组名称。 |


<span id="Response parameters"></span>
## 返回调用结果

关于唯一的API专属返回调用结果，请参见下表。更多详情请参考[返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|RelaySourceConfigList |[RelaySourceConfigList](https://docs.byteplus.com/en/docs/24/106984#relaysourceconfiglist)数组 |`-` |回源配置组列表。 |


<span id="relaysourceconfiglist"></span>
### RelaySourceConfigList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|应用 |String |`live` |AppName字段。 |
|GroupDetails |[GroupDetails](https://docs.byteplus.com/en/docs/24/106984#groupdetails)数组 |`-` |该组的回源配置。 |


<span id="groupdetails"></span>
### GroupDetails


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Group |String |`relay1` |回源配置组名称。 |
|Servers |[Servers](https://docs.byteplus.com/en/docs/24/106984#servers)数组 |`-` |源站配置列表。 |


<span id="servers"></span>
### Servers


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|RelaySourceProtocol |String |`rtmp` |流协议。 |
|RelaySourceDomain |String |`example.org` |回源地址。 |
|RelaySourceParams |JSON Map |`{"key1": "value1","key2": "value2"}` |自定义回源参数。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeRelaySourceV3&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeRelaySource",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "RelaySourceConfigList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "GroupDetails": [
                    {
                        "Group": "relay1",
                        "Servers": [
                            {
                                "RelaySourceProtocol": "rtmp",
                                "RelaySourceDomain": "example.org",
                                "RelaySourceParams": {
                                    "key1": "value1",
                                    "key2": "value2"
                                }
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106984#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该AccountID未开通计费情况，请激活服务或充值。 |视频直播服务尚未开启或账户存在欠费，导致无法获取账单。请检查服务激活状态和账户欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
