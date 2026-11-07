---
title: "在 Android 上運行 VeLiveQuickStartDemo"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android-zh-TW"
---

為了探索 BytePlus MediaLive SDK 的功能，您可以在 Android 裝置上運行 VeLiveQuickStartDemo。按照本主題中的步驟操作，將協助您成功編譯並啟動此示範程式，該程式展示了基本的推流與拉流、進階功能如自適應碼率，以及如連麥等互動功能。

VeLiveQuickStartDemo 包含三種類型的功能：


* 基本功能，包括推流與拉流。

* 進階功能，包括：

   * 自適應碼率

   * 推送外部音訊與視訊來源

   * H.265 硬體編碼

   * 子母畫面（PiP）

* 互動直播功能，包括與觀眾連麥及主播 PK 對戰。


<span id="e42b27e5"></span>
## 系統需求


* Android 5.0（SDK API Level 21）或更高版本

* Android Studio 4.0 或更高版本

* 一台運行 Android 5.0 或更高版本的實體 Android 裝置

* 請確保 CPU 架構為 armeabi\-v7a 或 arm64\-v8a


<span id="d1ed29bd"></span>
## 準備事項


* 註冊 BytePlus 帳號。詳細操作請參考 [註冊並驗證 BytePlus 帳號](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account)。

* 啟用 BytePlus MediaLive 服務，並於控制台新增推流與拉流的網域名稱。詳細操作請參考 [開始使用 BytePlus MediaLive](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-TW)。

* 若要體驗互動直播功能，還需啟用 BytePlus RTC 服務。詳細操作請參考 [啟用 RTC 服務](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。


<span id="5ba9ae47"></span>
## 準備工作

在運行示範程式前，請取得 SDK 授權、App ID 及 Token 資訊。

<span id="0706aa76"></span>
### **下載 MediaLive 授權**

請依照 [SDK 管理](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) 中的指引建立 SDK 應用，並下載對應的 SDK 授權。請記下 App ID 及套件名稱以便後續使用。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab6a8e0a0518458bbc61967cbc9e88cb~tplv-goo7wpa0wc-image.image) </span>

<span id="9ae537a8"></span>
### **取得 RTC App ID 及 App Key**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果你不打算測試互動直播功能，可以略過本節。</div>



1. 登入 [BytePlus RTC 控制台。](https://console.byteplus.com/rtc/workplaceRTC)

2. 於左側導覽欄點擊 **應用管理**。

3. 點擊 **建立應用**，並於彈出視窗中輸入您的應用名稱。**所屬專案** 欄位請保持預設值。

4. 點擊 **確定** 以儲存設定。

5. 於應用列表中找到您的應用，並記下 App ID 及 App Key。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b565075eda70420d85d70cc7cc950223~tplv-goo7wpa0wc-image.image) </span>


<span id="b01ced66"></span>
## 運行示範程式

本節將介紹設置與運行示範程式的詳細步驟。

<span id="30f72781"></span>
### 下載原始碼


1. 前往 GitHub 並複製 [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git) 儲存庫。

2. 示範程式的目錄結構如下：

   ```Plain
   Android/VeLiveQuickStartDemo/app/src/main/java/com/ttsdk/quickstart
   ├── app // Entry point of the demo app
   ├── features // Features
   │   ├── basic // Basic features
   │   │   ├── PullStreamActivity.java // Stream pulling
   │   │   └── PushCameraActivity.java // Video capture and stream pushing
   │   ├── advanced // Advanced features
   │   │   ├── PictureInPictureActivity.java // PiP
   │   │   ├── PushAutoBitrateActivity.java // Adaptive bitrate
   │   │   ├── PushBeautyActivity.java // Beauty AR and special effects
   │   │   ├── PushCustomActivity.java // Pushing external audio and video sources
   │   │   ├── PushH265CodecActivity.java // H.265 hardware encoding
   │   │   └── PullRTMActivity.java // Pulling an RTM stream
   │   └── interact // Interactive live features
   │       ├── link // Co-hosting with audience members
   │       ├── manager // Common host and audience activities
   │       └── pk // Host PK battle
   └── helper // Utilities, such as SDK initialization and external video capture
   ```
   


<span id="743d56e6"></span>
### 整合 SDK 授權


1. 請將您下載的 MediaLive SDK 授權重新命名為 `ttsdk.lic`。

2. 將 `Android/VeLiveQuickStartDemo/app/src/main/assets/` 目錄下原有的 `ttsdk.lic` 檔案替換為您自己的 SDK 授權。


<span id="e7a73684"></span>
### Gradle 同步


1. 於 Android Studio 中開啟 `Android/VeLiveQuickStartDemo`。

2. 點擊 **Sync Project with Gradle Files** 以同步專案與 Gradle 檔案。


<span id="77e37fbf"></span>
### 配置推流與拉流


1. 於 Android Studio 中，前往 `app/src/main/java/com.ttsdk.quickstart/helper` 並開啟 `VeLiveSDKHelper.java` 檔案。

2. 完成以下配置。

   ```Java
   // app ID
   public static String TTSDK_APP_ID = "536123";
   
   // 授權檔案名稱。若你更換授權檔案，需在此修改檔案名稱。為快速驗證 SDK，可替換原始授權檔案（ttsdk.lic）的內容。
   public static String TTSDK_LICENSE_NAME = "ttsdk.lic";
   
   // 配置 AccessKey ID 與 AccessKey secret，用於 API 請求驗證。
   public static String ACCESS_KEY_ID = "";
   public static String SECRET_ACCESS_KEY = "";
   
   // domain name space
   public static String LIVE_VHOST = "push.example.com";
       
   /*
   * 推流與拉流地址範例：https://{DomainName}/{AppName}/{StreamName}.flv
   * The AppName 用於推流與拉流地址，支援大小寫字母、數字、底線 (_)、連字號 (-)，最大長度為 30 字元。例如：live
   */
   public static String LIVE_APP_NAME = "live";
   
   // 配置推流域名
   public static String LIVE_PUSH_DOMAIN = "push.example.com";
   
   // 配置拉流域名
   public static String LIVE_PULL_DOMAIN = "pull.example.com";
   ```
   


<span id="5609c16c"></span>
### 配置連麥與主播 PK 對戰


1. 於 Android Studio 中，開啟 `app/src/main/java/com.ttsdk.quickstart/helper/VeLiveSDKHelper.java` 檔案。

2. 輸入 RTC App ID 及 App Key。

   ```Java
   // The RTC app ID
   public static String RTC_APPID ="";   
   // The RTC app key
   public static String RTC_APPKEY ="";    
   ```
   


<span id="3c9d8600"></span>
### 配置套件名稱


1. 於 Android Studio 中，開啟 `app/build.gradle` 檔案。

2. 請將 `applicationId` 設為您於 [下載 MediaLive 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android#0706aa76) 階段建立 SDK 應用時所使用的套件名稱。


<span id="67945fc7"></span>
### 編譯示範程式


1. 將您於 [準備事項](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android#d1ed29bd) 階段準備的實體 Android 裝置連接至電腦，並於 Android Studio 中設為目標裝置。

2. 點擊 **Run** 以啟動編譯流程。


若編譯流程無任何錯誤完成，示範應用程式將會安裝到已連接的行動裝置上。
