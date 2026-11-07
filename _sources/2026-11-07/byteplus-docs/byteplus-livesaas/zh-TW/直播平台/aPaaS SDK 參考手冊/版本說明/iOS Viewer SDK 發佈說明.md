---
title: "iOS Viewer SDK 發佈說明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ios-viewer-sdk-fa-bu-shuo-ming-zh-TW"
---

本發佈說明提供 iOS Viewer SDK 所有更新的完整記錄。您可以使用本文件追蹤每個版本的新功能、相容性變更、優化及問題修復。

## 2026 年 10 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2026\-10\-23 |1.66.4 |**新功能**<br><br>新增支援透過 Swift Package Manager (SPM) 整合 SDK。SDK 以預編譯的 `.xcframework` 透過 SPM 二進位目標（binary target）分發。如需更多資訊，請參閱[整合 iOS 版 Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-ios-ban-viewer-sdk-zh-TW#b1a1a0ed)。 |

## 2025 年 11 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-11\-25 |1.65.2 |**問題修復**<br><br>修復部分問題。 |
|2025\-11\-17 |1.65.1 |**問題修復**<br><br>修復部分問題。 |
|2025\-11\-12 |1.65.0 |* **新功能**<br><br>   * 新增 [customizeFloatingViewImageViewImage](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#customizefloatingviewimageviewimage) 屬性，用於設置浮窗圖片視圖。<br><br>   * 多語言<br><br>      * 新增 [preferLanguage](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#preferlanguage) 屬性，用於設置觀看頁面的偏好語言。<br><br>      * 支援更多 SDK 語言類型：<br><br>         * 他加祿語<br><br>         * 高棉語<br><br>         * 寮語<br><br>         * 緬甸語<br><br>         * 馬來語<br><br>         * 印地語<br><br>         * 法語<br><br>         * 德語<br><br>         * 義大利語<br><br>* **問題修復**<br><br>   修復部分問題。 |

## 2025 年 8 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-09\-25 |1.64.0 |**相容性變更**<br><br>於 [BDLFloatingController](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlfloatingcontroller)：<br><br><br>* 移除 `floatingCardView`（浮動商品卡片視圖）屬性。該視圖現已由 [BDLFloatingControllerViewTag](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLFloatingControllerViewTag) 取代。<br><br>* 更新 [customizeFloatingCardView](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLFloatingController-customizefloatingcardview) 的回傳型別為 **BOOL**，用於指示是否顯示浮動商品卡片視圖。<br><br><br>**優化**<br><br>SDK 現已支援播放日誌上報，提升故障排查能力。 |
|2025\-09\-09 |1.63.0 |**相容性變更**<br><br>移除 `BDLTaskAwardRuleContactOptions`（獲獎者聯絡資訊）及 `BDLInteractiveAwardContactOptions`（獲獎者所需資訊）。請改用 [BDLAwardContactOptions](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlawardcontactoptions)（獲獎者所需資訊）。 |
|2025\-08\-26 |1.62.1 |**相容性變更**<br><br><br>* 刪除以下商品卡片點擊回調。請改用 [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock) 商品卡片點擊回調於 `BDLShoppingCardController`：<br><br>   * viewTappedBlock 於 `BDLCardView`<br><br>   * cardViewTappedBlock 於 `BDLShoppingCardView`<br><br>   * viewTappedBlock 於 `BDLFloatingCardView`<br><br>   * onCardClickBlock 於 `BDLFloatingController`<br><br>* [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock) 回調於 **BDLShoppingCardController** 新增 `clickPosition`（商品卡片點擊位置）參數，用於區分商品卡片的不同點擊位置。 |
|2025\-08\-12 |1.62.0 |同步 iOS 直播 SDK 的版本號。 |

## 2025 年 7 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-07\-28 |1.61.2 |* **相容性變更**<br><br>   部分屬性、方法或視圖已棄用或刪除：<br><br>   * 於 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29)，棄用 `inputBoxPromptColor` 屬性。請改用 [inputBoxPromptTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-inputboxprompttextcolor) 屬性。<br><br>   * 於 [BDLInteractiveToolController](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlinteractivetoolcontroller)，刪除 `customizeAwardContactView` 方法（用於自訂獲獎者個人資訊對話框視圖）。<br><br>   * 於 [BDLAwardWinnersView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlawardwinnersview)，刪除 `initWithAwardId:` 方法（用於初始化獲獎者名單視圖實例）。<br><br>   * 刪除 `BDLAwardContactView`（獲獎者個人資訊對話框視圖）。<br><br>* **新功能**<br><br>   * 新增 [topCommentFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentfontcolor) 屬性，用於設置置頂評論內容的文字顏色。<br><br>   * 新增 [topCommentBackgroundWidthFitContent](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentbackgroundwidthfitcontent) 屬性，用於設置置頂評論背景寬度是否隨內容寬度調整。<br><br>   * 新增 [topCommentViewCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentviewcornerradius) 屬性，用於設置置頂評論背景的圓角。<br><br>   * 新增 [topCommentNicknameColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentnicknamecolor) 屬性，用於設置置頂評論暱稱的顏色。<br><br>   * 新增 [topCommentNicknameFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentnicknamefont) 屬性，用於設置置頂評論暱稱的字型及字型大小。<br><br>   * 新增 [topCommentContentLineSpacingExtra](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentcontentlinespacingextra) 屬性，用於設置置頂評論內容的行距。<br><br>   * 新增 [topCommentBackgroundColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentbackgroundcolor) 屬性，用於設置置頂評論背景顏色。<br><br>   * 新增 [commentContentLineSpacingExtra](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentcontentlinespacingextra) 屬性，用於設置評論內容的行距。<br><br>   * 新增 [commentCellCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentcellcornerradius) 屬性，用於設定評論單元格的圓角半徑。<br><br>   * 新增 [popupInputBoxPromptTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#popupinputboxprompttextcolor) 屬性，用於設定評論輸入框在啟用狀態（即鍵盤顯示時）的佔位文字顏色。<br><br>   * 新增 [popupInputBoxTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#popupinputboxtextcolor) 屬性，用於設定評論輸入框在啟用狀態（即鍵盤顯示時）所輸入文字的顏色。<br><br>   * 新增 [inputBoxPromptTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-inputboxprompttextcolor) 屬性，用於設定評論輸入框在未啟用狀態（即鍵盤隱藏時）的佔位文字顏色。<br><br>   * 新增 [FunctionEntranceButtonCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#functionentrancebuttoncornerradius) 屬性，用於設定直播間右下角功能按鈕（如購物車、互動工具按鈕）的圓角半徑。<br><br>   * 新增錯誤碼 `BDLErrorCodeForceOffline`，表示當前觀眾已被封禁，無法進入直播間。更多資訊請參見 [Viewer SDK for iOS: Error codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-error-codes)。<br><br>* **問題修復**<br><br>   修復部分問題。 |
|2025\-07\-15 |1.60.0 |* **相容性變更**<br><br>   修改 `Podfile` 檔案中 BPLive 的引用方式。更多資訊請參見 [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed)。<br><br>* **優化項**<br><br>   優化觀看頁面實時抽獎功能的 UI 風格，提升用戶體驗，並支援在抽獎對話框中顯示獎品圖片。 |
|2025\-07\-01 |1.59.0 |**問題修復**<br><br>修復部分問題。 |

## 2025 年 6 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-06\-04 |1.58.0 |同步 iOS 直播 SDK 的版本號。 |

## 2025 年 5 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-05\-20 |1.57.0 |* **優化項**<br><br>   優化 SDK 日誌上報資訊，提升故障排查能力。<br><br>* **問題修復**<br><br>   修復 SDK 初始化相關問題。 |
|2025\-05\-06 |1.56.1 |**問題修復**<br><br>修復部分問題。 |

## 2025 年 4 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-04\-29 |1.56.0 |* **相容性變更**<br><br>   * 修改初始化方式。更多資訊請參見 [Step 4: Initialize BPLive](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#f951ba1a)。<br><br>   * 新增依賴時，刪除 `pod 'RangersAppLog', :podspec => ' https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/RangersAppLog/6.16.2/RangersAppLog.podspec.json'`。更多資訊請參見 [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed)。<br><br>   * 刪除方法<br><br>      在 `BDLShoppingCardController` 中，刪除商品 URL 加載時觸發的回調 `openUrlBlock`。請改用 [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock)。<br><br>   * 參數變更<br><br>      以下方法新增參數 `cardModel`（商品卡片模型），用於獲取商品資訊。<br><br>      * [viewTappedBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCardView)（於 `BDLCardView`）<br><br>      * [cardViewTappedBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardView)（於 `BDLShoppingCardView`）<br><br>      * [viewTappedBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLFloatingCardView)（於 `BDLFloatingCardView`）<br><br>* **新功能**<br><br>   * 商品卡片<br><br>      新增以下商品卡片被點擊時觸發的回調。<br><br>      * [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLFloatingController)（於 `BDLFloatingController`）<br><br>      * [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock)（於 `BDLShoppingCardController`）<br><br>   * 初始化<br><br>      * 新增 SDK 初始化方法。更多資訊請參見 [startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-startwithauthinfo-complete)。<br><br>      * 支援獲取 `BDLiveManager` 實例。更多資訊請參見 [sharedInstance](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-sharedinstance)。<br><br>* **問題修復**<br><br>   修復部分問題。 |
|2025\-04\-16 |1.55.1 |**優化項**<br><br>優化部分越南語 UI 文本。 |
|2025\-04\-15 |1.55.0 |* **相容性變更**<br><br>   * 參數變更<br><br>      以下方法中的參數 `reason` 改為 `info`：<br><br>      * [onUserForceOfflineBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#onuserforceofflineblock)<br><br>      * [basePlayerView:onUserForceOffline:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#baseplayerview-onuserforceoffline)<br><br>      * [playerView:onUserForceOffline:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#playerview-onuserforceoffline)<br><br>      * [floatingPlayer:onUserForceOffline:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#floatingplayer-onuserforceoffline)<br><br>   * 枚舉值類型變更<br><br>      在 [BDLForceOfflineReason](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlforceofflinereason) 中，`BDLiveForceOfflineReasonMultiLogin` 改為 `BDLForceOfflineReasonMultiLogin`，`BDLiveForceOfflineReasonCheckInTimeout` 改為 `BDLForceOfflineReasonCheckInTimeout`。<br><br>* **新功能**<br><br>   * 在 [BDLForceOfflineReason](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlforceofflinereason) 中，新增以下觀眾被強制移出直播間的原因：<br><br>      * `BDLForceOfflineReasonIPBanned`（IP 地址被封禁）<br><br>      * `BDLForceOfflineReasonKickOut`（被踢出）<br><br>   * 支援將觀眾踢出直播間及封禁觀眾 IP 地址。<br><br>* **優化項**<br><br>   優化觀看頁面簽到功能的 UI 風格，提升用戶體驗。<br><br>* **問題修復**<br><br>   修復部分問題。 |
|2025\-04\-01 |1.54.0 |* **相容性變更**<br><br>   * 刪除部分方法。<br><br>      * 已刪除用於設定是否允許觀眾在評論輸入框輸入內容的方法 `textFieldShouldBeginEditing`。請改用方法 [textViewShouldBeginEditing](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-textviewshouldbeginediting)。<br><br>      * 在 [BDLCommentInputBaseView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentinputbaseview) 中，已刪除用於自訂評論輸入框的方法 `customizeTextField`。請改用 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 或 [BDLCommentBaseConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration%28Config%29) 中的屬性。<br><br>      * 在 [BDLCommentInputBaseView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentinputbaseview) 中，已刪除屬性 `textField`（評論輸入框）。<br><br>      * 在 [BDLCommentBaseConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration%28Config%29) 中，已刪除屬性 `inputTextIconImage`（評論輸入框左側圖示）。<br><br>   * 方法名稱變更<br><br>      重置評論輸入框的方法由 `resetTextField:` 改為 [resetTextView:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#resettextview)。<br><br>* **新功能**<br><br>   * 數據上報。<br><br>      新增數據上報支援。詳情請參見 [externalReportConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#externalreportconfig)。<br><br>   * 自訂評論輸入框<br><br>      * 支援設定評論輸入框允許輸入的最大字數。詳情請參見 [commentInputCountLimit](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentinputcountlimit)。<br><br>      * 支援設定評論輸入框內輸入文字的顏色。詳情請參見 [inputBoxTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxtextcolor)。 |

## 2025 年 3 月

|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-03\-18 |1.53.0 |* **相容性變更**<br><br>   * 刪除部分屬性<br><br>      在 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 中，已刪除 `likeIconImage`（未點讚評論圖示）及 `likedIconImage`（已點讚評論圖示）。請改用 [commentLikeIcon](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-commentlikeicon) 和 [commentLikedIcon](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-commentlikedicon)。<br><br>   * 部分屬性已棄用<br><br>      在 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 中，屬性 `welcomeTextColor`（歡迎訊息文字顏色）已棄用。請改用 [systemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-systemcommentcolor)。<br><br>   * 範圍變更<br><br>      * [commentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentfont) 現僅支援設定非主播評論的字型、字型大小及其他屬性。如需設定主播評論的相關屬性，請使用 [hostCommentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hostcommentfont)。<br><br>      * [hostCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hostcommentcolor) 現僅支援設定主播評論的文字顏色。如需設定主播標籤顏色，請使用 [hostTagColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hosttagcolor)。<br><br>* **新功能**<br><br>   * 自訂評論輸入框<br><br>      * 支援設定是否允許觀眾在評論輸入框輸入內容。詳情請參見 [textFieldShouldBeginEditing](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-textviewshouldbeginediting)。<br><br>      * 支援設定評論輸入框在非編輯狀態（即鍵盤未彈出，觀眾進入直播間前後）時的以下屬性：<br><br>         * 背景顏色。詳情請參見 [inputBoxBackgroundColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxbackgroundcolor)。<br><br>         * 圓角半徑。詳情請參見 [inputBoxCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxcornerradius)。<br><br>         * 邊框寬度。詳情請參見 [inputBoxBorderWidth](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxborderwidth)。<br><br>         * 邊框顏色。詳情請參見 [inputBoxBorderColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxbordercolor)。<br><br>         * 提示文字顏色。詳情請參見 [inputBoxPromptColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxpromptcolor)。<br><br>   * 自訂評論區樣式<br><br>      * 支援設定直播間直式描述及歡迎訊息的以下屬性：<br><br>         * 標籤的字型、字型大小及其他屬性。詳情請參見 [systemTagFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#systemtagfont)。<br><br>         * 標籤顏色。詳情請參見 [systemTagColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#systemtagcolor)。<br><br>         * 主體的字型、字型大小及其他屬性。詳情請參見 [systemCommentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#systemcommentfont)。<br><br>         * 主體文字顏色。詳情請參見 [systemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-systemcommentcolor)。<br><br>      * 支援設定相鄰評論單元格之間的間距。詳情請參見 [distanceBetweenCell](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#distancebetweencell)。<br><br>      * 支援設定評論列表底部與評論輸入框頂部之間的間距。詳情請參見 [commentListViewBottomMargin](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentlistviewbottommargin)。<br><br>      * 支援設定下拉刷新組件內容顏色，例如 `↓ Pull to load more comments`。詳情請參見 [commentListPullToRefreshColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentlistpulltorefreshcolor)。<br><br>      * 支援設定主播標籤顏色及主播評論的字型、字型大小等屬性。詳情請參見 [hostTagColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hosttagcolor) 和 [hostCommentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hostcommentfont)。<br><br>   * 新增屬性 [floatingControllerConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#floatingcontrollerconfig)（浮動視窗控制器配置），支援設定當鍵盤彈出時，是否自動隱藏所有浮動視窗控制項，例如浮動商品卡、浮動廣告及互動工具浮窗。<br><br>* **已修復問題**<br><br>   修復部分問題。 |
|2025\-03\-04 |1.52.0 |* **相容性變更**<br><br>   * 邏輯更新<br><br>      更新直播過程中卡頓的處理邏輯。當 [isNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#isneedautodemote) 的值為 `YES` 時，新增判斷，根據 [backupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLBasePlayerConfiguration-backupdowngradewhenstall) 的值直接切換主備流。<br><br>   * 刪除部分方法<br><br>      於 [BDLMultiLanguageView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlmultilanguageview)，<br><br>      * 刪除用於顯示語言選擇對話框視圖的 `show` 方法。請改用 [bottomShowInView:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bottomshowinview-completion) 方法。<br><br>      * 刪除用於隱藏語言選擇對話框視圖的 `hide` 方法。請改用 [hideWithCompletion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hidewithcompletion) 方法或 [hideWithAnimation:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hidewithanimation-completion) 方法。<br><br>* **新功能**<br><br>   * 主播帳號<br><br>      * 支援關注主播。<br><br>      * 新增 [businessAccountConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#businessaccountconfig)（主播帳號配置）屬性，支援設定「關注」及「已關注」狀態按鈕的文字與背景圖片。<br><br>   * 多語言<br><br>      * 支援以下語言：<br><br>         * 韓語<br><br>         * 泰語<br><br>         * 越南語<br><br>         * 阿拉伯語<br><br>         * 土耳其語<br><br>         * 西班牙語<br><br>         * 印尼語<br><br>         * 葡萄牙語<br><br>         * 俄語<br><br>      * [highLightString](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#highlightstring) 現已支援多語言。 |

## 2025 年 2 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2025\-02\-24 |1.51.1 |同步 iOS 直播 SDK 的版本號。 |
|2025\-02\-18 |1.51.0 |* **相容性變更**<br><br>   * 刪除部分方法、屬性、回調及視圖<br><br>      * 刪除 `BDLBottomNoticeView`（橫屏直播間入口消息視圖）及 `BDLEnterLiveRoomNoticeView`（直屏直播間入口消息視圖）。請改用 [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCommentAndNoticeView)（評論及通知視圖）。<br><br>      * 刪除 `BDLBottomNoticeViewProtocol`（底部消息通知視圖協議）。<br><br>      * 於 [BDLTopCommentView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdltopcommentview)，刪除 `shouldHandleGestureRecognizerWithTouch:` 方法（是否處理手勢）。<br><br>      * 於 [BDLFloatingCardView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlfloatingcardview)，刪除屬性 `containerView`（容器視圖）、`titleLabel`（商品名稱標籤）、`highLightBgView`（零售價背景視圖）、`highLightLabel`（零售價標籤）、`imageView`（商品圖片）、`closeButton`（關閉按鈕）、`goImageView`（GO 圖標視圖）、`explainingButton`（講解標籤）。<br><br>      * 於 [BDLCommentView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentview)，<br><br>         * 刪除底部消息通知視圖屬性 `bottomNoticeView`。<br><br>         * 刪除自定義底部消息通知視圖方法 `customizeBottomNoticeView`。請改用 [customizeCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLMenuBarView-customizecommentandnoticeview) 方法，自定義橫屏及直屏直播間的評論及通知視圖。<br><br>      * 於 [BDLLivePullViewController()](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLivePullViewController%28%29)，刪除評論視圖屬性 `commentView`。請改用評論及通知視圖屬性 [commentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLivePullViewController%28%29-commentandnoticeview)。<br><br>      * 於 [BDLMenuBarView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlmenubarview)，<br><br>         * 刪除橫屏直播間菜單欄評論視圖屬性 `commentView`。請改用橫屏直播間評論及通知視圖屬性 [commentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#commentandnoticeview-2)。<br><br>         * 刪除橫屏直播間菜單欄自定義評論視圖方法 `customizeCommentView`。請改用橫屏直播間自定義評論及通知視圖方法 [customizeCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#customizecommentandnoticeview)。<br><br>      * 因置頂評論 UI 風格變更，刪除 `topTagFont` 屬性（[BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 中置頂標籤字體及字體大小）。<br><br>   * 方法移動<br><br>      * 以下方法由 [BDLCommentView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCommentView) 移至 [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentandnoticeview)。<br><br>         * `topCommentClickBlock`（點擊置頂文字評論時觸發的回調）<br><br>         * `topCommentNicknameClickBlock`（點擊置頂評論暱稱時觸發的回調）<br><br>      * 以下方法已從[BDLLivePullViewControllerConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdllivepullviewcontrollerconfig)移至[BDLCommentAndNoticeViewConfiguration](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentandnoticeviewconfiguration)。<br><br>         * `customizePortraitCommentViewHeight`用於自訂直式直播間評論區（包含文字框）的高度。<br><br>         * `customizeCommentView`用於自訂直式直播間的評論視圖。<br><br>         * `customizeNoticeContainerView`用於自訂通知容器視圖。<br><br>   * 已更新[setNickname:complete: ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLUserInfoConfiguration-setnickname-complete)方法的實現邏輯。此方法現在僅支援在觀眾進入直播間之前呼叫。若註冊失敗，SDK會使用`nickname`的值完成註冊，並於下一次嘗試時觸發完成回調。若再次註冊失敗，SDK將在後續嘗試中持續重試，直到成功為止。<br><br>   * 預設值變更<br><br>      * 置頂評論顯示行數的預設值已從`2`變更為`1`。詳情請參閱[rowsOfTopComment](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-rowsoftopcomment)。<br><br>      * 直式直播間評論區（包含評論文字框）的預設高度已從完整功能直播間高度的0.4倍變更為241點。詳情請參閱[customizePortraitCommentViewHeight](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCommentAndNoticeViewConfiguration-customizeportraitcommentviewheight)。<br><br>   * 適用範圍變更<br><br>      [backgroundColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration%28Config%29-backgroundcolor)屬性現在也適用於進場訊息。<br><br>* **新功能**<br><br>   * 商品卡片選單<br><br>      新增[productOriginalPriceShowStrikethrough](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#productoriginalpriceshowstrikethrough)方法，用於設定是否顯示商品原價的刪除線。<br><br>   * 浮動商品卡片<br><br>      新增[cornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#cornerradius-2)屬性，用於設定浮動商品卡片背景的圓角。<br><br>   * 進場訊息<br><br>      * 新增[joinRoomMsgNicknameColor ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-joinroommsgnicknamecolor)屬性，用於設定進場訊息中暱稱文字的顏色。<br><br>      * 新增[joinRoomMsgContentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-joinroommsgcontentcolor)屬性，用於設定進場訊息內容文字的顏色。<br><br>   * 置頂評論<br><br>      新增[topCommentView:didClickComment: ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#topcommentview-didclickcomment)方法。當觀眾點擊置頂評論中的文字評論或空白區域時，SDK會呼叫此方法。<br><br>   * 直播間配置<br><br>      新增評論與通知視圖的配置。詳情請參閱[commentAndNoticeViewConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLLiveRoomConfiguration-commentandnoticeviewconfig)。<br><br>   * 錯誤碼<br><br>      新增錯誤碼`BDLErrorCodeUserHasJoinLiveRoom`，表示呼叫[setNickname:complete: ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLUserInfoConfiguration-setnickname-complete)方法時設定用戶暱稱失敗。詳情請參閱[Viewer SDK for iOS: Error codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-error-codes)。<br><br>* **優化項目**<br><br>   優化商品卡片、置頂評論及進場訊息的UI樣式，提升用戶體驗。 |

## 2025 年 1 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2025\-01\-21 |1.50.0 |* **相容性變更**<br><br>   刪除屬性<br><br>   於`BDLPlayerLandscapeConfiguration`中，刪除`popularityFont`（人氣標籤文字的字型與字型大小）及`popularityImage`（人氣圖示）屬性。<br><br>* **新功能**<br><br>   直播間人氣<br><br>   支援配置人氣圖示，以及人氣標籤文字的字型、字型大小與顏色。 |
|2025\-01\-08 |1.49.0 |* **相容性變更**<br><br>   * 於`BDLPlayerViewDelegate`中，刪除觀眾雙擊播放器時呼叫的`playerViewDidDoubleTap:`方法。<br><br>   * 變更導入SDK的URL及整合SDK時需新增的BPLive依賴。詳情請參閱[Integrating the Viewer SDK for iOS](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios)。<br><br>* **新功能**<br><br>   * 若載入直播流時發生錯誤，可透過`liveError`取得具體錯誤資訊。<br><br>   * 新增日誌查詢的單點追蹤支援，提升識別SDK問題的能力。<br><br>* **修復問題**<br><br>   修復部分問題。 |

## 2024 年 12 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-12\-24 |1.48.0 |**修復問題**<br><br>修復部分問題。 |
|2024\-12\-10 |1.47.3 |* **相容性變更**<br><br>   自訂直式直播間中`customizePageAdView`框架的方法已變更：現在不再於`customizeViewConstraints`中使用`mas_remakeConstrain`，而是必須直接修改`frame`。然而，`frame.origin`會被忽略，這表示僅能修改`frame.size`。<br><br>* **新功能**<br><br>   支援在直播間右上角顯示自訂浮動視圖。<br><br>* **問題修復**<br><br>   修復部分問題。 |
|2024\-12\-03 |1.47.2 |**新功能**<br><br>支援使用 TTSDK 的靜態庫版本。更多資訊請參見[Using the static library version of TTSDK](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#e0af7cf0)。 |

## 2024 年 11 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-11\-26 |1.47.1 |**問題修復**<br><br>修復部分問題。 |

## 2024 年 10 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-10\-31 |1.46.1 |* **優化**<br><br>   適配 iOS 18。<br><br>* **問題修復**<br><br>   修復部分問題。 |
|2024\-10\-24 |1.46.0 |* **新功能**<br><br>   * Now Playing 資訊區塊（您的應用播放的媒體）。<br><br>      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71c238a4a84348d3833ad3942d38ede2~tplv-goo7wpa0wc-image.image)<br><br>      * 新增支援自訂 Now Playing 資訊。<br><br>      * 新增支援設定是否響應 Now Playing 資訊區塊中的用戶操作。<br><br>* **問題修復**<br><br>   修復部分問題。 |
|2024\-10\-15 |1.45.0 |* **優化**<br><br>   優化直式直播間的 UI 風格。<br><br>* **問題修復**<br><br>   修復部分問題。 |

## 2024 年 9 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-09\-12 |1.44.0 |* 新增簽到功能。<br><br>* 適配 Xcode 16。<br><br>* 在`BDLRiskWarningView`中，`maskView`屬性更名為`bottomMaskView`。<br><br>* 在`BDLPlayerView`中，`maskView`屬性更名為`playerMaskView`。 |
|2024\-09\-04 |1.43.3 |修復部分問題。 |

## 2024 年 8 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-08\-22 |1.43.2 |新增[showCloseButtonWhenClearingScreen](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#showclosebuttonwhenclearingscreen)屬性，用於配置清屏時是否顯示關閉直播間按鈕。 |
|2024\-08\-15 |1.43.0 |SDK 現已支援橫屏模式下顯示購物車圖示。 |
|2024\-08\-06 |1.42.1 |修復部分問題。 |
|2024\-08\-01 |1.42.0 |* 更改`TTNetworkManager`依賴的版本號。更多資訊請參見[Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed)。<br><br>* 在`BDLBasePlayerConfiguration`中，新增`isNeedAutoDemote`方法，用於設定直播過程中網路卡頓時是否支援自動降級或提供提示。 |

## 2024 年 7 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-07\-23 |1.41.0 |優化直播預約邏輯。 |

## 2024 年 6 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-06\-28 |1.40.1 |* 在`BDLUpperAdView`的`viewTappedBlock`方法中新增`enableFloating`參數。<br><br>* 修復部分問題。 |
|2024\-06\-26 |1.40.0 |* 刪除[BDLActivity](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-api-zh-TW#0b6ae4e5)中的`nickName`屬性。<br><br>* 在[BDLLiveEngine](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-api-zh-TW#e53a9ad6)中棄用`joinLiveRoomWithActivity:`方法。<br><br>* 在`BDLLiveRoomConfiguration`中新增`userInfoConfig`屬性（用戶資訊配置）。<br><br>* 新增用戶資訊配置`BDLUserInfoConfiguration`，包含`setNickname:complete:`方法，於公開驗證模式下設定用戶暱稱。<br><br>* 在`BDLCommentView`中新增`imageTextButton`（直式模式下圖文菜單按鈕）及`imageTextClickBlock`（直式模式下圖文菜單按鈕點擊回調）方法。<br><br>* 在`BDLCommentViewConfiguration`中新增`imageTextButtonImage`（直式模式下圖文菜單按鈕圖片）屬性。<br><br>* 支援直式模式下顯示圖文菜單。<br><br>* 優化 UI 風格。<br><br>* 修復部分問題。 |
|2024\-06\-07 |1.39.0 |更新整合 SDK 時需新增的 BPLive 依賴。更多資訊請參見[Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed)。 |

## 2024 年 5 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-05\-30 |1.35.0 |刪除用於置頂評論及 H5 頁面的`BDLAlertController`（如觀眾點擊商品卡片或廣告後浮層顯示的頁面），並新增`BDLPopupTopCommentView`及`BDLPopupWebView`以提升兼容性。 |

## 2024 年 4 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-04\-29 |1.34.0 |* 新增禮物獎勵功能。<br><br>* 修復 PiP 的相關問題。 |
|2024\-04\-15 |1.33.0 |* 支援優化 SDK 套件大小。如需更多資訊，請參閱 [Optimizing the SDK package size](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#762f64ce)。<br><br>* 修復部分問題。 |

## 2024 年 3 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-03\-27 |1.32.2 |修復部分問題。 |
|2024\-03\-11 |1.32.1 |* 優化依賴項。當僅整合 iOS Viewer SDK 時，`TTVideoEditor` 依賴項不再需要。如需更多資訊，請參閱 [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-ios#6fbbbde0)。<br><br>* 修復部分問題。 |

## 2024 年 2 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-02\-29 |1.32.0 |支援在直式模式下顯示直播間描述。 |

## 2024 年 1 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-01\-24 |1.26.0 |* 若要更新至此版本，必須修改 `Podfile` 檔案以新增 BPLive 依賴項。如需更多資訊，請參閱 [Integrating the Viewer SDK for iOS](https://docs.byteplus.com/en/byteplus-livesaas/docs/integrating-the-viewer-sdk-for-ios?version=v1.0#6fbbbde0)。<br><br>* 新增以下功能：<br><br>   * 自訂分享地址<br><br>   * 倒數計時<br><br>   * 預約直播<br><br>   * 切換不同場館<br><br>   * 邀請海報<br><br>   * 系統通知<br><br>   * 歡迎訊息<br><br>   * 風險提示<br><br>   * 全螢幕浮水印<br><br>   * 問卷調查<br><br>   * 投票<br><br>   * 即時抽獎<br><br>      如需更多資訊，請參閱 [Feature comparison between SaaS and aPaaS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas)。<br><br>* 優化點讚功能：支援顯示點讚數並可自訂相關配置。<br><br>* 支援回報直播品質數據。 |

## 2023 年 8 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2023\-08\-04 |1.25.2 |修復評論刪除相關的錯誤。 |

## 2023 年 7 月

|發佈日期 |版本 |說明 |
|---|---|---|
|2023\-07\-20 |1.25.0 |修復部分問題。 |
