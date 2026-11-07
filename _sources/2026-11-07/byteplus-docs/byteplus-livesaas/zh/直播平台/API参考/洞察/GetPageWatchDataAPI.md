---
title: "GetPageWatchDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getpagewatchdataapi-zh-CN"
---

调用此 API 获取直播活动的基础数据，包括页面浏览量、独立访客数、总访问时长、每位访客的平均访问时长，以及每位访客的页面浏览量。数据每五分钟更新一次。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 行为：`GetPageWatchDataAPI`

* 请求方式：GET

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=GetPageWatchDataAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 1,000 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 行为。 |
|Version |String |是 |此 API 行为的版本。当前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播活动的 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)获取该 ID。 |
|Source |Integer |否 |指定返回数据的来源。默认值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有地址的数据。<br><br>* `0`：仅返回默认地址的数据。<br><br>* `1`：仅返回地址 A 的数据。<br><br>* `2`：仅返回地址 B 的数据。<br><br>* `3`：仅返回地址 C 的数据。<br><br>* `4`：仅返回地址 D 的数据。 |


<span id="Sample request"></span>
### 请求示例

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetPageWatchDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|ActivityId |Integer |直播活动的 ID。 |
|PageClicks |PageClicks 对象[PageClicks](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getpagewatchdataapi-zh-CN#PageClicks) |包含直播活动的基础数据。 |


<span id="PageClicks"></span>
#### PageClicks


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|PV |Integer |页面浏览量。 |
|UV |Integer |独立访客数。 |
|TotalTime |Integer |总访问时长（单位：分钟）。 |
|AvgTime |Float |每位访客的平均访问时长（单位：分钟）。 |
|AvgNumber |Float |每位访客的平均页面浏览量。 |
|Pcu |Integer |峰值同时在线访客数。 |


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetPageWatchDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result": {
        "ActivityId": 1231231231,
        "PageClicks": { 
            "PV": 33,
            "UV": 7, 
            "TotalTime": 844, 
            "AvgTime": 120.57142857142857, 
            "AvgNumber": 4.714285714285714,  
            "Pcu": 1  
        }
    }
}
```


<span id="c8a9401d"></span>
## 错误码

常见错误码列表请参见[共享错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
