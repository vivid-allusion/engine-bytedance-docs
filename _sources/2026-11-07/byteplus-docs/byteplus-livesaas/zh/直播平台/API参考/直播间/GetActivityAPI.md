---
title: "GetActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityapi-zh-CN"
---

调用 GetActivityAPI 接口以获取直播间的基本信息，例如其状态和观看页地址。

<span id="requirement"></span>
## 需求

配额：每个账号每分钟 120 次查询

<span id="http-request"></span>
## HTTP 请求


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01`

* 方法：GET


<span id="request-parameters"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`GetActivityAPI` |API 操作。 |
|Version |字符串 |是 |`2020-06-01` |本接口的版本号。当前版本：`2020-06-01`。 |
|ActivityId |长整型 |是 |`17218346****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Id |长整型 |`17218346****` |直播间的活动 ID。 |
|Name |字符串 |`Live Room A` |直播间名称。 |
|LiveTime |长整型 |`1642070520` |直播流开始时间，Unix 时间戳格式。单位：秒。<br><br>该时间不一定为直播流的实际开始时间。 |
|IsBeginLiveEnable |整型 |`0` |指示是否启用定时开播。<br><br>可选值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。只能在指定的开播时间后进行开播。 |
|IsAutoEndEnable |整型 |`1` |指示流是否配置为在指定时间自动结束。<br><br>可选值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|EndTime |长整型 |`1642170520` |直播流结束时间，Unix 时间戳格式。单位：秒。 |
|CoverImage |字符串 |`//example.image` |横屏模式下封面图的 URL。<br><br>若通过 API 调用配置，URL 包含协议头；若通过控制台配置，则不包含协议头。 |
|VerticalCoverImage |字符串 |`//example.image` |竖屏模式下封面图的 URL。<br><br>如未指定，则默认为 `CoverImage` 的值。<br><br>若通过 API 调用配置，URL 包含协议头；若通过控制台配置，则不包含协议头。 |
|Status |整型 |`2` |直播间状态。<br><br>可选值：<br><br><br>* `1`：直播中。<br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：已结束。 |
|ViewUrl |字符串 |`https://live.byteplus.com/7420/*******` |直播间观看页的 URL。 |
|IsPageViewEnable |整型 |`-` |已废弃。 |
|IsLockPreview |整型 |`1` |指示预告是否被锁定。<br><br>可选值：<br><br><br>* `0`：预告未锁定。<br><br>* `1`：预告已锁定。观看页在 **预告** 状态下被锁定，无法播放直播流或其回放。 |
|OwnerSubAccount |字符串 |`admin@bytedance.com` |创建该直播间的账号。如果该值为 `admin@example.com`，则直播间由您的主 BytePlus 账号创建。 |
|LiveMode |整型 |`1` |直播延时类型。<br><br>可选值：<br><br><br>* `1`：超低延时，延时为 1 到 2 秒。<br><br>* `2`：普通延时，延时为 5 到 10 秒。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=17218346****
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetActivityAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1",
        "SystemTime":1632070520
    },
    "Result":{
        "Id":17218346****,      
        "Name":"Live Room A",
        "LiveTime":1642070520,
        "IsBeginLiveEnable": 0,
        "EndTime": 1642170520,
        "IsAutoEndEnable": 1,
        "CoverImage":"//example.image",
        "VerticalCoverImage":"//example.image",
        "Status":2,
        "ViewUrl":"https://live.byteplus.com/7420/*******", 
        "IsPageViewEnable"：1,
        "IsLockPreview":1,  
        "OwnerSubAccount":"admin@bytedance.com",
        "LiveMode":1        
    }
}
```


<span id="error-codes"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
