---
title: "API 發布說明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/api-fa-bu-shuo-ming-zh-TW"
---

BytePlus Live API 發布說明提供所有 API 及回調更新的完整且按時間順序排列的記錄。您可以使用本文件追蹤新功能、重大變更及增強項，確保您的應用程式保持相容並保持最新。

<span id="4c1f9e72"></span>
## 2026 年 7 月


|API/回調 |說明 |發布日期 |
|---|---|---|
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW) |新增 `UAInfo` 和 `DirectUrls` 參數，以支援商品卡片的多環境直達連結功能。 |2026\-07\-23 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW) |新增 `UAInfo` 和 `DirectUrls` 參數，以支援商品卡片的多環境直達連結功能。 |2026\-07\-23 |
|BytePlus Live API Endpoint |支援將 BytePlus Live API 的建議 Endpoint 更新為 `https://livesaas.byteplusapi.com`。原 Endpoint `https://open.byteplusapi.com` 仍可繼續使用。 |2026\-07\-10 |


<span id="5f0af7a2"></span>
## 2026 年 4 月


|API/回調 |說明 |發布日期 |
|---|---|---|
|[GetVoteListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI-zh-TW) |調用 `GetVoteListAPI` 以獲取指定直播間的投票配置信息。 |2026\-04\-01 |
|[GetVoteStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-TW) |調用 `GetVoteStatisticsAPI` 以獲取直播間的投票數據。 |2026\-04\-01 |
|[UpdatePresenterAwardConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig-zh-TW) |調用 `UpdatePresenterAwardConfigAPI` 以新增、更新或刪除直播間的即時抽獎活動。 |2026\-04\-01 |
|[ListAwardConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-TW) |調用 `ListAwardConfigsAPI` 以獲取抽獎活動的配置詳情。 |2026\-04\-01 |
|[SendAward](https://docs.byteplus.com/docs/byteplus-livesaas/SendAward-zh-TW) |調用 `SendAward` 以在直播間啟動即時抽獎。 |2026\-04\-01 |
|[WithdrawAward](https://docs.byteplus.com/docs/byteplus-livesaas/WithdrawAward-zh-TW) |調用 `WithdrawAward` 以從直播間撤回即時抽獎。注意，已撤回的抽獎活動無法再次發送或更新。 |2026\-04\-01 |
|[UpdateActivityQuizConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-TW) |調用 `UpdateActivityQuizConfigAPI` 以更新指定直播間未發送問答的配置信息。 |2026\-04\-01 |
|[ListActivityQuizConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-TW) |調用 `ListActivityQuizConfigsAPI` 以獲取指定直播間的問答配置信息。 |2026\-04\-01 |
|[ListQuizStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-TW) |調用 `ListQuizStatisticsAPI` 以獲取問答及其互動統計的分頁列表。數據包括參與人數、答對人數，以及指定直播間的其他相關詳情。 |2026\-04\-01 |
|[GetQuizDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI-zh-TW) |調用 `GetQuizDataAPI` 以獲取指定直播間的問答詳細信息。內容包括參與人數、答對人數及每個選項的內容。 |2026\-04\-01 |
|[GetCheckInListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI-zh-TW) |調用 `GetCheckInListAPI` 以獲取指定直播間的所有簽到或指定簽到信息，包括簽到 ID、參與人數、簽到時長等。 |2026\-04\-01 |
|[GetCheckInRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-TW) |調用 `GetCheckInRecordStatisticsAPI` 以獲取指定直播間的簽到記錄。 |2026\-04\-01 |
|[UpdateFloatingAdvertisementAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateFloatingAdvertisement-zh-TW) |調用 `UpdateFloatingAdvertisementAPI` 以更新指定直播間浮動廣告的狀態、連結及其他配置信息。 |2026\-04\-01 |
|[GetTaskAwardItemListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-TW) |調用 `GetTaskAwardItemListAPI` 以獲取直播間已發送的觀看時長抽獎獎品列表。 |2026\-04\-01 |
|[ListAwardRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-TW) |調用 `ListAwardRecordStatisticsAPI` 以獲取指定直播間特定抽獎活動的參與或中獎觀眾列表。 |2026\-04\-01 |
|[ActivityAwardInfoCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityAwardInfoCallBack-zh-TW) |當舉辦即時抽獎時，BytePlus Live 會向您的自定義 URL 發送 POST 請求，並在請求正文中傳遞如直播間 ID、獎品信息及中獎者信息等數據。 |2026\-04\-01 |
|[ActivityTaskAwardInfoCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack-zh-TW) |當用戶參與觀看時長抽獎並中獎時，BytePlus Live 會向您的自定義 URL 發送 POST 請求，並在請求正文中傳遞直播間 ID、獎品信息及中獎者信息。 |2026\-04\-01 |
|[CheckinStatusModifyCallback](https://docs.byteplus.com/docs/byteplus-livesaas/CheckinStatusModifyCallback-zh-TW) |當發生簽到事件（如簽到創建、刪除、發送或截止時間到達）時，BytePlus Live 會向您的自定義 URL 發送 POST 請求，並在請求正文中傳遞直播間 ID 及更新後的簽到狀態。 |2026\-04\-01 |


<span id="db5a960a"></span>
## 2026 年 1 月


|API/回調 |說明 |發布日期 |
|---|---|---|
|[ActivityAutoReplayCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityautoreplaycallback-zh-TW) |新增參數`LiveStartTime`和`LiveEndTime`，用於顯示與播放影片對應的直播開始時間與結束時間。 |2026\-01\-27 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |此 API 已停用。如需協助，請聯繫技術支援。 |2026\-01\-14 |


<span id="28480351"></span>
## 2025 年 11 月


|API/Callback |說明 |發布日期 |
|---|---|---|
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |為`LanguageType`新增以下值：<br><br><br>* `13`：塔加洛語。<br><br>* `14`：高棉語。<br><br>* `15`：寮語。<br><br>* `16`：緬甸語。<br><br>* `17`：馬來語。<br><br>* `18`：印地語。<br><br>* `19`：法語。<br><br>* `20`：德語。<br><br>* `21`：義大利語。 |2025\-11\-12 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |||
|[UpdateAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateawarditem) |支援管理您帳戶的獎品，包括新增、更新、刪除及查詢獎品資訊。 |2025\-11\-12 |
|[GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) ||2025\-11\-12 |
|[DeleteAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteawarditem) ||2025\-11\-12 |


<span id="3b98587b"></span>
## 2025 年 8 月


|API/Callback |說明 |發布日期 |
|---|---|---|
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW) |商品卡片中`Title`及`Remark`的字數上限提升至 3315 字。 |2025\-08\-12 |


<span id="3f218069"></span>
## 2025 年 7 月


|API/Callback |說明 |發布日期 |
|---|---|---|
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |* 新增請求參數`FollowerUserName`，可取得由特定帳戶建立的直播間。<br><br>* 新增回應參數`VerticalCoverImage`及`SubAccountName`，可取得直播間直式封面圖片的 URL 及建立直播間的帳戶名稱。 |2025\-07\-17 |
|[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) |支援取得 BytePlus Live 中特定帳戶的 STS 簽名。此簽名可讓您使用 iframe 將 BytePlus Live 控制台的功能模組嵌入至您的頁面。 |2025\-07\-15 |
|[ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi) |支援查詢媒體庫下影片庫或暫存區的影片資訊，包括影片 ID 與名稱。 |2025\-07\-15 |
|[TempToMediaActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/temptomediaactivitymediaapi) |支援將暫存區的影片轉移至影片庫指定分類，永久保存。 |2025\-07\-15 |
|[GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree) |支援查詢您帳戶下預設分類或指定分類及其子分類的資訊。 |2025\-07\-15 |


<span id="4e15c53b"></span>
## 2025 年 2 月


|API/Callback |說明 |發布日期 |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |新增請求參數`SortBy`、`SortOrder`及`SiteTagNews`，可依特定規則與順序排序直播間，並依分類標籤值篩選直播間。 |2025\-02\-25 |
|[ExplainProduct](https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct) |支援將商品置頂於選單並於浮動視窗顯示。您也可取消置頂，將商品恢復至原位置並移除浮動視窗顯示。 |2025\-02\-20 |
|[ActivityExplainProductCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityexplainproductcallBack-zh-TW) |新增回調`ActivityExplainProductCallBack`，當您的直播間商品處於以下任一情境時觸發：<br><br><br>* 置頂於選單並於觀看頁面浮動視窗顯示。<br><br>* 恢復至選單原位置且不再於觀看頁面浮動視窗顯示。 |2025\-02\-20 |


<span id="24ee1531"></span>
## 2025 年 1 月


|API/Callback |說明 |發布日期 |
|---|---|---|
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) |新增請求參數`ExternalPlatformId`，可依外部平台 ID 篩選主播帳戶。 |2025\-01\-16 |


<span id="6adff0b3"></span>
## 2024 年 12 月


|API/Callback |說明 |發布日期 |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |新增回應參數`SiteTags`，可取得每個直播間的分類標籤列表。 |2024\-12\-05 |


<span id="7b10e826"></span>
## 2024 年 11 月


|API/Callback |說明 |發布日期 |
|---|---|---|
|[ListActivityProductCommons](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityproductcommons) |支援一次查詢一個或多個直播間的商品庫資訊。 |2024\-11\-21 |
|[UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) |支援新增主播帳戶、更新現有主播帳戶資訊、刪除主播帳戶，以及查詢您帳戶下的主播帳戶資訊。 |2024\-11\-07 |
|[DeleteHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/deletehostaccount) ||2024\-11\-07 |
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) ||2024\-11\-07 |
|[UpdateActivityHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount) |支援更新與直播間關聯的主辦帳號，以及配置是否啟用直播間的帳號設定功能。 |2024\-11\-07 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) |新增回應參數`IsFollowEnable`，用於指示觀眾是否可在觀看頁面關注主辦。 |2024\-11\-07 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |新增請求參數`SortBy`與`SortOrder`，用於設定返回直播間的排序規則與順序。 |2024\-11\-07 |


