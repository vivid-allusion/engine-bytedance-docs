---
title: "ListAnActivityStartAndEndTimeAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi-zh-CN"
---

调用此 API 可获取指定直播间中每个已发生直播流的开始和结束时间。

<span id="f270d7d5"></span>
## 需求

配额：每个账号每分钟 120 次查询

<span id="b9c6469a"></span>
## HTTP 请求


* URL: `https://livesaas.byteplusapi.com/?Action=ListAnActivityStartAndEndTimeAPI&Version=2020-06-01`

* 方法：GET


<span id="924137a8"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="70cc26ca"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`ListAnActivityStartAndEndTimeAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218346****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="0b7c1c03"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|StartAndEndTime |Array of[StartAndEndTime](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi-zh-CN#f3921d52) |`-` |每个直播流的开始和结束时间。 |


<span id="f3921d52"></span>
### StartAndEndTime


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|OrderNumber |Integer |`1` |直播流开始和结束时间的序号，表示发生的顺序。 |
|StartTime |Long |`1625811440` |直播流开始时的 Unix 时间戳（秒）。 |
|EndTime |Long |`1625811571` |直播流结束时的 Unix 时间戳（秒）。<br><br>值 `0` 表示直播流尚未结束。 |


<span id="b2bcadd6"></span>
## 示例

<span id="c8a1ed92"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAnActivityStartAndEndTimeAPI&Version=2020-06-01&ActivityId=17218346****
```


<span id="61b76c18"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202201201826170101501312091D1C09D2",
    "Action": "ListAnActivityStartAndEndTimeAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656067132
  },
  "Result": {
    "StartAndEndTime": [
      {
        "OrderNumber": 1,
        "StartTime": 1625811440,
        "EndTime": 1625811571
      },
      {
        "OrderNumber": 2,
        "StartTime": 1625811609,
        "EndTime": 1626405481
      },
      {
        "OrderNumber": 3,
        "StartTime": 1626405692,
        "EndTime": 0
      }
    ]
  }
}
```


<span id="5a39ebb7"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
