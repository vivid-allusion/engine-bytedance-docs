---
title: "ListActivityFeedInfosAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi-zh-TW"
---

取得您帳戶下所有現有直播間的基本資訊，包括封面圖片、虛擬人氣、主播帳號及建立時間。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每分鐘最多 120 次請求

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=ListActivityFeedInfosAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格並未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityFeedInfosAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|PageNumber |Integer |否 |`1` |要返回的頁碼。預設值：`1`。此值必須等於或大於 1。 |
|PageSize |Integer |否 |`10` |每頁返回的結果數量。預設值：`10`。值範圍：[1,100]。 |
|SortBy |String |否 |`Status` |直播間排序規則。預設值：`Status`。若您傳入的值非下列之一，將使用預設值。<br><br>有效值：<br><br><br>* `Status`：先依直播間狀態排序，再於每個狀態內依直播間開始時間遞減排序。<br><br>* `LiveTime`：依直播間開始時間排序。<br><br>* `CreateTime`：依直播間建立時間排序。 |
|SortOrder |String |否 |`Desc` |直播間排序順序。預設值：`Asc`。若您傳入的值非下列之一，將使用預設值。<br><br>有效值：<br><br><br>* `Desc`：遞減排序。<br><br>* `Asc`：遞增排序。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>SortBy</code>設為<code>Status</code>時，直播間狀態的遞增順序為：Live、Preview、Playback、Over。無論<code>SortOrder</code>值為何，直播間都會在每個狀態內依開始時間遞減排序。</div><br> |
|SiteTagNews |[SiteTagNews](https://docs.byteplus.com/en/docs/11/103181#sitetagnews)陣列 |否 |`-` |將返回包含任一這些分類標籤值的直播間。<br><br>您可透過呼叫[ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2)取得分類標籤列表。 |


<span id="sitetagnews"></span>
### SiteTagNews


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Value |String 陣列 |是 |`["1","2"]` |分類標籤值。<br><br>將返回包含任一這些分類標籤值的直播間。 |
|Name |String |否 |`Tag A` |分類標籤名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請傳入<code>Name</code>或<code>Index</code>其中之一。若同時傳入，僅<code>Name</code>生效。若皆未傳入，則使用<code>Index</code>的預設值。</div><br> |
|Index |Integer |否 |`0` |分類標籤索引，用於識別[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。<br><br>預設值：`0`。值範圍：[0,19]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請傳入<code>Name</code>或<code>Index</code>其中之一。若同時傳入，僅<code>Name</code>生效。若皆未傳入，則使用<code>Index</code>的預設值。</div><br> |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PageNumber |Integer |`1` |要返回的頁碼。 |
|PageSize |Integer |`10` |每頁返回的結果數量。 |
|TotalCount |Integer |`1` |返回的直播間總數。 |
|列表 |[列表](https://docs.byteplus.com/en/docs/11/103181#list)陣列 |`-` |返回的直播間列表。 |


<span id="list"></span>
### List


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ActivityId |Long |`1810625882058998` |返回直播間的活動 ID。 |
|ActivityName |String |`直播間 A` |返回直播間的名稱。 |
|Status |Integer |`2` |返回直播間的狀態。有效值：<br><br><br>* `1`：直播。<br><br>* `2`：預覽。<br><br>* `3`：回放。<br><br>* `4`：結束。 |
|CoverImageUrl |String |`//example.image` |返回直播間橫向封面圖片的 URL。<br><br>若透過 API 呼叫設定封面圖片，URL 會包含協議頭。若透過控制台設定，則不包含協議頭。 |
|VerticalCoverImageUrl |String |`//example.image` |返回直播間直向封面圖片的 URL。<br><br>若透過 API 呼叫設定封面圖片，URL 會包含協議頭。若透過控制台設定，則不包含協議頭。 |
|Token |String |`qIZSTa` |Web Viewer SDK 公開模式下的使用者 token。<br><br>整合 Web Viewer SDK 時，請將 `token` 的值設為目前參數值，並將 `mode` 的值設為 `1`。 |
|VirtualPeopleCount |Integer |`100` |返回直播間的虛擬人氣值。 |
|HostName |String |`主持人 A` |主持人帳號名稱。 |
|HostAvatarImageUrl |String |`//example.image` |主持人帳號頭像的 URL。<br><br>若透過 API 呼叫設定頭像，URL 會包含協議頭。若透過控制台設定，則不包含協議頭。 |
|CreateTime |Integer |`1726818793` |返回直播間的建立時間（Unix 時間戳格式）。單位：秒。 |
|SiteTags |[SiteTags](https://docs.byteplus.com/en/docs/11/103181#sitetags)陣列 |`-` |返回直播間的分類標籤列表。 |


<span id="sitetags"></span>
### SiteTags


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Name |String |`標籤 A` |分類標籤名稱。 |
|Value |String |`1` |分類標籤值。 |
|Index |Integer |`0` |分類標籤的索引，用於標識在 [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) 上的顯示順序。<br><br>取值範圍：[0,19]。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://livesaas.byteplusapi.com/?Action=ListActivityFeedInfosAPI&Version=2023-08-01
{
    "PageNumber": 1,
    "PageSize": 10,
    "SortBy": "Status",
    "SortOrder": "Desc",
    "SiteTagNews": [
        {
            "Value": [
                "1",
                "2"
            ],
            "Name": "Tag A",
            "Index": 0
        }
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "Action": "ListActivityFeedInfosAPI",
        "Version": "2023-08-01",
        "SystemTime": 1826818793
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "List": [
            {
                "ActivityId": 181062****058998,
                "ActivityName": "Live room A",
                "Status": 2,
                "CoverImageUrl": "//example.image",
                "VerticalCoverImageUrl": "//example.image",
                "Token": "qI****",
                "VirtualPeopleCount": 100,
                "HostName": "Host A",
                "HostAvatarImageUrl": "//example.image",
                "CreateTime": 1726818793,
                "SiteTags": [
                    {
                        "Name": "Tag A",
                        "Value": "1",
                        "Index": 0
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
