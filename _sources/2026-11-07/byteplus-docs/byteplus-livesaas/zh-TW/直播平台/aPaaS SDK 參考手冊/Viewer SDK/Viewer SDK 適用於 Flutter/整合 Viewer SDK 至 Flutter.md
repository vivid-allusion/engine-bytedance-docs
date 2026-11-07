---
title: "整合 Viewer SDK 至 Flutter"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/zheng-he-viewer-sdk-zhi-flutter-zh-TW"
---

為了在 Flutter 應用中啟用直播與隨選視訊（VOD）播放，本指南提供整合 Viewer SDK 的逐步操作說明。請依照以下步驟新增相依套件、配置 Android 與 iOS 的平台專屬設定，並加入所需的授權檔案，以準備專案進行開發。

<span id="60f21c26"></span>
## 系統需求


* Flutter 版本：Flutter stable channel 3.0.0 或以上

* Dart 版本：Dart 2.17.0 及以上

* 系統版本：

   * iOS 12.0 及以上

   * Android 5.0（minSdkVersion: 21）及以上

* 開發工具：Visual Studio Code 或 Android Studio（建議使用最新版）


<span id="494cbce1"></span>
## 先決條件

請聯繫 BytePlus Live 技術支援以取得您的直播與隨選視訊（VOD）授權檔案、申請授權時所用的應用名稱，以及產生的 app ID。

<span id="da55573e"></span>
## 專案結構

Viewer SDK for Flutter 的專案結構如下。

```Shell
├── CHANGELOG.md
├── LICENSE
├── README.md
├── analysis_options.yaml
├── android
├── example
├── ios
├── lib
├── pubspec.lock
└── pubspec.yaml
```


主要目錄及其對應說明如下。


|目錄 |說明 |必需 |
|---|---|---|
|lib |基於原生 SDK 所建構的 Flutter 插件層。 |是 |
|android |Android 原生程式碼。 |是 |
|ios |iOS 原生程式碼。 |是 |
|example |以 Flutter 建構的全功能直播間範例。 |否 |


<span id="f27e47f0"></span>
## 整合步驟

<span id="a40a1392"></span>
### Step 1: 新增相依套件

目前，Viewer SDK for Flutter 僅支援本地相依套件。


1. 點擊[這裡](https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/release/flutter/1.65.0/bdlive-flutter-viewer.zip)下載最新版 SDK 套件至本地環境並解壓縮。

2. 將 SDK 資料夾複製到您的專案目錄中。

3. 於`pubspec.yaml`檔案中，新增`bdlive_flutter_viewer`相依套件，如下所示。

   ```YAML
   dependencies:
       flutter:
           sdk: flutter
       # 將 <SDK_PATH> 替換為您專案中 SDK 的檔案路徑。
       bdlive_flutter_viewer: 
           path: <SDK_PATH>
   ```
   


<span id="c7fc6e43"></span>
### Step 2: 平台設定

配置 Android 與 iOS 的相關設定。

<span id="43fb4df8"></span>
#### Android


1. 開啟`build.gradle`檔案（位於`app`目錄），並新增以下設定。

   ```Groovy
   android {
       defaultConfig {
           minSdkVersion 21
           ndk {
           // Recommended CPU architectures to filter.
               abiFilters "arm64-v8a"
           }
       } 
    
      // Enable data binding.
       buildFeatures {
           dataBinding true
       }
   } 
   ```
   

2. 開啟`AndroidManifest.xml`檔案（位於`app`目錄），並新增以下權限。

   ```XML
   <!-- 存取本機儲存空間 -->
   <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
   <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
   
   <!-- 網路狀態 -->
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
   <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/>
   <uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
   
   <!-- 系統提示視窗 -->
   <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
   
   <!-- 行事曆 --> 
   <uses-permission android:name="android.permission.READ_CALENDAR"/> 
   <uses-permission android:name="android.permission.WRITE_CALENDAR"/>
   ```
   

3. 開啟`proguard-rules.pro`檔案（位於`app`目錄），並新增以下混淆規則。

   ```XML
   -keep class com.pandora.**{*;}
   -keep class com.ss.**{*;} 
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.bytertc.**{*;}
   -keep class org.webrtc.**{*;}
   -keep class log.**{*;}
   ```
   


<span id="08ea213e"></span>
#### iOS


1. 開啟終端機視窗，執行`cd`指令切換至您的 iOS 專案目錄。執行`pod install`指令以安裝相依套件。

