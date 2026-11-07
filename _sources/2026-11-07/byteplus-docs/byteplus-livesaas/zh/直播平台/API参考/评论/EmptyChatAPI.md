---
title: "EmptyChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-emptychatapi-zh-CN"
---

调用此 API 可清除某直播活动的所有聊天消息。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`EmptyChatAPI`

* 请求方式：GET

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=EmptyChatAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |是 |整数 |直播活动的 ID。 |


<span id="Sample request"></span>
### 请求示例

```JSON
Get http://livesaas.byteplusapi.com/?Action=EmptyChatAPI&Version=2020-06-01&ActivityId=1231231231&ChatId=0&Count=20&PollingType=0
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Status |布尔值 |操作结果：<br><br><br>* true：成功<br><br>* false：失败 |


<span id="Sample response"></span>
### 返回示例

以下为成功请求的返回示例：

```JSON
{
     "ResponseMetadata" :{
         "RequestId" : "202201201826170101501312091D1C09D2" ,
         "Action" : "EmptyChatAPI" ,
         "Version" : "2020-06-01" ,
         "Service" : "livesaas" ,
         "Region" : "ap-singapore-1" 
    },
     "Result" :{
         "Status" : true
    }
}
```