<span id="c9c85566"></span>
## 2024 年 10 月


|API/Callback |說明 |發佈日期 |
|---|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |新增請求參數IsBeginLiveEnable，用於指定是否啟用直播開始時間功能。 |2024\-10\-10 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |新增回應參數IsBeginLiveEnable，用於指示直播開始時間功能是否已啟用。 |2024\-10\-10 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |* 新增請求參數IsBeginLiveEnable，用於指定是否啟用直播開始時間功能。<br><br>* 新增請求參數`IsInteractiveEnable`，用於指定是否允許主辦僅在網頁端直播頁面管理指定的互動工具。<br><br>* 新增請求參數`InteractiveShowSetting`，用於指定主辦可在網頁端直播頁面管理的互動工具。 |2024\-10\-10 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |* 新增回應參數`IsBeginLiveEnable`，用於指示直播開始時間功能是否已啟用。啟用後，僅能於指定開始時間後開啟直播。<br><br>* 新增回應參數`IsInteractiveEnable`，用於指示主辦是否僅能在網頁端直播頁面管理指定的互動工具。<br><br>* 新增回應參數`InteractiveShowSetting`，用於指示主辦可在網頁端直播頁面管理的互動工具。 |2024\-10\-10 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |新增錯誤碼`200027`。 |2024\-10\-10 |
|[ResumeLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-resumelivestreamapi) |新增錯誤碼`200027`。 |2024\-10\-10 |


