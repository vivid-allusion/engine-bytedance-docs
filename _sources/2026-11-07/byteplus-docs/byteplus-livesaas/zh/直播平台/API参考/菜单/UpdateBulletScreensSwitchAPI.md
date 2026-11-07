---
title: "UpdateBulletScreensSwitchAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatebulletscreensswitchapi-zh-CN"
---

调用此 API 以配置客户端是否显示弹幕开关。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 接口行为：`UpdateBulletScreensSwitchAPI`

* 请求方式：POST

* 请求 URL：`https://open.byteplusapi.com/?Action=UpdateBulletScreensSwitchAPI&Version=2020-06-01`

* 配额：每个账号每分钟 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 接口行为。 |
|Version |是 |字符串 |本 API 接口行为的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整数 |直播活动的 ID。 |
|BulletScreensSwitch |是 |整数 |指定客户端是否显示弹幕开关：<br><br><br>* 0：不显示<br><br>* 1：显示 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST https://open.byteplusapi.com/?Action=UpdateBulletScreensSwitchAPI&Version=2020-06-01
{
     "ActivityId":123,
     "BulletScreensSwitch":1
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

以下是一次成功请求的返回示例：

```JSON
{
   "ResponseMetadata":{
     "RequestId":"201806041104200100100232280022D30",
     "Action":"UpdateBulletScreensSwitchAPI",
     "Version":"2020-06-01",
     "Service":"livesaas",
     "Region":"ap-singapore-1" 
  },
   "Result":{
       "Status":true
  }
}
```
