---
title: "Android Viewer SDK 發行說明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/android-viewer-sdk-fa-xing-shuo-ming-zh-TW"
---

Android Viewer SDK 發行說明提供所有更新的詳細記錄。本文件記錄每個版本的新功能、改進、相容性變更及修復問題，協助您掌握最新動態並規劃升級。

<span id="5b5274a3"></span>
## 2025 年 11 月


|發行日期 |版本 |說明 |
|---|---|---|
|2025\-11\-12 |1.65.0 |**改進**<br><br>支援更多 SDK 語言類型：<br><br><br>* 他加祿語<br><br>* 高棉語<br><br>* 寮語<br><br>* 緬甸語<br><br>* 馬來語<br><br>* 印地語<br><br>* 法語<br><br>* 德語<br><br>* 義大利語 |


<span id="5d9e0fee"></span>
## 2025 年 10 月


|發行日期 |版本 |說明 |
|---|---|---|
|2025\-10\-28 |1.64.1 |**問題修復**<br><br>修復部分問題。 |


<span id="8f3765ba"></span>
## 2025 年 9 月


|發行日期 |版本 |說明 |
|---|---|---|
|2025\-09\-25 |1.64.0 |**改進**<br><br><br>* 適配 Android 16 KB 功能。<br><br>* 支援播放日誌上報，提升故障排查能力。 |
|2025\-09\-09 |1.63.0 |**問題修復**<br><br>修復部分問題。 |


<span id="5537e8e4"></span>
## 2025 年 8 月


|發行日期 |版本 |說明 |
|---|---|---|
|2025\-08\-12 |1.62.0 |同步 Android Live Streaming SDK 的版本號。 |


<span id="1496aac1"></span>
## 2025 年 7 月


