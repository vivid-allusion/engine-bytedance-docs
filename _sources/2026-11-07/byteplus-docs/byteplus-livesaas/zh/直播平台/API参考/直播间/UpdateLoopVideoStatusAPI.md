---
title: "UpdateLoopVideoStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateloopvideostatusapi-zh-CN"
---

调用此 API 以启用或禁用指定直播活动的循环播放功能。

<span id="request"></span>
## 请求

<span id="details"></span>
### 详情


* API 操作：`UpdateLoopVideoStatusAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoStatusAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="query-string-parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="body-parameters"></span>
### 请求体参数


|**参数名称** |**必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整数 |直播活动的 ID。 |
|IsStartLoopVideo |是 |整数 |指定是否启动或停止循环播放：<br><br><br>* 1：启动。当循环播放启动时，直播活动也会启动。<br><br>* 2：停止。当循环播放停止时，直播活动也会停止。 |
|LineId |是 |整数 |直播流的 ID。 |


<span id="sample-request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoStatusAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "IsStartLoopVideo":1,
    "LineId":123
}
```


<span id="response"></span>
## 返回调用结果

<span id="response-schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|状态 |布尔值 |表示循环播放状态是否已成功更新。 |


<span id="sample-response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata":{
    "RequestId":"2018060411042001001002322800xxxx",
    "Action":"UpdateLoopVideoStatusAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
  "Result":{
   "Status":true
}
}
```
