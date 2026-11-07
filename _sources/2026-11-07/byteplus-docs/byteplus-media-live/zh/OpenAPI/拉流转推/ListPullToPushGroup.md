---
title: "ListPullToPushGroup"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023-zh-CN"
---

调用`ListPullToPushGroup` API 查询分组名称列表。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListPullToPushGroup&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListPullToPushGroup` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本次 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|PageNum |Integer |是 |`1` |页码。BytePlus MediaLive 会将查询结果分页，仅返回指定页码的数据。支持范围：1–1000。 |
|PageSize |Integer |是 |`10` |每页返回的数据条数。支持范围：1–1000。 |
|StatusList |Integer 数组 |否 |`0` |分组状态，取值及含义如下。<br><br><br>* `0`：（默认）可用；<br><br>* `1`：已删除，不可用。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于 API 专属的唯一返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|List |[List](https://docs.byteplus.com/en/docs/24/107018#list) 数组 |`-` |分组信息列表。 |
|Total |Integer |`1` |查询结果的数据条数。 |


<span id="list"></span>
### 列表


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Name |String |`group001` |分组名称。 |
|ProjectName |String |`default` |分组所属项目。 |
|Status |Integer |`0` |分组状态，取值及含义如下。<br><br><br>* `0`：（默认）可用；<br><br>* `1`：已删除，不可用。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListPullToPushGroup&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 10
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListPullToPushGroup",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "Name": "Group001",
                "ProjectName": "default",
                "Status": 0
            }
        ],
        "Total": 1
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/107018#request-parameters)说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParameter.Tags.Key |指定的参数 Tags.Key 无效。 |参数`Tags.Key`校验未通过。请检查参数是否正确。 |
|400 |InvalidParameter.Tags.Value |指定的参数 Tags.Value 无效。 |参数`Tags.Value`校验未通过。请检查参数是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |请求创建的资源已存在，请重命名 |请求创建的资源（包括域名空间、域名、应用名称、配置、证书）已存在。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
