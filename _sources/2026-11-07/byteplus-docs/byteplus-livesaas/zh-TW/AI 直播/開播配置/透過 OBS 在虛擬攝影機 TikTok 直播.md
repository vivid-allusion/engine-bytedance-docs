---
title: "透過 OBS 在虛擬攝影機 TikTok 直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/obs-go-live-zh-TW"
---

本指南提供完整的設定流程，協助您使用 OBS Studio 和 TikTok Live Studio，將 BytePlus AI 虛擬人直播到 TikTok。您將學習如何設定所有必要軟體、在應用程式間傳遞音訊與視訊訊號，以及排除常見問題，確保直播順利進行。

<span id="202b2df4"></span>
## 系統需求

在開始之前，請確認您的電腦符合系統需求，並安裝下方列出的必要軟體。


* **RAM：**  最少 16 GB（若低於此規格，直播可能會延遲或當機）

* **GPU：**  GTX 1080 / RTX 2070 / RTX 3060 或更高

* **CPU：**  Intel i9、Intel i7\-9700K 或 AMD Ryzen 5 3600X 或更高


<span id="18fb01ff"></span>
## 先決條件


* 需有 BytePlus 帳號，或具備 **Marketing toolkits** \> **Edit** 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [Managing users, organizations, and roles](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。

* 擁有在 TikTok 上開啟直播的權限。如需更多資訊，請參閱 [Who can use LIVE on TikTok](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

* 您已下載以下軟體：



|**軟體名稱** |**下載連結** |**用途** |
|---|---|---|
|Google Chrome |[下載 Google Chrome](https://www.google.com/chrome/) |BytePlus AI 人像平台必須使用。僅支援 Chrome。 |
|OBS Studio |[下載 OBS Studio](https://obsproject.com/download)（請以預設選項安裝） |視訊擷取與串流軟體。 |
|VB\-Audio Virtual Cable |請聯絡業務取得下載連結 |虛擬音訊裝置，可將 OBS 音訊導向 TikTok。 |
|TikTok Live Studio |[下載 TikTok Live Studio](https://www.tiktok.com/studio/download) |TikTok 官方串流助手。 |


<span id="a159f787"></span>
## 操作步驟

<span id="448e55b2"></span>
### Step 1: 設定 Google Chrome 瀏覽器


1. 在電腦上開啟 **Google Chrome**。

2. 點擊瀏覽器視窗頂部的網址列，並精確貼上以下網址：


```Plain
chrome://settings/content/popups
```



3. 在鍵盤上按下 **Enter**。

4. 啟用「網站可傳送彈出視窗並使用重新導向」。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15fa2a981c43491d8ec1d9d8598f587c~tplv-goo7wpa0wc-image.image) </span>


<span id="f0f7c889"></span>
### Step 2: 設定 VB\-Audio Virtual Cable


1. 聯絡銷售團隊以取得 VB\-Audio Virtual Cable 的下載連結。

2. 解壓縮 ZIP 檔案。

3. 在 VB\-Cable 資料夾內，右鍵點擊 `VBCABLE_Setup_x64.exe`，選擇「以系統管理員身分執行」。

4. 安裝程式開啟後，點擊 **Install Driver** 按鈕。若已存在舊版本，請先點擊「Remove Driver」，再重新安裝。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a683c1ad239b44a1afc7c75a21d3e316~tplv-goo7wpa0wc-image.image) </span>


<span id="4f131f1d"></span>
### **Step 3: 設定音效**


1. 按下 **Win + I** 開啟 **Windows 設定**。

2. 前往 **System** \> **Sound**。

3. 在 **Input** 下方，選擇 **CABLE Output (VB\-Audio Virtual Cable)**  作為預設輸入裝置。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eb0ed44a0f94955a3a97258cef953f7~tplv-goo7wpa0wc-image.image) </span>

4. 如有需要，點擊 **All sound devices** 以檢視完整裝置清單，並確認兩個虛擬音訊線裝置皆可用：

   * **CABLE Input** 應顯示於 **Output devices** 下方

   * **CABLE Output** 應顯示於 **Input devices** 下方

5. 停用您不打算使用的錄音裝置，確保虛擬音訊線為啟用的輸入路徑。


<span id="28c94099"></span>
### **步驟 4：** 啟動 AI 直播

請參考 [啟動 AI 直播](https://docs.byteplus.com/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW) 完成開啟直播的流程，並確保串流成功啟動。當直播串流啟動時，螢幕上會顯示影片預覽。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/621856507af14628a00986a367b92c3c~tplv-goo7wpa0wc-image.image) </span>

<span id="8cdb2f65"></span>
### **Step 5: 取得拉流地址**


1. 在頂部導覽列中，點擊 **Live platform** 按鈕。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image) </span>

2. 於 **Live platform** 對話框中，選擇 **TikTok** 作為直播平台，並選擇 **Virtual camera** 作為串流方式。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56b641374be9477ead9cbde9d6097879~tplv-goo7wpa0wc-image.image) </span>

3. 請在 TikTok App 中取得下方所示的 ID。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a0e3fc1adba4f5fb470be530312ebb4~tplv-goo7wpa0wc-image.image) </span>

