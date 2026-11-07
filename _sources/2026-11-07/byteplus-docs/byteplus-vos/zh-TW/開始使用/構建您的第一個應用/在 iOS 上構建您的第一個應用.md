---
title: "在 iOS 上構建您的第一個應用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-ios--zh-TW"
---

要構建具備互動直播和影片播放功能的 iOS 應用，您可以按照本分步指南執行 VideoOne Demo 專案。本文件將帶您完成整個流程，包括完成前置條件、配置專案、編譯並在實體裝置上執行應用。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">GitHub 示例專案不包含示例應用中的全部功能，例如美顏 AR。請參考解決方案實施指南，瞭解這些功能的實現方法。如需進一步協助，請聯絡您的<a href="https://console.byteplus.com/workorder/create">技術支援</a>。</div>


<span id="5a07e3aa"></span>
## 前置條件

在開始之前，請完成以下任務。建議您集中記錄每項任務完成後獲得的資訊，以便在專案設定過程中隨時查閱。

部分任務針對特定功能，如果您不需要這些功能，可以跳過。例如，如果您只需使用影片播放，則無需啟用 BytePlus RTC 和 BytePlus MediaLive 服務。


|**任務** |**相關功能** |**任務說明** |**完成後獲得的資訊** |
|---|---|---|---|
|1. 註冊 BytePlus 賬號。<br><br>2. 為賬號建立訪問金鑰。 |全部功能 |* [註冊 BytePlus 賬號](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)<br><br>* [建立訪問金鑰](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey) |* 訪問金鑰 ID（AK）<br><br>* 訪問金鑰（SK） |
|1. 開通 BytePlus RTC 服務。<br><br>2. 建立 RTC 應用。 |* 互動直播<br><br>* RTC API 示例 |* [使用 RTC 服務前](https://docs.byteplus.com/byteplus-rtc/docs/69865) |* AppId<br><br>* AppKey |
|1. 開通 BytePlus MediaLive 服務。<br><br>2. 建立 MediaLive 應用並獲取許可證。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已建立 BytePlus VOD 應用，請繫結已有應用，無需新建。   </div><br>    |互動直播 |* [開通 MediaLive 服務](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#activating-the-medialive-service)<br><br>* SDK 管理<br><br>   * [建立 SDK 應用](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)<br><br>   * [訪問您的 SDK 許可證](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license) |* App ID<br><br>* BytePlus MediaLive SDK 許可證檔案 |
|1. 開通 BytePlus VOD 服務。<br><br>2. 建立 VOD 應用並獲取許可證。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您已建立 BytePlus MediaLive 應用，請繫結已有應用，無需新建。   </div><br>    |影片播放 |* [步驟 1：啟用 BytePlus VOD 服務](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#step-1-enable-the-byteplus-vod-service)<br><br>* [應用管理](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management)<br><br>* [許可證管理](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) |* App ID<br><br>* BytePlus VOD SDK 許可證檔案 |


<span id="bfda08e6"></span>
### 系統要求


* Xcode 14.0 或更高版本

* CocoaPods 1.10.0 或更高版本

* 執行 iOS 13.0 或更高版本的實體移動裝置。


<span id="74286d48"></span>
## 操作流程

部分任務僅針對特定功能，如果您不需要體驗這些功能，可以跳過。例如，如果您只需體驗互動直播，則無需完成影片播放的設定。

<span id="9d161712"></span>
### 克隆專案

請按照以下步驟克隆 Demo 專案：


1. 前往 GitHub，克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 倉庫。

2. 開啟 Terminal，並將當前目錄切換到 `Client/iOS`，該目錄為專案根目錄。

3. 將您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-TW#5a07e3aa)部分獲取的許可證檔案移動到 `Component/AppConfig/License` 目錄。如果您有多個同名許可證檔案，可能需要重新命名這些檔案。

4. 執行 `pod install` 以安裝依賴項。


<span id="32bcb285"></span>
### 設定應用伺服器


1. 在專案根目錄下，使用 Xcode 開啟 `VideoOne.xcworkspace` 檔案。

2. 導航至 `Pods/Development Pods/AppConfig`，並在 Xcode 中開啟 `BuildConfig.h` 檔案。

3. 指定您的應用伺服器地址：

   * 如需使用 BytePlus 提供的應用伺服器，將 `ServerUrl` 欄位設定為 `https://videocloud.byteplusapi.com/videoone_opensource`。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">該地址僅用於測試，不能用於生產環境。      </div>
      

   * 如需部署自有應用伺服器，請參照部署應用伺服器（[為 Android 和 iOS 部署伺服器](https://docs.byteplus.com/docs/byteplus-vos/docs-backend-deployment-guide-zh-TW)、[部署 Web 伺服器](https://docs.byteplus.com/docs/byteplus-vos/docs-deploying-the-server-web-zh-TW)）的說明操作，並將 `ServerUrl` 欄位設定為 `http://{your_server_address}:{port_number}/videoone_opensource`。


<span id="60922590"></span>
### 專案設定


1. 在 Xcode 中使用您的 Apple ID 登入。

2. 參考 [Assign a project to a team](https://help.apple.com/xcode/mac/current/#/dev23aab79b4) 配置應用簽名。

3. 設定 **Bundle Identifier**。如果您申請了 BytePlus MediaLive SDK 或 BytePlus VOD SDK 的許可證，Bundle Identifier 必須與申請許可證時填寫的名稱一致。

4. 如果您使用 Xcode 15，需額外完成構建設定配置：

   1. 導航至 **TARGETS** 頁面，並切換到 **Build Settings** 標籤頁。

   2. 搜尋 **Other Linker Flags** 設定項。

   3. 在 **Other Linker Flags** 行的數值區域雙擊。

   4. 在彈出視窗中，點選  **+**  按鈕，新增 `-ld64` 連結器標誌。


<span id="a1e62caa"></span>
### RTC 設定

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需使用互動直播功能，必須完成此任務。</div>


在 Xcode 中，導航至 `Pods/Development Pods/AppConfig`，並開啟 `BuildConfig.h` 檔案。使用您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-TW#5a07e3aa)部分獲得的數值配置以下欄位。該資訊用於客戶端與 BytePlus RTC 服務通訊時的身份驗證。


|**欄位名稱** |**說明** |**示例** |
|---|---|---|
|RTCAPPID |您的 BytePlus RTC 應用的 **AppId**。 |123456\*\*\*\*\*\*\*\*3deb567a86 |
|RTCAPPKey |您的 BytePlus RTC 應用的 **AppKey**。 |1bfaa8e\*\*\*\*\*\*\*\*fjb6j6hhde68c07d |
|AccessKeyID |您的 BytePlus 賬號的 **訪問金鑰 ID（AK）** 。 |AKAPZ7\*\*\*\*\*\*\*\*FLB0D38CM8DK49SO39D83KD820DFK4k9 |
|SecretAccessKey |您的 BytePlus 賬號的 **訪問金鑰（SK）** 。 |8dk39vK\*\*\*\*\*\*\*\*k7D93KDHS8DJSLud830DJEO37EI3UDK37WODKu3oQ |


<span id="f15de15f"></span>
### MediaLive 設定

<span id="b758f198"></span>
#### 準備域名

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需使用互動直播功能，必須完成此任務。</div>



|**子任務** |**任務說明** |**所需資訊** |
|---|---|---|
|**新增域名。** <br><br>您應至少新增兩個域名，一個用於推流，另一個用於拉流。 |[新增域名](https://docs.byteplus.com/en/byteplus-media-live/docs/domain?version=v1.0#bb9e1337) |* 推流域名<br><br>* 拉流域名 |
|**為您的域名新增 CNAME 記錄。** <br><br>新增域名後，系統會自動為您的域名分配一個 BytePlus MediaLive 域名。您必須為您的域名新增 CNAME 記錄，將其指向分配的 BytePlus MediaLive 域名。 |[新增 CNAME 記錄](https://docs.byteplus.com/en/byteplus-media-live/docs/adding-a-cname-record?version=v1.0) |/ |
|**啟用 URL 鑑權。** <br><br>為保障推流安全並防止直播資訊被未經授權下載，您可以啟用 URL 鑑權。此步驟可防止域名被未經授權使用。 |[URL 鑑權](https://docs.byteplus.com/en/byteplus-media-live/docs/url-authentication?version=v1.0) |* 主金鑰 |
|**配置轉碼模板。** <br><br>您可以對原始直播流進行轉碼，以滿足不同使用者的觀看需求。 |[配置轉碼任務](https://docs.byteplus.com/en/byteplus-media-live/docs/configuring-transcoding) |* AppName |


<span id="cf1eeec6"></span>
#### 設定流地址

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗互動直播場景，此任務為必選項。</div>


在 Xcode 中，導航至 `Pods/Development Pods/AppConfig`，開啟 `BuildConfig.h` 檔案，並將上一步獲取的資訊填寫到對應欄位。這些資訊用於拼接推流和拉流地址。


|**欄位名稱** |**描述** |**示例** |
|---|---|---|
|LivePullDomain |http://{domain_name}，其中“domain_name”指 **拉流域名**。 |`http://pull-demo.com` |
|LivePushDomain |rtmp://{domain_name}，其中“domain_name”指 **推流域名**。 |`rtmp://push-demo.com` |
|LivePushKey |**主金鑰**，用於 URL 鑑權。 |`XED45d5dDLSH********KDFD` |
|LiveAppName |您已配置轉碼模板的 **AppName**。 |`videoone_demo` |


<span id="2c5d644a"></span>
#### 整合許可證

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗互動直播場景或直播相關功能，此任務為必選項。</div>


請按照以下步驟整合 BytePlus MediaLive SDK 許可證：


1. 在 Xcode 中，導航至 `Pods/Development Pods/AppConfig`，開啟 `BuildConfig.h` 檔案。

2. 設定以下欄位：



|**欄位名稱** |**描述** |**示例** |
|---|---|---|
|LiveAPPID |您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-TW#5a07e3aa)部分建立或繫結的 MediaLive 應用的 **App ID**。 |5\*\*\*\*1 |
|LiveLicenseName |您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-TW#5a07e3aa)部分獲得的 **BytePlus MediaLive SDK 許可證檔案**名稱。 |livelicense.lic |



3. 參考 [生成流地址](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator)，準備推流和拉流 URL。


<span id="047a3955"></span>
### VOD 設定

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需體驗影片播放場景及相關功能，此任務為必選項。</div>


請按照以下步驟整合 BytePlus VOD SDK 許可證：


1. 在 Xcode 中，導航至 `Pods/Development Pods/AppConfig`，開啟 `BuildConfig.h` 檔案。

2. 設定以下欄位：

   
   |**欄位名稱** |**描述** |**示例** |
   |---|---|---|
   |VODAPPID |您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-TW#5a07e3aa)部分建立或繫結的 VOD 應用的 **App ID**。 |5\*\*\*\*1 |
   |VODLicenseName |您在[前置條件](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-TW#5a07e3aa)部分獲得的 **BytePlus VOD SDK 許可證檔案**名稱。 |vodlicense.lic |
   


<span id="02dbf3ad"></span>
### 專案編譯


1. 將移動裝置連線至電腦，並在 Xcode 中設定為目標裝置。

2. 點選 **Product** \> **Run**，啟動編譯流程。


<span id="cc07540a"></span>
### 應用體驗

若編譯流程無錯誤完成，VideoOne 應用將安裝到已連線的移動裝置上，並自動跳轉至登入介面。使用郵箱登入應用後，即可開始探索應用內提供的不同場景和功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您使用的是免費 Apple 開發者賬號，可能需要調整移動裝置設定以允許來自非信任開發者的應用執行。大多數情況下，您可以進入 <strong>設定</strong> \> <strong>通用</strong> \> <strong>裝置管理</strong>，信任開發者證書。</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fbbafc47ec843529888b307d1af14f2~tplv-goo7wpa0wc-image.image) </span>

<span id="f5f5fc6f"></span>
## 程式碼解析

示例專案的目錄結構如下：

```Plain
. 
├── VideoOne                           # Entry point of the project 
└── Pods 
    ├── Podfile 
    └── Development Pods 
        ├── App                        # Entry point of the demo app 
        ├── AppConfig                  # App configurations 
        ├── LoginKit                   # Login          
        ├── ToolKit                    # Common tools  
        ├── InteractiveLive            # The interactive live streaming solution 
        │   ├── Common                 # Common components 
        │   └── Feature                # Features 
        │       ├── Controller 
        │       ├── Model 
        │       └── View 
        ├── RTCAPIExample               # The RTC API Example solution 
        │   ├── QuickStart            
        │   ├── VideoManager
        │   ├── AudioManager       
        │   └── ...                    # Many other RTC features       
        ├── MediaLive                   # The MediaLive solution 
        │   ├── Entry                   # Entrance
        │   ├── MediaLive.podspec
        │   ├── Pull                    # Live stream pulling
        │   ├── Push                    # Live stream pushing
        │   ├── Resources               # Multilingual copywriting
        │   ├── ScreenCapture           # Screen-sharing stream pushing
        │   ├── VELCommon               # Common tools
        │   └── VELSettings             # Configuration related to stream pushing and pulling
        └── VideoPlaybackEdit          # The video playback and editing solution     
            ├── FeedVideo              # Mid-form video 
            ├── LongVideo              # Long-form video 
            └── ShortVideo             # Short-form video 
            └── SingleFunction         # Code for separate functions 
                 ├── PlayList          # Video playlist 
# Screen capture protection
                 ├── SmartSubtitles    # Smart subtitling 
                 ├── VideoPlayback     # Other playback-related functions 
```