2. 於 Xcode 的 app target，完成以下步驟：

   1. 開啟`info.plist`檔案，新增參數`SSAppID`，並將參數值設為您已核准授權申請的 app ID。

   2. 於`info.plist`檔案中，透過以下其中一種方式新增權限：

      * 點擊\*\*+**新增 ** **`NSPhotoLibraryAddUsageDescription`** ** 鍵（顯示為**Privacy \- Photo Library Additions Usage Description\*\*）與 `NSCalendarsUsageDescription` 鍵（顯示為**Privacy \- Calendars Usage Description**），選擇**String**作為**Type**，然後於**Value**輸入系統授權對話框中顯示的提示訊息。

      * 以原始碼模式開啟`info.plist`檔案，並新增以下鍵值與字串。您可自訂字串內容作為系統授權對話框中顯示的提示訊息。

         ```JavaScript
         <!-- Write access to photo library -->
         <key>NSPhotoLibraryAddUsageDescription</key> 
         <string>The app needs permission to save images to your photo library. 
         <!-- 行事曆寫入權限 -->
         <key>NSCalendarsUsageDescription</key>
         <string>Used to remind viewers before live stream starts</string>
         ```
         

3. （選用）若需讓應用於背景執行時持續播放音訊，或需使用子母畫面（PiP）功能，請完成以下步驟：

   1. 於**Signing & Capabilities**分頁下點擊\*\*+ Capability\*\*，並雙擊新增**Background Modes**。

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acd720b361e33d38cd9d34fa8778bc0c.png) </span>

   2. 於**Background Modes**區塊中，勾選**Audio, AirPlay, and Picture in Picture**核取方塊。

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7fd45366e83df22b9d668b0df54fb16.png) </span>

4. （選用）若您的 iOS 專案啟用了 Bitcode，則需將 Bitcode 關閉。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b66610c96ad455dbc270fdfb55f28a6~tplv-goo7wpa0wc-image.image) </span>

   1. 點擊**Build Settings**分頁。

   2. 於**Build Options**區塊中，將**Enable Bitcode**設為**No**。

5. 在全螢幕模式下播放直播、預覽或回放時，配置所支援的螢幕方向。

   1. 點擊**一般**標籤。

   2. 在**部署資訊**區段，為**iPhone 螢幕方向**和**iPad 螢幕方向**選取**直向**及**橫向（右）** 核取方塊。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d945974cbdbe4e50b94b1d69391ea5b0~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">要讓螢幕在全螢幕模式下於橫向間自動旋轉，必須符合以下條件：   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">觀眾裝置的直向鎖定已關閉。關於如何關閉直向鎖定，請參閱 <a href="https://support.apple.com/en-us/118226">Apple 官方文件</a>。   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">在<strong>橫向（左）</strong>及<strong>橫向（右）</strong>核取方塊皆於<strong>部署資訊</strong>區段中選取。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">為避免觀眾在點擊全螢幕按鈕時全螢幕動畫顯示異常，請務必選取<strong>橫向（右）</strong>核取方塊。   </div>
   


<span id="c6ec173e"></span>
### 步驟 3：新增授權檔案


1. 將您取得的直播授權檔案和 VOD 授權檔案放入您的 Flutter 專案中。以下範例將檔案放在專案根目錄下的`assets`資料夾中。

   ```YAML
   ├── assets
   │   ├── live.lic
   │   └── vod.lic
   ├── pubspec.yaml
   ```
   

2. 在`pubspec.yaml`檔案中，於`assets`下新增授權檔案的路徑。

   ```YAML
    assets:
     - assets/live.lic
     - assets/vod.lic
   ```
   

3. 初始化 SDK 時，您必須傳入授權檔案的路徑。如需更多資訊，請參閱[初始化 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/gong-neng-shi-xian-zh-TW#a4ab4a00)。


<span id="77ab57b8"></span>
## 套件大小


* iOS

   對於 iOS，套件大小指的是：

   * 整合後壓縮 IPA 檔案大小的增加量。這是整合 SDK 前後檔案大小的差異。

   * 整合後未壓縮 IPA 檔案大小的增加量。這是整合 SDK 前後檔案大小的差異。

      壓縮 IPA 檔案大小代表您的應用程式下載大小，而未壓縮 IPA 檔案大小則對應於裝置上安裝後的應用程式大小。

      裝置上實際的未壓縮 IPA 檔案大小會小於下表所列，因為安裝時僅保留適用於當前裝置的資源。

   
   |版本 |壓縮 IPA 檔案增加量 |未壓縮 IPA 檔案增加量 |
   |---|---|---|
   |1.58.0\-1 |約 30.8 MB |約 64.7 MB |
   

* Android

   對於 Android，這是指整合 SDK 後 APK 檔案大小的增加量。這是整合前後 APK 大小的差異。

   以下數據僅基於應用程式僅支援 arm64\-v8a CPU 架構。

   若您的應用程式支援多種 CPU 架構，套件大小將相應增加。

   
   |版本 |套件增加量 |
   |---|---|
   |1.58.0\-1 |約 19.4 MB |
   


<span id="fbb6c796"></span>
## 後續步驟

如需更多有關如何在 Flutter 中使用 Viewer SDK（例如進入和離開直播間）的資訊，請參閱[功能實現](https://docs.byteplus.com/docs/byteplus-livesaas/gong-neng-shi-xian-zh-TW)。
