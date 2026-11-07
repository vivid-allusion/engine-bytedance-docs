---
title: "透過 RTMP 在 Shopee 開啟直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp-zh-TW"
---

您可以將 BytePlus AI Live 的直播串流推送至 Shopee，讓觀眾能在 Shopee 上觀看您的 AI 虛擬人物。本指南說明如何在 AI Live 中設定 Shopee 為串流目的地、從 Shopee 取得伺服器 URL 和串流金鑰，以及使用 Live Connector 瀏覽器擴充功能來轉發觀眾留言。完成留言同步設定後，您的 AI 虛擬人物可根據知識庫與提示生成並語音回覆。

<span id="fdde2b5d"></span>
## 先決條件


* 您已建立 AI 直播間並準備好開啟直播。如需更多資訊，請參閱[啟動 AI Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW)。

* 您擁有在 Shopee 開啟直播的權限，並可從 Shopee 直播後台取得 RTMP 伺服器 URL 與串流金鑰。

* 為讓您的 AI 虛擬人物回覆觀眾留言，您已準備並設定回覆用的知識庫。如需更多資訊，請參閱[準備與上傳知識庫檔案](https://docs.byteplus.com/en/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-TW)。

* 為收集留言，您已安裝 Google Chrome 或 Microsoft Edge，並聯絡 BytePlus 技術支援取得**Live Connector** 擴充功能套件。


<span id="621db0ae"></span>
## 操作流程

<span id="d2716de0"></span>
### Step 1: 在 AI Live 中設定 Shopee RTMP 串流參數

在 AI Live 中，於**直播平台**對話框設定 Shopee 的 RTMP 串流參數。


1. 登入[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，並開啟您要直播的 AI 直播間。

2. 在頂部導覽列中，點選**直播平台**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image) </span>

3. 於**直播平台**對話框中設定以下參數，然後點選**儲存**。

   
   |設定 |說明 |
   |---|---|
   |直播平台設定 |選擇 **Other** 以將 Shopee 設為串流目的地。 |
   |平台名稱 |請輸入名稱，例如 `Shopee`，以便識別串流目的地。 |
   |伺服器 URL |請輸入目前 Shopee 直播的 RTMP 伺服器 URL。請在 Shopee 直播控制台建立直播，以取得伺服器 URL 和串流金鑰。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de402a754958448c8ad6747bdf7e44de~tplv-goo7wpa0wc-image.image) </span> |
   |串流金鑰 |請輸入上述伺服器 URL 對應的 Shopee 串流金鑰。 |
   |串流推送 |啟用此選項以將你的 AI Live 串流推送至 Shopee。 |
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6143bd00a92c4ada8b19ea234a4487f6~tplv-goo7wpa0wc-image.image) </span>


<span id="ff658d8a"></span>
### Step 2: 在 AI Live 與 Shopee 開啟直播


1. 啟動您的 AI Live。如需更多資訊，請參閱[啟動 AI Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW)。

2. 開啟目前直播的 Shopee 直播後台。確認 Shopee 已接收來自 BytePlus 的影音後，於右上角點選**開始直播**。

3. 確認 Shopee 頁面顯示**直播中**及已直播時間。


<span id="67f662d9"></span>
### （選用）Step 3: 將 Shopee 觀眾留言轉發至您的 AI 直播間

使用**Live Connector**瀏覽器擴充功能，從 Shopee 直播後台收集觀眾留言並發送至您指定的 BytePlus AI 直播間。您的 AI 虛擬人物即可根據知識庫與提示生成並語音回覆。

下方顯示的 Live Connector 介面為中文。本指南保留中文標籤，並提供說明協助您定位各控制項。

<span id="a8715f56"></span>
#### Step 1: 安裝 Live Connector


1. 聯絡 BytePlus 技術支援取得 Live Connector 擴充功能套件，並解壓縮至本機資料夾。

2. 開啟 Chrome 或 Edge。在網址列輸入`chrome://extensions/`（Chrome）或`edge://extensions/`（Edge），開啟擴充功能管理頁面。

3. 開啟**開發人員模式**。

4. 點選**載入未封裝項目**，並選擇已解壓縮的 Live Connector 擴充功能資料夾。

5. 確認**Live Connector**已出現在擴充功能清單並啟用。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/322b352162ef416c802a15d7e0b090d2~tplv-goo7wpa0wc-image.image) </span>

6. 點選瀏覽器網址列右側的**擴充功能**圖示，再點選**Live Connector**。擴充功能會在瀏覽器側邊欄開啟。您也可以將擴充功能釘選至工具列以便快速存取。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0afeaaa89b5452fa3157d1d94dbf7d3~tplv-goo7wpa0wc-image.image) </span>


<span id="c2cae86b"></span>
#### Step 2: 連接您的 BytePlus 帳戶


1. 在擴充功能的**登录 BytePlus**步驟中，點擊**去 BytePlus 登录**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47536cdfd0364931baf73e69dd38a398~tplv-goo7wpa0wc-image.image) </span>

2. 在開啟的 BytePlus 頁面上完成登入。請使用擁有本次串流 AI 直播間的帳號，並在安裝 Live Connector 的同一瀏覽器及瀏覽器設定檔中完成登入。

3. 返回擴充功能並點擊**我已登录，连接账号**。

