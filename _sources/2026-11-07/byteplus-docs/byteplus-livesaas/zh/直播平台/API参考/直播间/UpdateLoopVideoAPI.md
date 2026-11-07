---
title: "UpdateLoopVideoAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateloopvideoapi-zh-CN"
---

调用此 API 以编辑指定直播活动的循环视频配置。

<span id="request"></span>
## 请求

<span id="details"></span>
### 详情


* API 接口行为：`UpdateLoopVideoAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoAPI&Version=2020-06-01`

* 配额：每个账号每分钟 120 次查询


<span id="query-string-parameters"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 接口行为。 |
|Version |是 |字符串 |此 API 接口行为的版本。当前版本：`2020-06-01`。 |


<span id="body-parameters"></span>
### 请求体参数


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整型 |直播活动的 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |
|LineId |是 |整型 |直播流的 ID。可通过调用[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN)获取该 ID。 |
|LoopNumber |是 |整型 |视频播放次数。当前仅支持设置为`1`。 |
|LoopVideo |是 |数组[UpdateLoopVideoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideoapi-zh-CN) |循环回放配置。 |


<span id="loopvideo"></span>
#### LoopVideo


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Index |是 |整型 |视频索引，从`1`开始，依次递增。 |
|VideoCoverImage |否 |整型 |视频的封面图。该参数已废弃。 |
|VideoName |是 |字符串 |视频名称。 |
|VideoVid |是 |字符串 |视频的唯一 ID。可通过调用[ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi)获取该 ID。 |


<span id="sample-request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "LineId":1234,
    "LoopNumber":1,
    "LoopVideo":[
        {
            "Index":1,
            "VideoName":"video.mp4",
            "VideoVid":"v02a49370000b****gbiokkno91"
        }
    ]
}
```


<span id="response"></span>
## 返回调用结果

<span id="response-schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Id |整型 |循环回放配置的 ID。 |


<span id="sample-response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata":{
    "RequestId":"201806041104200100100232280022D30",
    "Action":"UpdateLoopVideoAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
  "Result":{
   "Id": 123
}
}
```
