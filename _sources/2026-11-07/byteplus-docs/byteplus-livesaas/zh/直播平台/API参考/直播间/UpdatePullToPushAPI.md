---
title: "UpdatePullToPushAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatepulltopushapi-zh-CN"
---

UpdatePullToPushAPI 操作用于根据指定 URL，为直播活动启动或停止拉流。

<span id="request"></span>
## 请求

<span id="details"></span>
### 详情


* API 操作：`UpdatePullToPushAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=UpdatePullToPushAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="query-string-parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |API 版本。当前版本：`2020-06-01`。 |


<span id="body-parameters"></span>
### 请求体参数


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整数 |直播活动的 ID。 |
|LineId |否 |整数 |直播流的 ID。调用 `GetStreamsAPI` 操作以获取活动的流 ID。一个活动可以拥有多个直播流。 |
|PullStreamUrl |是 |字符串 |要拉取的流的 URL。 |
|PullStreamStatus |是 |整数 |指定是否启动或停止拉流：<br><br><br>* 1：启动拉流。<br><br>* 2：停止拉流。 |
|PullStreamMode |否 |整数 |指定操作主流或备用流：<br><br><br>* 0：主流<br><br>* 1：备用流 |


<span id="sample-request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdatePullToPushAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "PullStreamUrl": "https://xxxx/xxxx/xxxx.flv",
    "PullStreamStatus": 1
}
```


<span id="response"></span>
## 返回调用结果

<span id="sample-response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata":{
    "RequestId":"201806041104200100100232280022D30",
    "Action":"UpdatePullToPushAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
}
```
