---
title: "UpdatePresenterNameAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatepresenternameapi-zh-CN"
---

您可以调用此 API，在直播活动中发送聊天消息时，更新显示的主播名称。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`UpdatePresenterNameAPI`

* 请求方式：POST

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=UpdatePresenterNameAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整数 |直播活动的 ID。 |
|PresenterName |是 |字符串 |主播名称。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdatePresenterNameAPI&Version=2020-06-01
{
     "ActivityId":123,
     "PresenterName":"abc" 
}
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

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30",
     "Action" : "UpdatePresenterNameAPI",
     "Version" : "2020-06-01",
     "Service" : "livesaas",
     "Region" :  "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
