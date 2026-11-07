---
title: "ResumeLiveStreamAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-resumelivestreamapi-zh-CN"
---

调用此 API，可恢复直播间中指定直播源被禁用的流。

若要在恢复流后再次禁用该流，请确保在调用本 API 操作后至少等待 30 秒再调用 [ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi-zh-CN)。

<span id="requirement"></span>
## 需求

配额：每个账号每分钟最多可查询 120 次

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=ResumeLiveStreamAPI&Version=2020-06-01`

* 方法：POST


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### Query


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`ResumeLiveStreamAPI` |API 操作。 |
|Version |字符串 |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="body"></span>
### Body


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |整型 |是 |`17218312****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|LineId |整型数组 |否 |`[356218,356219]` |需要恢复流的直播源 ID。若未指定，则恢复直播间所有源的流。<br><br>一个直播间可包含多个源，每个源都有自己的流。可通过调用 [GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN) 获取直播间的源 ID。 |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|状态 |布尔值 |`true` |指示指定流是否已恢复。<br><br><br>* `true`：所有指定流均已恢复。<br><br>* `false`：至少有一个指定流未被恢复。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=ResumeLiveStreamAPI&Version=2020-06-01
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
        "Action": "ResumeLiveStreamAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1662570420
    },
    "Result": {
        "Status": true
    }
}
```


<span id="error-codes"></span>
## 错误码

下表列出了本 API 操作的专用错误码。通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。


|状态码 |错误码 |错误信息 |接口行为 |
|---|---|---|---|
|200 |200027 |因启用直播流开始时间或结束时间功能而被禁用的流无法恢复。要恢复此类流，必须先禁用这些功能。 |请在 BytePlus Live 控制台或通过调用 [UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) 禁用“直播流开始时间”和“结束时间”功能。 |
