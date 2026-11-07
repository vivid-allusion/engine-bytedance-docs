---
title: "啟動 AI 直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW"
---

本指南提供使用 BytePlus Live 控制台設定並啟動自動化 AI Live 的逐步操作說明。你將學習如何建立直播腳本、配置智慧回覆以進行觀眾互動、管理直播設定，以及開始你的直播。如需功能概述及端到端工作流程，請參閱 [AI 直播概覽](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-overview-zh-TW)。

## 先決條件

* **訂閱 AI Live 服務**：請參閱 [訂閱計費方式](https://docs.byteplus.com/docs/byteplus-livesaas/subscription-billing-method-zh-TW) 並聯絡銷售以訂閱 AI Live 服務。

* **訓練你的虛擬人偶**：訓練你自己的虛擬人偶及聲音，以便在直播中使用。詳情請參閱 [訓練虛擬人與聲音](https://docs.byteplus.com/docs/byteplus-livesaas/xun-lian-shu-zi-ren-zh-TW)。

* **準備產品及知識庫**：為讓主持人展示商品並回答產品問題，請先將你的產品新增至 **產品庫**並上傳相應的知識庫檔案。詳情請參閱 [管理商品庫](https://docs.byteplus.com/docs/byteplus-livesaas/manage-digital-human-livestream-product-zh-TW) 和 [知識庫設定](https://docs.byteplus.com/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-TW)。

## 操作流程

請依照以下步驟設定並啟動你的 AI Live。

### 步驟 1：建立 AI Live 房間

1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在頂部導覽列點擊 **AI Live** 。

3. 於 **Live Room** 頁面，點擊  **+New liveroom**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef3aeee5a60a49349568177223f3a92d~tplv-goo7wpa0wc-image.image)

   該直播房間將自動標記為 **Digital Human Streaming**，方便識別。

4. 在 **Create live room** 對話框中，設定房間名稱、聲音、虛擬人偶及語速，然後點擊 **Create** 以開啟腳本配置頁面。

   |**設定** |**說明** |
   |---|---|
   |**直播間名稱** |輸入直播間的名稱。名稱最多可達150個字元。 |
   |**語言** |系統會自動偵測語音的語言。 |
   |**Avatar** |為直播間選擇一個 Avatar。若您的對話框顯示無可用 Avatar，請參考 [訓練虛擬人與聲音](https://docs.byteplus.com/docs/byteplus-livesaas/xun-lian-shu-zi-ren-zh-TW)。 |
   |**Avatar 語音** |* 從可用選項中選擇一個語音。若您的對話框顯示無可用語音，請參考 [訓練虛擬人與聲音](https://docs.byteplus.com/docs/byteplus-livesaas/xun-lian-shu-zi-ren-zh-TW)。<br><br>* 調整 Avatar 說話的速度。請於直播前設定；直播期間無法更改說話速度。範圍為 [0.5,2]。 |

### 步驟 2：新增直播腳本

虛擬人偶會根據腳本主持直播。你可以新增兩種類型的腳本，並在單場直播中混合多個腳本。詳情請參閱 [產生直播腳本](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts-zh-TW)。

你可以查看預估的語音時長及字數，並點擊 **聆聽腳本**，在直播前預聽所選聲音的朗讀效果。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fd5a3aef27847b58d9e7b88cb237a31~tplv-goo7wpa0wc-image.image)

你可以新增多個產品腳本，並點擊拖曳圖示調整順序。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ff21d518f5040d7b15809c86712c9b4~tplv-goo7wpa0wc-image.image)

當你在此新增產品腳本時，其對應的產品知識庫也會自動啟用以回覆訊息。你可以點擊**直播互動**來查看設定。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3ca9fb746dd44fb83c7e40ee0c3bd17~tplv-goo7wpa0wc-image.image)

### 步驟 3：配置互動設定

AI Live 可於直播期間自動回應觀眾留言及互動事件。完成 **Live interaction** 配置後，AI 主持人會在適當時機暫停目前腳本，根據你的知識庫、提示及過濾規則生成回覆，然後繼續朗讀腳本。詳情請參閱 [設定 AI Live 互動](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-ai-live-interactions-zh-TW)。

### 步驟 4：配置串流目的地

設定 AI 串流推送位置，以便在 TikTok、BytePlus Live 或其他平台上播放。

1. 在頂部導覽列點擊 **Live platform**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

2. 於 **Live platform** 對話框中，配置以下設定，然後點擊 **Save**。

   |**設定** |**說明** |
   |---|---|
   |直播平台設定 |選擇串流推送位置：**TikTok**、**BytePlus Live** 或 **其他**。 |
   |串流方式 |此選項僅在您選擇 **TikTok** 作為直播平台時顯示。<br><br><br>* **RTMP**：使用 RTMP 協定拉取串流。請參閱 [通過 RTMP 在 TikTok 開啟直播](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-TW)。<br><br>* **虛擬攝影機**。透過 OBS 進行直播。請參閱 [透過 OBS 在虛擬攝影機 TikTok 直播](https://docs.byteplus.com/docs/byteplus-livesaas/obs-go-live-zh-TW)。 |
   |TikTok ID |**TikTok 用戶 ID** 用於從直播中擷取觀眾活動。此選項僅在你選擇 **TikTok** 作為直播平台時顯示。請依下方所示，在你的 TikTok 應用程式中取得該 ID。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image) |
   |URL Server |輸入目標平台的推流 URL（RTMP 伺服器位址）。詳情請參閱 [取得伺服器 URL 和串流金鑰](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-TW#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |串流金鑰 |輸入目標平台的串流金鑰。詳情請參閱 [取得伺服器 URL 和串流金鑰](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-TW#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |串流推送 |啟用此選項以將 Avatar 串流推送至所選平台。 |

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9269d0affec041ab96bc5e24801eb065~tplv-goo7wpa0wc-image.image)

### (選用) 步驟 5：新增直播浮水印

新增浮水印，例如「AI\-Generated」標籤，會顯示於直播畫面右下角。

1. 在右上工具列點擊 **More** ( **...** ) 圖示，然後選擇 **Live Settings**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36909d863cff43708758decab9fe46ef~tplv-goo7wpa0wc-image.image)

