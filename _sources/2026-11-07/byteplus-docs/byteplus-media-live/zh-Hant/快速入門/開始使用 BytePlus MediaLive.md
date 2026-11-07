---
title: "開始使用 BytePlus MediaLive"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getting-started-zh-TW"
---

本主題將完整說明如何進行初始設定，以便開始使用 BytePlus MediaLive 進行直播內容串流。您將學會如何啟用服務、添加並配置推流與拉流的網域名稱、產生串流地址，以及開始您的首次直播。

<span id="6cf2b444"></span>
## 先決條件


* 一個 BytePlus 帳戶。

* 若您是首次登入 [BytePlus 控制台](https://console.byteplus.com)，請完成認證。

* 若您尚未擁有推流與拉流所需的網域名稱，可使用 MediaLive 提供的測試網域名稱。

* 若您希望使用自有網域名稱，則必須至少新增兩個：一個用於推流，一個用於拉流。推流與拉流的網域名稱必須位於同一個網域名稱空間。


<span id="b3bed337"></span>
## 操作流程

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a390beb258b4fb589a233096aa071f3~tplv-goo7wpa0wc-image.image) </span>

<span id="da5a6a63"></span>
### 啟用 MediaLive 服務


1. 登入 [BytePlus 控制台](https://console.byteplus.com/)。

2. 於 **產品** 區塊中，點擊 **BytePlus MediaLive**。

3. 如畫面提示您輸入帳單資訊，請依指示填寫。否則，請進行下一步。

4. 點擊 **立即啟用**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/718efbc829a14a5c939be63e0b4f3dbf~tplv-goo7wpa0wc-image.image) </span>

5. 依照畫面指示填寫您的資訊，然後點擊 **申請啟用**。

6. 啟用完成後，請登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。


<span id="fc8ae6de"></span>
### 新增網域名稱

要使用 BytePlus MediaLive，您必須至少新增兩個網域名稱，一個用於推流，另一個用於拉流。

MediaLive 會透過網域名稱空間來關聯推流與拉流的網域名稱。服務於同一業務線的推流與拉流網域名稱需位於同一個網域名稱空間。請參閱 [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost)，以瞭解推流與拉流網域名稱之間的詳細關聯說明。


1. 於左側導覽窗格中，點擊 **網域名稱**。

2. 於出現的 **網域名稱** 頁面上，點擊 **新增網域名稱**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ec6554b63b6491d81155cd2a980b6c5~tplv-goo7wpa0wc-image.image) </span>

3. 完成以下設定：

   * **新增網域名稱**：

      1. 選擇 **推流** 作為網域名稱類型。網域名稱新增後，無法變更其類型。

      2. 輸入用於推流的網域名稱。不可新增萬用字元網域名稱。建議您使用二級網域名稱，例如 `example.live.com`。每個帳戶最多可新增 10 個網域名稱。

      3. 若您需使用 [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction) 協議，則必須為您的網域名稱配置 SSL 憑證。

   * **關聯網域名稱空間**：

      * 建議以首個新增的網域名稱作為網域名稱空間的名稱。

      * 請輸入以小寫字母組成且以「.com」結尾的網域名稱

      * 請輸入二級網域名稱或子網域。

      * 一個網域名稱會關聯至一個網域名稱空間。預設可新增 10 個網域名稱空間。如需新增更多，請聯絡 [BytePlus 技術支援](https://console.byteplus.com/workorder/create)。

   * **加速區域：**  選擇您希望加速內容傳遞的區域。直播服務費用會依加速區域而有所不同。請參閱 [直播服務收費標準](https://docs.byteplus.com/docs/byteplus-media-live/docs-live-streaming-service-fees) 以獲取詳細價格資訊。

      :::提示

      如果你選擇**全球加速**或**中國大陸**，則必須為該網域名稱取得互聯網內容提供者（ICP）許可證。你可以在[ICP/IP 地址/網域名稱資訊備案管理系統](https://beian.miit.gov.cn/#/Integrated/index)上完成驗證流程。

      :::

   * **專案**：為網域名稱空間選擇一個專案。將網域名稱空間與專案關聯後，你可以依專案管理資源使用情況與計費。如需瞭解更多有關專案的資訊，請參閱[關於專案](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects)。

4. 點擊**下一步**以儲存設定。

5. 重複步驟 2 至 4 以新增拉流用的網域名稱。請記得選擇**拉流**作為網域類型。


新增的網域名稱會顯示在網域名稱清單中。

<span id="f55c33b3"></span>
### 設定 CNAME 記錄

為網域名稱新增 CNAME 記錄，指向其自動分配的對應 BytePlus MediaLive 網域名稱。如此一來，所有前往你網域名稱的流量都會導向 BytePlus MediaLive 網域名稱。


1. 在網域名稱清單中，找到你要設定的網域名稱，然後複製**CNAME**欄中的對應 BytePlus MediaLive 網域名稱。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5facfd095c54e19b6fb629e262ad6df~tplv-goo7wpa0wc-image.image) </span>

2. 登入你的網域服務供應商的 DNS 平台。為該網域名稱新增 CNAME 記錄，指向 BytePlus MediaLive 網域名稱。

3. 執行`ping`或`dig`指令，以檢查 CNAME 記錄是否生效。如果輸出顯示 BytePlus MediaLive 網域名稱為 CNAME，則設定成功，該網域名稱即可使用。你也可以透過確認 BytePlus MediaLive 網域名稱旁的圖示變為綠色勾號來驗證設定。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8f1391c173444ff8a74ca5db24385da~tplv-goo7wpa0wc-image.image) </span>


如需更詳細的 CNAME 記錄設定說明，請參閱[新增 CNAME 記錄](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record)。

<span id="4f17ce32"></span>
### （選用）HTTPS 及其他網域名稱設定

你可以設定其他網域名稱選項，以滿足你的特定需求，例如設定 SSL 憑證或 Referer 限制。請參閱以下主題，取得完成設定的詳細指引。


* [新增 SSL 憑證](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)

* [Referer](https://docs.byteplus.com/docs/byteplus-media-live/docs-referer)

* [URL 驗證](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication)

* [IP 限制](https://docs.byteplus.com/docs/byteplus-media-live/docs-ip-blocklist-and-allowlist)


本主題以 SSL 憑證設定為範例。若要為你的網域名稱設定 SSL 憑證，請完成以下步驟：

<span id="7a4f3332"></span>
#### 新增 SSL 憑證


1. 在左側導覽窗格中，點擊**憑證**。

2. 於**憑證**頁面，點擊**新增憑證**以開啟**新增 HTTPS 憑證**對話方塊。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9223e729e0c74fc2a6075fbaed9b4043~tplv-goo7wpa0wc-image.image) </span>

3. 輸入憑證名稱、憑證內容及私鑰。目前僅支援新增 PEM 格式的憑證。

4. 點擊**確認**以儲存 SSL 憑證。


<span id="67853b4d"></span>
#### 啟用 HTTPS


1. 在左側導覽窗格中，點擊**網域**。

2. 於出現的**網域**頁面，找到你要設定的網域名稱，並在**操作**欄點擊**設定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86933bf66e50428889bd16253b570a0e~tplv-goo7wpa0wc-image.image) </span>

3. 於開啟的網域名稱頁面，點擊**HTTPS**分頁。

4. 在**HTTPS**開關右側，點擊**編輯**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10c428c6e1f14e32b86461545b03bf08~tplv-goo7wpa0wc-image.image) </span>

