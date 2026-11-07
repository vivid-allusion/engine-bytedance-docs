---
title: "GetAdvertisementDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getadvertisementdataapi-zh-CN"
---

获取直播活动的营销数据。数据每五分钟更新一次。

<span id="d4dafd6e"></span>
## 请求

<span id="9623f49a"></span>
### 详情


* API 接口行为：`GetAdvertisementDataAPI`

* 请求方式：GET

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=GetAdvertisementDataAPI&Version=2020-06-01`

* 配额：每个账号每分钟 120 次查询


<span id="be58fd4e"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 接口行为。 |
|Version |String |是 |本 API 接口行为的版本。当前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播活动的 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)获取 ID。 |
|Source |Integer |否 |指定要返回的数据来源。默认值：`0`。<br><br>可选值：<br><br><br>* `-1`：返回所有地址的数据。<br><br>* `0`：仅返回默认地址的数据。<br><br>* `1`：仅返回地址 A 的数据。<br><br>* `2`：仅返回地址 B 的数据。<br><br>* `3`：仅返回地址 C 的数据。<br><br>* `4`：仅返回地址 D 的数据。 |


<span id="f1bb0c6c"></span>
### 请求示例

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetAdvertisementDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="ff6e95c8"></span>
## 返回调用结果

<span id="6d62ca05"></span>
### 返回结构说明


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|ActivityId |Integer |直播活动的 ID。 |
|AccountClicks |[ClicksStruct](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#ClicksStruct) |品牌账号的点击数据。 |
|AdvertisingClicks |[ClicksStruct](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#ClicksStruct) |广告的点击数据。 |
|AdInfo |[AdInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#AdInfo) 数组 |广告的详细数据。 |
|ShowThumbUpNumber |Integer |直播活动在观看页展示的虚拟点赞数。 |
|ActualThumbUpNumber |Integer |直播活动的实际点赞数。 |


<span id="b664a990"></span>
#### ClicksStruct


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|PV |Integer |页面浏览量。 |
|UV |Integer |独立访客数。 |
|TotalTime |Integer |已废弃。 |


<span id="f8766d4b"></span>
#### AdInfo


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|PageAdvertiseType |Integer |表示广告类型。<br><br>可选值：<br><br><br>* `1`：页头广告。<br><br>* `2`：页中广告。<br><br>* `3`：浮标广告。<br><br>* `4`：商品卡片广告。 |
|Content |String |广告内容。 |
|Link |String |广告链接。 |
|Title |String |广告标题。 |
|PV |Integer |广告的页面浏览量。 |
|UV |Integer |广告的独立访客数。 |


<span id="d7e7b340"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetAdvertisementDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681977443
    },
    "Result": {
        "ActivityId": 1231231231,
        "AccountClicks": {
            "PV": 6,
            "UV": 2,
            "TotalTime": 0
        },
        "AdvertisingClicks": {
            "PV": 6,
            "UV": 1,
            "TotalTime": 0
        },
        "AdInfo": [
            {
                "PageAdvertiseType": 3,
                "Content": "//p16-live-sg.ibyteimg.com/xxx/xxx-image.image",
                "Link": "www.example.com",
                "PV": 1,
                "UV": 1,
                "Title": ""
            },
            {
                "PageAdvertiseType": 1,
                "Content": "",
                "Link": "www.example.com",
                "PV": 1,
                "UV": 1,
                "Title": ""
            },
            {
                "PageAdvertiseType": 2,
                "Content": "//p16-live-sg.ibyteimg.com/xxx/xxx-image.image",
                "Link": "www.example.com",
                "PV": 0,
                "UV": 0,
                "Title": ""
            },
            {
                "PageAdvertiseType": 4,
                "Content": "//p16-live-sg.ibyteimg.com/xxx/xxx-image.image",
                "Link": "www.example.com",
                "PV": 3,
                "UV": 1,
                "Title": "Product A"
            }
        ],
        "ShowThumbUpNumber": 30,
        "ActualThumbUpNumber": 20
    }
}
```


<span id="7155c925"></span>
## 错误码

常见错误码请参见[通用错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