<span id="f9c963c8"></span>
## 2024 年 9 月


|API/Callback |說明 |發佈日期 |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |支援獲取BytePlus帳號下所有現有直播間的基本資訊（包含IAM用戶建立的直播間），包括封面圖片、虛擬人氣、主辦帳號及建立時間。 |2024\-09\-26 |


<span id="efa3ac0b"></span>
## 2024 年 8 月


|API/Callback |說明 |發佈日期 |
|---|---|---|
|[CreateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/createactivityproductlibrary) |支援為指定直播間新增一個或多個商品庫。然後，可於直播間從Shopify或自有系統的商品庫獲取商品。 |2024\-08\-15 |
|[UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) |支援更新指定直播間內商品庫的資訊，包括商品庫名稱、類型及配置。 |2024\-08\-15 |
|[DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) |支援刪除指定直播間的一個或多個商品庫。 |2024\-08\-15 |
|[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig) |支援獲取指定直播間商品的配置，包括商品庫ID、名稱、類型及配置。 |2024\-08\-15 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW) |新增回應參數`ExternalProductId`。 |2024\-08\-15 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW) |新增請求參數`ExternalProductId`。 |2024\-08\-15 |


<span id="cb6b0136"></span>
## 2024 年 7 月


|API/Callback |說明 |發佈日期 |
|---|---|---|
|[ActivityClickReservationCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityclickreservationcallBack-zh-TW) |新增回調`ActivityClickReservationCallBack`。 |2024\-07\-23 |
|[GetActivityReservationAPIV2](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityreservationapiv2) |新增API`GetActivityReservationAPIV2`。 |2024\-07\-23 |


<span id="20b727ae"></span>
## 2024 年 6 月


