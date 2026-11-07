---
title: "ListActivityMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityMediaAPI-zh-TW"
---

獲取媒體庫下的影片庫或臨時存儲中的影片資訊，包括影片 ID 和名稱。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">使用 IAM 使用者呼叫此 API 時，只能獲取該 IAM 使用者可存取或編輯的影片資訊。如需瞭解如何配置 IAM 使用者的使用者範圍與分類範圍，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">管理使用者、組織與角色</a>。</div>


<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每分鐘最多 120 次請求

* 前提條件：需有 BytePlus 帳戶或具備以下權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參閱[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。

   * **媒體庫** \> **影片** \> **臨時存儲** \> **編輯**或**僅檢視**權限：用於獲取臨時存儲中的影片資訊。

   * **媒體庫** \> **影片** \> **影片庫** \> **編輯**或**僅檢視**權限：用於獲取影片庫中的影片資訊。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=ListActivityMediaAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參閱[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityMediaAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|PageNum |Integer |否 |`1` |要返回的頁碼。預設值：`1`。值必須大於或等於 1。 |
|PageSize |Integer |否 |`10` |每頁返回的結果數。預設值：`10`。 |
|SearchType |Integer |是 |`2` |影片的存儲位置。有效值：<br><br><br>* `1`：影片庫<br><br>* `2`：臨時存儲 |
|Vid |String |否 |`v02a49g10000ckitq63c77u8uhf09ebg` |影片的 Vid。 |
|Name |String |否 |`A` |影片名稱，支援模糊搜尋且不區分大小寫。例如，若參數值為`A`，則會返回名稱為`Video A`和`video abc`等影片。 |
|SourceType |Integer |否 |`2` |影片來源。預設會返回所有來源的影片。有效值：<br><br><br>* `1`：上傳，表示影片為本地上傳。<br><br>* `2`：錄製，表示直播結束後自動生成影片。<br><br>* `3`：雲剪輯，表示使用雲剪輯功能剪輯影片。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>SearchType</code>值為<code>1</code>時，該參數才生效。</div><br> |
|OrderKey |String |否 |`create_time` |影片的排序方式。預設按影片更新時間降序排列。有效值：<br><br><br>* `create_time`：按影片建立時間降序排列。<br><br>* `其他值`：按影片更新時間降序排列。更新時間指影片資訊（如封面圖與名稱）被更新的時間。 |
|FolderId |Long |否 |`0` |分類 ID。將返回該分類下的影片。預設值為`0`，表示返回所有分類下的影片。可透過呼叫[GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree)獲取分類 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當<code>SearchType</code>值為<code>1</code>時，該參數才生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當以 IAM 使用者呼叫此 API 並需要傳遞此參數時，請確保具有此 ID 的分類對 IAM 使用者可見。如需瞭解如何設定 IAM 使用者的分類範圍，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">管理使用者、組織和角色</a>。</div><br> |
|IncludeSubFolder |Boolean |否 |`false` |是否包含子分類。預設值：`false`。有效值：<br><br><br>* `true`：包含，表示會返回當前分類及其子分類下的所有影片。<br><br>* `false`：不包含，表示僅返回當前分類下的影片。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>SearchType</code> 的值為 <code>1</code> 時，此參數才會生效。</div><br> |
|IsCloseDated |Boolean |No |`true` |是否篩選30天內到期的直播暫存，僅在SearchType為2時生效。 |


<span id="Response parameters"></span>
## 回應參數


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Data |Array of [Data](https://docs.byteplus.com/en/docs/11/113731#data) |`-` |返回影片列表。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/11/113731#pagination) |`-` |分頁資訊。 |


<span id="data"></span>
### 資料


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |`430998` |影片ID。 |
|MediaName |String |`video A` |影片名稱。 |
|CoverImage |String |`https://www.example.com.image` |影片封面圖片URL。預設封面圖片的URL包含協議頭，通過控制台上傳的封面圖片URL則不包含協議頭。 |
|Vid |String |`v02a49g10000ckitq63c77u8uhf09ebg` |影片Vid。 |
|MediaVideoDuration |Integer |`191` |影片時長。單位：秒。 |
|MediaLibraryVideoType |Integer |`2` |影片存儲位置。有效值：<br><br><br>* `1`：影片庫<br><br>* `2`：暫存 |
|ReviewStatus |Integer |`2` |影片審核狀態。有效值：<br><br><br>* `1`：未審核。<br><br>* `2`：已審核 |
|CreateTime |Integer |`1696980251` |影片的創建時間（Unix時間戳格式）。單位：秒。若影片從暫存轉移至影片庫，則表示轉移至影片庫的時間。 |
|UpdateTime |Integer |`1696990559` |影片最近一次更新時間（Unix時間戳格式），即影片資訊（如封面圖片、名稱）最後一次更新的時間。單位：秒。 |
|Creator |String |`admin@bytedance.com` |影片創建者。值`admin@bytedance.com`表示當前影片由BytePlus帳號創建。 |
|SourceType |Integer |`2` |影片來源。有效值：<br><br><br>* `1`：上傳，表示影片為本地上傳。<br><br>* `2`：錄製，表示直播結束後自動生成影片。<br><br>* `3`：雲剪輯，表示使用雲剪輯功能剪輯影片。 |
|ActivityVideo |Array of [ActivityVideo](https://docs.byteplus.com/en/docs/11/113731#activityvideo) |`-` |與影片關聯的直播間，即正在使用該影片的直播間。 |
|FailureTime |Integer |`1796980251` |影片到期時間。值`0`表示影片永久保存，無到期時間。 |
|MediaSize |Integer |`24725029` |影片大小。單位：位元組。 |
|VideoWidth |Long |`1080` |影片水平像素數。`VideoWidth`與`VideoHeight`共同決定影片解析度。 |
|VideoHeight |Long |`1920` |影片垂直像素數。`VideoWidth`與`VideoHeight`共同決定影片解析度。 |
|FolderName |String |`Category A` |分類名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>MediaLibraryVideoType</code> 的值為 <code>1</code> 時，此參數才會生效。</div><br> |
|FolderId |Long |`0` |分類ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>MediaLibraryVideoType</code> 的值為 <code>1</code> 時，此參數才會生效。</div><br> |


<span id="pagination"></span>
### 分頁


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|PageNum |Integer |`1` |返回頁碼。 |
|PageSize |Integer |`10` |每頁返回結果數。 |
|TotalCount |Integer |`1` |返回影片總數。 |


<span id="activityvideo"></span>
### ActivityVideo


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |Long |`1779341234622756` |直播間活動ID。 |
|Name |String |`Live room A` |直播間名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListActivityMediaAPI&Version=2020-06-01&PageNum=1&PageSize=10&SearchType=2&Vid=v02a49g10000ckitq63c77u8uhf09ebg&Name=A&SourceType=2&OrderKey=create_time&FolderId=0&IncludeSubFolder=false
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListActivityMediaAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Data": [
            {
                "Id": "430998",
                "MediaName": "video A",
                "CoverImage": "https://www.example.com.image",
                "Vid": "v02a49g10000ckitq63c77u8uhf09ebg",
                "MediaVideoDuration": 191,
                "MediaLibraryVideoType": 2,
                "ReviewStatus": 2,
                "CreateTime": 1696980251,
                "UpdateTime": 1696990559,
                "Creator": "admin@bytedance.com",
                "SourceType": 2,
                "ActivityVideo": [
                    {
                        "Id": 1779341234622756,
                        "Name": "Live room A"
                    }
                ],
                "FailureTime": 1796980251,
                "MediaSize": 24725029,
                "FolderId": 0,
                "FolderName": "Category A",
                "VideoHeight": 1920,
                "VideoWidth": 1080
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 10,
            "TotalCount": 1
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需常見錯誤碼列表，請參閱[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
