---
title: "API 清單"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/api-qing-dan-zh-TW"
---

若要將 BytePlus Live 功能整合至您的應用程式，您可以參考本完整的 API 文件。本文件列出了所有可用的 API，並依功能分類，例如直播間、直播串流、洞察分析等，協助您快速找到所需的特定端點。

<span id="Activity management"></span>
## 直播間


|**API** |**說明** |
|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |建立直播間以進行直播活動。 |
|[DeleteActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deleteactivityapi) |刪除指定的直播間。 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |取得您的 BytePlus 帳戶下所有現有直播間的基本資訊。 |
|[UpdateActivityStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitystatusapi) |更新直播間的狀態。您可以將直播間恢復為**預覽**狀態、鎖定預覽及解除預覽鎖定。 |
|[UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi) |啟動或停止從指定 URL 為直播間拉取串流。 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |取得直播間的基本資訊，例如其狀態及觀看頁面地址。 |
|[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi) |取得推送串流至直播間或從第三方平台拉取串流所需的資訊。 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |取得直播間的基本設定，例如背景圖片及預覽。 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |更新直播間的基本設定，例如背景圖片及預覽。 |
|[UpdateLoopVideoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideoapi) |編輯直播間的循環播放影片。 |
|[UpdateLoopVideoStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideostatusapi) |啟用或停用循環播放。 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |禁止直播間中特定直播來源的串流。串流被禁止後，觀眾將無法觀看該串流，且不會產生回放。 |
|[ResumeLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-resumelivestreamapi) |恢復直播間中特定直播來源被禁止的串流。 |
|[GetLiveStreamForbidStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi) |檢查直播間中特定直播來源的串流是否被禁止。 |
|[GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi) |取得您的 BytePlus 帳戶下直播間範本清單。 |
|[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi) |取得在網頁瀏覽器的直播串流頁面上上傳或透過直播間互動工具選單分享的檔案清單。若要取得檔案的下載 URL，您可以使用回應中的檔案 ID 呼叫[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi)。 |
|[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi) |取得在網頁瀏覽器的直播串流頁面上上傳或透過直播間互動工具選單分享的檔案下載 URL。 |
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |取得您的 BytePlus 帳戶及 IAM 使用者下所有現有直播間的基本資訊，包括封面圖片、虛擬人氣、主播帳戶及建立時間。 |


<span id="7f23d224"></span>
## 直播串流


|**API** |**說明** |
|---|---|
|[GetTemporaryLoginTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gettemporarylogintokenapi-zh-TW) |取得直播間的密鑰，用於啟動直播串流。 |
|[GetWebPushLiveClientAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getwebpushliveclientapi-zh-TW) |取得直播間的直播串流頁面 URL，讓主播可在未登入的情況下於網頁瀏覽器啟動直播。 |
|[GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi-zh-TW) |取得直播間的直播串流頁面 URL，讓主播可在未登入的情況下於網頁瀏覽器啟動直播。返回的 URL 在指定時間後會過期。 |


<span id="Playback management"></span>
## 回放


|**API** |**說明** |
|---|---|
|[UploadReplayAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-uploadreplayapi-zh-TW) |綁定影片至直播間作為其回放內容。您必須先將影片上傳至媒體庫後才能執行此操作。 |
|[ListMediasAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listmediasapi-zh-TW) |取得當前直播間播放列表中的影片資訊。 |
|[UpdateMediaOnlineStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatemediaonlinestatusapi-zh-TW) |釋出、撤回或移除一個回放。在執行操作前，必須先將影片上傳為回放。 |
|[DeleteMediaAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletemediaapi-zh-TW) |從直播間的播放列表中刪除一部影片。 |
|[DeleteMediasAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletemediasapi-zh-TW) |每次最多可從直播間播放列表中刪除100部影片。 |


<span id="faf21ca5"></span>
## 敏感詞


|**API** |**說明** |
|---|---|
|[AddActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addactivityantidirtapi-zh-TW) |向直播間新增敏感詞。 |
|[GetActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityantidirtapi-zh-TW) |取得直播間已設定的敏感詞列表。你可以選擇取得所有敏感詞，或包含特定關鍵字的敏感詞。 |
|[DelActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-delactivityantidirtapi-zh-TW) |從直播間刪除敏感詞。 |


<span id="Statistics"></span>
## 洞察分析


