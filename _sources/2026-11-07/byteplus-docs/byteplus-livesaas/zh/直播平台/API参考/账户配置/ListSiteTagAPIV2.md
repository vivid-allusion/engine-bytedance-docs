---
title: "ListSiteTagAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-CN"
---

调用此 API 以获取在你的 BytePlus 账户下配置的所有 直播间 分类标签和文本标签的完整列表。

<span id="cfe8a431"></span>
## 请求

<span id="7160a064"></span>
### 详情


* API 行为：`ListSiteTagAPIV2`

* 请求方式：GET

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=ListSiteTagAPIV2&Version=2020-06-01`

* 配额：每个账户每分钟最多 120 次查询


<span id="e3183224"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见 [共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 行为。 |
|Version |String |是 |此 API 行为的版本。当前版本：`2020-06-01`。 |


<span id="db442151"></span>
### 请求示例

```JSON
Get https://livesaas.byteplusapi.com/?Action=ListSiteTagAPIV2&Version=2020-06-01
```


<span id="916b2c22"></span>
## 返回调用结果

<span id="426c0334"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|SiteTags |Array of[Tag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-CN#539ba0fe) |分类标签列表。 |
|TextSiteTags |Array of[TextTag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-CN#b066ce5e) |文本标签列表。 |


<span id="539ba0fe"></span>
#### Tag


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Name |String |分类标签名称。 |
|Value |Array of String |标签值。 |
|Show |Integer |已弃用。 |
|Index |Integer |分类标签在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序索引。 |


<span id="b066ce5e"></span>
#### TextTag


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Name |String |文本标签名称。 |
|Index |Integer |文本标签在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序索引。 |


<span id="d6c5e207"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "ListSiteTagAPIV2",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846 
    },
    "Result": {
        "SiteTags": [
            {
                "Index": 0,
                "Name": "Label 1",
                "Value": [
                    "A"
                ],
                "Show": 0
            },
            {
                "Index": 1,
                "Name": "Label 2",
                "Value": [
                    "B",
                    "C",
                    "D",
                    "E"
                ],
                "Show": 0
            }
        ],
        "TextSiteTags": [
            {
                "Index": 0,
                "Name": "Label 3"
            },
            {
                "Index": 1,
                "Name": "Label 4"
            }
        ]
    }
}
```


<span id="f43dff76"></span>
## 错误码

常见错误码列表请参见 [共享错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
