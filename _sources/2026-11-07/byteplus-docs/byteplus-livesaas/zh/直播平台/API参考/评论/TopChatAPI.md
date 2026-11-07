---
title: "TopChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-topchatapi-zh-CN"
---

调用此 API，可在直播活动期间将聊天消息置顶或取消置顶。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`TopChatAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=TopChatAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整数 |直播活动的 ID。 |
|ChatId |是 |整数 |聊天消息的 ID。 |
|TopStatus |是 |整数 |指定消息的置顶状态。<br><br><br>* 1：将消息置顶<br><br>* 2：取消消息置顶 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=TopChatAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "ChatId" : 1245231,
     "TopStatus" : 2
}
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Status |布尔值 |表示操作是否成功。<br><br><br>* true：成功<br><br>* false：失败 |


<span id="Sample response"></span>
### 返回示例

以下为请求成功时的返回示例。

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30" ,
     "Action" : "TopChatAPI" ,
     "Version" : "2020-06-01",
     "Service" : "livesaas",
     "Region" :  "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
