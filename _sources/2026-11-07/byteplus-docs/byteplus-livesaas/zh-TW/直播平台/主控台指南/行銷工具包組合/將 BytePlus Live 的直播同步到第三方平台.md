---
title: "將 BytePlus Live 的直播同步到第三方平台"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/jiang-byteplus-live-de-zhi-bo-tong-bu-dao-di-san-f-zh-TW"
---

您可以使用多平台串流功能，將 BytePlus Live 的直播同步到第三方平台，讓觀眾能夠在不同平台同時觀看相同的直播，並擴展您的直播內容覆蓋範圍。

<span id="70e3cc74"></span>
## 前置條件

擁有 BytePlus 帳戶，或具備 **行銷工具包** \> **編輯** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。

<span id="e053edc6"></span>
## 操作流程


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播間列表中，點擊以開啟直播間。

3. 於左側導覽列，點擊 **行銷工具包** \> **多平台串流**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6f1411fec524fed9624f4d489f54cb5~tplv-goo7wpa0wc-image.image) </span>

4. 您可以新增第三方平台，或取得本直播間的拉流地址。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若直播間有多個直播來源，僅第一個來源的直播流能同步至已新增的第三方平台。如需瞭解多個直播來源的更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-ji-shi-lai-yuan-zh-TW">管理直播來源</a>。若要同步其他來源的直播流，請聯絡業務代表以進行自訂設定。若您沒有業務代表，請點擊<a href="https://www.byteplus.com/en/contact">此處</a>以填寫此表單，讓我們的業務團隊與您聯絡。   </div>
   

   * 新增第三方平台：點擊 **新增平台**。在 **新增平台** 對話框中，選擇您要同步直播的目標平台。然後，輸入平台名稱及推流地址。**推流**開關預設為開啟。如需瞭解如何取得推流地址，請參閱 [如何將直播同步到主流直播平台](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-byteplus-live-de-zhi-bo-tong-bu-dao-di-san-f-zh-TW#4995291e)。

      啟用**推流**開關後，當您的直播活動開始時，串流會自動同步至該平台，觀眾可同時在 BytePlus Live 與第三方平台觀看。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/032aa5707a0c4a1cbe5163059bee305a~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">僅支援 RTMP 格式的推流地址。      </div>
      

   * 取得拉流地址：點擊 **取得拉流地址**，並複製彈出對話框中的地址。您可以在第三方平台使用此地址，將本直播間的直播同步至該平台。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6af2461666c4a9dacc07c17f53b41e1~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">每個直播間僅有一個拉流地址。      </div>
      

5. 使用除預錄影片外的播出方式開始直播。

6. （可選）新增第三方平台後，您可以執行以下操作。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2df6c1cbf4c4d91a0b2c178330dfd63~tplv-goo7wpa0wc-image.image) </span>

   * 查看推流狀態。

   * 編輯或刪除平台資訊。

   * 開啟或關閉**推流**開關，以同步或停止同步直播到指定平台。


<span id="4995291e"></span>
## 如何將直播同步到主流直播平台

本節說明如何在以下主流直播平台取得伺服器 URL 與串流金鑰：TikTok、YouTube Live、MetaLive（Facebook）、LinkedIn Live、Twitch 和 Instagram。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">以下平台可能因政策變動而更改推流地址取得方式及開播條件。請參考各平台的最新要求。</div>


* <div data-tips="true" data-tips-type="tip">請確保您符合在目標平台開啟直播的要求。</div>



<span id="4ea4230a"></span>
### TikTok


1. 登入 [TikTok Live](https://www.tiktok.com/live?lang=en)。

2. 於左側導覽列，點擊 **Go LIVE**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96fff1487b7e4601883709f023ce991e~tplv-goo7wpa0wc-image.image) </span>

3. 在 TikTok 上開始直播。然後，複製伺服器 URL 與串流金鑰。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecdededb88a44a6cbfbcea4888592333~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">每次在 TikTok 開啟直播時，您都必須複製伺服器 URL 和串流金鑰。   </div>
   

4. 使用斜線（/）將伺服器 URL 與串流金鑰串接。請確保伺服器 URL 在前，串流金鑰在後。

5. 將串接後的字串作為推流地址，輸入至 **新增平台** 對話框中的 BytePlus Live 控制台。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a28dd17f142344008e47081117852f4b~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要在 TikTok Live 開啟直播，您必須：</div>



* <div data-tips="true" data-tips-type="tip">擁有至少 1000 名粉絲。</div>


* <div data-tips="true" data-tips-type="tip">年滿 18 歲或以上。</div>



<span id="33d493fe"></span>
### YouTube Live


