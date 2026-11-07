---
title: "ListPullToPushTaskV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-2023-zh-CN"
---

调用 `ListPullToPushTaskV2` API 分页查询转推任务列表，支持按任务名称模糊搜索。

## 要求

速率限制：每个账号每秒 15 次查询。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=ListPullToPushTaskV2&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`ListPullToPushTaskV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|GroupNames |Array of String |否 |`default` |任务所属的组名称。你可以调用 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 获取组名称。<br><br>> **说明**<br><br><br><br>* > 使用主账号调用时，该字段不是必填字段。<br><br><br>* > 使用子账号调用时，该字段为必填字段。<br> |
|Title |String |否 |`doc` |转推任务的名称。搜索不区分大小写，并支持模糊搜索。例如，如果将`Title`设置为`doc`，可能会获取名称中包含`doc`的转推任务列表，例如`docspace`、`docs`和`DOC`。 |
|Page |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|Size |Integer |否 |`20` |每页查询结果数量。取值范围：[1,500]。默认值：`20`。<br><br>> **说明**<br><br><br>> 如果将该参数设置为 `0`，则使用默认值。<br> |

## 响应参数

下表列出了该 API 特有的响应参数。更多详情，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|List |Array of [List](https://docs.byteplus.com/en/docs/24/106982#list) |`-` |你的转推任务列表。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/106982#pagination) |`-` |分页信息。 |

### List

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Title |String |`task001` |转推任务的名称。 |
|TaskId |String |`fde6aa0281d*******9a6e24236` |任务 ID。 |
|StartTime |String |`2022-04-01T00:00:00Z` |转推任务的开始时间（RFC 3339 格式的 UTC 时间）。 |
|EndTime |String |`2022-04-02T00:00:00Z` |转推任务的结束时间（RFC 3339 格式的 UTC 时间）。 |
|CallbackURL |String |`http://example.mtime.cn/live/example/callbackapi` |用于接收转推任务事件的回调地址。 |
|Type |Integer |`0` |流来源类型。取值包括：<br><br><br>* `0`：从直播源拉取流内容。<br><br>* `1`：从点播视频拉取流内容。 |
|CycleMode |Integer |`-1` |流的循环模式。唯一有效值为 `-1`：顺序循环。 |
|DstAddr |String |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|SrcAddr |String |`http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |拉流地址。当 Type 为 0 时返回。 |
|SrcAddrS |Array of String |`["http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |点播视频列表。当 Type 为 1 时返回。 |
|Status |String |`未开始` |转推任务的状态。<br><br><br>* `Disabled`：转推任务已禁用。<br><br>* `Pending`：转推任务已准备启动。<br><br>* `Enabled`：表示转推任务正在进行，并在定义的开始时间激活。<br><br>* `Ended`：该状态在转推任务定义的结束时间后出现。 |
|DstAddrType |Integer |`1` |推流地址的类型。取值包括：<br><br><br>* `1`：BytePlus MediaLive 的推流地址。<br><br>* `2`：第三方推流地址。 |
|GroupName |String |`group001` |任务所属的组名称。你可以调用 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 获取组名称。<br><br>> **说明**<br><br><br><br>* > 使用主账号调用时，该字段不是必填字段。<br><br><br>* > 使用子账号调用时，该字段为必填字段。<br> |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageCur |Integer |`1` |当前页码。 |
|PageSize |Integer |`10` |每页结果数量。 |
|PageTotal |Integer |`108` |总页数。 |
|TotalCount |Integer |`1073` |结果总数。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=ListPullToPushTaskV2&Version=2023-01-01
{
    "Page": 1,
    "Size": 20,
    "Title": "task001",
    "GroupNames": [
        "default"
    ]
}
```

### 示例响应

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311457440101742350380352BCC7",
        "Action": "ListPullToPushTaskV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
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
                "Status": "未开始",
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

以下是与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106982#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |请求被拒绝。当前账号下没有所请求的资源（资源包括域名空间、域名、应用、配置模板、证书），或没有 API 权限。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
