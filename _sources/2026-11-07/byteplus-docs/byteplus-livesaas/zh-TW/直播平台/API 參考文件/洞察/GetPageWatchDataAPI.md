---
title: "GetPageWatchDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getpagewatchdataapi-zh-TW"
---

調用此 API 以獲取直播活動的基礎數據，包括頁面瀏覽量、獨立訪客、總訪問時長、每位訪客的平均訪問時長，以及每位訪客的頁面瀏覽量。數據每五分鐘更新一次。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`GetPageWatchDataAPI`

* 請求方法：GET

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=GetPageWatchDataAPI&Version=2020-06-01`

* 配額：每個帳號每分鐘 1,000 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播活動的 ID。可通過調用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)獲取 ID。 |
|Source |Integer |否 |指定要返回的數據來源。預設值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有地址的數據。<br><br>* `0`：僅返回預設地址的數據。<br><br>* `1`：僅返回地址 A 的數據。<br><br>* `2`：僅返回地址 B 的數據。<br><br>* `3`：僅返回地址 C 的數據。<br><br>* `4`：僅返回地址 D 的數據。 |


<span id="Sample request"></span>
### 請求範例

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetPageWatchDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|ActivityId |Integer |直播活動的 ID。 |
|PageClicks |Object of[PageClicks](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getpagewatchdataapi-zh-TW#PageClicks) |包含該直播活動的基礎數據。 |


<span id="PageClicks"></span>
#### PageClicks


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|PV |Integer |頁面瀏覽量。 |
|UV |Integer |獨立訪客。 |
|TotalTime |Integer |總訪問時長（分鐘）。 |
|AvgTime |Float |每位訪客的平均訪問時長（分鐘）。 |
|AvgNumber |Float |每位訪客的平均頁面瀏覽量。 |
|Pcu |Integer |同時在線訪客峰值。 |


<span id="Sample response"></span>
### 回應範例

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
## 錯誤碼

常見錯誤碼請參見[通用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
