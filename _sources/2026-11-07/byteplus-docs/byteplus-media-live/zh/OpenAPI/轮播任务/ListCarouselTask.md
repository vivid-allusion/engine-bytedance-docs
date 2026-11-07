---
title: "ListCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask-zh-CN"
---

调用 `ListCarouselTask` API 获取所有当前轮播任务的列表，包括任务ID、状态和创建时间，可用于任务管理和批量查询。

<span id="Requirements"></span>
## 要求

限速：每个账号每秒最多查询10次。

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListCarouselTask` |API操作。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Page |Integer |是 |`1` |查询数据的页码。 |
|PageSize |Integer |是 |`30` |每页显示的数据条数，最大值为1000。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的API专属返回参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107002#data)对象 |`-` |轮播任务数据对象。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Count |Integer |`29` |符合查询条件的轮播任务总数。 |
|Result |[Result](https://docs.byteplus.com/en/docs/24/107002#result)数组 |`-` |轮播任务数组，每个元素代表一个任务的详细信息。 |


<span id="result"></span>
### 结果


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CreatedAt |[CreatedAt](https://docs.byteplus.com/en/docs/24/107002#createdat)对象 |`{"Time":"2023-03-15T08:00:00+08:00"}` |任务的创建时间，RFC3339格式的时间戳，精确到秒。 |
|Name |String |`Carousel test` |轮播任务名称。 |
|Status |String |`running` |轮播任务的当前状态。取值及含义如下：<br><br><br>* `pending`：任务等待调度；<br><br>* `prepare`：任务初始化中；<br><br>* `running`：任务运行中；<br><br>* `prestop`：任务停止中；<br><br>* `done`：任务已停止。 |
|StoppedAt |[StoppedAt](https://docs.byteplus.com/en/docs/24/107002#stoppedat)对象 |`{"Time":"2023-03-16T08:00:00+08:00"}` |任务的结束时间，RFC3339格式的时间戳，精确到秒。 |
|TaskID |String |`e1fb009334fc5b16` |轮播任务的唯一标识。 |
|UpdatedAt |[UpdatedAt](https://docs.byteplus.com/en/docs/24/107002#updatedat)对象 |`{"Time":"2023-03-15T10:00:00+08:00"}` |任务的更新时间，RFC3339格式的时间戳，精确到秒。 |


<span id="createdat"></span>
### CreatedAt


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Time |String |`2024-10-30T15:25:07+08:00` |任务的创建时间，RFC3339格式的时间戳，精确到秒。 |


<span id="stoppedat"></span>
### StoppedAt


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Time |String |`0001-01-01T00:00:00Z` |任务的结束时间，RFC3339格式的时间戳，精确到秒。 |


<span id="updatedat"></span>
### UpdatedAt


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Time |String |`2024-10-30T15:25:08+08:00` |任务的更新时间，RFC3339格式的时间戳，精确到秒。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListCarouselTask&Version=2023-01-01
{
    "Page": 1,
    "PageSize": 30
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301540353C34785110C816119A9E",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "Count": 29,
            "Result": [
                {
                    "CreatedAt": {
                        "Time": "2024-10-30T15:25:07+08:00"
                    },
                    "Name": "Carousel test",
                    "Status": "running",
                    "StoppedAt": {
                        "Time": "0001-01-01T00:00:00Z"
                    },
                    "TaskID": "e1fb009334fc5b16",
                    "UpdatedAt": {
                        "Time": "2024-10-30T15:25:08+08:00"
                    }
                }
            ]
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参见[请求参数](#Request Parameters)说明进行检查。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
