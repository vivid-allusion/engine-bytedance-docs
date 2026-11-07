---
title: "GetActivityBasicConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW"
---

呼叫此 API 以取得指定直播間的完整基礎配置集。

<span id="d0b91ad4"></span>
## 需求

頻率限制：每個帳戶每分鐘最多 120 次請求

<span id="826d1a0d"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityBasicConfigAPI&Version=2020-06-01`

* 方法：GET


<span id="b4dd1ba6"></span>
## 請求參數

以下表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="6edbb8f4"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityBasicConfigAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得 ID。 |


<span id="662b150c"></span>
## 回應參數


|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|ActivityId |Long |`17218312****` |直播間的活動 ID。 |
|名稱 |String |`Live Room A` |直播間名稱。 |
|LiveTime |Long |`1666258566` |直播開始時間，Unix 時間戳格式。單位：秒。<br><br>此時間可能不是直播實際開始的時間。 |
|IsBeginLiveEnable |Integer |`0` |表示是否啟用直播開始時間功能。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。僅能在指定開始時間後開啟直播。 |
|IsCoverImageEnable |Integer |`1` |表示是否啟用封面圖片。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|CoverImageUrl |String |`//example.image` |橫版封面圖片的 URL。<br><br>若透過 API 呼叫配置，URL 包含協議頭；若透過控制台配置則不包含。 |
|CoverImageUrlDefault |String |`//example.image` |橫版預設封面圖片的 URL，不含協議頭。 |
|VerticalCoverImageUrl |String |`//example.image` |直版封面圖片的 URL。<br><br>若未指定，參數值將設為 `CoverImageUrl` 的值。<br><br>若透過 API 操作配置封面圖片，URL 包含協議頭。但若透過控制台配置封面圖片，則不包含協議頭。 |
|IsPcBackImageEnable |Integer |`1` |表示是否啟用 PC 背景圖片或顏色。<br><br>有效值：<br><br><br>* `0`：背景圖片未啟用。<br><br>* `1`：背景圖片已啟用。<br><br>* `2`：背景顏色已啟用。 |
|PcBackImageUrl |String |`//example.image` |PC 背景圖片的 URL。僅當 `IsPcBackImageEnable` 為 `1` 時此參數生效。 |
|PcBackImageUrlDefault |String |`https://example.image` |PC 預設背景圖片的 URL，包含協議頭。 |
|IsMobileBackImageEnable |Integer |`1` |表示是否啟用行動裝置背景圖片或顏色。<br><br>有效值：<br><br><br>* `0`：背景圖片未啟用。<br><br>* `1`：背景圖片已啟用。<br><br>* `2`：背景顏色已啟用。 |
|MobileBackImageUrl |String |`//example.image` |行動裝置背景圖片的 URL。僅當 `IsMobileBackImageEnable` 的值為 `1` 時此參數生效。 |
|MobileBackImageUrlDefault |String |`https://example.image` |行動裝置預設背景圖片的 URL，包含協議頭。 |
|MobileBackgroundColor |String |`#060815` |行動裝置背景顏色，採用 RGB 色彩模式。<br><br>僅當 `IsMobileBackImageEnable` 的值為 `2` 時此參數生效。 |
|IsPreviewVideoEnable |整數 |`0` |指示是否啟用預覽。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|PreviewVideoUrl |字串 |`-` |已棄用。 |
|PreviewVideoVid |字串 |`v03a49g10000ckkavibc77uejmsb****` |預覽影片的影片 ID。僅當`IsPreviewVideoEnable`的值為`1`時，此參數才生效。 |
|PreviewVideoVidDefault |字串 |`-` |已棄用。 |
|IsPeopleCountEnable |整數 |`0` |指示觀看頁面是否顯示觀眾人數。<br><br>有效值：<br><br><br>* `0`：不顯示。<br><br>* `1`：顯示。 |
|IsHeaderImageEnable |整數 |`0` |指示是否啟用行動裝置的標頭圖片。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|HeaderImageUrl |字串 |`//example.image` |行動裝置標頭圖片的 URL。僅當`IsHeaderImageEnable`的值為`1`時，此參數才生效。 |
|IsWatermarkImageEnable |整數 |`0` |指示是否啟用播放器標誌。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|WatermarkImageUrl |字串 |`//example.image` |播放器標誌的 URL。僅當`IsWatermarkImageEnable`的值為`1`時，此參數才生效。 |
|IsThumbUpEnable |整數 |`0` |指示觀眾是否可以對直播間按讚。有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|ThumbUpUrl |字串 |`//example.image` |按讚圖示的 URL。僅當`IsThumbUpEnable`的值為`1`時，此參數才生效。 |
|ThumbUpUrlDefault |字串 |`https://example.image` |預設按讚圖示的 URL，包含協定標頭。 |
|IsShareIconEnable |整數 |`0` |指示是否啟用分享圖示。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|ShareIconUrl |字串 |`//example.image` |分享圖示的 URL。僅當`IsShareIconEnable`的值為`1`時，此參數才生效。 |
|ShareIconUrlDefault |字串 |`https://example.image` |預設分享圖示的 URL，包含協定標頭。 |
|IsCommentTranslateEnable |整數 |`-` |已棄用。 |
|IsAnnouncementEnable |整數 |`0` |指示是否啟用直播間描述。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|Announcement |字串 |`直播間描述` |直播間的描述。僅當`IsAnnouncementEnable`的值為`1`時，此參數才生效。 |
|BackgroundColor |字串 |`#060815` |PC 端背景色，採用十六進位 RGB 格式。<br><br>僅當`IsPcBackImageEnable`的值為`2`時，此參數才生效。 |
|InteractionColor |字串 |`#202124` |PC 端互動區域的背景色，採用 RGB 色彩模型。 |
|FontColor |字串 |`#ffffff` |字體顏色，採用 RGB 色彩模型。 |
|ColorThemeIndex |字串 |`dark` |主題。<br><br>有效值：<br><br><br>* `light`：亮色模式。<br><br>* `dark`：暗色模式。<br><br>* `cold`：經典模式。<br><br>* `holiday`：節慶模式。 |
|IsPCHeaderImageEnable |整數 |`0` |指示是否啟用 PC 端標頭圖片。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|PCHeaderImageUrl |字串 |`//example.image` |PC 端標頭圖片的 URL。僅當`IsPCHeaderImageEnable`的值為`1`時，此參數才生效。 |
|IsCountDownEnable |整數 |`0` |指示是否啟用倒數計時。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|IsAutoStartEnable |整數 |`0` |指示是否啟用自動開播功能。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|IsPageLimitEnable |整數 |`0` |指示是否啟用觀看頁面限制。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|PageLimitType |字串 |`pc` |觀看頁面限制。僅當`IsPageLimitEnable`的值為`1`時，此參數才生效。<br><br>有效值：<br><br><br>* `pc`：僅可在 PC 端觀看影片。<br><br>* `mobile`：僅可在行動裝置觀看影片。 |
|IsLanguageEnable |整數 |`0` |表示在觀看頁面是否啟用語言選擇器。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|LanguageType |整數陣列 |`[0,1]` |觀眾可在觀看頁面選擇的語言。僅當`IsLanguageEnable`的值為`1`時，此參數才生效。<br><br>有效值：<br><br><br>* `0`：簡體中文。<br><br>* `1`：英文。<br><br>* `2`：日文。<br><br>* `3`：繁體中文。<br><br>* `4`：韓文。<br><br>* `5`：泰文。<br><br>* `6`：越南文。<br><br>* `7`：阿拉伯文。<br><br>* `8`：土耳其文。<br><br>* `9`：西班牙文。<br><br>* `10`：印尼文。<br><br>* `11`：葡萄牙文。<br><br>* `12`：俄文。<br><br>* `13`：塔加洛語。<br><br>* `14`：高棉文。<br><br>* `15`：寮文。<br><br>* `16`：緬甸文。<br><br>* `17`：馬來文。<br><br>* `18`：印地語。<br><br>* `19`：法文。<br><br>* `20`：德文。<br><br>* `21`：義大利文。 |
|SiteTags |陣列[SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW#290a4055) |`-` |直播間的分類標籤列表。 |
|TextSiteTags |陣列[TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW#7af58dd6) |`-` |直播間的文字標籤列表。 |
|AutoStartType |整數 |`0` |自動啟動直播的模式。僅當`IsAutoStartEnable`的值為`1`時，此參數才生效。<br><br>有效值：<br><br><br>* `0`：不自動啟動直播。<br><br>* `1`：自動播放預錄影片。<br><br>* `2`：自動拉流啟動。 |
|PreviewVideoId |長整數 |`431674` |預覽的媒體庫 ID。僅當`IsPreviewVideoEnable`的值為`1`時，此參數才生效。 |
|AccountId |長整數 |`-` |已棄用。 |
|PreviewVideoReviewStatus |整數 |`-` |已棄用。 |
|DefaultSubtitleLanguage |字串 |`-` |已棄用。 |
|SourceSubtitleLanguage |字串 |`-` |已棄用。 |
|OpenLiveAvextractorTask |整數 |`-` |已棄用。 |
|IsTimeShift |整數 |`0` |此功能目前尚未開放。固定值：`0` |
|PreviewVideoCoverImage |字串 |`https://example.image` |預覽封面圖片的 URL。 |
|PreviewVideoMediaName |字串 |`Video.mp4` |預覽的名稱。 |
|IsPreviewPromptEnable |整數 |`1` |表示是否啟用預覽文字。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|PreviewPrompt |字串 |`直播即將開始。` |預覽文字。僅當`IsPreviewPromptEnable`的值為`1`時，此參數才生效。 |
|IsReservationEnable |整數 |`1` |表示是否啟用預約功能。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|IsReservationSmsEnable |整數 |`1` |表示是否啟用預約簡訊提醒。僅當`IsReservationEnable`的值為`1`時，此參數才有效。<br><br>有效值：<br><br><br>* `1`：已啟用。<br><br>* `2`：未啟用。 |
|ReservationTime |整數 |`300` |指定在直播開始前多少秒發送簡訊提醒。<br><br>單位：秒。<br><br>僅當`IsReservationSmsEnable`的值為`1`時，此參數才有效。 |
|ReservationText |字串 |`-` |已棄用。 |
|WatermarkPosition |整數 |`0` |播放器標誌的位置。<br><br>有效值：<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：播放器右下角。 |
|IsReplayBulletChat |整數 |`-` |已棄用。 |
|PresenterChatColor |字串 |`#FFD58B` |主持人字體顏色，採用 RGB 色彩模式。 |
|IsLiveBulletChat |整數 |`-` |已棄用。 |
|IsBackgroundBlur |整數 |`0` |表示是否啟用背景模糊。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：行動裝置啟用。<br><br>* `2`：電腦啟用。<br><br>* `3`：電腦與行動裝置皆啟用。 |
|FeedbackMessage |字串 |`-` |已棄用。 |
|IsFeedbackEnable |整數 |`-` |已棄用。 |
|IsThumbUpNumberEnable |整數 |`1` |表示在觀看頁面是否顯示直播間的按讚數。<br><br>有效值：<br><br><br>* `0`：不顯示。<br><br>* `1`：顯示。 |
|SmsLanguage |整數 |`0` |簡訊訊息的語言。<br><br>有效值：<br><br><br>* 預設+86開頭的電話號碼為中文，其他號碼為英文。<br><br>* `1`：中文。<br><br>* `2`：英文。<br><br>* `3`：同時顯示中英文。 |
|MobileChatBackgroundColor |字串 |`#000000` |行動裝置上評論的背景顏色，採用RGB色彩模式。 |
|ConfigVersion |整數 |`1` |配置版本。固定值：`1` |
|LiveZone |整數 |`480` |時區。<br><br>有效值：<br><br><br>* `-60`：GMT\-01:00 Ponta del Gada（葡萄牙）。<br><br>* `-120`：GMT\-02:00 Fernando de Noronha（巴西）。<br><br>* `-180`：GMT\-03:00 Brasilia（巴西）。<br><br>* `-240`：GMT\-04:00 Santiago（智利）。<br><br>* `-300`：GMT\-05:00 Washington, D.C.（美國）。<br><br>* `-360`：GMT\-06:00 Mexico City（墨西哥）。<br><br>* `-420`：GMT\-07:00 Denver（美國）。<br><br>* `-480`：GMT\-08:00 Vancouver（加拿大）。<br><br>* `-540`：GMT\-09:00 Alaska（美國）。<br><br>* `-570`：GMT\-09:30 Teojae（法屬波利尼西亞）。<br><br>* `-600`：GMT\-10:00 Hawaii（美國）。<br><br>* `-660`：GMT\-11:00 Alofi（紐埃）。<br><br>* `0`：GMT+00:00 London（英國）。<br><br>* `60`：GMT+01:00 Paris（法國）。<br><br>* `120`：GMT+02:00 Damascus（敘利亞）。<br><br>* `180`：GMT+03:00 Moscow（俄羅斯）。<br><br>* `210`：GMT+03:30 Tehran（伊朗）。<br><br>* `240`：GMT+04:00 Dubai（阿拉伯聯合大公國）。<br><br>* `300`：GMT+05:00 New Delhi（印度）。<br><br>* `330`：GMT+05:30 Mumbai（印度）。<br><br>* `360`：GMT+06:00 Dhaka（孟加拉）。<br><br>* `390`：GMT+06:30 Yangon（緬甸）。<br><br>* `420`：GMT+07:00 Bangkok（泰國）。<br><br>* `480`：GMT+08:00 Beijing（中國）。<br><br>* `525`：GMT+08:45 Yukla（澳洲）。<br><br>* `540`：GMT+09:00 Tokyo（日本）。<br><br>* `570`：GMT+09:30 Darwin（澳洲）。<br><br>* `600`：GMT+10:00 Canberra（澳洲）。<br><br>* `630`：GMT+10:30 Lord Howe Island（澳洲）。<br><br>* `660`：GMT+11:00 Sydney（澳洲）。<br><br>* `720`：GMT+12:00 Suva（斐濟）。<br><br>* `780`：GMT+13:00 Phoenix Islands（基里巴斯）。<br><br>* `825`：GMT+13:45 Chatham Islands（紐西蘭）。<br><br>* `840`：GMT+14:00 Christmas Island（基里巴斯）。 |
|RiskWarningSetting |物件類型：[RiskWarningSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW#98e49104) |`-` |觀眾進入直播間時顯示的提醒彈窗配置。 |
|IsColorSync |整數 |`1` |表示色彩配置是否同步至直式模式。<br><br>有效值：<br><br><br>* `0`：不同步。<br><br>* `1`：同步。 |
|IsPlayerTopEnable |整數 |`0` |表示是否啟用播放器置頂功能。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|PlayerTopType |整數陣列 |`[1,2]` |播放器置頂於頁面頂部的終端。<br><br>有效值：<br><br><br>* `0`：已淘汰。<br><br>* `1`：播放器在PC端頁面頂部置頂。<br><br>* `2`：播放器在行動裝置橫屏模式頁面頂部置頂。 |
|IsReplayAutoOnlineEnable |整數 |`0` |表示直播結束後回放是否自動發布至觀看頁面。<br><br>有效值：<br><br><br>* `0`：不自動發布。<br><br>* `1`：自動發布。 |
|IsSDKPlayEnable |整數 |`1` |表示集成Web Viewer SDK的觀看頁面上的播放器是否啟用直播播放功能。<br><br>有效值：<br><br><br>* `0`：未啟用。為避免不必要的播放，直播同時被禁用。因此，無論是否在集成Web Viewer SDK的觀看頁面，觀眾皆無法觀看直播。<br><br>* `1`：已啟用。 |
|SDKPlayStatus |整數 |`2` |Web Viewer SDK觀看頁面上顯示的直播間狀態。此狀態可能與實際直播間狀態不同。<br><br>僅當`IsSDKPlayEnable`的值為`0`時，此參數才有效。<br><br>有效值：<br><br><br>* `2`：預覽。<br><br>* `3`：回放。<br><br>* `4`：結束。 |
|IsVideoChatDisplayed |整數 |`1` |表示在網頁瀏覽器直播頁面是否啟用協同主持功能。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|IsSharedAddressDisplayed |整數 |`1` |指示是否在網頁瀏覽器的直播頁面上顯示觀看頁面地址。<br><br>有效值：<br><br><br>* `0`：不顯示。<br><br>* `1`：顯示。 |
|IsReleaseNoticeDisplayed |整數 |`1` |指示是否在網頁瀏覽器的直播頁面上啟用鎖定預覽功能。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|IsInteractiveEnable |整數 |`0` |指示主持人是否只能在網頁瀏覽器的直播頁面上管理指定的互動工具。<br><br>有效值：<br><br><br>* `0`：主持人可以管理以下所有互動工具。<br><br>   * 問卷<br><br>   * 文件<br><br>   * 簽到<br><br>   * 測驗<br><br>   * 抽獎<br><br>   * 公告<br><br>* `1`：主持人只能管理指定的互動工具。 |
|InteractiveShowSetting |Object of[InteractiveShowSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-TW#61593802) |`-` |主持人可在網頁瀏覽器的直播頁面上管理的互動工具。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>IsInteractiveEnable</code>為 <code>1</code>時，此參數才會生效。</div><br> |
|EndTime |長整數 |`1666358566` |直播結束時間，採用 Unix 時間戳格式。單位：秒。 |
|IsAutoEndEnable |整數 |`1` |指示是否啟用在指定結束時間自動結束直播的功能。<br><br>有效值：<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |


<span id="61593802"></span>
#### InteractiveShowSetting


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|IsQuestionnaireDisplayed |整數 |`0` |指示主持人是否可在網頁瀏覽器的直播頁面上管理問卷。<br><br>有效值：<br><br><br>* `0`：主持人無法管理問卷。<br><br>* `1`：主持人可以管理問卷。 |
|IsDocDisplayed |整數 |`0` |指示主持人是否可在網頁瀏覽器的直播頁面上管理文件。<br><br>有效值：<br><br><br>* `0`：主持人無法管理文件。<br><br>* `1`：主持人可以管理文件。 |
|IsCheckInDisplayed |整數 |`0` |指示主持人是否可在網頁瀏覽器的直播頁面上管理簽到。<br><br>有效值：<br><br><br>* `0`：主持人無法管理簽到。<br><br>* `1`：主持人可以管理簽到。 |
|IsQuizDisplayed |整數 |`0` |指示主持人是否可在網頁瀏覽器的直播頁面上管理測驗。<br><br>有效值：<br><br><br>* `0`：主持人無法管理測驗。<br><br>* `1`：主持人可以管理測驗。 |
|IsLuckDrawDisplayed |整數 |`0` |指示主持人是否可在網頁瀏覽器的直播頁面上管理抽獎。<br><br>有效值：<br><br><br>* `0`：主持人無法管理抽獎。<br><br>* `1`：主持人可以管理抽獎。 |
|IsAnnouncementDisplayed |整數 |`0` |指示主持人是否可在網頁瀏覽器的直播頁面上管理公告。<br><br>有效值：<br><br><br>* `0`：主持人無法管理公告。<br><br>* `1`：主持人可以管理公告。 |


<span id="290a4055"></span>
#### SiteTags


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|名稱 |字串 |`Tag A` |分類標籤名稱。 |
|值 |字串 |`1` |分類標籤值。 |
|索引 |整數 |`0` |分類標籤的索引，標識其在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。<br><br>取值範圍：[0,19]。 |
|DbIndex |整數 |`-` |已棄用。 |
|Show |整數 |`-` |已棄用。 |
|Id |整數 |`-` |已棄用。 |


<span id="7af58dd6"></span>
#### TextSiteTags


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|名稱 |字串 |`Tag B` |文字標籤名稱。 |
|值 |字串 |`3` |文字標籤值。 |
|索引 |整數 |`0` |文字標籤的索引，標識其在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。<br><br>取值範圍：[0,4]。 |
|DbIndex |整數 |`-` |已棄用。 |
|Show |整數 |`-` |已棄用。 |
|Id |整數 |`-` |已棄用。 |


<span id="98e49104"></span>
#### RiskWarningSetting


|IsRiskWarningEnable |整數 |0 |描述 |
|---|---|---|---|
|是否啟用風險警告 |整數 |`0` |表示是否啟用提醒彈窗。<br><br>有效值：<br><br><br>* `0`：停用。<br><br>* `1`：啟用。 |
|RiskWarningButtonText |字串 |`已了解` |提醒彈窗的按鈕名稱。 |
|RiskWarningContent |字串 |`歡迎來到直播間！請遵守主辦方及您所在國家的法律法規，勿發送色情、非法、低俗或誹謗性評論。成為其他人的模範觀眾。我們誠摯請您勿以惡意搗亂或其他惡意行為破壞直播間的良好秩序。若您遇到與主播之間的私人商品推介，請運用您的常識判斷。` |提醒的內容。 |
|RiskWarningTitle |字串 |`提醒` |提醒彈窗的標題。 |


<span id="2168184b"></span>
## 範例

<span id="9acd03f7"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityBasicConfigAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="afba2dab"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityBasicConfigAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1666121102
    },
     "Result": {
        "ActivityId": 17218312****,
        "Name": "Live Room A",
        "LiveTime": 1666258566,
        "IsBeginLiveEnable": 0, 
        "IsCoverImageEnable": 1,
        "CoverImageUrl": "//example.image",
        "CoverImageUrlDefault": "//example.image",
        "VerticalCoverImageUrl": "//example.image",
        "IsPcBackImageEnable": 1,
        "PcBackImageUrl": "//example.image",
        "PcBackImageUrlDefault": "https://example.image",
        "IsMobileBackImageEnable": 1,
        "MobileBackImageUrl": "//example.image",
        "MobileBackImageUrlDefault": "https://example.imagee",
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
        "IsPreviewPromptEnable": 1,
        "PreviewPrompt": "The live stream will start soon.",
        "IsReservationEnable": 1,
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
        "IsColorSync": 1,
        "RiskWarningSetting": {
            "IsRiskWarningEnable": 0,
            "RiskWarningTitle": "",
            "RiskWarningContent": "",
            "RiskWarningButtonText": ""
        },
        "IsSDKPlayEnable": 1,
        "SDKPlayStatus": 2,
        "IsVideoChatDisplayed": 1,
        "IsSharedAddressDisplayed": 1,
        "EndTime": 1666358566,
        "IsAutoEndEnable": 1,
        "IsReleaseNoticeDisplayed": 1,
        "IsInteractiveEnable": 1,
        "InteractiveShowSetting": {
            "IsQuestionnaireDisplayed": 1,
            "IsDocDisplayed": 1,
            "IsCheckInDisplayed": 1,
            "IsQuizDisplayed": 0,
            "IsLuckDrawDisplayed": 0,
            "IsAnnouncementDisplayed": 0
        }
    }
}
```


<span id="50cace0d"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