5. 於出現的**編輯 HTTPS 資訊**對話方塊中，**HTTPS**會自動開啟。選擇你要使用的 SSL 憑證，然後點擊**確認**。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">要顯示於<strong>憑證</strong>清單中，您的 SSL 憑證必須在<strong>主體替代名稱</strong>欄位中包含您的網域名稱。</div>


* <div data-tips="true" data-tips-type="tip">HTTPS 加密約需 10 分鐘生效。若設定未生效，請聯繫您的技術支援以獲得協助。</div>



<span id="fc6a3cf4"></span>
### （選填）轉碼及其他功能設定

BytePlus MediaLive 亦為您提供多種增值服務，例如轉碼與錄製。請參閱以下主題，獲取有關如何使用這些服務的詳細說明：


* [設定轉碼任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)

* [設定錄製任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-recordings)

* [設定截圖任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-screenshot-capturing)

* [設定回源拉流任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings)

* [設定時移任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-time-shifting)

* [設定浮水印任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-live-stream-watermarks)

* [設定回調任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task)


<span id="f4551ba7"></span>
### 產生串流位址

您可以使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)或依據一組串接規則手動組建，來產生推流與拉流位址。詳情請參閱[產生直播串流位址](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses)。

<span id="Starting the live stream"></span>
### 開始串流

您可以透過以下任一方式開始串流：


* 使用[Web 推流](https://console.byteplus.com/live/main/WebPushStream)及[Web 拉流](https://console.byteplus.com/live/main/webPullStream/play)，這些是 BytePlus MediaLive 控制台內建的網頁工具，可直接從您的網頁瀏覽器推送及拉取直播串流。請參閱以下主題，瞭解如何使用這些工具：

   * [透過控制台推流](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-push)

   * [透過控制台拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull)

* 使用第三方串流工具（如 Open Broadcaster Software (OBS)）及影音播放器（如 VLC）進行推流與拉流。

* 將 BytePlus MediaLive Broadcast SDK 及 BytePlus MediaLive Player SDK 整合至您的應用程式中，以進行推流與拉流：

   * Android 與 iOS：[SDK 介紹](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)

   * Web：[Player SDK for Web：SDK 概覽](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-player-sdk-for-web)及[Broadcast SDK for Web：SDK 概覽](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-broadcast-sdk-for-web)


<span id="1f2fd5c3"></span>
### （選填）使用 OpenAPI

除了使用 BytePlus MediaLive 控制台外，您也可以透過 OpenAPI 存取 MediaLive 服務。請參閱

[BytePlus MediaLive OpenAPI 介紹](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-with-your-api)，瞭解如何開始使用 MediaLive OpenAPI。

此外，BytePlus MediaLive 提供伺服器端 SDK，內含以 Java、Python、Go 及 PHP 撰寫的 API 請求範例。詳情請參閱[伺服器端 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk)。