|API/Callback |說明 |發佈日期 |
|---|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |新增請求參數`EndTime`與`IsAutoEndEnable`。 |2024\-06\-25 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |新增請求參數`EndTime`與`IsAutoEndEnable`。 |2024\-06\-25 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |新增回應參數`EndTime`與`IsAutoEndEnable`。 |2024\-06\-25 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |新增回應參數`EndTime`與`IsAutoEndEnable`。 |2024\-06\-25 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |將`ForbidTime`參數的最大值與預設值從7 × 24 × 60 × 60調整為31 × 24 × 60 × 60。 |2024\-06\-12 |
|[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi) |支援獲取在網頁瀏覽器的直播頁面上上傳的檔案清單，或在特定直播間互動工具選單下發送的檔案清單。 |2024\-06\-06 |
|[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi) |支援獲取在網頁瀏覽器的直播頁面上上傳的檔案下載網址，或在特定直播間互動工具選單下發送的檔案下載網址。 |2024\-06\-06 |
|[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-TW) |支援獲取問答選單下的問題。 |2024\-06\-06 |
|[ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-TW) |支援獲取問答選單下特定問題的回覆。 |2024\-06\-06 |
|[ActivityQuestionChatCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityquestionchatcallback-zh-TW) |當使用者在問答選單下發送問題時，BytePlus Live 會向您的自訂 URL 發送 POST 請求，並在請求主體中傳遞問題資料。 |2024\-06\-06 |


<span id="c7280a1f"></span>
## 2024 年 5 月


|API/Callback |描述 |發佈日期 |
|---|---|---|
|[GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi-zh-TW) |支援獲取直播間的直播頁面網址，讓主播可直接於網頁瀏覽器發起直播，無需登入。返回的網址在指定時效後失效。 |2024\-05\-31 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |新增回應參數 `IsVideoChatDisplayed`、`IsSharedAddressDisplayed` 及 `IsReleaseNoticeDisplayed`。 |2024\-05\-31 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |新增請求參數 `IsVideoChatDisplayed`、`IsSharedAddressDisplayed` 及 `IsReleaseNoticeDisplayed`。 |2024\-05\-31 |
|[DelActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-delactivityantidirtapi-zh-TW) |新增請求參數 `DeleteAll`。 |2024\-05\-10 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |新增請求參數 `HostAccountId`、`HostAccountName` 及 `LiveMode`，以及回應參數 `HostAccountId`、`HostAccountName` 和 `LiveMode`。 |2024\-05\-10 |
|[ListUserBehaviorDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-TW) |新增請求參數 `ScrollId`，以及回應參數 `ScrollId` 和 `SilenceStatus`。 |2024\-05\-10 |
|[PollingChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-TW) |新增回應參數 `IsTipOff`。 |2024\-05\-10 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW) |新增回應參數 `ProductsPosition` 和 `DefaultRedirectImage`。 |2024\-05\-10 |
|[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) |新增請求參數 `InviteToken`、`AvatarUrl` 及 `CustomComment`。 |2024\-05\-10 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |新增請求參數 `IsReservationSmsEnable`。 |2024\-05\-10 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |新增回應參數 `IsReservationSmsEnable`。 |2024\-05\-10 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |新增回應參數 `VerticalCoverImage` 和 `LiveMode`。 |2024\-05\-10 |
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |新增請求參數 `LiveMode`。 |2024\-05\-10 |


<span id="96b75c0a"></span>
## 2024 年 2 月


|**API/Callback** |**描述** |**發佈日期** |
|---|---|---|
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW) |新增回應參數 `TagName`。 |2024\-02\-29 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW) |新增請求參數 `TagName`。 |2024\-02\-29 |
|[GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi) |支援獲取您 BytePlus 帳號下的直播間範本清單。 |2024\-02\-29 |


<span id="56febbb1"></span>
## 2024 年 1 月


|**API/Callback** |**描述** |**發佈日期** |
|---|---|---|
|[GetActivityQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-TW) |支援在指定時間範圍內獲取直播間的直播品質數據。 |2024\-01\-23 |
|[GetAccountQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-TW) |支援在指定時間範圍內獲取您 BytePlus 帳號下所有直播間的直播品質數據。 |2024\-01\-23 |


<span id="1a178e1a"></span>
## 2023 年 11 月


|**API/Callback** |**描述** |**發佈日期** |
|---|---|---|
|[UpdateBusinessAccountInfoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatebusinessaccountinfoapi-zh-TW) |支援更新直播間的品牌帳號資訊。 |2023\-12\-21 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi-zh-TW) |支援獲取直播間的品牌帳號資訊。 |2023\-12\-21 |
|[GetAccountDataByTimeIntervalAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi-zh-TW) |支援獲取您 BytePlus 帳號下所有直播間的數據，包括累計觀看次數及唯一觀眾數。 |2023\-11\-30 |
|[ListActivityDetailAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-TW) |支援獲取您 BytePlus 帳號下特定直播間的數據，包括累計直播時長及每位觀眾的平均觀看時長。 |2023\-11\-30 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |新增請求參數 `VerticalCoverImageUrl`。 |2023\-11\-30 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |新增回應參數 `VerticalCoverImageUrl`。 |2023\-11\-30 |
