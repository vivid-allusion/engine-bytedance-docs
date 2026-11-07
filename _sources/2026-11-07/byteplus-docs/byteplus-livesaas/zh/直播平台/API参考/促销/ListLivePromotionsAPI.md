---
title: "ListLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listlivepromotionsapi-zh-CN"
---

调用此 API 以获取已添加到指定直播流活动的第三方直播流推广平台列表。

<span id="ac70d9a3"></span>
## 请求

<span id="8f3ec89a"></span>
### 详情


* API 操作：`ListLivePromotionsAPI`

* 请求方式：GET

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=ListLivePromotionsAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="2fdeadeb"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播流活动的 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)操作获取该 ID。 |


<span id="63c837a9"></span>
### 请求示例

```JSON
Get https://livesaas.byteplusapi.com/?Action=ListLivePromotionsAPI&Version=2020-06-01&ActivityId=1231231231
```


<span id="33f74cf8"></span>
## 返回调用结果

<span id="55db58b6"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|LivePromotionsInfos |Array of[LivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listlivepromotionsapi-zh-CN#LivePromotionsInfos) |直播流推广平台列表。 |


<span id="13a56d96"></span>
#### **LivePromotionsInfos**


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Id |Integer |平台 ID。 |
|Name |String |平台名称。 |
|PushUrl |String |推流地址。 |
|Status |Integer |指定该平台是否已开启直播流推广。<br><br>有效值：<br><br><br>* `1`：已开启。<br><br>* `2`：未开启。 |


<span id="b6394dd7"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "ListLivePromotionsAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
            "LivePromotionsInfos":[ 
                  { 
                        "Id": 123, 
                        "Name": "Platform A", 
                        "PushUrl": "rtmp://example", 
                        "Status": 1 
                  } 
            ] 
      } 
} 
```


<span id="b117450f"></span>
## 错误码

常见错误码列表请参见[共享错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
