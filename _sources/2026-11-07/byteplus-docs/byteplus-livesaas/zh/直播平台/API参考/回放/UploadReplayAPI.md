---
title: "UploadReplayAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-uploadreplayapi-zh-CN"
---

调用此 API，将视频绑定到直播流活动作为回放。在执行该操作前，必须先将视频上传至媒体库。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 接口行为：`UploadReplayAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=UploadReplayAPI&Version=2020-06-01`

* 配额：每个账号每分钟 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 接口行为。 |
|Version |String |是 |该 API 接口行为的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|ActivityId |Integer |是 |直播流活动的 ID。 |
|Media |Array |是 |视频信息。 |


<span id="Media"></span>
#### **Media**


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Name |String |是 |媒体库中视频的名称。 |
|Vid |String |是 |媒体库中视频的 ID。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UploadReplayAPI&Version=2020-06-01
{
  "ActivityId": 178465844575,
  "Media": {
    "Name": "123",
    "Vid": "id123"
  }
}
```


<span id="Response"></span>
## 返回调用结果

<span id="Sample response"></span>
### 返回示例

```JSON
{
   "ResponseMetadata":{
     "RequestId":"201806041104200100100232280022D30",
     "Action":"UploadReplayAPI",
     "Version":"2020-06-01",
     "Service":"livesaas",
     "Region":"ap-singapore-1",
     "SystemTime":1656067132
  }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码请参见[通用错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