4. 點擊 **Copy** 按鈕。地址開頭為「rtmp://pull\-rtmp\-...」。


<span id="3d5cd8e0"></span>
### **Step 6:**  透過 Media Source 將拉流導入 OBS


1. 開啟 OBS Studio。

2. 在 **Sources** 面板中，點擊  **+**  按鈕並選擇 **Media**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb4b58c328b41ef95646c2bdf7ec532~tplv-goo7wpa0wc-image.image) </span>

3. 於 **Create/Select Source** 對話框中，確認名稱後點擊 **OK**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61355af960bb4352b8d8c1203b86fa04~tplv-goo7wpa0wc-image.image) </span>

4. 在 **Properties for 'Media'**  對話框中，取消勾選「Local File」，將第 5 步取得的直播串流網址貼入輸入欄位，將 **Input Format** 設為 flv，然後點擊 **OK**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/237cf3914e2045d78e42bcd8328382fa~tplv-goo7wpa0wc-image.image) </span>


<span id="08bd8cd5"></span>
### Step 7: 將 OBS 音訊導入虛擬麥克風


1. 在 OBS 中，點擊音訊混音器面板右下角的齒輪圖示以開啟音訊屬性對話框。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9a038fa968a4dbf94ce4f51553e58bc~tplv-goo7wpa0wc-image.image) </span>

2. 在 **Media** Source 列，將音訊監控設為「**Monitor and Output**」。此設定會將串流音訊導入 VB\-Cable 虛擬麥克風，讓 TikTok Live Studio 能夠擷取音訊。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6107940fa304cc4ab9b5bb35ccc7bc0~tplv-goo7wpa0wc-image.image) </span>

3. 然後在 OBS 中於 **Controls** 面板點擊 **Start Virtual Camera**，啟用虛擬攝影機。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5466bb9d7b1e41c68cf793061baf9f65~tplv-goo7wpa0wc-image.image) </span>


<span id="7b713c58"></span>
### Step 8: 在 TikTok Live Studio 新增攝影機並開始直播


1. 開啟 TikTok LIVE Studio。

2. 在來源面板中，點擊 **Add Source**。

3. 在 **Add Source** 對話框中，選擇 **Camera**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4fa84fc27d94c5c9bcf4193f386c84b~tplv-goo7wpa0wc-image.image) </span>

4. 在 **Camera** 下拉選單中，選擇 **OBS Virtual Camera**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29f01a49481b41ffac345d2747025c46~tplv-goo7wpa0wc-image.image) </span>

5. 確認預覽畫面顯示你的 OBS 場景。若畫面顛倒，請點擊 **Rotate** 或 **Flip** 進行調整。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24e186f9e96d4c508e39180ca237b51a~tplv-goo7wpa0wc-image.image) </span>

6. 點擊底部工具列的音訊混音器圖示，再點擊  **+ Add**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3a436b5a3274a1cb12acd9461a8e595~tplv-goo7wpa0wc-image.image) </span>

7. 選擇 **CABLE Output (VB\-Audio Virtual Cable)**  ，然後點擊 **Add**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1cb4dc32038413f9fd90f9568e8158f~tplv-goo7wpa0wc-image.image) </span>

8. 將其他麥克風靜音。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cbd2c8c73f14b2e82ddde59739a71e4~tplv-goo7wpa0wc-image.image) </span>

9. 確認你能看到串流的影像，且麥克風音量指示器有動作。當一切都正常時，點擊右下角的 **Start Live**。


<span id="8a791e48"></span>
## 故障排除

音訊問題是此設定中最常見的問題。以下是用戶最常回報的症狀，以及每個問題的精確解決方法。

<span id="7d8d33f8"></span>
### 串流回音（觀眾聽到你的音訊重複）

**可能原因：** 


* OBS 音訊監聽設定為「Monitor and Output」，且該來源同時被你的麥克風捕捉（例如桌面喇叭和麥克風）。

* 桌面音訊和 Media Source 都被送入虛擬音訊線，因此 TikTok 會捕捉到同一聲音兩次。

* Windows 的「Listen to this device」在 CABLE Output 上啟用，導致音訊回傳到喇叭。