|**API** |**說明** |
|---|---|
|[GetPageWatchDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getpagewatchdataapi-zh-TW) |取得直播間的基礎數據，包括頁面瀏覽量、唯一頁面瀏覽量、總觀看時長等。數據每五分鐘更新一次。 |
|[GetAdvertisementDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi-zh-TW) |取得直播間的行銷數據。 |
|[ListUserBehaviorDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-TW) |取得直播間的觀眾行為數據。 |
|[ListQuestionnaireAnswerDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnaireanswerdataapi-zh-TW) |取得直播間問卷的答案（最多可查詢10,000筆結果）。 |
|[ListQuestionnaireDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnairedataapi-zh-TW) |取得直播間的問卷數據。 |
|[ListAnActivityStartAndEndTimeAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi-zh-TW) |取得直播間每場直播的開始與結束時間。 |
|[GetAccountDataByTimeIntervalAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi-zh-TW) |取得你的 BytePlus 帳戶下所有直播間的數據，包括累計觀看次數與唯一觀眾數。 |
|[ListActivityDetailAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-TW) |取得你的 BytePlus 帳戶下特定直播間的數據，包括總直播時長與平均觀看時長。 |
|[GetActivityQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-TW) |取得直播間在指定時間範圍內的直播品質數據。 |
|[GetAccountQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-TW) |取得你的 BytePlus 帳戶下所有直播間在指定時間範圍內的直播品質數據。 |
|[GetActivityReservationAPIV2](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityreservationapiv2) |取得特定直播間的預約資訊。 |


<span id="Chat management"></span>
## 評論


|**API** |**說明** |
|---|---|
|[PresenterChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-presenterchatapi-zh-TW) |以直播間主持人身份發送評論。 |
|[PollingChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-TW) |取得直播間內的評論。 |
|[GetHotChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gethotchatapi-zh-TW) |取得直播間的置頂評論。BytePlus Live 會將獲得大量點讚的評論識別為置頂評論。 |
|[GetTopChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gettopchatapi-zh-TW) |取得置頂於聊天區的評論。 |
|[DeleteChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletechatapi-zh-TW) |從直播間刪除特定評論。 |
|[LikeChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-likechatapi-zh-TW) |點讚評論。 |
|[TopChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-topchatapi-zh-TW) |將評論置頂於聊天區。 |
|[EmptyChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-emptychatapi-zh-TW) |清除直播間所有評論。 |
|[UpdateChatReviewStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatechatreviewstatusapi-zh-TW) |啟用或停用聊天審核功能。 |
|[ConfirmReviewChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-confirmreviewchatapi-zh-TW) |審核評論。 |
|[SilenceUserAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-silenceuserapi-zh-TW) |禁止直播間特定觀眾發送評論。 |
|[GetSilenceUserListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsilenceuserlistapi-zh-TW) |取得被禁止發送評論的觀眾列表。 |


<span id="Menu management"></span>
## 選單


|**API** |**說明** |
|---|---|
|[GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-TW) |取得直播間的菜單列表。 |
|[UpdateActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitymenuapi-zh-TW) |更新直播間的菜單。 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW) |取得直播間商品卡片的配置。 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW) |更新直播間商品卡片的配置。 |
|[ExplainProduct](https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct) |將商品置頂於菜單並在觀看頁面以浮窗顯示，或將商品恢復至菜單原位置並從觀看頁面移除浮窗顯示。 |
|[CreateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/createactivityproductlibrary) |向特定直播間新增一個或多個商品庫。然後，你可以在直播間取得 Shopify 或你自有系統的商品庫中的商品。 |
|[UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) |更新特定直播間的商品庫資訊，包括商品庫的名稱、類型及配置。 |
|[DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) |刪除特定直播間的一個或多個商品庫。 |
|[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig) |獲取指定直播間的商品配置，包括商品庫的 ID、名稱、類型及配置。 |
|[ListActivityProductCommons](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityproductcommons) |一次獲取一個或多個直播間的商品庫資訊。 |
|[UpdatePresenterNameAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepresenternameapi-zh-TW) |更新發送評論時使用的主播暱稱。 |
|[UpdateBulletScreensSwitchAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatebulletscreensswitchapi-zh-TW) |配置是否在觀看頁面顯示彈幕開關。 |
|[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-TW) |從問答菜單獲取問題，按點讚數或發送時間排序，最受歡迎或最新的問題優先返回。為獲取問題的回覆，可使用回應中的問題 ID 呼叫 [ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-TW)。 |
|[ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-TW) |從問答菜單獲取特定問題的回覆，按點讚數或發送時間排序，最受歡迎或最新的回覆優先返回。 |


<span id="Viewing restrictions"></span>
## 觀看限制


|**API** |**說明** |
|---|---|
|[UpdateCustomizationViewPermissionAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatecustomizationviewpermissionapi-zh-TW) |更新觀看及評論限制的登入連結。 |


