---
title: "DescribeRecordTaskFileHistory"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023-zh-CN"
---

查询指定域名空间的历史录制信息，包括时长、文件格式、开始时间和结束时间等。不会检索正在进行中的录制。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多查询10次。

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeRecordTaskFileHistory&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还需包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeRecordTaskFileHistory` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空间。默认情况下为空，表示将查询你BytePlus MediaLive下的所有域名空间。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名所属的域名空间。 |
|应用 |String |否 |`live` |直播流URL中的AppName字段。默认情况下为空，表示将查询该域名空间下的所有AppName。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。 |
|流 |String |否 |`stream-123` |直播流URL中的StreamName字段。默认情况下为空，表示将查询该应用下的所有StreamName。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若指定<code>流</code>，则必须同时指定<code>应用</code>。</div><br> |
|DateFrom |String |是 |`2023-11-01T00:00:00Z` |查询范围的开始时间（本地时间，RFC 3339格式，精确到秒）。查询指定录制任务详情时，DateFrom应设置为录制任务开始时间之前的任意时间。 |
|DateTo |String |是 |`2023-11-07T23:59:59Z` |查询范围的结束时间（本地时间，RFC 3339格式，精确到秒）。DateTo必须晚于DateFrom，且DateTo与DateFrom之间的间隔不得超过7天。 |
|PageNum |Integer |是 |`1` |页码。BytePlus MediaLive将查询结果分页，仅返回指定页码的结果。 |
|PageSize |Integer |是 |`30` |每页查询结果数量。 |
|Type |String |否 |`tos` |存储类型。<br><br><br>* `tos`：BytePlus TOS；<br><br>* `vod`：BytePlus 视频点播。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的API专属返回调用结果参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|数据 |[数据](https://docs.byteplus.com/en/docs/24/106949#data)数组 |`-` |录制记录列表。 |
|分页 |[分页](https://docs.byteplus.com/en/docs/24/106949#pagination)对象 |`-` |分页信息。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|应用 |String |`live` |AppName字段。 |
|流 |String |`stream-123` |StreamName字段。 |
|存储桶 |字符串 |`live-record-test` |存储桶名称或 BytePlus TOS。 |
|路径 |字符串 |`est6/record/push.example.org/live/testStream413` |录制文件的存储路径，格式为 `/record/{vhost}/{app}/{stream}`。 |
|时长 |字符串 |`01:34` |录制文件的长度。 |
|格式 |字符串 |`m3u8` |录制文件的格式。 |
|开始时间 |字符串 |`2023-11-01 00:49:17` |录制的开始时间。 |
|结束时间 |字符串 |`2023-11-01 00:45:44` |录制的结束时间。 |
|文件名 |字符串 |`1630331125_16303312***.m3u8` |录制文件的名称。 |
|Vid |字符串 |`v03713g100**********bob16pnh65g` |录制文件在视频点播中的 ID。 |
|开始时间 UTC |字符串 |`2023-10-31T16:49:17Z` |录制的开始时间（UTC 时间，RFC 3339 格式，精确到秒）。 |
|结束时间 UTC |字符串 |`2023-10-31T00:45:44Z` |录制的结束时间（UTC 时间，RFC 3339 格式，精确到秒）。 |


<span id="pagination"></span>
### 分页


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PageCur |整数 |`1` |当前页码。 |
|PageSize |整数 |`10` |每页结果数量。 |
|PageTotal |整数 |`1` |总页数。 |
|TotalCount |整数 |`1` |检索到的录制文件总数。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST
{
    "Vhost": "push.example.com",
    "App": "live",
    "Stream": "stream-123",
    "DateFrom": "2023-11-01T00:00:00Z",
    "DateTo": "2023-11-07T23:59:59Z",
    "PageNum": 1,
    "PageSize": 30,
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202108302155380102252431000500BC2E",
        "Action": "DescribeRecordTaskFileHistory",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "Stream": "testStream413",
                "Bucket": "live-test6",
                "Path": "est6/record/push.example.com/live/testStream413",
                "Duration": "01:34",
                "StartTime": "2021-08-16 00:00:00",
                "EndTime": "2021-08-17 00:00:00",
                "StartTimeUTC": "2021-08-16T00:00:00Z",
                "EndTimeUTC": "2021-08-17T00:00:00Z",
                "Format": "",
                "FileName": "1630331125_16303312***.m3u8"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 1,
            "TotalCount": 1
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106949#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。若仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
