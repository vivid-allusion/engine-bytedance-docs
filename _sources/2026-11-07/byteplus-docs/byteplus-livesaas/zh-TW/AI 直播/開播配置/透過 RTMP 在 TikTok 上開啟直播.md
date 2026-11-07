---
title: "透過 RTMP 在 TikTok 上開啟直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-TW"
---

您可以透過 RTMP 將 BytePlus AI Live 的直播推送到 TikTok，讓觀眾在 TikTok 上觀看您的 AI 虛擬人物。本指南說明如何在 AI Live 中將 TikTok 設定為串流目的地，並使用 TikTok 應用程式或 TikTok LIVE Center 取得伺服器 URL 和串流金鑰。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b107d695409a419c88170e89cfbb29b6~tplv-goo7wpa0wc-image.image)

## 先決條件

* 您已建立 AI 虛擬人物直播間，並準備開始直播。如需更多資訊，請參閱 [啟動 AI 直播](https://docs.byteplus.com/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW)。

* 您已獲得在 TikTok 上開啟直播的權限。如需更多資訊，請參閱 [誰可以在 TikTok 使用 LIVE](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

## 操作流程

在 AI Live 中，於 **直播平台**對話框設定 TikTok 的 RTMP 串流參數。

1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)並開啟您的 AI 直播間。

2. 在頂部導覽列中，點選 **直播平台**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

3. 於 **直播平台**對話框中設定以下參數，然後點選 **儲存**。

   |**設定** |**說明** |
   |---|---|
   |直播平台設定 |選擇 **TikTok 作為**串流目的地。 |
   |串流方式 |當您選擇 **TikTok** 作為直播平台時，請選擇 **RTMP** 作為串流方式。關於 **Virtual Camera**，請參閱 [透過 OBS 在虛擬攝影機 TikTok 直播](https://docs.byteplus.com/docs/byteplus-livesaas/obs-go-live-zh-TW)。 |
   |TikTok ID |請依下方說明於 TikTok 應用程式中取得 ID。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image) |
   |URL 伺服器 |請輸入您目前 TikTok 直播的推流 URL（RTMP 伺服器地址）。操作說明請參閱 [取得伺服器 URL 和串流金鑰](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-TW#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |串流金鑰 |請輸入上述伺服器 URL 對應的 TikTok 串流金鑰。操作說明請參閱 [取得伺服器 URL 和串流金鑰](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-TW#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |推流 |啟用此選項以將您的 AI 直播推送至 TikTok。 |

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9269d0affec041ab96bc5e24801eb065~tplv-goo7wpa0wc-image.image)

4. 啟動您的 AI Live。詳情請參閱 [啟動 AI 直播](https://docs.byteplus.com/docs/byteplus-livesaas/qi-dong-shu-zi-ren-zhi-bo-zh-TW)。

### 取得伺服器 URL 和串流金鑰

本節說明如何使用 TikTok 應用程式或 TikTok LIVE Center 取得伺服器 URL 和串流金鑰。隨著 TikTok 政策更新，方法及直播權限要求可能會有所變動。

1. 在 TikTok 上尋找並複製伺服器 URL 和串流金鑰。

   > **说明**

   > 每次在 TikTok 開始直播時，您都必須複製伺服器 URL 與串流金鑰。

   **TikTok 應用程式**

在 TikTok 應用程式中尋找並複製伺服器 URL 與串流金鑰。

      1. 開啟您的 TikTok 應用程式。

      2. 前往底部導覽列並點擊加號「+」按鈕。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f75eece96c4641228a643f1cd42f32c8~tplv-goo7wpa0wc-image.image)

      3. 選擇 **Stream key** 選項，然後點擊 **Go LIVE**。

         > **说明**

         > 若此選項未顯示，代表你的帳戶沒有直播權限。如需更多資訊，請參閱[Who can use LIVE on TikTok](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d3e968f9536438288b68d3c759612d6~tplv-goo7wpa0wc-image.image)

      4. 依需求選擇您的直播主題。接著即可看到伺服器 URL 與串流金鑰。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a414115857ec46c18bdac55cb92dcf15~tplv-goo7wpa0wc-image.image)

   **TikTok LIVE Center**

在 TikTok LIVE Center 中尋找並複製伺服器 URL 與串流金鑰。

      1. 前往 [TikTok LIVE Center](https://livecenter.tiktok.com/producer)。

      2. 在左側導覽窗格中，點擊 **Go LIVE**。

         > **说明**

         > 若此選項未顯示，代表你的帳戶沒有直播權限。如需更多資訊，請參閱[Who can use LIVE on TikTok](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d076bd36c2974227b8d36c5643953aca~tplv-goo7wpa0wc-image.image)

      3. 輸入您的直播詳細資訊，並視需要上傳 LIVE 封面。

      4. 點擊 **Save & Go LIVE**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80d6e9c8b8f84967b36611d3ebd26a51~tplv-goo7wpa0wc-image.image)

         這尚未啟動你的直播。這會產生你的伺服器 URL 和串流金鑰，你需要將其新增至 BytePlus 才能開始直播。伺服器 URL 和串流金鑰將會保持有效 5 分鐘，因此你需要在此時間內完成下一步。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85bdf73e46c1475e8592a9ffd3fce217~tplv-goo7wpa0wc-image.image)

