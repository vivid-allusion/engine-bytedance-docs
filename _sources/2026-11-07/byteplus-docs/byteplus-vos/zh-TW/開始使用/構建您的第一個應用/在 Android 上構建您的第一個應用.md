---
title: "在 Android 上構建您的第一個應用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-android--zh-TW"
---

要在 Android 上構建您的第一個影片應用，請按照本分步指南執行 VideoOne Demo 專案。編譯成功後，您將獲得一個包含互動直播和影片播放功能的 Android 應用。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">該 Demo 專案未包含 Demo 應用中的所有功能，例如美顏 AR。請參考解決方案實施指南，瞭解如何實現這些功能。如需進一步協助，請聯絡您的<a href="https://console.byteplus.com/workorder/create">技術支援</a>。</div>


<span id="a0c6863a"></span>
## 前置條件

在開始之前，請完成以下任務。建議您在完成每項任務後集中記錄獲得的資訊，以便在專案設定過程中隨時查閱。

部分任務僅針對特定功能，如果您不需要這些功能，可以跳過相應任務。例如，如果您只需使用影片播放功能，則無需開通 BytePlus RTC 和 BytePlus MediaLive 服務。


|**任務** |**相關功能** |**任務說明** |**需記錄的資訊** |
|---|---|---|---|
|1. 註冊 BytePlus 賬號。<br><br>2. 為賬號建立訪問金鑰。 |全部功能 |* [註冊 BytePlus 賬號](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)<br><br>* [建立訪問金鑰](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey) |* 訪問金鑰 ID（AK）<br><br>* 訪問金鑰（SK） |
|1. 開通 BytePlus RTC 服務。<br><br>2. 建立 RTC 應用。 |互動直播 |* [使用 RTC 服務前](https://docs.byteplus.com/byteplus-rtc/docs/69865) |* AppId<br><br>* AppKey |
|1. 開通 BytePlus MediaLive 服務。<br><br>2. 建立 MediaLive 應用並獲取許可證。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已建立 BytePlus VOD 應用，請繫結已有應用，無需新建。   </div><br>    |互動直播 |* [開通 MediaLive 服務](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started)<br><br>* SDK 管理<br><br>   * [建立 SDK 應用](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)<br><br>   * [訪問您的 SDK 許可證](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license) |* App ID<br><br>* BytePlus MediaLive SDK 許可證檔案 |
|1. 開通 BytePlus VOD 服務。<br><br>2. 建立 VOD 應用並獲取許可證。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已建立 BytePlus MediaLive 應用，請繫結已有應用，無需新建。   </div><br>    |影片播放 |* [步驟 1：啟用 BytePlus VOD 服務](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#step-1-enable-the-byteplus-vod-service)<br><br>* [應用管理](https://docs.byteplus.com/byteplus-vod/docs/sdk-management)<br><br>* [許可證管理](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) |* App ID<br><br>* BytePlus VOD SDK 許可證檔案 |


<span id="db012043"></span>
## 系統要求


* Android Studio Arctic Fox 或更高版本。建議使用最新版本的 Android Studio 以獲得最佳效能。

* 一臺執行 Android 5.0 或更高版本的實體移動裝置。

* 請確保您使用的 CPU 架構為 armv7 或 arm64。


<span id="7114bbd5"></span>
## 操作流程

部分任務僅針對特定功能，如果您不需要體驗這些功能，可以跳過相應任務。例如，如果您只需體驗互動直播功能，則無需完成影片播放的相關設定。

<span id="a4ed37cb"></span>
### 克隆專案

請按照以下步驟克隆 Demo 專案：


1. 前往 GitHub 並克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 倉庫。

2. 在 `Client` 目錄下，使用 Android Studio 開啟 `Android` 資料夾。該資料夾為 Demo 專案的根目錄。


<span id="bd8233cf"></span>
### 設定應用伺服器

在根目錄下，開啟 `gradle.properties` 檔案，並指定您的應用伺服器地址：


* 如需使用 BytePlus 提供的應用伺服器，將 `SERVER_URL` 欄位設定為 `https://videocloud.byteplusapi.com/videoone_opensource`。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">該地址僅用於測試，不能用於生產環境。   </div>
   

* 如需部署自有應用伺服器，請參照部署應用伺服器（[為 Android 和 iOS 部署伺服器](https://docs.byteplus.com/docs/byteplus-vos/docs-backend-deployment-guide-zh-TW)、[部署 Web 伺服器](https://docs.byteplus.com/docs/byteplus-vos/docs-deploying-the-server-web-zh-TW)）的說明操作，然後將 `SERVER_URL` 欄位設定為 `http://{your_server_address}:{port_number}/videoone_opensource`。


<span id="8ec44536"></span>
### 設定包名

在 `app` 目錄下，開啟 `build.gradle` 檔案，並將 `applicationId` 設定為您的 Android 應用包名。如果您已申請 BytePlus MediaLive 或 VOD SDK 許可證，包名必須與申請許可證時填寫的名稱完全一致。

<span id="ab53744f"></span>
### RTC 配置

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗互動直播，該任務為必選項。</div>


在根目錄下，開啟 `gradle.properties` 檔案，並將[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-TW#a0c6863a)部分獲取的值配置到以下欄位中。這些資訊用於客戶端與 BytePlus RTC 服務通訊時的身份驗證。


|**欄位名稱** |**描述** |**示例** |
|---|---|---|
|APP_ID |您的 BytePlus RTC 應用的**AppId**。 |123456\*\*\*\*\*\*\*\*3deb567a86 |
|APP_KEY |您的 BytePlus RTC 應用的**AppKey**。 |1bfaa8e\*\*\*\*\*\*\*\*fjb6j6hhde68c07d |
|ACCESS_KEY_ID |您的 BytePlus 賬號的**訪問金鑰 ID（AK）** 。 |AKAPZ7\*\*\*\*\*\*\*\*FLB0D38CM8DK49SO39D83KD820DFK4k9 |
|SECRET_ACCESS_KEY |您的 BytePlus 賬號的**訪問金鑰金鑰（SK）** 。 |8dk39vK\*\*\*\*\*\*\*\*k7D93KDHS8DJSLud830DJEO37EI3UDK37WODKu3oQ |


<span id="1653077f"></span>
### MediaLive 配置

<span id="81fa8179"></span>
#### 準備域名

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗互動直播場景，該任務為必選項。</div>



|**子任務** |**任務說明** |**必填資訊** |
|---|---|---|
|**新增域名。** <br><br>您需至少新增兩個域名，一個用於推流，另一個用於拉流。 |[新增域名](https://docs.byteplus.com/byteplus-media-live/docs/domain) |* 推流域名<br><br>* 拉流域名 |
|**為您的域名新增 CNAME 記錄。** <br><br>新增域名後，BytePlus MediaLive 會自動為其分配一個對應的 MediaLive 域名。然後，您必須新增 CNAME 記錄，將您的域名指向分配的 MediaLive 域名。 |[新增 CNAME 記錄](https://docs.byteplus.com/byteplus-media-live/docs/adding-a-cname-record) |/ |
|**啟用 URL 鑑權。** <br><br>啟用 URL 鑑權可保護您的流媒體內容，防止未授權的域名使用。 |[URL 鑑權](https://docs.byteplus.com/en/byteplus-media-live/docs/url-authentication?version=v1.0) |* 主金鑰 |
|**配置轉碼模板。** <br><br>您可以對原始直播流進行轉碼，以滿足不同使用者的觀看需求。 |[配置轉碼任務](https://docs.byteplus.com/en/byteplus-media-live/docs/configuring-transcoding) |* AppName |


<span id="a001fbcb"></span>
#### 設定流地址

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗互動直播場景，需完成此任務。</div>


在 Demo 專案的 `solutions/interactivelive` 目錄下，開啟 `gradle.properties` 檔案，並將上一步獲取的資訊填寫到對應欄位中。這些資訊用於構建推流和拉流地址。


|**欄位名** |**說明** |**示例** |
|---|---|---|
|LIVE_PULL_DOMAIN |http://{domain_name}，其中 "domain_name" 表示**拉流域名**。 |`http://pull-demo.com` |
|LIVE_PUSH_DOMAIN |rtmp://{domain_name}，其中 "domain_name" 表示**推流域名**。 |`rtmp://push-demo.com` |
|LIVE_PUSH_KEY |用於 URL 鑑權的**主金鑰**。 |`XED45d5dDLSH********KDFD` |
|LIVE_APP_NAME |已配置轉碼模板的**AppName**。 |`videoone_demo` |


<span id="d9803aef"></span>
#### 整合許可證

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗互動直播場景或直播相關功能，需完成此任務。</div>


請按照以下步驟整合在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-TW#a0c6863a)部分獲取的 **BytePlus MediaLive SDK 許可證檔案**：


1. 將許可證檔案重新命名為 `ttsdk.lic`。

2. 將許可證檔案移動到目標目錄：

   1. 如需體驗互動直播場景，請將許可證檔案移動到 `solutions/interactivelive/src/main/assets`。

   2. 如果您希望體驗與直播相關的功能，請將許可證檔案移動到 `solutions/media-live/live-entrance/src/main/assets`。

3. 開啟 `gradle.properties` 檔案，並將 `LIVE_TTSDK_APP_ID` 設定為您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-TW#a0c6863a)部分建立的 MediaLive 應用的**App ID**。

4. 請參考[生成流地址](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator)，準備用於推流的直播流 URL 和用於拉流的直播流 URL。


<span id="f8211e2d"></span>
### 點播設定

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗影片播放場景及相關功能，需完成此任務。</div>


整合您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-TW#a0c6863a)部分獲得的 BytePlus VOD SDK 許可證：


1. 將許可證檔案移動到 `solutions/vod/vod-common/src/main/assets/vodlicense` 目錄。

2. 在 `solutions/vod/vod-common/` 目錄下，開啟 `gradle.properties` 檔案，並配置以下欄位：



|**欄位名** |**說明** |**示例** |
|---|---|---|
|VOD_APP_ID |您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-TW#a0c6863a)部分建立的 VOD 應用的**App ID**。 |5\*\*\*\*1 |
|VOD_APP_CHANNEL |您的應用分發渠道。 |googleplay |
|VOD_LICENSE_URI |您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-TW#a0c6863a)部分獲取的**BytePlus VOD SDK 證書檔案**的儲存路徑。 |assets:///vodlicense/{LICENSE_NAME}.lic |


<span id="00c4fcba"></span>
### 專案編譯


1. 將移動裝置連線到您的電腦，並在 Android Studio 中設定為目標裝置。

2. 點選**Sync Project with Gradle Files**按鈕，同步專案與 Gradle 檔案。

3. 點選**Run**按鈕，啟動編譯流程。


<span id="2669bf25"></span>
### 應用執行

如果編譯過程無錯誤完成，VideoOne 應用將安裝到已連線的移動裝置上，並自動跳轉至登入介面。使用您的郵箱登入應用，開始探索其功能與特性。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33f9ae7de2ca4e41a5c73e26ae22d630~tplv-goo7wpa0wc-image.image) </span>

<span id="7d5db6c4"></span>
## 程式碼解析

Demo 專案的目錄結構如下：

```Plain
. 
├── app                    # Entry point of the app 
├── build.gradle 
├── component              # Public components 
│   ├── Avatars                # Avatar resources 
│   ├── LoginKit               # Login 
│   └── SolutionBase           # Base library 
│   └── ToolKit                # Common tools 
├── gradle 
├── gradle.properties           # Common configurations 
├── gradlew 
├── gradlew.bat 
├── local.properties 
├── settings.gradle 
└── solutions                 # Solutions 
    ├── VideoPlaybackEdit     # The video playback and editing demo 
    │   └── Vod
    ├── interactivelive       # The interactive live streaming demo 
    │   ├── build.gradle
    │   ├── consumer-rules.pro
    │   ├── gradle.properties
    │   ├── proguard-rules.pro
    │   └── src
    ├── media-live            # MediaLive SDK configurations 
    │   ├── live-common       # Common tools  
    │   ├── live-entrance     # Entrance
    │   ├── live-player       # Live stream pulling
    │   ├── live-pusher       # Live stream pushing
    └── rtc-api-example       # RTC API Example 
         └── rtc-api-example-entry    # Entrance
```
