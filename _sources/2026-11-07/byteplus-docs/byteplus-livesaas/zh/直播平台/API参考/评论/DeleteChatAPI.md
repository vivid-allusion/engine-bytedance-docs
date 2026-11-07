---
title: "DeleteChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletechatapi-zh-CN"
---

该 API 用于删除直播活动中的指定聊天消息。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`DeleteChatAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=DeleteChatAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |该 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整数 |直播活动的 ID。 |
|ChatId |是 |整数 |聊天消息的 ID。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=DeleteChatAPI&Version=2020-06-01
{
 "ActivityId":732412312,
 "ChatId": 1245231
}
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Status |布尔值 |聊天消息是否已被删除：<br><br><br>* true：已删除<br><br>* false：未删除 |


<span id="Sample response"></span>
### 返回示例

以下为请求成功时的返回示例。

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30",
     "Action" : "DeleteChatAPI",
     "Version": "2020-06-01",
     "Service": "livesaas",
     "Region" : "ap-singapore-1" 
  },
   "Result" : {
       "Status": true
  }
}
```
