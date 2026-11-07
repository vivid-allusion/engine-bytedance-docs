---
title: "整合 Android 版 Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-TW"
---

本主題說明如何整合 Android 版 Player SDK。

## 系統需求

* Android 5.0 (API 21) 或更高版本。

* CPU 架構：armeabi\-v7a 或 arm64\-v8a

## 先決條件

您已建立 SDK 應用程式並取得 SDK 授權。如需詳細資訊，請參閱[取得 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。

> **說明**

> 如需各授權類型支援功能的資訊，請參閱[用戶端 SDK：SDK 概觀](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)。如需定價資訊，請參閱 [SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses)。

## 整合 SDK

您可以透過以下其中一種方式整合 SDK：

* 自動整合（建議）：使用 Gradle 自動下載 SDK 套件。

* 手動整合：手動下載 AAR 檔案並匯入專案。如需詳細指引，請[聯絡技術支援](https://console.byteplus.com/workorder/create)。

本節說明如何自動整合 SDK。

### 步驟 1：設定 Maven 儲存庫

若要整合 SDK，請設定多個 Maven 儲存庫，以確保正確下載所有必要相依性。請依照以下步驟操作：

1. 開啟根目錄中的 `build.gradle` 檔案。

2. 將主要儲存庫 URL 設為 `https://artifact.byteplus.com/repository/public`。以下範例程式碼顯示此設定：

   ```Groovy
   allprojects {
       repositories {
           google()
           mavenCentral()
           maven {
               url "https://artifact.byteplus.com/repository/public" // BytePlus 公開 Maven 儲存庫
           }
       }
   }
   ```

3. 為主要儲存庫中沒有的元件設定其他 Maven 儲存庫：

   * **對於 7.1 以下的 AGP 版本**：將此行新增至根目錄的 `build.gradle`：

      ```Groovy
      apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
      ```

   * **對於 AGP 7.1 及以上版本**：將 `https://ve-vos.volccdn.com/script/vevos-repo-base.gradle` 中的 Maven 設定複製到 `settings.gradle` 的 `dependencyResolutionManagement` 區塊中。

### 步驟 2：設定環境與相依性

1. 開啟 `app/build.gradle` 檔案並新增以下設定：

   * 在 `defaultConfig` 中設定應用程式使用的 CPU 架構。SDK 支援 armeabi\-v7a 和 arm64\-v8a。

   * 在 `dependencies` 中新增相依性。

   ```Groovy
   android {
      defaultConfig {
          ndk {
              // 將 SO (Shared Object) 程式庫架構設為支援 armeabi-v7a 或 arm64-v8a。
              abiFilters 'armeabi-v7a', 'arm64-v8a'
           }
      }
   }
   
   dependencies {
      // ...
      // 對於 1.49.100.2 或更新版本，新增此相依性以使用基本拉流功能。
      implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:x.x.x.x' 
   }
   ```

   * 對於 1.51.300.2 或更新版本，新增 `implementation 'com.bytedanceapi:ttsdk-ttbmf:x.x.x.x'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以使用超解析度 (SR) 和影片銳化功能。

   * 對於 1.49.100.2 或更新版本，將 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:x.x.x.x'` 替換為 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以使用進階授權支援的功能。

   * 對於 1.49.100.2 或更新版本，新增 `implementation 'com.bytedanceapi:ttsdk-ttquic:x.x.x.x'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以透過 QUIC 拉流。

   * 對於 1.49.100.2 或更新版本，新增 `implementation 'com.bytedanceapi:ttsdk-ttcmaf:x.x.x.x'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'`，以播放 CMAF 串流。

   > **說明**

   * > 將 `x.x.x.x` 替換為您要整合的 SDK 版本。建議使用最新版本。如需可用版本，請參閱 [Android 版 Player SDK 版本資訊](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)。

   * > 對於 1.48.200.2 版本：

      * > 若要使用基本拉流功能，請新增 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`。

      * > 若要透過 QUIC 拉流，請新增 `implementation 'com.bytedanceapi:ttsdk-ttquic:1.48.200.2'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`。

      * > 若要透過 RTM 拉流，請新增 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:1.48.200.2'`。

      * > 若要播放 CMAF 串流，請新增 `implementation 'com.bytedanceapi:ttsdk-ttcmaf:1.48.200.2'` 和 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`。

   * > 對於 1.48.100.103 或更早版本：

      * > 若要使用基本拉流功能，包括透過 QUIC 拉流和播放 CMAF 串流，請新增 `implementation 'com.bytedanceapi:ttsdk-ttlivepull:x.x.x.x'`。

      * > 若要透過 RTM 拉流，請新增 `implementation 'com.bytedanceapi:ttsdk-ttlivepull_rtc:x.x.x.x'`。

2. 按一下 **Sync Project with Gradle Files** 以同步 SDK。SDK 將自動下載並整合至專案。如果整合失敗，請檢查您與 Maven 儲存庫的網路連線。

## 設定權限

在 `AndroidManifest.xml` 檔案中宣告 Player SDK 所需的權限。

```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

## 新增授權

將依照[取得 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)取得的授權檔案複製到您的專案目錄。例如，將 `License2_test.lic` 檔案複製到 `assets` 目錄，如下列螢幕擷取畫面所示。請記下授權檔案的路徑，因為初始化 SDK 時會使用它。

![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0c295cb-file_path2.png)

## 實作程式碼混淆

將以下幾行新增至 `proguard-rules.pro` 檔案，以排除 SDK 相關類別的混淆。

```Plain
-keep class com.pandora.**{*;}
-keep class com.ss.**{*;}
-keep class com.bytedance.**{*;}
-keep class com.pandora.ttlicense2.**{*;}
-keep class com.bytertc.**{*;}
-keep class log.**{*;}
```

如果您正在整合 RTC SDK，還需要為 RTC SDK 設定混淆規則。如需詳細資訊，請參閱[混淆 Android 應用程式的程式碼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-78295)。
