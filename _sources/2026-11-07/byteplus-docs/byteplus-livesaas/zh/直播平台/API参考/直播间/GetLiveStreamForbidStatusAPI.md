---
title: "GetLiveStreamForbidStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi-zh-CN"
---

调用此 API 以检查直播间中某个直播源的流是否被禁播。

<span id="requirement"></span>
## 需求

配额：每个账号每分钟最多查询 120 次

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetLiveStreamForbidStatusAPI&Version=2020-06-01`

* 方法：POST


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有共享请求参数。完整列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`GetLiveStreamForbidStatusAPI` |API 操作。 |
|Version |字符串 |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="body"></span>
### 请求体


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |整数 |是 |`17218312****` |直播间的活动 ID。你可以通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|LineId |整数数组 |否 |`[356218,356219]` |直播源的 ID 列表。如果省略此参数，API 会返回直播间内所有直播源的流状态。<br><br>一个直播间可以包含多个直播源，每个直播源拥有自己的流。你可以通过调用 [GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN) 获取直播间的直播源 ID。 |


<span id="response-parameters"></span>
## 返回调用结果


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|StreamForbidStatus |数组[GetLiveStreamForbidStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi-zh-CN) |`-` |指定直播源的流状态列表。 |


<span id="forbidstatus"></span>
### ForbidStatus


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|StreamStatus |整数 |`0` |流的状态。<br><br><br>* `0`：未被禁播。<br><br>* `1`：已被禁播。 |
|ForbidTime |字符串 |`2024-07-13T02:59:50Z` |流被禁播的截止时间（UTC+0）。<br><br>值为 `"0"` 表示流未被禁播。 |
|LineId |整数 |`356218` |直播源 ID。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetLiveStreamForbidStatusAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "LineId": [356218,356219]
}
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "GetLiveStreamForbidStatusAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1718161649
    },
    "Result": {
        "StreamForbidStatus": [
            {
                "StreamStatus": 0,
                "ForbidTime": "0",
                "LineId": 356218
            },
            {
                "StreamStatus": 1,
                "ForbidTime": "2024-07-13T02:59:50Z",
                "LineId": 356219
            }
        ]
    }
}
```
