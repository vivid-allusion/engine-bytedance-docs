---
title: "SaaS 與 aPaaS 的功能比較"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/saas-yu-apaas-de-gong-neng-bi-jiao-zh-TW"
---

為滿足你在自有產品環境中進行直播與觀看的需求，BytePlus Live 已整合並封裝底層能力，提供可獨立集成至你產品中的 aPaaS 解決方案。SaaS 解決方案與 aPaaS 解決方案在觀看頁面上的功能存在一定差異。詳情請參見下表。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">透過 iframe 嵌入所支援的功能與 SaaS 解決方案所支援的功能相同。詳情請參見 <a href="https://docs.byteplus.com/byteplus-livesaas/docs/embedding-a-viewing-page-with-iframe?version=v1.0">iframe</a>。</div>


* <div data-tips="true" data-tips-type="tip">下表中的 <strong>不適用</strong> 表示該功能在當前解決方案中無使用場景。</div>


* <div data-tips="true" data-tips-type="tip">下表中，若某功能僅支援自定義模式，則表示該功能適用於以下場景：</div>


   * <div data-tips="true" data-tips-type="tip">直播間的驗證模式設為自定義模式（適用於 Android/iOS/Flutter 的 Viewer SDK）。</div>


   * <div data-tips="true" data-tips-type="tip">直播間的驗證模式設為公開模式，且符合以下條件時（適用於 Android/iOS 的 Viewer SDK）：</div>


      * <div data-tips="true" data-tips-type="tip">對於 iOS 的 Viewer SDK：<code>BDLActivity</code> 的 <code>nickName</code> 值為空，且已調用 <code>setLoginProvider:</code> 方法。</div>


      * <div data-tips="true" data-tips-type="tip">對於 Android 的 Viewer SDK：已調用 <code>setCustomLoginListener</code> 方法。</div>




