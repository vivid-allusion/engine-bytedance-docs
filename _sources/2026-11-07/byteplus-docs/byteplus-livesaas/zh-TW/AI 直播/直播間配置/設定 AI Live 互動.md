---
title: "設定 AI Live 互動"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/configuring-ai-live-interactions-zh-TW"
---

AI Live 可於直播期間自動回應觀眾留言及互動事件。完成**Live interaction**設定後，AI 主播會在適當時機暫停目前腳本，根據您的知識庫、提示詞及篩選規則產生回覆，然後繼續朗讀腳本。

本指南說明如何設定留言回覆、互動回覆及 AI 回覆測試。

> **注意**

> 直播期間無法更改互動設定。建議在直播前充分測試並完成相關設定。

## 先決條件

* 開始前，請先準備用於回覆的知識庫。詳情請參閱[知識庫設定](https://docs.byteplus.com/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-TW)。

* 若要在 TikTok 直播，請確保已新增欲開播 TikTok 帳號的 TikTok 使用者 ID：

   1. 於頂部導覽列輸入您的**TikTok user ID**，以擷取直播間的觀眾活動。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40fe23bba5e54a25ba69f4c6fa060a55~tplv-goo7wpa0wc-image.image)

      您可於 TikTok App 依下圖取得該 ID。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image)

* 若要在 Shopee 直播，請確保已安裝 Live Connector 瀏覽器擴充功能，將 Shopee 直播間的觀眾留言轉發至 BytePlus AI Live。詳情請參閱[透過 RTMP 在 Shopee 開啟直播](https://docs.byteplus.com/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp-zh-TW)。

## 操作步驟

1. 登入[BytePlus Live console](https://console.byteplus.com/)。

2. 於頂部導覽列選擇**AI Live**。

3. 在**Live Room**頁面，點選以開啟現有直播間或建立新直播間。

4. 於頂部導覽列點選**Live interaction**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a503096289f4da690c236f6c926b6cf~tplv-goo7wpa0wc-image.image)

   **Live interaction**視窗將側滑顯示。您可於此設定留言回覆策略及互動回覆。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02aa9041d7a54864b563c1cd587f42be~tplv-goo7wpa0wc-image.image)

### 設定留言回覆策略

1. 於**Comment reply**分頁下，新增先前建立的一般知識庫。僅於您將商品腳本加入直播並於**Knowledge base**頁面上傳對應檔案時，商品知識庫才會啟用。詳情請參閱[知識庫設定](https://docs.byteplus.com/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-TW)。

2. （選填）於**Prompt Settings**欄位自訂指引 AI 回覆風格的說明。

3. 調整**Dense Weight**以控制搜尋偏好。此數值（0.2 至 1.0）可平衡關鍵字比對與語意理解。較高的數值會優先考量問題的語意而非精確字詞。預設值為 0.5。

4. 於**Chat Settings**下設定忽略無關留言的規則。

   |**篩選規則** |**說明** |
   |---|---|
   |純表情符號訊息攔截 |忽略僅包含表情符號的留言。（支援 BytePlus Live 表情符號、標準表情符號及 TikTok 表情符號）。 |
   |重複洗版篩選 |篩選重複洗版的垃圾訊息。 |
   |聊天敏感詞 |攔截包含自訂敏感詞清單中詞語的留言。詳情請參閱[敏感詞攔截](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-sensitive-words)。 |
   |字數篩選 |設定留言可回覆的最小與最大字數。預設為 0 至 50 字，超過 50 字的留言將被忽略。 |
   |留言回覆策略 |* **虛擬人回覆**：虛擬人會語音朗讀並回覆留言。目前僅支援此策略。<br><br>* **留言區回覆**：自動在聊天室發送回覆。此選項尚未支援。 |

### 設定互動回覆策略

除了回覆留言外，虛擬主播亦可主動回應觀眾活動。於**Engage reply**分頁，開啟所需的回應類型並設定觸發頻率。直播期間，主播會暫停目前腳本，語音播報回應內容，然後繼續腳本。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94c1109d7cdd4c9fbb55cc7aa2eaaac0~tplv-goo7wpa0wc-image.image)

|**回應類型** |**說明** |
|---|---|
|**進房歡迎** |觀眾進入房間後，產生歡迎語並請主持人朗讀。你可設定觀眾進房觸發歡迎語的機率。預設值為 30%。 |
|**互動感謝** |觀眾按讚、分享或追蹤後，產生感謝語並請主持人朗讀。你可設定互動觸發感謝語的機率。預設值為 100%。 |

### 測試 AI 回覆

開播前，請模擬觀眾行為以預覽虛擬主播的回應方式。如此可驗證您的留言回覆及互動回應設定，並於需要時進行優化。

1. 於腳本設定頁的**Explanation text**區域右上角，點選**AI reply test**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b18a0c4eecc641f283a2f7dca1363a4e~tplv-goo7wpa0wc-image.image)

2. 在**AI response test**對話框中，您將扮演觀眾：傳送訊息給 AI 回覆機器人並查看其回覆。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08d3051167ec45c5b066859058a499a8~tplv-goo7wpa0wc-image.image)

3. （選填）於**Viewer nickname**欄位編輯測試所用名稱。

   * 觸發一項活動或發送留言以測試對應回覆：

   * **Join** / **Like** / **Follow** / **Gifting**：點選按鈕以模擬觀眾加入、按讚、關注或送禮。AI 回覆機器人會產生並顯示相符的互動回應。

   * **留言**：在文字框中輸入訊息，然後點擊**發送**。AI 回覆機器人會根據你的留言回覆設定和知識庫進行回覆。

4. 請在對話區檢查回覆內容，以確認其是否符合你的預期。如有需要，請調整互動設定、提示詞或知識庫，然後再次測試。

## 常見問題

### 問：部分觀眾暱稱包含表情符號或無法辨識的符號。我該怎麼做？

請在留言回覆設定中的**提示詞**加入指示，讓 AI 在回覆前將無法辨識的暱稱轉換為可讀文字。例如：

```Plain
If the username is emoji or unreadable symbol, transform those into readable before answering the question.
```

### 問：觀眾留言已進入直播間，但 AI 主持人未回覆。我該怎麼做？

請檢查以下項目：

* 留言是否因純表情符號、重複垃圾訊息、敏感詞或字數篩選規則而被攔截。

* 直播間是否已新增一般知識庫，或目前產品是否已上傳產品知識庫。

* 若留言來自第三方平台，請確認留言同步工具是否仍在同步，且留言是否已進入 BytePlus AI 直播間的**聊天**列表。
