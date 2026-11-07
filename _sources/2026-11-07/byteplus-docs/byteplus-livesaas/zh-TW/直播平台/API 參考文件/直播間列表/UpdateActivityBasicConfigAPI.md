---
title: "UpdateActivityBasicConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-TW"
---

呼叫此 API 以更新直播間的基本配置，例如背景圖片與預覽。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">在呼叫此 API 操作前，必須先呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW">GetActivityBasicConfigAPI</a>。根據需要更新 <code>GetActivityBasicConfigAPI</code> 的回應參數值，並在呼叫此 API 操作時作為請求參數值傳入。若有自訂需求，為避免參數值被預設值取代，即使該參數非必填，也必須傳入對應的參數值。</div>


<span id="f20e18f2"></span>
## 需求

頻率限制：每個帳戶每分鐘最多 120 次請求

<span id="7be59498"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=UpdateActivityBasicConfigAPI&Version=2020-06-01`

* 方法：POST


<span id="c924e2f3"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityBasicConfigAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="83d6dacc"></span>
### Body


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得 ID。 |
|名稱 |String |是 |`Live Room A` |直播間名稱，長度不得超過 1950 字元。 |
|LiveTime |Long |否 |`1666258566` |直播開始時間，Unix 時間戳格式。單位：秒。時間可精確到分鐘。<br><br>此為預定開始時間。實際開始時間可能依主持人開播時間而有所不同。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The <code>LiveTime</code> 必須早於 <code>EndTime</code>，最大差值為 259,200（72 小時）。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">直播進行中不可修改此參數值。</div><br> |
|IsBeginLiveEnable |Integer |否 |`0` |指定是否啟用直播開始時間功能。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。僅能在指定開始時間後開啟直播。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">直播進行中不可修改此參數值。</div><br> |
|IsAutoEndEnable |Integer |否 |`0` |指定是否啟用於指定結束時間自動結束直播的功能。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">直播進行中不可修改此參數值。</div><br> |
|EndTime |Long |否 |`1666358566` |直播結束時間，Unix 時間戳格式。單位：秒。時間可精確到分鐘。<br><br>`EndTime` 必須晚於 `LiveTime`，最大差距為 259,200（72 小時）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>IsAutoEndEnable</code> 的值為 <code>1</code> 時，此參數為必填。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">直播進行中不可修改此參數值。</div><br> |
|IsCoverImageEnable |Integer |否 |`0` |指定是否啟用封面圖片。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用封面圖片。<br><br>* `1`：啟用封面圖片。 |
|CoverImageUrl |String |否 |`https://example.image` |橫式封面圖片的 URL。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">通常參數值需為帶協議頭的 URL。但是，如果你取得的是透過<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>上傳的圖片 URL（例如，通過調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW">GetActivityBasicConfigAPI</a>來獲取直播間中通過控制台上傳的封面圖片 URL），則無協議頭的 URL 也可以作為參數值使用。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當<code>IsCoverImageEnable</code>的值為<code>1</code>時，此參數為必填。</div><br> |
|VerticalCoverImageUrl |String |否 |`https://example.image` |直式封面圖片的 URL。<br><br>若未指定，參數值將設定為 `CoverImageUrl` 的值。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">通常，作為參數值時需要帶有協議頭的 URL。但是，如果你取得的是透過<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>上傳的圖片 URL（例如，通過調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW">GetActivityBasicConfigAPI</a>來獲取直播間中通過控制台上傳的封面圖片 URL），則無協議頭的 URL 也可以作為參數值使用。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當<code>IsCoverImageEnable</code>的值為<code>1</code>時，此參數為必填。</div><br> |
|IsPcBackImageEnable |Integer |否 |`0` |指定是否啟用 PC 背景圖片或背景色。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用背景圖片。<br><br>* `1`：啟用背景圖片。<br><br>* `2`：啟用背景色。 |
|PcBackImageUrl |String |否 |`//example.image` |PC 端背景圖片的 URL。當 `IsPcBackImageEnable` 的值為 `1` 時，該參數為必填。 |
|PcBackImageUrlDefault |String |否 |`https://example.image` |PC 端預設背景圖片的 URL，需包含協議頭。 |
|BackgroundColor |String |否 |`#060815` |PC 端的背景顏色，遵循 RGB 色彩模型。當 `IsPcBackImageEnable` 的值為 `2` 時，該參數為必填。您必須設置與 [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW) 回應中返回值相同的值。 |
|IsMobileBackImageEnable |Integer |否 |`0` |指定是否啟用移動裝置的背景圖片或顏色。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：關閉背景圖片。<br><br>* `1`：啟用背景圖片。<br><br>* `2`：啟用背景顏色。 |
|MobileBackImageUrl |String |否 |`//example.image` |移動裝置背景圖片的 URL。當 `IsMobileBackImageEnable` 的值為 `1` 時，該參數為必填。 |
|MobileBackImageUrlDefault |String |否 |`https://example.image` |移動裝置預設背景圖片的 URL，需包含協議頭。 |
|MobileBackgroundColor |String |否 |`#060815` |移動裝置的背景顏色，遵循 RGB 色彩模型。當 `IsMobileBackImageEnable` 的值為 `2` 時，該參數為必填。您必須設置與 [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW) 回應中返回值相同的值。 |
|IsPreviewVideoEnable |Integer |否 |`0` |指定是否啟用預覽功能。預設值：`0`<br><br>有效值：<br><br><br>* `0`：關閉預覽。<br><br>* `1`：啟用預覽。 |
|PreviewVideoUrl |String |否 |`-` |已棄用。 |
|PreviewVideoVid |String |否 |`v03a49g10000ckkavibc77uejmsb****` |預覽影片的 ID。當 `IsPreviewVideoEnable` 的值為 `1` 時，該參數為必填。 |
|PreviewVideoVidDefault |String |否 |`-` |已棄用。 |
|IsPeopleCountEnable |Integer |否 |`0` |指定是否在觀看頁面顯示觀看人數。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不顯示觀看人數。<br><br>* `1`：顯示觀看人數。 |
|IsHeaderImageEnable |Integer |否 |`0` |指定是否啟用移動裝置的標頭圖片。預設值：`0`<br><br>有效值：<br><br><br>* `0`：關閉標頭圖片。<br><br>* `1`：啟用標頭圖片。 |
|HeaderImageUrl |String |否 |`//example.image` |移動裝置標頭圖片的 URL。當 `IsHeaderImageEnable` 的值為 `1` 時，該參數為必填。 |
|IsWatermarkImageEnable |Integer |否 |`0` |指定是否啟用播放器標誌。預設值：`0`<br><br>有效值：<br><br><br>* `0`：關閉標誌。<br><br>* `1`：啟用標誌。 |
|WatermarkImageUrl |String |否 |`//example.image` |播放器標誌的 URL。當 `IsWatermarkImageEnable` 的值為 `1` 時，該參數為必填。 |
|IsThumbUpEnable |Integer |否 |`0` |指定是否啟用直播間按讚功能。預設值：`0`<br><br>有效值：<br><br><br>* `0`：關閉此功能。<br><br>* `1`：啟用此功能。 |
|ThumbUpUrl |String |否 |`//example.image` |按讚圖示的 URL。當 `IsThumbUpEnable` 的值為 `1` 時，該參數為必填。 |
|ThumbUpUrlDefault |String |否 |`https://example.image` |預設按讚圖示的 URL，需包含協議頭。 |
|IsShareIconEnable |Integer |否 |`0` |指定是否啟用分享圖示。預設值：`0`<br><br>有效值：<br><br><br>* `0`：關閉分享圖示。<br><br>* `1`：啟用分享圖示。 |
|ShareIconUrl |String |否 |`//example.image` |分享圖示的 URL。當 `IsShareIconEnable` 的值為 `1` 時，該參數為必填。 |
|ShareIconUrlDefault |String |否 |`https://example.image` |預設分享圖示的 URL，包含協議標頭。 |
|IsCommentTranslateEnable |整數 |否 |`-` |已棄用。 |
|IsAnnouncementEnable |整數 |否 |`0` |指定是否啟用直播間描述。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用描述。<br><br>* `1`：啟用描述。 |
|Announcement |字串 |否 |`直播間描述` |直播間的描述。當`IsAnnouncementEnable`的值為`1`時，此參數為必填。 |
|InteractionColor |字串 |否 |`#202124` |PC 端互動區域的背景色，採用 RGB 色彩模型。必須設定與[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW)回應中返回的值相同。 |
|FontColor |字串 |否 |`#ffffff` |字體顏色，採用 RGB 色彩模型。必須設定與[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW)回應中返回的值相同。 |
|ColorThemeIndex |字串 |否 |`dark` |主題。預設值：`dark`<br><br>有效值：<br><br><br>* `light`：明亮模式。<br><br>* `dark`：暗色模式。<br><br>* `cold`：經典模式。<br><br>* `holiday`：節慶模式。 |
|IsPCHeaderImageEnable |整數 |否 |`0` |指定是否啟用 PC 端標頭圖片。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用標頭圖片。<br><br>* `1`：啟用標頭圖片。 |
|PCHeaderImageUrl |字串 |否 |`//example.image` |PC 端標頭圖片的 URL。當`IsPCHeaderImageEnable`的值為`1`時，此參數為必填。 |
|IsCountDownEnable |整數 |否 |`0` |指定是否啟用倒數計時。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用倒數計時。<br><br>* `1`：啟用倒數計時。 |
|IsAutoStartEnable |整數 |否 |`0` |指定是否自動啟動直播。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不自動啟動直播。<br><br>* `1`：自動啟動直播。 |
|AutoStartType |整數 |否 |`0` |自動啟動直播的模式。當`IsAutoStartEnable`的值為`1`時，此參數為必填。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不自動啟動直播。<br><br>* `1`：自動啟動預錄影片。<br><br>* `2`：自動啟動拉流。 |
|IsPageLimitEnable |整數 |否 |`0` |指定是否啟用觀看頁面限制。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用限制。<br><br>* `1`：啟用限制。 |
|PageLimitType |字串 |否 |`pc` |觀看頁面限制。當`IsPageLimitEnable`的值為`1`時，此參數為必填。<br><br>有效值：<br><br><br>* `pc`：僅能在 PC 端觀看影片。<br><br>* `mobile`：僅能在行動裝置觀看影片。 |
|IsLanguageEnable |整數 |否 |`0` |指定是否啟用觀看頁面的語言選擇器。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用語言選擇器。<br><br>* `1`：啟用語言選擇器。 |
|LanguageType |整數陣列 |否 |`[0,1]` |觀看頁面可供觀眾選擇的語言。當`IsLanguageEnable`的值為`1`時，此參數為必填。預設值：`0`。最多可選擇 13 種語言。<br><br>有效值：<br><br><br>* `0`：簡體中文。<br><br>* `1`：英文。<br><br>* `2`：日文。<br><br>* `3`：繁體中文。<br><br>* `4`：韓文。<br><br>* `5`：泰文。<br><br>* `6`：越南文。<br><br>* `7`：阿拉伯文。<br><br>* `8`：土耳其文。<br><br>* `9`：西班牙文。<br><br>* `10`：印尼文。<br><br>* `11`：葡萄牙文。<br><br>* `12`：俄文。<br><br>* `13`：塔加洛語。<br><br>* `14`：高棉文。<br><br>* `15`：寮文。<br><br>* `16`：緬甸文。<br><br>* `17`：馬來文。<br><br>* `18`：印地語。<br><br>* `19`：法文。<br><br>* `20`：德文。<br><br>* `21`：義大利文。 |
|SiteTags |Array of[SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-TW#a144fb32) |否 |`-` |直播間分類標籤列表。 |
|TextSiteTags |Array of[TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-TW#979852d4) |否 |`-` |直播間文字標籤列表。 |
|PreviewVideoId |Long |否 |`431674` |預覽的媒體庫 ID。當 `IsPreviewVideoEnable` 的值為 `1` 時，此參數為必填。 |
|AccountId |Long |否 |`-` |已棄用。 |
|PreviewVideoReviewStatus |Integer |否 |`-` |已棄用。 |
|DefaultSubtitleLanguage |String |否 |`-` |已棄用。 |
|SourceSubtitleLanguage |String |否 |`-` |已棄用。 |
|OpenLiveAvextractorTask |Integer |否 |`-` |已棄用。 |
|IsTimeShift |Integer |否 |`0` |此功能目前不可用。固定值：`0` |
|PreviewVideoCoverImage |String |否 |`https://example.image` |預覽的封面圖片 URL。 |
|PreviewVideoMediaName |String |否 |`Video.mp4` |預覽的名稱。 |
|IsPreviewPromptEnable |Integer |否 |`0` |指定是否啟用預覽文字。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用預覽文字。<br><br>* `1`：啟用預覽文字。 |
|PreviewPrompt |String |否 |`直播即將開始。` |預覽文字。當 `IsPreviewPromptEnable` 的值為 `1` 時，此參數為必填。 |
|IsReservationEnable |Integer |否 |`0` |指定是否啟用預約功能。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用此功能。<br><br>* `1`：啟用此功能。 |
|IsReservationSmsEnable |Integer |否 |`1` |指定是否啟用預約的簡訊提醒。預設值：`1`。<br><br>有效值：<br><br><br>* `1`：啟用簡訊提醒。<br><br>* `2`：不啟用簡訊提醒。<br><br><br>僅當 `IsReservationEnable` 的值為 `1` 時，此參數有效。 |
|ReservationTime |Integer |否 |`300` |指定直播開始前發送簡訊提醒給觀眾的時間（秒）。<br><br>單位：秒。<br><br>僅當 `IsReservationSmsEnable` 的值為 `1` 時，此參數有效。 |
|ReservationText |String |否 |`-` |已棄用。 |
|WatermarkPosition |Integer |否 |`0` |播放器標誌的位置。預設值：`0`<br><br>有效值：<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：播放器右下角。 |
|IsReplayBulletChat |Integer |否 |`-` |已棄用。 |
|PresenterChatColor |String |否 |`#FFD58B` |講者聊天訊息的字體顏色，採用 RGB 色彩模式。必須設定為 [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW) 回應中返回的值。 |
|IsLiveBulletChat |Integer |否 |`-` |已棄用。 |
|IsBackgroundBlur |Integer |否 |`0` |指定是否啟用背景模糊。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不啟用此功能。<br><br>* `1`：在行動裝置上啟用此功能。<br><br>* `2`：在電腦上啟用此功能。<br><br>* `3`：在電腦及行動裝置上啟用此功能。 |
|FeedbackMessage |String |否 |`-` |已棄用。 |
|IsFeedbackEnable |Integer |否 |`-` |已棄用。 |
|IsThumbUpNumberEnable |Integer |否 |`0` |指定是否在觀看頁面顯示直播間按讚數。預設值：`0`<br><br>有效值：<br><br><br>* `0`：不顯示按讚數。<br><br>* `1`：顯示按讚數。 |
|SmsLanguage |Integer |否 |`0` |簡訊訊息的語言。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：若手機號碼以 +86 開頭則為中文，其他則為英文。<br><br>* `1`：中文。<br><br>* `2`：英文。<br><br>* `3`：中英文皆有。 |
|MobileChatBackgroundColor |String |否 |`#000000` |行動裝置評論的背景顏色，採用 RGB 色彩模式。必須設定為 [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW) 回應中返回的值。 |
|ConfigVersion |Integer |否 |`1` |配置版本。固定值：`1`。 |
|LiveZone |整數 |否 |`480` |時區。預設值：`480`。<br><br>有效值：<br><br><br>* `-60`：GMT\-01:00 Ponta del Gada（葡萄牙）。<br><br>* `-120`：GMT\-02:00 Fernando de Noronha（巴西）。<br><br>* `-180`：GMT\-03:00 Brasilia（巴西）。<br><br>* `-240`：GMT\-04:00 Santiago（智利）。<br><br>* `-300`：GMT\-05:00 Washington, D.C.（美國）。<br><br>* `-360`：GMT\-06:00 Mexico City（墨西哥）。<br><br>* `-420`：GMT\-07:00 Denver（美國）。<br><br>* `-480`：GMT\-08:00 Vancouver（加拿大）。<br><br>* `-540`：GMT\-09:00 Alaska（美國）。<br><br>* `-570`：GMT\-09:30 Teojae（法屬波利尼西亞）。<br><br>* `-600`：GMT\-10:00 Hawaii（美國）。<br><br>* `-660`：GMT\-11:00 Alofi（紐埃）。<br><br>* `0`：GMT+00:00 London（英國）。<br><br>* `60`：GMT+01:00 Paris（法國）。<br><br>* `120`：GMT+02:00 Damascus（敘利亞）。<br><br>* `180`：GMT+03:00 Moscow（俄羅斯）。<br><br>* `210`：GMT+03:30 Tehran（伊朗）。<br><br>* `240`：GMT+04:00 Dubai（阿拉伯聯合大公國）。<br><br>* `300`：GMT+05:00 New Delhi（印度）。<br><br>* `330`：GMT+05:30 Mumbai（印度）。<br><br>* `360`：GMT+06:00 Dhaka（孟加拉）。<br><br>* `390`：GMT+06:30 Yangon（緬甸）。<br><br>* `420`：GMT+07:00 Bangkok（泰國）。<br><br>* `480`：GMT+08:00 Beijing（中國）。<br><br>* `525`：GMT+08:45 Yukla（澳洲）。<br><br>* `540`：GMT+09:00 Tokyo（日本）。<br><br>* `570`：GMT+09:30 Darwin（澳洲）。<br><br>* `600`：GMT+10:00 Canberra（澳洲）。<br><br>* `630`：GMT+10:30 Lord Howe Island（澳洲）。<br><br>* `660`：GMT+11:00 Sydney（澳洲）。<br><br>* `720`：GMT+12:00 Suva（斐濟）。<br><br>* `780`：GMT+13:00 Phoenix Islands（基里巴斯）。<br><br>* `825`：GMT+13:45 Chatham Islands（紐西蘭）。<br><br>* `840`：GMT+14:00 Christmas Island（基里巴斯）。 |
|RiskWarningSetting |Object of[RiskWarningSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-TW#f2cf2062) |否 |`-` |觀眾進入直播間時顯示的提醒彈窗配置。 |
|IsColorSync |整數 |否 |`0` |指定是否將顏色配置同步至直式模式。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：不同步至直式模式。<br><br>* `1`：同步至直式模式。 |
|IsPlayerTopEnable |整數 |否 |`0` |指定是否啟用播放器置頂功能。預設值：`0`<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。 |
|PlayerTopType |整數陣列 |否 |`[1,2]` |播放器在頁面頂部置頂的終端設備。預設值：`[1,2]`<br><br>當`IsPlayerTopEnable`的值為`1`時，此參數為必填。<br><br>有效值：<br><br><br>* `0`：已淘汰。<br><br>* `1`：播放器在電腦端頁面頂部置頂。<br><br>* `2`：播放器在行動裝置橫式模式下置頂於頁面頂部。 |
|IsReplayAutoOnlineEnable |整數 |否 |`0` |指定直播結束後是否自動在觀看頁面發布回放。<br><br>有效值：<br><br><br>* `0`：不自動發布回放。<br><br>* `1`：自動發布回放。 |
|IsSDKPlayEnable |整數 |否 |`1` |指定是否啟用整合 Web Viewer SDK 的觀看頁面播放器播放直播影片。預設值：`1`。<br><br>有效值：<br><br><br>* `0`：禁止播放器播放直播影片。為避免不必要的播放，直播同時被停用。因此，無論是否在整合 Web Viewer SDK 的觀看頁面，觀眾皆無法觀看直播影片。<br><br>* `1`：允許播放器播放直播影片。 |
|SDKPlayStatus |整數 |否 |`2` |在整合 Web Viewer SDK 的觀看頁面顯示的直播間狀態，可能與直播間實際狀態不同。<br><br>若未指定，則顯示直播間實際狀態。<br><br>此參數僅在`IsSDKPlayEnable`值為`0`時有效。<br><br>有效值：<br><br><br>* `2`：預覽。<br><br>* `3`：回放。<br><br>* `4`：結束。<br><br><br>如果你將狀態設為 `2`（預覽）或 `3`（回放），但對應內容不可用，頁面將顯示 `Over` 狀態。例如，若你將狀態設為 `3`，但尚未發布回放，頁面將顯示 `Over`，而非 `Playback`。 |
|IsVideoChatDisplayed |整數 |否 |`0` |指定是否在網頁瀏覽器中的直播頁面啟用聯合主持功能。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。 |
|IsSharedAddressDisplayed |整數 |否 |`0` |指定是否在網頁瀏覽器中的直播頁面顯示觀看頁面地址。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：不顯示地址。<br><br>* `1`：顯示地址。 |
|IsReleaseNoticeDisplayed |整數 |否 |`0` |指定是否在網頁瀏覽器中的直播頁面啟用鎖定預覽功能。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。 |
|IsInteractiveEnable |整數 |否 |`0` |指定是否允許主持人在網頁瀏覽器中的直播頁面僅管理指定的互動工具。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：主持人可管理以下所有互動工具。<br><br>   * 問卷<br><br>   * 文件<br><br>   * 簽到<br><br>   * 測驗<br><br>   * 抽獎<br><br>   * 公告<br><br>* `1`：主持人僅可管理指定的互動工具。 |
|InteractiveShowSetting |[InteractiveShowSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-TW#f46bb856)的物件 |否 |`-` |主持人在網頁瀏覽器中的直播頁面可管理的互動工具。至少配置一項互動工具。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果 <code>IsInteractiveEnable</code>的值為 <code>1</code>，則此參數為必填。</div><br> |


<span id="f46bb856"></span>
#### InteractiveShowSetting


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|IsQuestionnaireDisplayed |整數 |否 |`0` |指定是否允許主持人在網頁瀏覽器中的直播頁面管理問卷。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：主持人無法管理問卷。<br><br>* `1`：主持人可管理問卷。 |
|IsDocDisplayed |整數 |否 |`0` |指定是否允許主持人在網頁瀏覽器中的直播頁面管理文件。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：主持人無法管理文件。<br><br>* `1`：主持人可管理文件。 |
|IsCheckInDisplayed |整數 |否 |`0` |指定是否允許主持人在網頁瀏覽器中的直播頁面管理簽到。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：主持人無法管理簽到。<br><br>* `1`：主持人可管理簽到。 |
|IsQuizDisplayed |整數 |否 |`0` |指定是否允許主持人在網頁瀏覽器中的直播頁面管理測驗。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：主持人無法管理測驗。<br><br>* `1`：主持人可管理測驗。 |
|IsLuckDrawDisplayed |整數 |否 |`0` |指定是否允許主持人在網頁瀏覽器中的直播頁面管理抽獎。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：主持人無法管理抽獎。<br><br>* `1`：主持人可管理抽獎。 |
|IsAnnouncementDisplayed |整數 |否 |`0` |指定是否允許主持人在網頁瀏覽器中的直播頁面管理公告。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：主持人無法管理公告。<br><br>* `1`：主持人可管理公告。 |


<span id="a144fb32"></span>
#### SiteTags


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|值 |字串 |是 |`1` |分類標籤值。 |
|索引 |整數 |是 |`0` |分類標籤的索引，用於識別在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。<br><br>取值範圍：[0,19]。 |


<span id="979852d4"></span>
#### TextSiteTags


|名稱 |資料類型 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|值 |字串 |是 |`3` |文字標籤的值。 |
|索引 |整數 |是 |`0` |文字標籤的索引，用於識別在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。<br><br>取值範圍：[0,4]。 |


<span id="f2cf2062"></span>
#### RiskWarningSetting


|名稱 |資料類型 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|IsRiskWarningEnable |整數 |否 |`0` |指定是否啟用提醒彈窗。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：停用此功能。<br><br>* `1`：啟用此功能。 |
|RiskWarningButtonText |字串 |否 |`已了解` |提醒彈窗的按鈕名稱。 |
|RiskWarningContent |字串 |否 |`歡迎來到直播間！請遵守主辦方及您所在國家的法律法規，勿發送色情、非法、低俗或誹謗性評論。成為其他人的模範觀眾。我們誠摯請您勿以惡意行為或網路騷擾破壞直播間的良好秩序。如遇到您與主播之間的私人商品推銷，請自行判斷並保持理性。` |提醒內容。 |
|RiskWarningTitle |字串 |否 |`提醒` |提醒彈窗的標題。 |


<span id="7c4b3339"></span>
## 回應參數


|名稱 |資料類型 |範例值 |描述 |
|---|---|---|---|
|ActivityId |長整數 |`17218312****` |直播間的活動 ID。 |
|ActivityIdStr |字串 |`-` |已棄用。 |
|Status |整數 |`-` |已棄用。 |


<span id="7035792a"></span>
## 範例

<span id="d656903f"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityBasicConfigAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "IsSDKPlayEnable": 1,
    "SDKPlayStatus": 2,
    "Name": "Live Room A",
    "LiveTime": 1666258566,
    "IsBeginLiveEnable": 0,
    "IsCoverImageEnable": 0,
    "CoverImageUrl": "https://example.image",
    "VerticalCoverImageUrl": "https://example.image",
    "IsPcBackImageEnable": 0,
    "PcBackImageUrl": "//example.image",
    "PcBackImageUrlDefault": "https://example.image",
    "IsMobileBackImageEnable": 0,
    "MobileBackImageUrl": "//example.image",
    "MobileBackImageUrlDefault": "https://example.image",
    "IsPreviewVideoEnable": 0,
    "PreviewVideoUrl": "",
    "PreviewVideoVid": "",
    "PreviewVideoVidDefault": "",
    "IsPeopleCountEnable": 0,
    "IsHeaderImageEnable": 0,
    "HeaderImageUrl": "",
    "IsWatermarkImageEnable": 0,
    "WatermarkImageUrl": "",
    "IsThumbUpEnable": 0,
    "ThumbUpUrl": "",
    "ThumbUpUrlDefault": "",
    "IsShareIconEnable": 0,
    "ShareIconUrl": "",
    "ShareIconUrlDefault": "https://example.image",
    "IsCommentTranslateEnable": 0,
    "Announcement": "",
    "IsAnnouncementEnable": 0,
    "BackgroundColor": "#060815",
    "InteractionColor": "#202124",
    "FontColor": "#ffffff",
    "ColorThemeIndex": "dark",
    "IsPCHeaderImageEnable": 0,
    "PCHeaderImageUrl": "",
    "IsCountdownEnable": 0,
    "IsAutoStartEnable": 0,
    "IsPageLimitEnable": 0,
    "PageLimitType": "",
    "IsLanguageEnable": 0,
    "LanguageType": [],
    "SiteTags": [],
    "TextSiteTags": [],
    "AutoStartType": 0,
    "IsPlayerTopEnable": 0,
    "PlayerTopType": [],
    "IsReplayAutoOnlineEnable": 0,
    "PreviewVideoId": 0,
    "AccountId": 0,
    "PreviewVideoReviewStatus": 0,
    "DefaultSubtitleLanguage": "",
    "SourceSubtitleLanguage": "",
    "OpenLiveAvextractorTask": 0,
    "IsTimeShift": 0,
    "PreviewVideoCoverImage": "",
    "PreviewVideoMediaName": "",
    "IsPreviewPromptEnable": 0,
    "PreviewPrompt": "The live stream will start soon.",
    "IsReservationEnable": 0,
    "IsReservationSmsEnable": 1,
    "ReservationTime": 300,
    "ReservationText": "",
    "WatermarkPosition": 0,
    "IsReplayBulletChat": 0,
    "PresenterChatColor": "#FFD58B",
    "IsLiveBulletChat": 0,
    "IsBackgroundBlur": 0,
    "FeedbackMessage": "",
    "IsFeedbackEnable": 0,
    "IsThumbUpNumberEnable": 1,
    "SmsLanguage": 0,
    "MobileChatBackgroundColor": "#000000",
    "MobileBackgroundColor": "#060815",
    "ConfigVersion": 1,
    "LiveZone": 480,
    "IsColorSync": 0,
    "IsVideoChatDisplayed": 0,
    "IsSharedAddressDisplayed": 0,
    "IsReleaseNoticeDisplayed": 0,
    "IsInteractiveEnable": 1,
    "InteractiveShowSetting": {
        "IsQuestionnaireDisplayed": 1,
        "IsDocDisplayed": 1,
        "IsCheckInDisplayed": 1,
        "IsQuizDisplayed": 0,
        "IsLuckDrawDisplayed": 0,
        "IsAnnouncementDisplayed": 0
        },
    "EndTime": 1666358566,
    "IsAutoEndEnable": 0
    "RiskWarningSetting": {
        "IsRiskWarningEnable": 0,
        "RiskWarningTitle": "",
        "RiskWarningContent": "",
        "RiskWarningButtonText": ""
    },
}
```


<span id="Response"></span>
### 範例回應

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "UpdateActivityBasicConfigAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656358566
  },
  "Result": {
    "ActivityId": 17218312****,
    "ActivityIdStr": "",
    "Status": 0
  }
}
```


<span id="13430646"></span>
## 錯誤碼

下表列出此 API 操作專屬的錯誤碼。共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。


|狀態碼 |錯誤碼 |錯誤訊息 |描述 |
|---|---|---|---|
|200 |100000 |EndTime 不可早於現在。 |請修改 `EndTime` 參數值後重試。 |
|200 |100000 |EndTime 不可早於 LiveTime。 |請修改參數 `EndTime` 或 `LiveTime` 的值後重試。 |
|200 |100000 |EndTime 不可晚於 LiveTime 起算 72 小時。 |參數 `EndTime` 與 `LiveTime` 的最大差值為 259,200（72 小時）。請修改參數值後重試。 |
|200 |100000 |直播進行中不可修改 EndTime 或 IsAutoEndEnable。 |請先結束直播，再修改參數 `EndTime` 或 `IsAutoEndEnable` 的值。 |
|200 |100000 |直播進行中不可修改 LiveTime 或 IsBeginLiveEnable。 |請先結束直播，再修改參數 `LiveTime` 或 `IsBeginLiveEnable` 的值。 |
|200 |100000 |無效的 %s |參數無效。請依規範修改值後重試。 |
