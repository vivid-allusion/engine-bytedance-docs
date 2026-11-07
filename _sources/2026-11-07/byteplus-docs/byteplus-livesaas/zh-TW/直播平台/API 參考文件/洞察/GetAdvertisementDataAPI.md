---
title: "GetAdvertisementDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getadvertisementdataapi-zh-TW"
---

獲取直播活動的行銷數據。數據每五分鐘更新一次。

<span id="d4dafd6e"></span>
## 請求

<span id="9623f49a"></span>
### 詳細資訊


* API 操作：`GetAdvertisementDataAPI`

* 請求方法：GET

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=GetAdvertisementDataAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="be58fd4e"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播活動的 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)獲取 ID。 |
|Source |Integer |否 |指定要返回的數據來源。預設值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有地址的數據。<br><br>* `0`：僅返回預設地址的數據。<br><br>* `1`：僅返回地址 A 的數據。<br><br>* `2`：僅返回地址 B 的數據。<br><br>* `3`：僅返回地址 C 的數據。<br><br>* `4`：僅返回地址 D 的數據。 |


<span id="f1bb0c6c"></span>
### 請求範例

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetAdvertisementDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="ff6e95c8"></span>
## 回應

<span id="6d62ca05"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|ActivityId |Integer |直播活動的 ID。 |
|AccountClicks |[ClicksStruct](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#ClicksStruct) |品牌帳號的點擊數據。 |
|AdvertisingClicks |[ClicksStruct](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#ClicksStruct) |廣告的點擊數據。 |
|AdInfo |[AdInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#AdInfo) 陣列 |廣告的詳細數據。 |
|ShowThumbUpNumber |Integer |直播活動在觀看頁面顯示的虛擬按讚數。 |
|ActualThumbUpNumber |Integer |直播活動的實際按讚數。 |


<span id="b664a990"></span>
#### ClicksStruct


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|PV |Integer |頁面瀏覽量。 |
|UV |Integer |獨立訪客數。 |
|TotalTime |Integer |已棄用。 |


<span id="f8766d4b"></span>
#### AdInfo


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|PageAdvertiseType |Integer |表示廣告類型。<br><br>有效值：<br><br><br>* `1`：頁首廣告。<br><br>* `2`：頁內廣告。<br><br>* `3`：浮動廣告。<br><br>* `4`：商品卡片廣告。 |
|Content |String |廣告內容。 |
|Link |String |廣告連結。 |
|Title |String |廣告標題。 |
|PV |Integer |廣告的頁面瀏覽量。 |
|UV |Integer |廣告的獨立訪客數。 |


<span id="d7e7b340"></span>
### 回應範例

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
## 錯誤碼

常見錯誤碼請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