|發行日期 |版本 |說明 |
|---|---|---|
|2025\-07\-30 |1.61.4 |**問題修復**<br><br>修復部分問題。 |
|2025\-07\-28 |1.61.3 |* **相容性變更**<br><br>   在 `CustomSettings` 中，刪除以下方法：<br><br>   * 刪除 `setCommentEditViewHintTextColor` 方法。請改用 [setPopupInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#5fc5536f) 和 [setInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#e349d9b3)。<br><br>   * 刪除 `setCommentEditViewTextColor` 方法。請改用 [setPopupInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#a128a852) 和 [setInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#bb581984)。<br><br>* **新功能**<br><br>   * 新增 [setTopCommentBackgroundWidthFitContent](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#115fbc19) 方法，可設定置頂評論背景寬度是否隨內容寬度調整。<br><br>   * 新增 [setTopCommentViewCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#8b6e0523) 方法，可設定置頂評論背景的圓角半徑。<br><br>   * 新增 [setTopCommentNicknameColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#36d938dc) 方法，可設定置頂評論暱稱的顏色。<br><br>   * 新增 [setTopCommentNicknameFontSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#e85f2897) 方法，可設定置頂評論暱稱的字體大小。<br><br>   * 新增 [setTopCommentNicknameFontStyle](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#9891737b) 方法，可設定置頂評論暱稱的字體。<br><br>   * 新增 [setTopCommentContentLineSpacingExtra](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#826adc59) 方法，可設定置頂評論內容的行距。<br><br>   * 新增 [setTopCommentTagColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#452857ff) 方法，可設定置頂評論暱稱左側垂直線的顏色。<br><br>   * 新增 [setTopCommentBackgroundColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#b5661b0f) 方法，可設定置頂評論的背景顏色。<br><br>   * 新增 [setCommentContentLineSpacingExtra](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#016961d8) 方法，可設定評論內容的行距。<br><br>   * 新增 [setCommentCellCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#992d58e3) 方法，可設定評論 cell 的圓角半徑。<br><br>   * 新增 [setFunctionEntranceButtonCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#2a63cdb6) 方法，可設定直播間右下角功能按鈕（如購物車、互動工具按鈕）的圓角半徑。<br><br>   * 新增 [setPopupInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#5fc5536f) 方法，可設定評論輸入框編輯時（鍵盤顯示時）的佔位文字顏色。<br><br>   * 新增 [setPopupInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#a128a852) 方法，可設定評論輸入框編輯時（鍵盤顯示時）輸入文字的顏色。<br><br>   * 新增 [setInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#e349d9b3) 方法，可設定評論輸入框未編輯時（鍵盤隱藏時）的佔位文字顏色。<br><br>   * 新增 [setInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#bb581984) 方法，可設定評論輸入框未編輯時（鍵盤隱藏時）輸入文字的顏色。<br><br>   * 新增 [setInputBoxCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#40f70e3f) 方法，可設定評論輸入框未編輯時（鍵盤隱藏時）的圓角半徑。<br><br>* **問題修復**<br><br>   修復部分問題。 |
|2025\-07\-15 |1.60.0 |**改進**<br><br>優化了觀眾端即時抽獎功能的 UI 風格，提升用戶體驗，並支援在抽獎對話框中顯示獎品圖片。 |
|2025\-07\-01 |1.59.0 |**問題修復**<br><br>修復了一些問題。 |


<span id="f7d1c2fd"></span>
## 2025 年 6 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-06\-04 |1.58.0 |**新功能**<br><br>支援設定當螢幕鎖定時，PiP 視窗是否暫停影片播放。如需更多資訊，請參見[setPauseOnLockScreenInMiniWindow](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#f8150cf4)。 |


<span id="0c667da8"></span>
## 2025 年 5 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-05\-20 |1.57.1 |**功能優化**<br><br>優化了 SDK 日誌上報資訊，提升故障排查能力。 |


<span id="bd4b90e3"></span>
## 2025 年 4 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-04\-29 |1.56.0 |**問題修復**<br><br>修復了一些問題。 |
|2025\-04\-15 |1.55.2 |* **相容性變更**<br><br>   參數變更<br><br>   以下方法中的參數`reason`已更名為`info`：<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline)（於`ITVULiveRoomServerListener`中）<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline-2)（於`LiveRoomStatusListener`中）<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline-3)（於`SinglePlayerListener`中）<br><br>* **新功能**<br><br>   * 於[BDLForceOfflineReason](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#7321845b)中，新增觀眾被強制移出直播間的以下原因：<br><br>      * `BDLiveForceOfflineReasonIPBanned`（IP 位址被封禁）<br><br>      * `BDLiveForceOfflineReasonKickOut`（被踢出）<br><br>   * 支援將觀眾踢出直播間及封禁觀眾 IP 位址。<br><br>* **功能優化**<br><br>   優化了觀眾端簽到功能的 UI 風格，提升用戶體驗。 |
|2025\-04\-07 |1.54.2 |**問題修復**<br><br>Android 版本 1.49.0 \- 1.54.1 的 Viewer SDK 存在日誌事件上報問題。為避免影響線上問題的排查，請將這些版本升級至 1.54.2。 |
|2025\-04\-03 |1.54.1 |**問題修復**<br><br>修復了一些問題。 |
|2025\-04\-01 |1.54.0 |* **相容性變更**<br><br>   修改了 SDK 版本字尾。如需更多資訊，請參見[Integrating the Viewer SDK for Android](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android)。<br><br>   * 當匯入包含所有功能的 Viewer SDK 時，SDK 版本字尾由`pull-global:VersionNumber.external`變更為`pull:VersionNumber.globalFull`。例如，使用`com.bytedance.bdlive:bdlive-pull-global:1.53.0.external`可匯入包含所有功能的 Viewer SDK 1.53.0，使用`com.bytedance.bdlive:bdlive-pull:1.54.0.globalFull`可匯入包含所有功能的 Viewer SDK 1.54.0。<br><br>   * 當匯入不包含超低延遲直播功能的 Viewer SDK 時，SDK 版本字尾由`pull-global-remove-rtc:VersionNumber.external`變更為`pull:VersionNumber.globalLite`。例如，使用`com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external`可匯入不包含超低延遲直播功能的 Viewer SDK 1.53.0，使用`com.bytedance.bdlive:bdlive-pull:1.54.0.globalLite`可匯入不包含超低延遲直播功能的 Viewer SDK 1.54.0。<br><br>* **新功能**<br><br>   * 資料上報。<br><br>      支援資料上報。如需更多資訊，請參見[setBdlExternalReportConfiguration](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#543e5973)。<br><br>   * 自訂評論文字框<br><br>      支援設定評論文字框的最大字元數。如需更多資訊，請參見[setCommentInputCountLimit](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#542ef80d)。 |


<span id="da2a39bb"></span>
## 2025 年 3 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-03\-18 |1.53.0 |* **相容性變更**<br><br>   * 棄用部分方法<br><br>      設定直播間歡迎語文字顏色的方法`setWelcomeMsgFontColor`已棄用。請改用[setSystemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor)。<br><br>   * 範圍變更<br><br>      * [setHostCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentcolor)現僅支援設定主播評論的文字顏色。如需設定主播標籤顏色，請改用[setHostTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontcolor)。<br><br>      * [setCommentContentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentcontentfontstyle)現僅支援設定觀眾評論的字體。如需設定主播評論的字體，請改用[setHostCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontstyle)。<br><br>* **新功能**<br><br>   * 自訂評論文字框<br><br>      * 支援設定觀眾點擊評論文字框時是否自動彈出鍵盤。如需更多資訊，請參見[commentShouldInterceptEditing](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#6cc8bcc5)。<br><br>      * 支援設定評論文字框的事件攔截監聽器。如需更多資訊，請參見[setCommentEditingListener](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#71fed577)。<br><br>      * 支援在評論文字方塊非編輯狀態（即鍵盤未彈出時）設定以下內容：<br><br>         * 預設提示文字。如需更多資訊，請參閱 [setInputBoxPrompt](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#8682c301)。<br><br>         * 預設提示文字顏色。如需更多資訊，請參閱 [setInputBoxPromptColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#04aa818c)。<br><br>         * 背景顏色。如需更多資訊，請參閱 [setInputBoxBackgroundColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#4a693500)。<br><br>         * 圓角半徑。如需更多資訊，請參閱 [setInputBoxCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#740ee52f)。<br><br>         * 邊框寬度。如需更多資訊，請參閱 [setInputBoxBorderWidth](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#0e05259a)。<br><br>         * 邊框顏色。如需更多資訊，請參閱 [setInputBoxBorderColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#f81a58ab)。<br><br>   * 自訂評論區樣式<br><br>      * 支援設定直式模式下直播間描述與歡迎語的以下內容：<br><br>         * 標籤的字型、字型大小與顏色。如需更多資訊，請參閱 [setSystemCommentTagFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontstyle)、[setSystemCommentTagFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontsize) 及 [setSystemCommentTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontcolor)。<br><br>         * 主體的字型、字型大小與顏色。如需更多資訊，請參閱 [setSystemCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentfontstyle)、[setSystemCommentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentfontsize) 及 [setSystemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor)。<br><br>      * 支援設定相鄰評論之間的間距。如需更多資訊，請參閱 [setCommentItemSpacing](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentitemspacing)。<br><br>      * 支援設定評論列表底部與評論文字方塊頂部之間的間距。如需更多資訊，請參閱 [setRoomCommentListViewBottomMargin](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setroomcommentlistviewbottommargin)。<br><br>      * 支援設定下拉刷新元件的內容顏色，例如 `↓ 下拉載入更多評論`。如需更多資訊，請參閱 [setCommentListPullToRefreshColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentlistpulltorefreshcolor)。<br><br>      * 支援設定非主播暱稱與觀眾評論的字型大小。如需更多資訊，請參閱 [setCommentNicknameFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentnicknamefontsize) 及 [setCommentContentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentcontentfontsize)。<br><br>      * 支援設定主播標籤的字型大小與顏色。如需更多資訊，請參閱 [setHostTagFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontsize) 及 [setHostTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontcolor)。<br><br>      * 支援設定主播評論的字型與字型大小。如需更多資訊，請參閱 [setHostCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontstyle) 及 [setHostCommentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontsize)。 |
|2025\-03\-04 |1.52.1 |* **相容性變更**<br><br>   * 邏輯更新<br><br>      更新了直播過程中卡頓的處理邏輯。當 [setNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setneedautodemote) 的參數值為 `true` 時，新增根據 [setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall) 的參數值直接判斷是否切換主備流的檢查。<br><br>   * 用於設定部分自訂文字所需語言類型的 `setLanguageType` 方法已棄用。<br><br>* **新功能**<br><br>   * 新增 `TVULiveRoomServer` 實例建立成功時觸發的回調。如需更多資訊，請參閱 [onRoomServerCreated](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#38dde242)。<br><br>   * 新增 [getDynamicSettings](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#2323d292) 方法。可在觀眾進入直播間前或後呼叫此方法，以自訂直播間相關設定。<br><br>   * 支援在觀眾進入直播間後動態更新直播間 UI 及互動行為。如需更多資訊，請參閱 [Updating live room UI and interaction behaviors dynamically](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#7b1d80cb)。<br><br>   * 主播帳號<br><br>      * 支援關注主播。<br><br>      * 新增自訂驗證模式下觀眾關注事件的回調類。如需更多資訊，請參閱 [BDLUserFollowListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#35d14b67)。<br><br>      * 支援設定：<br><br>         * 關注或未關注主播時按鈕的文字與背景圖片。<br><br>         * 自訂驗證模式下觀眾關注主播事件的監聽器。<br><br>            如需更多資訊，請參閱 [DynamicCustomSettings](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings)。<br><br>   * 多語言<br><br>      支援以下語言：<br><br>      * 韓語<br><br>      * 泰語<br><br>      * 越南語<br><br>      * 阿拉伯語<br><br>      * 土耳其語<br><br>      * 西班牙語<br><br>      * 印尼語<br><br>      * 葡萄牙語<br><br>      * 俄語 |


<span id="1cfaefb3"></span>
## 2025 年 2 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-02\-24 |1.51.1 |**問題修復**<br><br>修復了部分問題。 |
|2025\-02\-18 |1.51.0 |* **相容性變更**<br><br>   * 刪除的方法<br><br>      由於置頂評論的 UI 樣式變更，刪除了以下方法：<br><br>      * 用於設定置頂標籤字型的 `setTopCommentTagFontStyle`。<br><br>      * `setTopCommentTagFontSize` 用於設定置頂標籤的字體大小。<br><br>      * `setTopCommentTagFontColor` 用於設定置頂標籤的文字顏色。<br><br>   * 預設值變更<br><br>      * 置頂評論顯示的最大行數預設值由 `2` 行變更為 `1` 行。詳情請參見 [setTopCommentRowCount](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#261f08a4)。<br><br>      * 直屏模式下直播間評論區高度預設值由螢幕高度的 1/3 變更為 194 dp。詳情請參見 [setPortraitCommentAreaHeight](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#4338c1b2)。<br><br>   * 適用範圍變更<br><br>      [setCommentItemBgColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#2b82be95) 方法現已同時適用於進場訊息。<br><br>* **新功能**<br><br>   商品卡片選單<br><br>   支援設定是否顯示商品標價的刪除線。詳情請參見 [setProductOriginalPriceShowStrikethrough](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#4a00b94d)。<br><br>* **優化項**<br><br>   優化商品卡片、置頂評論及進場訊息的 UI 樣式，提升用戶體驗。 |


<span id="21f31c7d"></span>
## 2025 年 1 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2025\-01\-21 |1.50.0 |**新功能**<br><br>支援設定人氣標籤文字的字體大小與顏色。詳情請參見 [setPeopleCountFontSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#d55a37d1) 和 [setPeopleCountTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#08753ee9)。 |
|2025\-01\-08 |1.49.0 |* **新功能**<br><br>   新增日誌查詢的單點追蹤能力，提升 SDK 問題定位能力。<br><br>* **修復問題**<br><br>   修復部分問題。 |


<span id="a40194d6"></span>
## 2024 年 12 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-12\-24 |1.48.0 |**修復問題**<br><br>修復部分問題。 |
|2024\-12\-10 |1.47.3 |* **兼容性變更**<br><br>   參數變更<br><br>   在 `addChildViewInLinearLayout` 方法中，用於指定直播間自定義浮窗組件顯示位置的參數由 `isLeftTop` 變更為 `location`。<br><br>* **新功能**<br><br>   支援在直播間右上角顯示自定義浮窗組件。 |


<span id="73bc45d7"></span>
## 2024 年 11 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-11\-26 |1.47.2 |* **新功能**<br><br>   浮窗廣告<br><br>   支援設定浮窗廣告是否顯示白色邊框及背景。<br><br>* **修復問題**<br><br>   修復部分問題。 |
|2024\-11\-07 |1.46.3 |* **新功能**<br><br>   漸層遮罩<br><br>   支援設定直屏模式下直播間頂部是否顯示漸層遮罩。若影片背景為白色，顯示漸層遮罩可提升直播間頂部白色文字的可視性。<br><br>* **修復問題**<br><br>   修復部分問題。 |


<span id="0384dd75"></span>
## 2024 年 10 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-10\-31 |1.46.2 |* **優化項**<br><br>   兼容 Android 15。<br><br>* **修復問題**<br><br>   修復部分問題。 |
|2024\-10\-28 |1.46.1 |**修復問題**<br><br>修復部分問題。 |
|2024\-10\-24 |1.46.0 |**修復問題**<br><br>修復部分問題 |
|2024\-10\-15 |1.45.0 |* **優化項**<br><br>   優化直屏模式下直播間的 UI 樣式。<br><br>* **修復問題**<br><br>   修復部分問題。 |


<span id="6ac25cae"></span>
## 2024 年 9 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-09\-12 |1.44.0 |新增簽到功能。 |
|2024\-09\-04 |1.43.4 |修復部分問題。 |


<span id="9b00f991"></span>
## 2024 年 8 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-08\-28 |1.43.3 |修復部分問題。 |
|2024\-08\-22 |1.43.2 |新增 [setShowCloseButtonWhenClearingScreen](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setshowclosebuttonwhenclearingscreen) 方法，用於配置清屏時是否顯示關閉直播間按鈕。 |
|2024\-08\-20 |1.43.1 |優化直屏模式下直播間底部購物車及禮物圖標的可點擊區域。 |
|2024\-08\-15 |1.43.0 |* 支援橫屏模式下顯示購物車圖標。<br><br>* SDK 已從 JCenter 遷移至 Maven Central。 |
|2024\-08\-06 |1.42.1 |修復部分問題。 |
|2024\-08\-01 |1.42.0 |新增 `setNeedAutoDemote` 方法，用於設定直播過程中網路卡頓時是否支援自動降級或提示。 |


<span id="4c21b251"></span>
## 2024 年 7 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-07\-23 |1.41.0 |優化預約直播的邏輯。 |


<span id="38c9288e"></span>
## 2024 年 6 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-06\-27 |1.40.0 |* 針對方法[joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#joinLiveRoom)，新增參數`joinRoomConfig`，並棄用參數`activityId`、`token`、`roomAuthMode`及`isPortrait`。<br><br>* 針對 `setPublicCommentNickName` 方法，新增 `nameRegisterListener` 參數。<br><br>* 新增[JoinRoomConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#f39b2118)，用於加入全功能直播間所需的配置。<br><br>* 新增[JoinResultListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#610d4532)，用於加入全功能直播間結果的回調類，包含[onJoinSuccess](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#fc43f86c)成功進入時及[onJoinFailed](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#7ff8f393)進入失敗時。<br><br>* 新增`PublicNickNameRegisterListener`，用於直播間驗證模式為公開時暱稱註冊結果的回調類，包含`onRegisterSuccess`註冊暱稱成功及`onRegisterFail`註冊失敗。<br><br>* 優化 UI 風格。<br><br>* 修復部分問題。 |
|2024\-06\-18 |1.39.3 |* 於`TVUSinglePlayerView`中新增`setCoverImageContainerVisibility`方法，用於配置直播間封面圖容器的顯示狀態。<br><br>* 修復部分問題。 |
|2024\-06\-12 |1.39.2 |修復部分問題。 |
|2024\-06\-11 |1.39.1 |* 新增[showFloatPermissionDialogInLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#98fe08db)方法，用於在全功能直播間顯示浮窗權限申請對話框。<br><br>* 新增[FloatUtil](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil)，直播間浮窗工具類，包含[checkPermission](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil#4b3dc68a)及[requestPermission](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil#f53394dc)方法，用於檢查 App 是否擁有系統浮窗權限，若無權限則跳轉至系統頁面申請該權限。<br><br>* 支援配置是否啟用資訊收集安全模式。更多資訊請參見[Step 5: Initialize the BDLive SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android#660b1619)。 |


<span id="abf86e2a"></span>
## 2024 年 4 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-04\-29 |1.32.0 |新增禮物獎勵功能。 |
|2024\-04\-15 |1.31.1 |支援優化 SDK 套件大小。更多資訊請參見[Optimizing the SDK package size ](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android#a90cb94f)。 |


<span id="098b07b9"></span>
## 2024 年 3 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-03\-28 |1.30.6 |修復部分問題。 |
|2024\-03\-27 |1.30.5 |修復部分問題。 |
|2024\-03\-11 |1.30.4 |修復部分問題。 |


<span id="b3c8eedb"></span>
## 2024 年 2 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-02\-29 |1.30.3 |支援在直式模式下顯示直播間描述。 |


<span id="cdd02e19"></span>
## 2024 年 1 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2024\-01\-23 |1.30.0 |* 新增以下功能：<br><br>   * 自訂分享地址<br><br>   * 倒數計時<br><br>   * 預約直播<br><br>   * 場館切換<br><br>   * 邀請海報<br><br>   * 系統通知<br><br>   * 歡迎訊息<br><br>   * 風險提示<br><br>   * 全螢幕浮水印<br><br>   * 問卷調查<br><br>   * 投票<br><br>   * 即時抽獎<br><br>      更多資訊請參見[SaaS 與 aPaaS 功能對比](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas)。<br><br>* 優化點讚功能：支援顯示點讚數並自訂相關配置。<br><br>* 支援上報直播品質數據。<br><br>* 新增混淆規則`log.**{*;}`。更多資訊請參見[Android 集成 Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android)。 |


<span id="2c6f1131"></span>
## 2023 年 11 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2023\-11\-13 |1.10.9 |相容 Android 14。 |


<span id="73379bac"></span>
## 2023 年 8 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2023\-08\-04 |1.10.7 |修復評論刪除相關的錯誤。 |


<span id="04d27ad2"></span>
## 2023 年 7 月


|發佈日期 |版本 |說明 |
|---|---|---|
|2023\-07\-20 |1.10.6 |* 將圖片庫組件遷移至 Glide。更多資訊請參見[Glide 版本相容性](https://docs.byteplus.com/en/byteplus-livesaas/docs/integrating-the-viewer-sdk-for-android#aca3bab7)。<br><br>* 修復部分問題。 |