<span id="f14a1a5e"></span>
## 推廣


|**API** |**說明** |
|---|---|
|[ListLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listlivepromotionsapi-zh-TW) |獲取直播間新增的直播推廣第三方平台列表。 |
|[AddLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-TW) |一次新增多個第三方平台，將直播間的直播同步推送至這些平台。直播間開始直播後，BytePlus Live 會將直播推送至已啟用直播推廣的平台。 |
|[UpdateLivePromotionsStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatelivepromotionsstatusapi-zh-TW) |更新直播間第三方平台的分發狀態，以指定該平台是否啟用直播推廣。 |
|[DeleteLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletelivepromotionsapi-zh-TW) |刪除直播間的直播推廣第三方平台。 |
|[UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) |新增主播帳號或更新您帳號下既有主播帳號的資訊。 |
|[DeleteHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/deletehostaccount) |刪除您帳號下的特定主播帳號。 |
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) |獲取您帳號下主播帳號的 ID、名稱、頭像 URL 等資訊。 |
|[UpdateActivityHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount) |更新特定直播間關聯的主播帳號，並配置是否啟用直播間的帳號設定功能。 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) |獲取特定直播間關聯的主播帳號的 ID、名稱、頭像 URL 等資訊。 |


<span id="3df50b3b"></span>
## 互動工具


|**API** |**說明** |
|---|---|
|[GetVoteListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI-zh-TW) |呼叫 `GetVoteListAPI` 以獲取指定直播間的投票配置資訊。 |
|[GetVoteStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-TW) |呼叫 `GetVoteStatisticsAPI` 以獲取直播間的投票數據。 |
|[UpdatePresenterAwardConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig-zh-TW) |呼叫 `UpdatePresenterAwardConfigAPI` 以新增、更新或刪除直播間的即時抽獎。 |
|[ListAwardConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-TW) |呼叫 `ListAwardConfigsAPI` 以獲取抽獎配置詳情。 |
|[SendAward](https://docs.byteplus.com/docs/byteplus-livesaas/SendAward-zh-TW) |呼叫 `SendAward` 以啟動直播間的即時抽獎。 |
|[WithdrawAward](https://docs.byteplus.com/docs/byteplus-livesaas/WithdrawAward-zh-TW) |呼叫 `WithdrawAward` 以撤回直播間的即時抽獎。注意，已撤回的抽獎無法再次發送或更新。 |
|[UpdateActivityQuizConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-TW) |呼叫 `UpdateActivityQuizConfigAPI` 以更新指定直播間未發送問答的配置資訊。 |
|[ListActivityQuizConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-TW) |呼叫 `ListActivityQuizConfigsAPI` 以獲取指定直播間的問答配置資訊。 |
|[ListQuizStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-TW) |呼叫 `ListQuizStatisticsAPI` 以獲取問答及其互動統計的分頁列表。數據包括參與人數、答對次數及指定直播間的其他相關詳情。 |
|[GetQuizDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI-zh-TW) |呼叫 `GetQuizDataAPI` 以取得指定直播間中某個問答的詳細資訊。這包括參與人數、答對人數，以及每個選項的內容。 |
|[GetCheckInListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI-zh-TW) |呼叫 `GetCheckInListAPI` 以取得指定直播間的所有簽到或指定簽到資訊，包括簽到 ID、參與人數、簽到時長等。 |
|[GetCheckInRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-TW) |呼叫 `GetCheckInRecordStatisticsAPI` 以取得指定直播間的簽到紀錄。 |
|[UpdateFloatingAdvertisementAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateFloatingAdvertisement-zh-TW) |呼叫 `UpdateFloatingAdvertisementAPI` 以更新指定直播間中浮動廣告的狀態、連結及其他配置細節。 |
|[GetTaskAwardItemListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-TW) |呼叫 `GetTaskAwardItemListAPI` 以取得直播間已發送的觀看時長抽獎獎品清單。 |
|[ListAwardRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-TW) |呼叫 `ListAwardRecordStatisticsAPI` 以取得指定直播間某個抽獎的參與或中獎觀眾清單。 |


<span id="0c8c230c"></span>
## 帳戶設定


|**API** |**說明** |
|---|---|
|[ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-TW) |取得您 BytePlus 帳戶下直播間的標籤清單。 |
|[UpdateSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-TW) |更新您 BytePlus 帳戶下直播間標籤的資訊。 |


<span id="Client SDK"></span>
## 用戶端 SDK


|**API** |**說明** |
|---|---|
|[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) |取得授權令牌，讓觀眾可透過整合 Viewer SDK 的網頁或應用程式進入直播間。 |
