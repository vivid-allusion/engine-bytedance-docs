---
title: "DeleteLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletelivepromotionsapi-zh-CN"
---

该API用于在直播流活动中删除第三方直播推广平台。

<span id="3bd1cae3"></span>
## 请求

<span id="b4b95ba8"></span>
### 详情


* API接口行为：`DeleteLivePromotionsAPI`

* 请求方式：POST

* 请求URI：`https://livesaas.byteplusapi.com/?Action=DeleteLivePromotionsAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多120次查询


<span id="15273936"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API接口行为。 |
|Version |String |是 |该API接口行为的版本。当前版本：`2020-06-01`。 |


<span id="da228a08"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|ActivityId |Integer |是 |直播流活动的ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)获取ID。 |
|Id |Integer |是 |推广平台的ID。可通过调用[ListLivePromotionsAPI](https://docs.byteplus.com/byteplus-livesaas/docs/listlivepromotionsapi)获取ID。 |


<span id="6cafa432"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=DeleteLivePromotionsAPI&Version=2020-06-01
{ 
    "ActivityId": 1231231231, 
    "Id": 123 
} 
```


<span id="e05f6486"></span>
## 返回调用结果

<span id="696aa8bd"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|ActivityId |Integer |直播流活动的ID。 |


<span id="fc31d626"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "DeleteLivePromotionsAPI", 
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


<span id="fd33babb"></span>
## 错误码

常见错误码列表请参见[共享错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