1. 登入 [YouTube Live](https://www.youtube.com/)。

2. 於頁面右上角，點擊 **建立**圖示並選擇 **Go live**。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果這是您首次啟用直播功能，可能需要最多 24 小時才能取得直播權限。   </div>
   

3. 在 **STREAM SETTINGS** 標籤頁，將串流 URL 與串流金鑰串接。請確保串流 URL 在前，串流金鑰在後。

4. 將串接後的字串作為推流地址，輸入至 **新增平台** 對話框中的 BytePlus Live 控制台。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6887d8038a4d8c868cc4f1b6318c14~tplv-goo7wpa0wc-image.image) </span>


<span id="c32ac0bb"></span>
### MetaLive


1. 登入 [Facebook](https://www.facebook.com/live/create)。

2. 於 **Go live** 區段中點擊 **Go live**。

3. 選擇 **串流軟體**作為您的影片來源。

4. 若要讓串流金鑰永久有效，請開啟**永久串流金鑰**開關。否則，串流金鑰在直播結束後將無法再次使用。

5. 使用斜線（/）將伺服器 URL 與串流金鑰串接。請確保伺服器 URL 在前，串流金鑰在後。

6. 將串接後的字串作為推流地址，輸入至**新增平台**對話框中的BytePlus Live 控制台。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/269d663243664680b93e050dd2e0f107~tplv-goo7wpa0wc-image.image) </span>


<span id="2603a655"></span>
### LinkedIn Live

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LinkedIn Live 僅限經審核通過的用戶使用。如需確認您是否符合資格，請進一步了解 <a href="https://www.linkedin.com/help/linkedin/answer/a568503?src=li-other&veh=www.linkedin.com%7Cli-other">LinkedIn Live</a> 的存取條件。</div>



1. 登入[LinkedIn Live](https://www.linkedin.com/video/golive/now/)。

2. 在頁面左上角的**新串流**下選擇**立即直播**。

3. 於**串流設定**標籤頁選擇您的區域，然後點擊**取得 URL**。

4. 將串流 URL 與串流金鑰串接。請確保串流 URL 在前，串流金鑰在後。

5. 將串接後的字串作為推流地址，輸入至**新增平台**對話框中的BytePlus Live 控制台。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b20f3fd0857c41bcab188dbaa97d19d3~tplv-goo7wpa0wc-image.image) </span>


<span id="f08497f6"></span>
### Twitch TV


1. 登入[Twitch TV](https://www.twitch.tv/)。

2. 點擊您的頭像，並於下拉清單中選擇**設定**。

3. 點擊**頻道與影片**標籤頁。

4. 於左側導覽窗格點擊**串流** \> **設定**。

5. 使用斜線（/）將伺服器 URL 與串流金鑰串接。請確保伺服器 URL 在前，串流金鑰在後。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Twitch TV 的 RTMP 伺服器 URL 永遠是 <code>rtmp:// live.twitch.tv/app</code>。   </div>
   

6. 將串接後的字串作為推流地址，輸入至**新增平台**對話框中的BytePlus Live 控制台。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9fcd551f7f49a5af90766164057405~tplv-goo7wpa0wc-image.image) </span>


<span id="b4238643"></span>
### Instagram


1. 啟用專業帳號。

   1. 登入[Instagram](https://www.instagram.com/)。

   2. 於左側導覽窗格選擇**更多** \> **設定**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cef1bc62f846f3867c45d8ebebf1ba~tplv-goo7wpa0wc-image.image) </span>

   3. 於**專業用戶**下點擊**帳號類型與工具**，然後點擊**切換為專業帳號**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359470824d7d4ac687621d41c153aaf1~tplv-goo7wpa0wc-image.image) </span>

   4. 依需求選擇**創作者**或**商業**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11dff9b0ecb64d0d9305c96c79ae75fa~tplv-goo7wpa0wc-image.image) </span>

2. 取得串流 URL 與串流金鑰。

   1. 於[Instagram](https://www.instagram.com/accounts/edit/)左側導覽窗格選擇**建立** \> **直播影片**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c8e825007124527b08baa146c13eb3f~tplv-goo7wpa0wc-image.image) </span>

   2. 在出現的對話框中，輸入您的直播影片標題並選擇觀眾。此處以選擇**公開**為例。然後點擊**下一步**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a18338b3834fc4b647dfa561bd9f7e~tplv-goo7wpa0wc-image.image) </span>

   3. 取得串流 URL 與串流金鑰。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eed50beb29d4b078372e9de3bdff193~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">每次 Instagram 直播都會產生新的串流金鑰。   </div>
   

3. 將串流 URL 與串流金鑰串接。請確保串流 URL 在前，串流金鑰在後。

4. 將串接後的字串作為推流地址，輸入至**新增平台**對話框中的BytePlus Live 控制台。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24b3336dd7854c32b15237ed71fefeb5~tplv-goo7wpa0wc-image.image) </span>
