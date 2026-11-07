---
title: "SilenceUserAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-silenceuserapi-zh-CN"
---

调用此 API 以管理直播活动中的用户聊天权限。您可以调用此 API，禁止指定用户发送消息，或解除之前施加的禁言。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`SilenceUserAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=SilenceUserAPI&Version=2020-06-01`

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
|UserId |是 |整数 |需要禁言的用户 ID。 |
|Status |是 |布尔值 |是否禁止用户发送聊天消息：<br><br><br>* true：禁言用户。<br><br>* false：解除禁言。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=SilenceUserAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "UserId" : 1245231,
     "Status" : true
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

以下是成功请求的返回示例：

```JSON
{
  "ResponseMetadata":{
  "RequestId":"201806041104200100100232280022D30",
  "Action":"SilenceUserAPI",
  "Version":"2020-06-01",
  "Service":"livesaas",
  "Region": "ap-singapore-1"
 },
  "Result": {
  "Status": true
 }
}
```
