---
title: "UpdateLivePromotionsStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatelivepromotionsstatusapi-zh-CN"
---

用于更新直播活动中第三方平台的分发状态，以指定该平台是否已开启直播流推广。

<span id="e3f87cdb"></span>
## 请求

<span id="bfd37204"></span>
### 详情


* API 接口行为：`UpdateLivePromotionsStatusAPI`

* 请求方式：POST

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateLivePromotionsStatusAPI&Version=2020-06-01`

* 配额：每个账号每分钟 120 次查询


<span id="4486e7e1"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |字符串 |是 |API 接口行为。 |
|Version |字符串 |是 |该 API 接口行为的版本。当前版本：`2020-06-01`。 |


<span id="5f330622"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|ActivityId |整数 |是 |直播活动的 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)获取该 ID。 |
|Id |整数 |是 |平台 ID。可通过调用[ListLivePromotionsAPI](https://docs.byteplus.com/byteplus-livesaas/docs/listlivepromotionsapi)获取该 ID。 |
|Status |整数 |是 |指定该平台是否已开启直播流推广。<br><br>有效取值：<br><br><br>* `1`：已开启。<br><br>* `2`：未开启。 |


<span id="3c33a17e"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateLivePromotionsStatusAPI&Version=2020-06-01
{ 
    "ActivityId": 1231231231, 
    "Id": 12, 
    "Status": 1 
} 
```


<span id="4713a872"></span>
## 返回调用结果

<span id="1d1c8f48"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|ActivityId |整数 |直播活动的 ID。 |


<span id="104a3dd9"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "UpdateLivePromotionsStatusAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
            "ActivityId": 1231231231 
      } 
} 
```


<span id="d3b604ed"></span>
## 错误码

常见错误码请参见[共享错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