2. 於 **Live Settings** 對話框中，開啟 **Live watermark**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e99ea7d2eef42e1873b375b1eeef501~tplv-goo7wpa0wc-image.image)

3. 點擊 **Upload Image** 上傳你的浮水印標誌，然後點擊 **Save**。圖片必須符合以下要求：

   * **格式**：JPG 或 PNG

   * **最大檔案大小**：500 KB

   * **最大尺寸**：540px（寬）× 300px（高）

### 步驟6：開始直播並管理串流

在開始直播前，BytePlus Live 會執行 **開始直播設定** 設定流程，檢查您的內容、載入 Avatar，並在播出前確認串流目的地。

1. 點擊 **開始直播**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/311ca298ee63456b814fbd870c404605~tplv-goo7wpa0wc-image.image)

   **開始直播設定** 設定流程會在 **直播間內容檢查** 開啟。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b069c5c5cf440fdb23ce9eb375db610~tplv-goo7wpa0wc-image.image)

2. 檢查直播前的內容。若任何檢查顯示警告，請點擊 **修改內容** 返回並修正您的腳本或知識庫，然後重新開始。

   |**檢查項目** |**需求** |
   |---|---|
   |腳本檢查 |建議預估的直播時間**超過 30 分鐘**。若低於此時長，請參考[產生直播腳本](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts-zh-TW)以豐富腳本內容。 |
   |重複檢查 |不允許長篇且完全重複的腳本。 |
   |知識庫檢查 |請新增 **至少一個知識庫**，以便 AI 主持人能正確回答觀眾問題。 |

3. 設定直播時長，然後點擊**下一步**。

4. 在直播時長下，選擇**腳本結束時結束直播**或**直播指定時數**，完成所需設定後，點擊**下一步**。

   若選擇**直播指定時數**，建議啟用 AI 重寫功能以避免腳本重複。

   > **说明**

   > 您可以設定直播最長運行24小時。當設定時長結束時，直播會自動關閉。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b70fd0fa53404d568a9b9738961799e1~tplv-goo7wpa0wc-image.image)

5. 等待 **Avatar 資源載入** 完成，然後點擊 **下一步**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ced49870982b4c9cb9d71ac0725561e0~tplv-goo7wpa0wc-image.image)

   > **说明**

   > Avatar 載入需時（現有 Avatar 約1分鐘，新 Avatar 約10分鐘）。請耐心等候。

6. 確認你在第 4 步設定的串流目的地，然後點擊**儲存**以開始直播。直播開始後，虛擬角色將會開始朗讀腳本。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04e36f806a7f4656a1d805a2fd144985~tplv-goo7wpa0wc-image.image)

7. 在 **聊天** 列表中，您可以依狀態篩選留言：依規則封鎖、未讀或已讀。

8. 點擊 **結束直播** 停止播出。

## 常見問題

### **問：部分觀眾暱稱包含表情符號及無法辨識的符號。我該怎麼做？**

在您的 AI 回覆設定中的 **提示** 加入指令，讓 AI 在回覆前將無法辨識的暱稱轉換為可讀文字。例如，將以下內容加入您的提示：

```Plain
If the username is emoji or unreadable symbol, transform those into readable before answering the question.
```
