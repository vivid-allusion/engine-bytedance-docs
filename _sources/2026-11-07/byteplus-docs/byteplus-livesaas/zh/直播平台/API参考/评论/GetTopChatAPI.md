---
title: "GetTopChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-gettopchatapi-zh-CN"
---

调用此 API 以获取特定直播活动中当前置顶的聊天消息列表。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`GetTopChatAPI`

* 请求方式：GET

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=GetTopChatAPI&Version=2020-06-01`

* 配额：每个账号每分钟 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |String |API 操作。 |
|Version |是 |String |本 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |是 |Integer |直播活动的 ID。 |


<span id="Sample request"></span>
### 请求示例

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetTopChatAPI&Version=2020-06-01&ActivityId=1231231231
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|ActivityId |Integer |直播活动的 ID。 |
|Data |Array |聊天消息对象数组。 |


<span id="Chat"></span>
#### Chat


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|ChatId |Integer |聊天消息的 ID。 |
|CreateTime |Integer |消息发送时的时间戳。 |
|TextContent |String |聊天消息内容。 |
|User |UserInfo |发送者信息。 |
|IsDelete |Boolean |聊天消息是否已被删除：<br><br><br>* true：已删除<br><br>* false：未删除 |
|LikeCount |Integer |消息的点赞总数。 |
|IsPresenter |Boolean |消息是否由主播发送：<br><br><br>* true：由主播发送<br><br>* false：由观众发送 |
|reviewStatus |Integer |聊天消息的审核状态：<br><br><br>* 0：无需审核<br><br>* 1：待审核<br><br>* 2：审核通过 |


<span id="UserInfo"></span>
#### UserInfo


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|UserId |Integer |发送者的 ID。 |
|Nickname |String |发送者昵称。 |


<span id="Sample response"></span>
### 返回示例

以下为请求成功时的返回示例：

```JSON
{
     "ResponseMetadata" :{
         "RequestId" : "202201201826170101501312091D1C09D2" ,
         "Action" : "GetTopChatAPI" ,
         "Version" : "2020-06-01" ,
         "Service" : "livesaas" ,
         "Region" : "ap-singapore-1" 
    },
     "Result" :{
         "Data" :[
            {
                 "ChatId" :31823336, 
                 "CreateTime" :1591860377, 
                 "TextContent" : "Hello!" , 
                 "User" :{
                     "Nickname" : "111" ,             
                     "UserId" :1669024344048647 
                },
                 "IsDelete" :true, 
                 "LikeCount" :3, 
                 "IsPresenter" :false, 
                 "reviewStatus" :0 
            }
        ]
    }
}
```
