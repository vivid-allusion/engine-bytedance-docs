---
title: "ListAnActivityStartAndEndTimeAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi-zh-TW"
---

呼叫此 API 以取得特定直播間中每場直播的開始與結束時間。

<span id="f270d7d5"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="b9c6469a"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ListAnActivityStartAndEndTimeAPI&Version=2020-06-01`

* 方法：GET


<span id="924137a8"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="70cc26ca"></span>
### 查詢


|名稱 |資料型態 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ListAnActivityStartAndEndTimeAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218346****` |直播間的活動 ID。你可以透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |


<span id="0b7c1c03"></span>
## 回應參數


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|StartAndEndTime |Array of[StartAndEndTime](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi-zh-TW#f3921d52) |`-` |每場直播的開始與結束時間。 |


<span id="f3921d52"></span>
### StartAndEndTime


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|OrderNumber |Integer |`1` |直播開始與結束時間的序號，表示其發生的順序。 |
|StartTime |Long |`1625811440` |直播開始時的 Unix 時間戳（秒）。 |
|EndTime |Long |`1625811571` |直播結束時的 Unix 時間戳（秒）。<br><br>值 `0` 表示直播尚未結束。 |


<span id="b2bcadd6"></span>
## 範例

<span id="c8a1ed92"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAnActivityStartAndEndTimeAPI&Version=2020-06-01&ActivityId=17218346****
```


<span id="61b76c18"></span>
### 範例回應

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
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
