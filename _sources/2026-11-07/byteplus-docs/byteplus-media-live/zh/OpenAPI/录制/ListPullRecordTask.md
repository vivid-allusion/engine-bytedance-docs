---
title: "ListPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask-zh-CN"
---

该 API 用于查询当前账号下创建的直播录制任务列表。支持按分页、域名、应用名称和流名称等条件组合查询。通过该 API，您可以获取任务的录制周期、任务状态等具体信息。这有助于跟踪录制进度、监控任务状态，并支持后续资源管理工作。

## 要求

* 速率限制：每个账号每秒 50 次查询。

* 计费：该 API 用于查询已创建的录制任务记录，不涉及实时录制或数据存储操作，因此不会产生费用。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=ListPullRecordTask&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 专用参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`ListPullRecordTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|PageNum |Integer |是 |`1` |页码。取值必须大于或等于 `1`。 |
|PageSize |Integer |是 |`5` |每页查询结果数量。取值范围：`[1,500]`。 |
|Vhost |String |否 |`example` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名所属的域名空间。 |
|Domain |String |否 |`push.example.com` |直播流使用的推流域名或拉流域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名。 |
|App |String |否 |`live` |应用名称，与直播流地址中的 `AppName` 字段取值相同，用于指定要更新的录制配置。默认值为空。您可以调用  [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取 `App` 值。 |
|Stream |String |否 |`example_stream` |流名称，其取值对应直播流地址中 `StreamName` 字段的值，用于指定要查询的录制任务。默认值为空。您可以调用  [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取 `Stream` 的值。 |

## 响应参数

API 专用的唯一响应参数见下表。更多详情，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|List |[List](https://docs.byteplus.com/en/docs/24/107036#list) 数组 |`-` |直播录制任务列表。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107036#pagination) 对象 |`-` |查询结果的分页信息。 |

### List

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|TaskId |String |`f831f3b0dc******aa4dcf7621` |任务 ID，任务的唯一标识符。 |
|StartTime |String |`2023-06-30T15:04:05Z` |录制开始时间，RFC3339 格式的 UTC 时间，精度为秒。 |
|EndTime |String |`2023-06-30T15:05:05Z` |录制结束时间，RFC3339 格式的 UTC 时间，精度为秒。 |
|Vhost |String |`push.example.com` |域名空间名称。 |
|Domain |String |`push.example.com` |推流域名或拉流域名。 |
|App |String |`Live` |应用名称。 |
|Stream |String |`example_stream` |流名称。 |
|Status |String |`Finished` |录制任务的状态。可能的取值如下。<br><br><br>* `停用`：录制任务已停止；<br><br>* `未开始`：录制任务尚未开始；<br><br>* `生效中`：录制任务正在进行；<br><br>* `已结束`：录制已完成。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageCur |Integer |`1` |当前页的页码。 |
|PageSize |Integer |`2` |每页显示的数据项数量。 |
|PageTotal |Integer |`43` |查询结果数据的总页数。 |
|TotalCount |Integer |`86` |查询结果中的数据项总数。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=ListPullRecordTask&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 2
}
```

### 示例响应

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "TaskId": "f831f3b0dc******aa4dcf7621",
                "StartTime": "2023-06-30T15:04:05Z",
                "EndTime": "2023-06-30T15:05:05Z",
                "Vhost": "push.example.com",
                "Domain": "push.example.com",
                "App": "Live",
                "Stream": "example_stream",
                "Status": "Finished"
            },
            {
                "TaskId": "a1b2c3d4e5******f6g7h8i9j0",
                "StartTime": "2023-06-30T16:04:05Z",
                "EndTime": "2023-06-30T16:05:05Z",
                "Vhost": "pull.example.com",
                "Domain": "pull.example.com",
                "App": "Live",
                "Stream": "another_stream",
                "Status": "InProgress"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 2,
            "PageTotal": 43,
            "TotalCount": 86
        }
    }
}
```

## 错误码

以下是与当前操作相关的错误码。关于其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回此错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](#Request Parameters)的描述进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数验证失败。请检查参数类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝。当前账号下没有请求的资源（域名空间、域名、应用、配置模板、证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝。当前账号下没有请求的资源（域名空间、域名、应用、配置模板、证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费情况。 |
|404 |ResourceNotFound |\- |未找到资源（域名空间、域名、应用、配置模板、证书）。建议重试。如果仍返回此错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |服务之间发生错误，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |服务之间存在错误，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
