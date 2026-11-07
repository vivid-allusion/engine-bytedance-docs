---
title: "ListPullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023-zh-CN"
---

调用 `ListPullToPushTask` API 分页查询转推任务列表，支持按任务名称模糊搜索。

## 要求

速率限制：每个账号每秒 15 次查询。

## HTTP 请求

* 方法：GET

* 端点：https://open.byteplusapi.com/?Action=ListPullToPushTask&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特有参数外，还必须包含[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`ListPullToPushTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |
|Page |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|Size |Integer |否 |`20` |每页查询结果数量。有效值：[1,500]。默认值：`20`。<br><br>> **说明**<br><br><br>> 如果将此参数设置为 `0`，则使用默认值。<br> |
|Title |String |否 |`doc` |转推任务的名称。搜索不区分大小写，并支持模糊搜索。例如，如果将 `Title` 设置为 `doc`，可能会返回名称中包含 `doc` 的转推任务列表，例如 `docspace`、 `docs` 和 `DOC`。 |

## 响应参数

API 特有的响应参数见下表。更多详情，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|List |[List](https://docs.byteplus.com/en/docs/24/106981#list) 数组 |`-` |您的转推任务列表。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/106981#pagination) 对象 |`-` |分页信息。 |

### List

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Title |String |`task001` |转推任务的名称。 |
|TaskId |String |`fde6aa0281d*******9a6e24236` |任务 ID。 |
|StartTime |String |`2022-04-01T00:00:00Z` |转推任务的开始时间（RFC 3339 格式的 UTC 时间）。 |
|EndTime |String |`2022-04-02T00:00:00Z` |转推任务的结束时间（RFC 3339 格式的 UTC 时间）。 |
|CallbackURL |String |`http://example.mtime.cn/live/example/callbackapi` |用于接收转推任务事件的回调地址。 |
|Type |Integer |`0` |流源类型。有效值包括：<br><br><br>* `0`：流内容从直播源拉取。<br><br>* `1`：流内容从点播视频拉取。 |
|CycleMode |Integer |`-1` |流的循环模式。唯一有效值为 `-1`：顺序循环。 |
|DstAddr |String |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|SrcAddr |String |`http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |拉流地址，当 Type 为 0 时返回。 |
|SrcAddrS |Array of String |`["http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |点播视频列表，当 Type 为 1 时返回。 |
|Status |String |`Pending` |转推任务的状态。<br><br><br>* `Disabled`：转推任务已禁用。<br><br>* `Pending`：转推任务已准备启动。<br><br>* `Enabled`：表示正在进行的转推任务，并在定义的开始时间激活。<br><br>* `Ended`：转推任务的定义结束时间之后显示此状态。 |
|DstAddrType |Integer |`1` |推流地址类型。有效值包括：<br><br><br>* `1`：BytePlus MediaLive 的推流地址。<br><br>* `2`：第三方推流地址。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageCur |Integer |`1` |当前页码。 |
|PageSize |Integer |`10` |每页的结果数量。 |
|PageTotal |Integer |`108` |总页数。 |
|TotalCount |Integer |`1073` |结果总数。 |

## 示例

### 请求示例

```json
GET https://open.byteplusapi.com/?Action=ListPullToPushTask&Version=2023-01-01&Page=1&Size=20&Title=doc
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311457440101742350380352BCC7",
        "Action": "ListPullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "CallbackURL": "",
                "CycleMode": -1,
                "DstAddr": "rtmp://example.org/Video/2022/02/04/mp4/190204084208765161.mp4",
                "EndTime": "2022-01-01T23:44:32+08:00",
                "SrcAddr": "http://example.org/Video/2003/02/04/mp4/190204084208765161.mp4",
                "SrcAddrS": [],
                "DstAddrType": 2,
                "StartTime": "2021-12-31T22:44:23+08:00",
                "Status": "Pending",
                "TaskId": "8fde6aa0281d9f6e15e6059a6e242365",
                "Title": "sutest007",
                "Type": 0
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 108,
            "TotalCount": 1073
        }
    }
}
```

## 错误码

以下是与当前操作相关的错误码。对于其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持团队](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106981#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数验证失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝。当前账号下没有请求的资源（域名空间、域名、应用、配置模板、证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未启用或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |请求被拒绝。当前账号下没有请求的资源（资源包括域名空间、域名、应用、配置模板、证书）或 API 权限。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持团队](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持团队](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持团队](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持团队](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持团队](https://console.byteplus.com/workorder/create)。 |
