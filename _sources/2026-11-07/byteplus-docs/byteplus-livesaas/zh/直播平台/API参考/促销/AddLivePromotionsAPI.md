---
title: "AddLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-CN"
---

调用此 API，可为直播活动添加多个第三方平台，实现同步直播。平台添加完成且活动流开始后，BytePlus Live 会自动将流推送至该平台，帮助你扩大观众覆盖范围。

<span id="f6dba5d6"></span>
## 请求

<span id="46fe124d"></span>
### 详情


* API 行为：`AddLivePromotionsAPI`

* 请求方式：POST

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=AddLivePromotionsAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="4136eabc"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整参数列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 行为。 |
|Version |String |是 |此 API 行为的版本。当前版本：`2020-06-01`。 |


<span id="d4b8acb3"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|ActivityId |Integer |是 |直播活动的 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)获取该 ID。 |
|AddLivePromotionsInfos |Array of[AddLivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-CN#AddLivePromotionsInfos) |是 |要添加用于直播流推广的第三方平台列表。 |


<span id="0b56e510"></span>
#### **AddLivePromotionsInfos**


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Name |String |是 |平台名称。最大长度为 100 个字符。 |
|PushUrl |String |是 |推流地址。 |


<span id="19bbf454"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=AddLivePromotionsAPI&Version=2020-06-01
{ 
    "ActivityId": 1231231231, 
    "AddLivePromotionsInfos":[ 
        { 
             "Name": "Platform A", 
             "PushUrl": "rtmp://example" 
        } 
    ] 
} 
```


<span id="19cab44c"></span>
## 返回调用结果

<span id="d13b0166"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|LivePromotionsInfos |Array of[LivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-CN#LivePromotionsInfos) |已添加平台的详细信息。 |


<span id="46024ed2"></span>
#### **LivePromotionsInfos**


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Id |Integer |平台 ID。 |
|Name |String |平台名称。 |
|PushUrl |String |推流地址。 |
|Status |Integer |表示该平台是否已开启直播流推广。<br><br>有效值：<br><br><br>* `1`：已开启。<br><br>* `2`：未开启。 |


<span id="96d00acd"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "AddLivePromotionsAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
        "LivePromotionsInfos": [ 
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


<span id="a499fffb"></span>
## 错误码

常见错误码列表请参见[通用错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
