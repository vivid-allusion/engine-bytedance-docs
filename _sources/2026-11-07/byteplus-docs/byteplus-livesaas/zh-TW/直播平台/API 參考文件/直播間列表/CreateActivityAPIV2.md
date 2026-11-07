---
title: "CreateActivityAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW"
---

要以程式方式建立直播間，可以呼叫 CreateActivityAPIV2 API。此 API 可用於從零開始建立新的直播間、從預先設定的範本建立，或複製現有直播間來建立。建立成功後，API 會回傳唯一的活動 ID，可搭配其他 API 使用，以管理和自訂直播間。

<span id="c32fa550"></span>
## 需求

配額：每個帳號每分鐘 120 次查詢

<span id="f1645296"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01`

* 方法：POST


<span id="fa579d1b"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整清單請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="e1d4ffd4"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`CreateActivityAPIV2` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。請設為`2020-06-01`。 |


<span id="8dfefedc"></span>
### 主體


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|名稱 |String |是 |`Live Room A` |要建立的直播間名稱，不能超過 1950 個字元。 |
|LiveTime |Long |否 |`1680193976` |直播開始時間，採用 Unix 時間戳格式。單位：秒。時間可精確到分鐘。<br><br>預設值：當前時間。<br><br>這是預定的開始時間，實際開播時間可能有所不同。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>LiveTime</code> 必須早於 <code>EndTime</code>，最大差值為 259,200（72 小時）。</div><br> |
|IsBeginLiveEnable |Integer |否 |`0` |指定是否強制執行預定開始時間。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。只能在指定的開始時間之後才能開啟直播。 |
|IsAutoEndEnable |Integer |否 |`0` |指定是否在指定的 EndTime 自動結束直播。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若即將透過複製現有直播間來建立新直播間，則現有直播間的此配置不會複製到新直播間。你可以使用此參數配置新直播間是否啟用此功能。</div><br> |
|EndTime |Long |否 |`1680293976` |直播結束時間，採用 Unix 時間戳格式。單位：秒。時間可精確到分鐘。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>EndTime</code> 必須晚於 <code>LiveTime</code>，最大差值為 259,200（72 小時）。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>IsAutoEndEnable</code> 的值為 <code>1</code> 時，此參數為必填且有效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">複製直播間時，此設定不會從原直播間繼承。請使用此參數配置新直播間的結束時間。</div><br> |
|LiveMode |Integer |否 |`2` |直播延遲型態。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：超低延遲或一般延遲，與直播間範本設定的型態一致。<br><br>* `1`：超低延遲，延遲 1 至 2 秒。<br><br>* `2`：一般延遲，延遲 5 至 10 秒。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若指定 <code>OldId</code>，則此參數會被忽略。此時，新直播間將與被複製的原直播間配置相同的延遲類型。</div><br> |
|ViewUrlPath |String |否 |`1234` |觀看頁面地址由基礎 URL（例如 `https://DomainName/****/`）加上`ViewUrlPath`組成。例如，若參數值為`abc`，則觀看頁面地址為`https://DomainName/****/abc`。若未指定，系統會自動產生隨機值。<br><br>長度必須在 [1, 20] 個字元內。支援的字元包括：<br><br><br>* 大寫英文字母 A–Z<br><br>* 小寫英文字母 a–z<br><br>* 數字 |
|CoverImage |String |否 |`https://tplv-gjr25qtd0-image.image` |直播間橫式封面圖片的 URL。若未指定，將使用預設封面圖片。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">通常，參數值需為帶有協議頭的 URL。然而，如果你取得透過<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>上傳的圖片 URL（例如，透過呼叫<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW">GetActivityBasicConfigAPI</a>來獲取在直播間中透過控制台上傳的封面圖片 URL），則無協定標頭的 URL 也可以作為參數值使用。</div><br> |
|VerticalCoverImage |String |否 |`https://gjr293lqtd0-image.image` |直播間直式封面圖片的 URL。若未指定，參數值與`CoverImage`相同。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">通常，作為參數值時需要帶有協定標頭的 URL。然而，如果你取得透過<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>上傳的圖片 URL（例如，透過呼叫<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW">GetActivityBasicConfigAPI</a>來獲取在直播間中透過控制台上傳的封面圖片 URL），則無協定標頭的 URL 也可以作為參數值使用。</div><br> |
|OldId |Long |否 |`17218346****` |要複製其設定到此新直播間的現有直播間活動 ID。你可以透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得 ID。<br><br>若要將現有直播間的配置複製到新直播間，則此參數為必填。 |
|CopyStream |Boolean |否 |`true` |指定在複製現有直播間時是否複製直播流。<br><br>預設值：`false`。<br><br>有效值：<br><br><br>* `true`：複製直播流。<br><br>* `false`：不複製直播流。 |
|TemplateId |Long |否 |`4984658` |直播間範本的 ID。新直播間將擁有與範本相同的配置。你可以透過呼叫 [GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-TW) 取得 ID。若省略此參數，則會使用預設範本。若不存在預設範本，則會建立無範本的直播間。<br><br>若要根據範本建立直播間，則此參數為必填。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">如果你設定了參數<code>OldId</code>的值，則此參數無效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如果範本包含大量抽獎配置，並且你想要複製基於該範本建立的直播間，請在直播間建立後至少等待 5 分鐘再進行複製。否則，抽獎配置可能無法被完整複製。</div><br> |
|SiteTags |Array of[SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW#32668f3e) |否 |`-` |直播間中的分類標籤列表。你可以透過呼叫 [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-TW) 取得支援的分類標籤。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果你即將透過複製現有直播間來建立新的直播間，則現有直播間所配置的分類標籤值將不會複製到新直播間。你可以使用此參數為新直播間配置分類標籤值。</div><br> |
|TextSiteTags |Array of[TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW#f895d19c) |否 |`-` |直播間中的文字標籤列表。你可以透過呼叫 [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-TW) 取得支援的文字標籤。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果你即將透過複製現有直播間來建立新的直播間，則現有直播間所配置的文字標籤值將不會複製到新直播間。你可以使用此參數為新直播間配置文字標籤值。</div><br> |


<span id="32668f3e"></span>
#### SiteTags


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |String |是 |1 |分類標籤的值。 |
|Index |Integer |是 |0 |分類標籤的索引，決定在 [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) 上的顯示順序。索引值越小，標籤顯示順序越高。<br><br>值範圍：[0,19] |


<span id="f895d19c"></span>
#### TextSiteTags


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |String |是 |2 |文字標籤的值。 |
|Index |Integer |是 |0 |文字標籤的索引，決定在 [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) 上的顯示順序。索引值越小，標籤顯示順序越高。<br><br>值範圍：[0,4] |


<span id="3f473073"></span>
## 回應參數


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`17218312****` |所建立直播間的活動 ID。 |
|ActivityIdStr |String |`-` |已棄用。 |
|Status |Integer |`-` |已棄用。 |


<span id="99abaa7e"></span>
## 範例

<span id="5c8e5061"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
{ 
    "Name": "Live Room A", 
    "LiveTime": 1680193976,
    "LiveMode": 2    
} 
```


<span id="c4e19f22"></span>
### 回應範例

```JSON
{
  "ResponseMetadata":{
                "RequestId":"2018060411042001001002322800209D2",
                "Action":"CreateActivityAPIV2",
                "Version":"2020-06-01",        
                "Service":"livesaas",
                "Region":"ap-singapore-1"，
                "SystemTime":1656067132
        },
        "Result":{
                "ActivityId":17218312****,
                "ActivityIdStr":"",
                "Status":
        }
}
```


<span id="29a13cf7"></span>
## 錯誤碼

共用錯誤碼清單請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