|功能 ||描述 |SaaS 解決方案（PC + 行動裝置） |Android/iOS/Flutter Viewer SDK |Web Viewer SDK |
|---|---|---|---|---|---|
|行銷推廣 |將直播間分享至社交平台 |觀眾可將直播間的 QR 碼或連結分享到 Facebook、WhatsApp 等社交平台。 |已支援 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">觀眾只能分享直播間的連結。</div><br> |已支援 |
||自定義觀看頁面的 favicon |自定義觀看頁面在瀏覽器地址列、書籤、分頁等位置顯示的 favicon。 |僅支援 PC |不適用 |未支援 |
||自定義分享地址 |自定義用於分享直播間的連結、QR 碼（包含邀請海報上顯示的碼）。 |已支援 |已支援 |已支援 |
||封面、背景與主題 |配置直播間的橫版與直版封面、背景圖片或顏色，以及主題。 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅電腦與橫屏模式的行動裝置支援背景圖片或顏色。</div><br> |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">不支援直式封面。</div><br> |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">背景圖片或顏色不適用。</div><br> |
||標頭圖片 |配置直播間的標頭圖片。 |僅支援 PC 及橫屏模式的行動裝置 |僅支援橫向模式 |僅於行動裝置橫向全頁整合時支援 |
||背景模糊 |將直播間背景進行模糊處理。 |僅支援 PC 及橫屏模式的行動裝置 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Android 僅支援直式模式。</div><br> |僅支援 PC 及橫屏模式的行動裝置 |
||播放器置頂 |隱藏標頭並將播放器置於觀看頁面頂部。 |僅支援 PC 及橫屏模式的行動裝置 |未支援 |僅支援 PC 及橫屏模式的行動裝置 |
||直播間橫版與直版模式 |橫版模式適用於培訓、會議、活動等場景，直版模式適用於行銷與電商等場景。 |已支援 |已支援 |已支援 |
||預覽 |上傳並播放直播預熱預覽，推廣內容並吸引更多用戶。 |已支援 |已支援 |已支援 |
||倒數計時 |觀眾在直播開始前進入直播間時，可以查看直播倒數計時。 |已支援 |已支援 |已支援 |
||顯示人氣值 |顯示直播間的線上觀眾人數。 |已支援 |已支援 |已支援 |
||預約直播 |觀眾可以預約直播。對於 SaaS 解決方案與 Web Viewer SDK，觀眾可在直播開始前收到簡訊通知。對於 Android Viewer SDK 與 iOS Viewer SDK，觀眾可將活動新增至手機的系統行事曆。 |已支援 |已支援 |已支援 |
||落地頁 |在行動裝置上，於觀眾進入觀看頁面前顯示有關直播的頁面。 |僅支援行動裝置 |未支援 |未支援 |
||主播帳號 |透過關聯主播帳號，觀眾可在觀看頁面關注主播，或前往其他平台（如 Facebook）上的主播主頁。 |已支援 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅 iOS 與 Android 支援關注主播，且需自訂驗證模式。</div><br> |已支援 |
||切換不同會場 |針對多會場直播（如線上就業博覽會或大型會議），可分享單一直播間連結，讓觀眾進入並切換不同會場。 |已支援 |已支援 |已支援 |
||邀請海報 |觀眾可分享直播間的邀請海報，邀請他人進入直播間。 |已支援 |已支援 |已支援 |
||播放器標誌 |在觀看頁面的播放器上顯示自訂標誌。 |已支援 |未支援 |僅於行動裝置橫向全頁整合、行動裝置直向模式及電腦端支援 |
||圖文選單 |自訂直播間圖文選單下方顯示的內容，包括圖片、文字與連結。 |已支援 |已支援 |已支援 |
||頁內廣告 |自訂頁面中間的廣告輪播，用於提升品牌知名度。觀眾點擊頁內廣告後，會跳轉至浮層或其他頁面。 |已支援 |已支援 |已支援 |
||頁首廣告 |自訂頁面頂部的跳轉網址。觀眾點擊頁首廣告後，會跳轉至浮層或其他頁面。 |僅支援 PC 及橫屏模式的行動裝置 |僅支援橫向模式 |僅於行動裝置橫向全頁整合時支援 |
||浮層廣告 |上傳圖片並自訂浮層廣告的跳轉網址。觀眾點擊浮層廣告後，會跳轉至浮層或其他頁面。 |已支援 |已支援 |已支援 |
||商品展示（商品卡片選單） |新增商品卡片選單，自訂商品資訊與跳轉網址，並調整商品顯示順序。觀眾點擊卡片後，會跳轉至浮層或其他頁面。亦可於播放器右側的浮動卡片中查看商品資訊。 |已支援 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">不支援在 BytePlus Live 控制台讀取顯示選單設定。</div><br> |已支援 |
||商品上架 |即時上架商品。 |已支援 |已支援 |已支援 |
||彙總直播選單 |建立推薦直播間列表。 |僅支援 PC 及橫屏模式的行動裝置 |未支援 |未支援 |
||子母畫面（PiP） |觀眾可在 PiP 模式下觀看直播、回放及預覽。 |僅支援 PC |已支援 |支援 PC 的 PiP 模式及行動裝置的小窗模式。 |
||系統通知 |在觀看頁面顯示抽獎通知、動態表情效果、禮物訊息及進場訊息。觀眾可封鎖此類系統通知。 |已支援 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">僅支援抽獎通知與進場訊息。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">僅自訂模式支援抽獎通知。</div><br> |已支援 |
||自訂簡訊 |自訂提醒簡訊，打造個性化直播間並提升友善度。 |已支援 |不適用 |已支援 |
|互動 |留言 |發送留言，包括彈幕留言 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅電腦與橫屏模式的行動裝置支援彈幕。</div><br> |支援留言，但不支援彈幕留言 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅電腦與橫屏模式的行動裝置支援彈幕。</div><br> |
||主持人留言 |突出顯示主持人留言。 |已支援 |已支援 |已支援 |
||置頂留言 |將留言置頂於聊天區。 |已支援 |已支援 |已支援 |
||按讚 |顯示按讚數量，自訂直播間按讚圖示，並允許觀眾對直播間或留言按讚。 |已支援 |已支援 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅支援在 BytePlus Live 控制台讀取按讚圖示設定。</div><br> |
||直播間簡介 |顯示直播間簡要介紹。 |僅支援 PC 及橫屏模式的行動裝置 |已支援 |僅支援 PC 及橫屏模式的行動裝置 |
||劇院模式 |網頁劇院模式，讓觀眾同時享受影片、留言及互動。 |僅支援 PC |不適用 |不適用 |
||即時抽獎 |手動或自動抽獎。VIP 名單中的成員有優先中獎權。 |已支援 |僅支援自訂模式 |已支援 |
||累積觀看時長抽獎 |觀眾在直播間累積觀看直播達一定時長即可參加抽獎。 |已支援 |未支援 |已支援 |
||禮物獎勵 |觀眾可使用免費禮物或兌換積分禮物來獎勵主持人。<br><br>如需讓觀眾兌換積分禮物，必須將積分系統與 BytePlus Live 整合。 |已支援 |僅支援自訂模式 |已支援 |
||問答選單 |觀眾可提問及回答問題。 |僅支援 PC 及橫屏模式的行動裝置<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅電腦支援在 BytePlus Live 控制台讀取顯示模式設定。</div><br> |未支援 |僅支援 PC 及橫屏模式的行動裝置<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在 BytePlus Live 控制台設定的顯示模式不會生效。只能透過 DOM 設定選單的顯示位置。</div><br> |
||簽到 |在直播間發起簽到。 |已支援 |已支援 |已支援 |
||問卷 |在直播間發送問卷。 |已支援 |已支援 |支援手動發送問卷及直播結束時發送問卷。 |
||投票 |在直播間發送投票。 |已支援 |已支援 |已支援 |
||預覽及下載文件 |觀眾可在直播間預覽及下載 Word、PPT 或 PDF 檔案。 |已支援 |未支援 |已支援 |
||互動選單 |在聊天中分享圖片及文字訊息以提供最新資訊或與觀眾互動，並可進行即時抽獎等其他互動。 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅電腦支援在 BytePlus Live 控制台讀取顯示模式設定。</div><br> |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">不支援在 BytePlus Live 控制台讀取顯示選單與顯示模式設定。</div><br> |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在 BytePlus Live 控制台設定的顯示模式不會生效。只能透過 DOM 設定選單的顯示位置。</div><br> |
||動態表情 |觀眾可在聊天區發送動態表情並觸發效果，增加留言數並提升直播間互動氛圍。 |已支援 |觀眾僅可在聊天區查看動態表情 |已支援 |
||選擇影片畫質 |觀眾可依需求選擇影片畫質。 |已支援 |已支援 |已支援 |
||全螢幕模式 |觀眾可在全螢幕模式下觀看直播、預覽及回放。 |已支援 |已支援 |已支援 |
||刷新直播 |直播期間，觀眾可重新整理頁面以重新連接至直播間。 |已支援 |已支援 |已支援 |
||查看歷史留言 |觀眾可透過向下滾動載入歷史留言。 |已支援 |已支援 |已支援 |
||熱門留言 |顯示按讚數最多的留言。 |僅支援 PC 及橫屏模式的行動裝置 |僅支援橫向模式 |僅支援 PC 及橫屏模式的行動裝置 |
|觀看限制 |公開訪問 |觀眾可直接進入直播間，無需登入。 |已支援 |已支援 |已支援 |
||密碼保護觀看 |觀眾必須輸入正確密碼才能進入直播間。 |已支援 |未支援 |未支援 |
||手機號登入 |提供簡訊驗證服務，以確保觀眾資訊的真實性。 |已支援 |未支援 |已支援 |
||手機號允許名單 |於直播開始前將觀眾的手機號加入允許名單，讓這些觀眾可直接進入直播間。你可選擇於直播開始前 5 分鐘向這些觀眾發送簡訊提醒。 |已支援 |未支援 |未支援 |
||邀請碼保護觀看 |觀眾必須輸入正確邀請碼才能進入直播間，每組邀請碼僅能邀請一位觀眾。 |已支援 |未支援 |未支援 |
||自定義授權 |授權你自有帳號系統，讓觀眾可使用你系統的用戶憑證進入直播間。 |已支援 |已支援 |已支援 |
||OAuth 2.0 |你的自有帳號系統支援使用 OAuth 2.0 標準授權協議進行單一登入。 |已支援 |未支援 |未支援 |
||備用觀看頁面地址 |生成備用連結以解決觀眾訪問問題。觀眾可使用此連結進入直播間，無任何觀看限制。 |已支援 |不適用 |不適用 |
|安全管控 |自定義敏感詞 |於直播間自定義敏感詞，含有敏感詞的留言僅對發送者可見，觀眾暱稱亦不可包含敏感詞。 |已支援 |已支援 |已支援 |
||留言審核後顯示 |留言需經審核後才會顯示於觀看頁面。 |已支援 |已支援 |已支援 |
||匯出、清除及刪除留言 |匯出、清除及刪除留言。 |已支援 |已支援 |已支援 |
||禁言觀眾 |對發送不當留言的觀眾進行禁言。 |已支援 |已支援 |已支援 |
||鎖定預覽 |將直播間狀態鎖定為**預覽**，即使你開始直播或發布回放，觀眾僅能在觀看頁面觀看預覽或查看封面。適用於需提前測試直播品質的場景。 |已支援 |已支援 |已支援 |
||歡迎訊息 |於聊天室顯示歡迎訊息，告知觀眾聊天規則，履行主辦方通知義務。 |已支援 |已支援 |已支援 |
||提醒 |觀眾進入直播間時顯示提醒彈窗，告知交易風險及聊天規則，履行主辦方通知義務。 |已支援 |已支援 |已支援 |
||更改暱稱 |觀眾可於直播間更改暱稱。 |已支援 |未支援 |已支援 |
||全螢幕浮水印 |以觀眾暱稱、手機號及其他資訊作為全螢幕浮水印。 |已支援 |已支援 |已支援 |
||全體觀眾禁言 |禁止所有觀眾發送留言。 |已支援 |已支援 |已支援 |
||踢出 |將觀眾踢出直播間，並阻止其重新加入直播間。 |已支援 |已支援 |已支援 |
||封鎖 IP 位址 |將觀眾踢出直播間，並阻止任何人透過被封鎖的 IP 位址存取直播間。 |已支援 |已支援 |已支援 |
|超低延遲直播 |超低延遲直播 |BytePlus Live 支援千萬級並發觀眾的超低延遲直播。與一般延遲直播（延遲為 5 至 10 秒）相比，超低延遲直播可將延遲降至 1 至 2 秒，為您帶來流暢且高品質的直播觀看體驗。 |已支援 |未支援 |已支援 |
|數據分析 |即時數據儀表板 |可在 BytePlus Live 控制台查看即時數據儀表板。 |已支援 |已支援 |已支援 |
||觀看數據 |可在 BytePlus Live 控制台查看基本數據，例如觀看時長、頁面瀏覽量（PV）、唯一觀眾（UV）及觀眾地理分布。您也可以查看並匯出詳細數據統計。 |已支援 |已支援 |已支援 |
||評論數據 |可在 BytePlus Live 控制台查看並匯出直播間的評論數據。 |已支援 |已支援 |已支援 |
||簽到數據 |可在 BytePlus Live 控制台查看並匯出簽到數據。 |已支援 |未支援 |已支援 |
||問卷數據 |可在 BytePlus Live 控制台查看並匯出問卷數據。 |已支援 |已支援 |已支援 |
||投票數據 |可在 BytePlus Live 控制台查看並匯出投票數據。 |已支援 |已支援 |已支援 |
||抽獎數據 |可在 BytePlus Live 控制台查看並匯出抽獎數據。 |已支援 |已支援 |已支援 |
||禮物數據 |可在 BytePlus Live 控制台查看並匯出禮物數據。 |已支援 |未支援 |已支援 |
||行銷數據 |可在 BytePlus Live 控制台查看直播間主帳號及廣告的 PV 和 UV。 |已支援 |已支援 |已支援 |
||直播預約數據 |可在 BytePlus Live 控制台查看並匯出直播預約數據。 |已支援 |未支援 |已支援 |
||觀眾行為數據 |可在 BytePlus Live 控制台查看並匯出觀眾行為數據。 |已支援 |已支援 |已支援 |
||帳號層級數據 |可在 BytePlus Live 控制台查看觀眾的用戶畫像。 |已支援 |已支援 |已支援 |
|回放 |自動發布回放至觀看頁面 |直播結束後產生的回放會自動發布至觀看頁面。 |已支援 |已支援 |已支援 |
||回放速度 |觀眾可選擇以 0.5 倍、0.75 倍、1.0 倍、1.25 倍、1.5 倍或 2 倍速度播放預覽或回放。 |已支援 |已支援 |已支援 |
||回放彈幕 |觀眾在觀看回放時可發送及查看播放器上滾動的彈幕。您可選擇將直播期間發送的彈幕顯示給觀看回放的觀眾。 |僅支援 PC 及橫屏模式的行動裝置 |未支援 |未支援 |
||標記精彩片段 |在回放中標記精彩片段，讓觀眾能輕鬆找到精彩時刻。 |僅支援 PC |未支援 |僅支援 PC |
|國際化 |多語言直播間 |觀眾可在直播間切換不同語言。 |已支援 |已支援 |已支援<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在電腦上，觀眾無法直接於觀看頁面切換語言，但可透過更改瀏覽器語言來變更觀看頁面的語言。</div><br> |
||評論翻譯 |評論可自動翻譯為多種語言。 |已支援 |已支援 |僅支援行動裝置 |