**解決方法：** 


* 在 OBS → 進階音訊屬性：僅有 Media Source（BytePlus 拉流）應設為「Monitor and Output」。將其他來源—桌面音訊、Mic/Aux、瀏覽器來源等—設為「Monitor Off」。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e520771d8754e33a649d5a3f3dcc976~tplv-goo7wpa0wc-image.image) </span>

* 若不需分享電腦音效，請在 OBS 混音器中將桌面音訊靜音。

* 開啟 Windows 音效 → 錄音 → CABLE Output → 屬性 → Listen 標籤，並取消勾選「Listen to this device」。

* 測試時請使用耳機而非喇叭—喇叭輸出被實體麥克風收音是常見回音來源。


<span id="46e3bc9e"></span>
### 雙重音訊輸入（音訊重複）

**可能原因：** 


* 你的實體麥克風和 VB\-Cable 虛擬麥克風都在 TikTok LIVE Studio 中啟用為輸入。

* OBS 同時將音訊送到虛擬音訊線和 TikTok 的直接捕捉（桌面音訊監聽）。

* OBS 中不小心新增了兩個 Media Sources，且皆拉取相同的 BytePlus 串流。

* VB\-Cable 安裝了兩次，產生 CABLE\-A 和 CABLE\-B，音訊同時經由兩者傳送。


**解決方法：** 


* 在 TikTok LIVE Studio 音訊設定中，只設一個主麥克風—CABLE Output（VB\-Audio Virtual Cable）。在下拉選單中停用其他麥克風。

* 在 Windows 音效 → 錄音，右鍵點擊所有非 CABLE Output 的輸入並選擇停用。僅保留 CABLE Output 啟用。

* 在 OBS 中，檢查來源列表並確保 BytePlus 拉流僅有一個 Media Source。刪除任何重複項。

* 在 OBS 音訊混音器中，將 Mic/Aux 靜音，除非你確實需要將自己的聲音疊加在數位主持人之上。

* 在 Windows 中開啟程式與功能；若 VB\-Audio Virtual Cable 出現兩次，請卸載兩者，重新啟動後再安裝一次。


<span id="50fab813"></span>
### 音訊無法傳送至 TikTok LIVE Studio


* 確認 OBS 正在播放 Media Source（你應該會看到該列的綠色 VU 音量表在移動）。

* 在 OBS → 進階音訊屬性中，將 Media Source 那一列設為「Monitor and Output」（不要只設為「Monitor Off」或「Monitor Only」）。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e520771d8754e33a649d5a3f3dcc976~tplv-goo7wpa0wc-image.image) </span>

* 在 Windows 音效 → 播放中，確保 CABLE Input（VB\-Audio Virtual Cable）已啟用。若未啟用，OBS 將無法將音訊導向該裝置。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eb0ed44a0f94955a3a97258cef953f7~tplv-goo7wpa0wc-image.image) </span>

* 在 TikTok LIVE Studio 中，確認主麥克風為 CABLE Output，並點擊**Test** 以觀察音量表移動。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cbd2c8c73f14b2e82ddde59739a71e4~tplv-goo7wpa0wc-image.image) </span>

* 更改音訊路由後請重新啟動 OBS——部分變更僅在重新啟動後生效。


<span id="4b88becc"></span>
### 音訊出現爆音、機械聲或失真


* 在 Windows 音效 → 錄音 → CABLE Output → 內容 → 進階中，將取樣率設為 48 000 Hz、16 位元（DVD 品質）。

* 在 Windows 音效 → 播放 → CABLE Input → 內容 → 進階中，設為相同取樣率（48 000 Hz、16 位元）。虛擬音訊線兩端的取樣率必須一致。

* 在 OBS → 設定 → 音訊中，將取樣率設為 48 kHz，聲道設為立體聲。

* 若 CPU 負載過高，請降低 OBS 的輸出解析度或影片位元率，以釋放 CPU 資源供音訊處理使用。


<span id="e46a54c3"></span>
### 串流延遲、卡頓或中斷


* 確認記憶體容量 ≥ 16 GB，且未執行其他高負載應用程式（如遊戲、多分頁瀏覽器、影片剪輯軟體）。

* 在 OBS → 設定 → 輸出中，將視訊位元率降至 4 000–6 000 kbps，並將編碼器設為 NVENC（NVIDIA）或 QuickSync（Intel），不要使用 x264。

* 請使用有線乙太網路連線，勿使用 Wi\-Fi。

* 若 Media Source 畫面凍結，請在 OBS 中右鍵點選並選擇重新啟動，或直接移除並以相同 flv URL 重新新增來源。