### 從 BytePlus Live 取得拉流地址

若第三方平台支援從外部 URL 拉取直播，您可以取得 BytePlus Live 直播間的拉流地址並在該平台使用。

1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)並開啟直播間。

2. 於左側導覽窗格中，點選 **行銷工具包** \> **多平台串流**。

3. 點選 **取得拉流地址**，並複製出現的對話框中的地址。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c4672bbd0f94f018254c6526b42a7cf~tplv-goo7wpa0wc-image.image)

> **说明**

> 每個直播間僅有一個拉流位址。

### 取得其他平台的推流地址

本節說明如何在其他主要直播平台取得伺服器 URL 和串流金鑰，或等效的推流地址。隨著各平台政策更新，方法及直播權限要求可能會有所變動。

#### YouTube Live

1. 登入 [YouTube Live](https://www.youtube.com/)。

2. 在頁面右上角，點選 **建立**圖示並選擇 **開啟直播**。

若首次啟用直播功能，最多可能需要 24 小時才能取得直播權限。

3. 於 **STREAM SETTINGS** 標籤頁，將串流 URL 與串流金鑰串接。請確保串流 URL 在前，串流金鑰在後。

4. 使用串接後的字串作為推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6887d8038a4d8c868cc4f1b6318c14~tplv-goo7wpa0wc-image.image)

#### MetaLive

1. 登入 [Facebook](https://www.facebook.com/live/create)。

2. 於 **開啟直播**區段中點選 **開啟直播**。

3. 選擇 **串流軟體**作為您的影片來源。

4. 若需讓串流金鑰永久有效，請開啟 **永久串流金鑰**開關。否則，直播結束後串流金鑰將無法再次使用。

5. 以斜線（/）將伺服器 URL 與串流金鑰串接。請確保伺服器 URL 在前，串流金鑰在後。

6. 使用串接後的字串作為推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/269d663243664680b93e050dd2e0f107~tplv-goo7wpa0wc-image.image)

#### LinkedIn Live

LinkedIn Live 僅限經審核的用戶使用。若要檢查您是否符合資格，請進一步了解 [LinkedIn Live](https://www.linkedin.com/help/linkedin/answer/a568503?src=li-other&veh=www.linkedin.com%7Cli-other) 的存取條件。

1. 登入 [LinkedIn Live](https://www.linkedin.com/video/golive/now/)。

2. 在頁面左上角的 **New stream** 下方，選擇 **Go live now**。

3. 於 **Stream settings** 標籤頁中，選擇您的地區，然後點擊 **Get URL**。

4. 將串流 URL 與串流金鑰進行串接。請確保串流 URL 在前，串流金鑰在後。

5. 使用串接後的字串作為推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b20f3fd0857c41bcab188dbaa97d19d3~tplv-goo7wpa0wc-image.image)

#### Twitch TV

1. 登入 [Twitch TV](https://www.twitch.tv/)。

2. 點擊您的頭像，並於下拉清單中選擇 **Settings**。

3. 點擊 **Channel and Videos** 標籤頁。

4. 在左側導覽窗格中，點擊 **Stream** \> **Settings**。

5. 以斜線（/）將伺服器 URL 與串流金鑰串接。請確保伺服器 URL 在前，串流金鑰在後。Twitch TV 的 RTMP 伺服器 URL 永遠是 `rtmp:// live.twitch.tv/app`。

6. 使用串接後的字串作為推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9fcd551f7f49a5af90766164057405~tplv-goo7wpa0wc-image.image)

#### Instagram

1. 啟用專業帳號。

   1. 登入 [Instagram](https://www.instagram.com/)。

   2. 在左側導覽窗格中，選擇 **More** \> **Settings**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cef1bc62f846f3867c45d8ebebf1ba~tplv-goo7wpa0wc-image.image)

   3. 於 **For professionals** 下方點擊 **Account type and tools**，然後點擊 **Switch to professional account**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359470824d7d4ac687621d41c153aaf1~tplv-goo7wpa0wc-image.image)

   4. 依需求選擇 **Creator** 或 **Business**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11dff9b0ecb64d0d9305c96c79ae75fa~tplv-goo7wpa0wc-image.image)

2. 取得串流 URL 與串流金鑰。

   1. 在 [Instagram](https://www.instagram.com/accounts/edit/) 左側導覽窗格中，選擇 **Create** \> **Live video**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c8e825007124527b08baa146c13eb3f~tplv-goo7wpa0wc-image.image)

   2. 於出現的對話框中，輸入您的直播標題並選擇觀眾。本範例請選擇 **Public**。然後點擊 **Next**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a18338b3834fc4b647dfa561bd9f7e~tplv-goo7wpa0wc-image.image)

   3. 取得串流 URL 與串流金鑰。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eed50beb29d4b078372e9de3bdff193~tplv-goo7wpa0wc-image.image)

每一次 Instagram 直播都會產生新的串流金鑰。

3. 將串流 URL 與串流金鑰進行串接。請確保串流 URL 在前，串流金鑰在後。

4. 使用串接後的字串作為推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24b3336dd7854c32b15237ed71fefeb5~tplv-goo7wpa0wc-image.image)
