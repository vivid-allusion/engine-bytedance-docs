---
title: "GetActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityapi-zh-TW"
---

調用 GetActivityAPI 操作以獲取直播間的基本資訊，例如其狀態和觀看頁面地址。

<span id="4aadd724"></span>
## 需求

配額：每個帳戶每分鐘 120 次查詢

<span id="d6e36402"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01`

* 方法：GET


<span id="f9f8d76a"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="68bc6a19"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218346****` |直播間的活動 ID。可通過調用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW)獲取 ID。 |


<span id="42fd3547"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|Id |Long |`17218346****` |直播間的活動 ID。 |
|名稱 |String |`直播間 A` |直播間名稱。 |
|LiveTime |Long |`1642070520` |直播開始時間，Unix 時間戳格式。單位：秒。<br><br>此時間可能不是實際的直播開始時間。 |
|IsBeginLiveEnable |Integer |`0` |指示是否啟用預定開始時間。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。僅可在指定開始時間後開始直播。 |
|IsAutoEndEnable |Integer |`1` |指示是否配置為在指定時間自動結束直播。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|EndTime |Long |`1642170520` |直播結束時間，Unix 時間戳格式。單位：秒。 |
|CoverImage |String |`//example.image` |橫向封面圖片的 URL。<br><br>若通過 API 調用配置，URL 包含協議頭；若通過控制台配置，則不包含。 |
|VerticalCoverImage |String |`//example.image` |縱向封面圖片的 URL。<br><br>如未指定，預設為 `CoverImage` 的值。<br><br>若通過 API 調用配置，URL 包含協議頭；若通過控制台配置，則不包含。 |
|Status |Integer |`2` |直播間狀態。<br><br>有效值：<br><br><br>* `1`：直播中。<br><br>* `2`：預覽中。<br><br>* `3`：回放中。<br><br>* `4`：已結束。 |
|ViewUrl |String |`https://live.byteplus.com/7420/*******` |直播間觀看頁面的 URL。 |
|IsPageViewEnable |Integer |`-` |已棄用。 |
|IsLockPreview |Integer |`1` |指示預覽是否被鎖定。<br><br>有效值：<br><br><br>* `0`：預覽未鎖定。<br><br>* `1`：預覽已鎖定。在**預覽**狀態下，觀看頁面被鎖定，無法播放直播或回放。 |
|OwnerSubAccount |String |`admin@bytedance.com` |創建該直播間的帳戶。若此值為`admin@example.com`，則該直播間由您的主 BytePlus 帳戶創建。 |
|LiveMode |Integer |`1` |直播延遲類型。<br><br>有效值：<br><br><br>* `1`：超低延遲，延遲 1 至 2 秒。<br><br>* `2`：普通延遲，延遲 5 至 10 秒。 |


<span id="a22e2b63"></span>
## 範例

<span id="85d6db4f"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=17218346****
```


<span id="291767b7"></span>
### 回應範例

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetActivityAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1",
        "SystemTime":1632070520
    },
    "Result":{
        "Id":17218346****,      
        "Name":"Live Room A",
        "LiveTime":1642070520,
        "IsBeginLiveEnable": 0,
        "EndTime": 1642170520,
        "IsAutoEndEnable": 1,
        "CoverImage":"//example.image",
        "VerticalCoverImage":"//example.image",
        "Status":2,
        "ViewUrl":"https://live.byteplus.com/7420/*******", 
        "IsPageViewEnable"：1,
        "IsLockPreview":1,  
        "OwnerSubAccount":"admin@bytedance.com",
        "LiveMode":1        
    }
}
```


<span id="6703fc71"></span>
## 錯誤碼

共用錯誤碼列表請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
