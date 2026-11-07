---
title: "ListActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi-zh-TW"
---

獲取您帳戶下所有現有直播間的基本資訊。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">此 API 操作最多可返回 10,000 個最新的直播間。您可以配置如房間狀態（<code>Status</code>）和直播時間（<code>LiveTime</code>）等條件來篩選搜尋結果。</div>


<span id="94c6bae7"></span>
## 需求

頻率限制：每個帳戶每分鐘 120 次請求

<span id="155ffcd9"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ListActivityAPI&Version=2020-06-01`

* 方法：POST


<span id="f551b2af"></span>
## 請求參數

下列表格未包含所有常用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="5a6525f9"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ListActivityAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |API 操作的版本。本操作的值為`2020-06-01`。 |


<span id="33219538"></span>
### 主體


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|PageNo |Integer |否 |`1` |要返回的頁碼。預設值：`1`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此 API 操作最多支援返回 10,000 筆結果，這表示 <code>PageNo</code> × <code>PageItemCount</code> 必須小於或等於 10,000。</div><br> |
|PageItemCount |Integer |否 |`10` |每頁返回的結果數量。預設值：`10`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此 API 操作最多支援返回 10,000 筆結果，這表示 <code>PageNo</code> × <code>PageItemCount</code> 必須小於或等於 10,000。</div><br> |
|名稱 |String |否 |`Live Room A` |返回名稱包含此值的直播間。<br><br>例如，若參數值為`Live Room A`，則返回名稱中包含關鍵字 Live Room A 的直播間，如 Live Room ABC、Live Room a 和 live room ab。 |
|Status |Integer |否 |`0` |返回指定狀態的直播間。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：全部。<br><br>* `1`：直播中。<br><br>* `2`：預告。<br><br>* `3`：回放。<br><br>* `4`：已結束。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Over 是指直播串流已結束但尚未釋出回放至觀看頁面的狀態。</div><br> |
|LiveTime |Long |否 |`1680193976` |以 Unix 時間戳格式表示的直播時間。單位：秒。<br><br>返回直播時間大於或等於此值的直播間。<br><br>此時間不一定為實際開播時間。 |
|IsLockPreview |Integer |否 |`0` |指定是否返回預覽被鎖定的直播間。預設值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有直播間。<br><br>* `0`：返回預覽未鎖定的直播間。<br><br>* `1`：返回預覽已鎖定的直播間。 |
|SiteTagNews |SiteTagNews 的陣列[SiteTagNews](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW#11ffe97f) |否 |`-` |返回包含任一這些分類標籤值的直播間。<br><br>可透過調用[ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-TW)獲取分類標籤列表。 |
|HostAccountId |Integer |否 |`112038` |主播帳戶的 ID。<br><br>返回與該主播帳戶關聯的直播間。<br><br>可透過調用[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi)獲取 ID。 |
|HostAccountName |String |否 |`Host A` |主播帳戶名稱。支援模糊搜尋。<br><br>返回與該主播帳戶關聯的直播間。<br><br>可透過調用[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi)獲取名稱。 |
|LiveMode |Integer |否 |`0` |返回指定直播延遲類型的直播間。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：超低延遲與普通延遲皆包含。<br><br>* `1`：超低延遲（延遲 1 至 2 秒）。<br><br>* `2`：普通延遲（延遲 5 至 10 秒）。 |
|SortBy |String |否 |`Status` |直播間排序規則。預設值：`Status`。有效值：<br><br><br>* `Status`：先按直播間狀態排序，再於每個狀態內依直播間開始時間倒序排列。<br><br>* `LiveTime`：依據直播間的開始時間排序。<br><br>* `CreateTime`：依據直播間的建立時間排序。 |
|SortOrder |字串 |否 |`Desc` |直播間排序的順序。預設值：`Asc`。有效值：<br><br><br>* `Desc`：降序。<br><br>* `Asc`：升序。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>SortBy</code> 設為 <code>Status</code> 時，結果會依狀態分組並以升序排列（Live、Preview、Playback、Over）。在每個分組內，直播間皆會依開始時間以降序排列，不論 <code>SortOrder</code> 的值為何。</div><br> |
|FollowerUserName |字串 |否 |`admin@bytedance.com` |用於建立直播間的帳號。預設情況下，會返回所有帳號建立的直播間。若需取得 BytePlus 帳號建立的直播間，請將參數值設為`admin@bytedance.com`。若需取得特定 IAM 使用者建立的直播間，請將參數值設為該 IAM 使用者的帳號。可於**帳號中心** \> **授權** \> **使用者**頁面，在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/accountManagement/userManage)取得 IAM 使用者的帳號。 |


<span id="11ffe97f"></span>
#### SiteTagNews


|Name |資料型別 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Value |字串陣列 |是 |`["1","2"]` |分類標籤值。<br><br>會返回包含任一分類標籤值的直播間。 |
|Name |字串 |否 |`Tag A` |分類標籤名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請指定 <code>Name</code> 或 <code>Index</code> 其中之一。若同時提供兩者，則以 <code>Name</code> 為優先。若皆未提供，則使用 <code>Index</code> 的預設值。</div><br> |
|Index |整數 |否 |`0` |分類標籤的索引，用於標識在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。<br><br>預設值：`0`。值域：[0,19]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請指定 <code>Name</code> 或 <code>Index</code> 其中之一。若同時提供兩者，則以 <code>Name</code> 為優先。若皆未提供，則使用 <code>Index</code> 的預設值。</div><br> |


<span id="1f1dafcd"></span>
## 回應參數


|Name |資料型別 |範例值 |描述 |
|---|---|---|---|
|PageNo |整數 |`1` |返回頁面的頁碼。 |
|PageItemCount |整數 |`10` |每頁返回的結果數量。 |
|TotalItemCount |整數 |`1` |返回的直播間總數。 |
|Activities |字串陣列[Activities](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW#521ce1cd) |`-` |返回的直播間列表。 |


<span id="521ce1cd"></span>
### Activities


|Name |資料型別 |範例值 |描述 |
|---|---|---|---|
|Id |長整數 |`17218346****` |返回直播間的活動 ID。 |
|Name |字串 |`Live Room A` |返回直播間的名稱。 |
|Status |整數 |`1` |返回直播間的狀態。<br><br><br>* `1`：直播中。<br><br>* `2`：預覽。<br><br>* `3`：回放。<br><br>* `4`：結束。 |
|CoverImage |字串 |`https://p1-live.****.image` |返回直播間橫版封面圖片的 URL，包含協議頭。 |
|CreateTime |整數 |`1680093000` |返回直播間建立的時間，Unix 時間戳格式。單位：秒。 |
|ViewUrl |字串 |`https://live.byteplus.com/7420/******` |返回直播間的觀看頁面地址。 |
|LiveTime |整數 |`1680193976` |直播時間，Unix 時間戳格式。單位：秒。<br><br>此時間可能不是直播實際開始的時間。 |
|StreamStartTime |整數 |`1681094000` |返回直播間最後一次推流的時間，Unix 時間戳格式。單位：秒。<br><br>若值為`0`，表示從未推流。<br><br>此時間為直播實際開始的時間。 |
|OnlineStatus |整數 |`-` |已棄用。 |
|IsLockPreview |整數 |`0` |表示返回的直播間預覽是否鎖定。<br><br><br>* `0`：預覽未鎖定。<br><br>* `1`：預覽已鎖定。 |
|SiteTags |字串陣列[SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW#0afe12a2) |`-` |返回直播間的分類標籤列表。 |
|TextSiteTags |字串陣列[TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW#3c3d5d47) |`-` |返回直播間的文字標籤列表。 |
|HostAccountId |整數 |`112038` |與返回直播間關聯的主持人帳號 ID。 |
|HostAccountName |字串 |`Host A` |與返回直播間關聯的主持人帳號名稱。 |
|LiveMode |整數 |`0` |返回的直播間的串流延遲類型。<br><br><br>* `0`：若直播間是在 BytePlus Live 支援超低延遲功能之前建立，且未更新串流延遲類型，則參數值為 `0`。換句話說，延遲類型為一般延遲。如需超低延遲功能的詳細資訊，請參閱 [超低延遲直播串流](https://docs.byteplus.com/docs/byteplus-livesaas/chao-di-yan-chi-zhi-bo-zh-TW)。<br><br>* `1`：超低延遲，延遲為 1 至 2 秒。<br><br>* `2`：一般延遲，延遲為 5 至 10 秒。 |
|VerticalCoverImage |String |`https://p2-live.xxxx.image` |返回的直播間直式封面圖片的 URL，包含協議標頭。 |
|SubAccountName |String |`admin@bytedance.com` |用於建立直播間的帳戶。參數值 `admin@bytedance.com` 表示該直播間由 BytePlus 帳戶建立。 |


<span id="0afe12a2"></span>
#### SiteTags


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Tag A` |分類標籤名稱。 |
|Value |String |`1` |分類標籤值。 |
|Index |Integer |`0` |分類標籤的索引，用於識別在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。 |
|DbIndex |Integer |`-` |已棄用。 |
|Show |Integer |`-` |已棄用。 |
|Id |Integer |`-` |已棄用。 |


<span id="3c3d5d47"></span>
#### TextSiteTags


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Tag B` |文字標籤名稱。 |
|Value |String |`3` |文字標籤值。 |
|Index |Integer |`0` |文字標籤的索引，用於識別在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。 |
|DbIndex |Integer |`-` |已棄用。 |
|Show |Integer |`-` |已棄用。 |
|Id |Integer |`-` |已棄用。 |


<span id="216bc15e"></span>
## 範例

<span id="946926a2"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=ListActivityAPI&Version=2020-06-01
{ 
    "PageNo": 1, 
    "PageItemCount": 10, 
    "SiteTagNews": [ 
            { 
                  "Index": 0, 
                  "Value": ["1","2"] 
            } 
    ]    
} 
```


<span id="468be8d1"></span>
### 範例回應

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202201201826170101501312091D1C09D2",
    "Action": "ListActivityAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1690293975
  },
  "Result": {
    "PageNo": 1,
    "PageItemCount": 10,
    "TotalItemCount": 1,
    "Activities": [
      {
        "Id": 17218346****,
        "Name": "Live Room A",
        "Status": 1,
        "CoverImage": "https://p1-live.****.image",
        "CreateTime": 1680093000,
        "ViewUrl": "https://live.byteplus.com/7420/******",
        "LiveTime": 1680193976,
        "StreamStartTime": 1681094000,
        "IsLockPreview": 0,
        "SiteTags": [
          {
            "Index": 0,
            "Name": "Tag A",
            "Value": 1,
            "DbIndex": 1,
            "Show": 0,
            "Id": 0
          }
        ],
        "TextSiteTags": [
          {
            "Index": 0,
            "Name": "Tag B",
            "Value": "3",
            "DbIndex": 1,
            "Show": 0,
            "Id": 0
          }
        ],
        "HostAccountId": 112038,
        "HostAccountName": "Host A",
        "LiveMode": 0,  
        "VerticalCoverImage": "https://p2-live.****.image",      
        "OnlineStatus": 0,
        "SubAccountName": "admin@bytedance.com"
      }
    ]
  }
}
```


<span id="38ee38c5"></span>
## 錯誤碼

常見錯誤碼列表請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
