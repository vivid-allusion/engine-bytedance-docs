---
title: "UpdateActivityMenuAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitymenuapi-zh-CN"
---

调用此 API 以更新直播活动的菜单。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`UpdateActivityMenuAPI`

* 请求方式：POST

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateActivityMenuAPI&Version=2020-06-01`

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
|Menus |是 |数组 |菜单的配置。 |


<span id="Menu"></span>
#### 菜单


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Name |是 |字符串 |标签页名称。 |
|Type |是 |整数 |标签页类型：<br><br><br>* 1：图文<br><br>* 2：卡片<br><br>* 3：聊天互动<br><br>* 4：直播内容<br><br>* 5：聚合直播<br><br>* 6：互动问答 |
|Location |是 |整数 |标签页的显示顺序，从左侧开始。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityMenuAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "Menus" : [
        {
             "Name" : "Menu name 1" ,
             "Type" : 2,
             "Location" : 1
        },
        {
             "Name" : "Menu name 2" ,
             "Type" : 2,
             "Location" : 2
        }
    ]
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

以下是请求成功处理时的返回示例：

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30" ,
     "Action" : "UpdateActivityMenuAPI" ,
     "Version" : "2020-06-01" ,
     "Service" : "livesaas" ,
     "Region" : "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