4. 在**选择直播间**步驟中，確認擴充功能顯示的是擁有您的 AI 直播間的帳號，以及狀態為**BytePlus 已连接**。若要切換帳號，請點擊**更换账号**，然後重新登入並連接。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610f294649944ad889cbcb5a6e75d7a9~tplv-goo7wpa0wc-image.image) </span>


<span id="feb97d9b"></span>
#### Step 3: 辨識 Shopee 直播串流並輸入您的 BytePlus AI 直播間 ID


1. 在安裝 Live Connector 的瀏覽器中，登入 Shopee 並開啟您在步驟 2 所啟動的直播串流儀表板。

2. 確認 Shopee 直播串流正在運行。擴充功能會自動偵測串流，並在**采集来源**下顯示其資訊，狀態為**直播中**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f639db64f1f487b929480ce87ace7fd~tplv-goo7wpa0wc-image.image) </span>

3. 在 BytePlus Live 控制台中，開啟正在推流至 Shopee 的 AI 直播間並複製其 ID（`ActivityId`）。將其貼到擴充功能的**上报目标**欄位。請使用目前正在串流的 BytePlus AI 直播間 ID，而非 Shopee 直播間 ID。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/351bafca8b4c4c7187423c1edaeb4d6d~tplv-goo7wpa0wc-image.image) </span>

4. 確認來源與目標皆正確後，點擊**下一步**，進入**开始同步**步驟。


<span id="b649a8fd"></span>
#### Step 4: 開始同步評論並驗證 AI 回覆


1. 在**确认连接，开始同步**頁面，再次檢查 Shopee 評論來源與 BytePlus 目標直播間，然後點擊**开始同步评论**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1aed26aa899d4b5a926a4ab9d6ef8194~tplv-goo7wpa0wc-image.image) </span>

2. 確認擴充功能顯示**连接完成**、狀態為**同步中**，並有**停止同步**按鈕。請保持瀏覽器及 Shopee 直播儀表板開啟並保持登入狀態。**關閉 Shopee 直播儀表板會停止評論收集。** 

3. 使用觀眾帳號在目前 Shopee 直播串流中發佈新的測試評論。提出您的知識庫能回答的問題，然後檢查以下項目：

   * 該評論會出現在 Shopee 直播儀表板的**Comments**區塊。

   * 同一評論會出現在擴充功能的**最近评论**區塊，且**已同步评论**數量會增加。

   * 該評論會出現在您的 BytePlus AI 直播間的**Chats**列表中。

4. 以 Shopee 觀眾身分收聽直播，並確認 AI 虛擬形象有發出相關回覆。評論出現在擴充功能中並不代表 AI 虛擬形象已產生或發出回覆。同時檢查 BytePlus 是否收到評論，以及回覆是否能在直播中聽到。


<span id="8e3c6ce0"></span>
## 常見問題

<span id="5890df38"></span>
### 啟動 AI Live 後，為何 Shopee 沒有顯示影片？

在**Live platform**對話框中，請確認**Stream pushing**已啟用，且**URL Server**與**Stream Key**與 Shopee 直播儀表板中目前串流所提供的值一致。同時請確認你已完成在 Shopee 上開播的所有步驟。

<span id="3d791ccd"></span>
### 如果評論來源顯示為待識別（Not yet detected）或正在等待聊天連接…（Waiting for the chat connection），我應該怎麼做？

請確認你已在安裝 Live Connector 的同一個 Chrome 或 Edge 瀏覽器設定檔中登入 Shopee，並且目前直播的控制台已開啟。請依照 Shopee 頁面顯示的狀態指示操作：


* **直播尚未開始：**  請確認 Shopee 已收到串流，然後點擊 **Go Live**。擴充功能會自動偵測頁面狀態。請等待狀態變更為 **直播中**（Live）；你無需手動重新整理頁面。

* **直播中：**  請確認頁面顯示 **Live** 及已直播的時間。請保持控制台開啟，並檢查頁面是否正確載入。

* **直播已結束：**  若頁面顯示 **Live Ended**，表示直播已結束。啟動另一場直播後，請再次確認評論來源及目標直播間，並開始同步評論。


<span id="bdc7fb75"></span>
### 為什麼我的 AI 角色沒有回覆 Shopee 評論？

首先，請在 BytePlus AI 直播間的 **Chats** 清單中檢查評論是否已到達：


* **尚未收到評論：**  請確認 Shopee 直播控制台的 **Comments** 下方有新評論出現。然後檢查擴充功能是否顯示 **同步中**（Syncing）、評論是否出現在 **最近評論**（Recent comments），以及 **已同步評論**（Synced comments）數量是否增加。同時檢查已連接的 BytePlus 帳號及目標直播間。`ActivityId` 必須能識別該帳號下目前正在直播的 AI 直播間。請保持 Shopee 直播控制台開啟。

* **已收到評論：**  請檢查是否有篩選規則阻擋評論，以及直播間是否已配置知識庫及評論回覆設定。如需更多資訊，請參閱[啟動 AI Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW)。


<span id="related-operations"></span>
## 相關操作

如需設定 AI 虛擬人物如何回覆 Shopee 觀眾留言，請參閱《啟動 AI Live》中的[配置留言回覆策略](https://docs.byteplus.com/en/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW#143bb4f1)，瞭解知識庫、提示詞及留言篩選規則的設定方式。
