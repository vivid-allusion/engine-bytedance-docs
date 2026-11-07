---
title: "整合 Android Viewer SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/zheng-he-android-viewer-sdk-zh-TW"
---

要為您的 Android 應用程式新增互動式直播功能，例如觀看直播、發送評論以及與主播互動，您可以整合 Viewer SDK。本指南提供整個整合流程的逐步操作說明，涵蓋從設定 Gradle 配置到初始化 SDK 及加入直播間的所有步驟。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">為避免排查問題時出現複雜情況，請升級至 1.54.2 或更高版本。</div>


<span id="Prerequisites"></span>
## 先決條件


* 建議使用 Android Studio 4.0 或以上版本。

* 實體裝置需運行 Android 5.0（API 等級 21）及以上版本。

* CPU 架構：armeabi\-v7a 或 arm64\-v8a。

* 僅支援 AndroidX 函式庫。

* minSdkVersion：21（Android 5.0）及以上。

* targetSdkVersion：minSdkVersion 及以上，最高至 35（Android 15）。

* JDK 版本：1.8.0 及以上。

* 請聯繫 BytePlus Live 技術支援以取得以下項目：您的授權檔案（直播與 VOD）、用於申請授權的應用程式名稱，以及對應的 app ID。


<span id="Integrating the SDK"></span>
## 整合步驟

<span id="8a9e8a55"></span>
### Step 1: 設定 Gradle 配置


1. 開啟專案根目錄下的 `build.gradle` 檔案，並新增以下配置。

   ```Groovy
   buildscript { 
       repositories { 
           google() 
           mavenCentral() 
       } 
       dependencies { 
           // We recommend that you use version 3.6.3 or later.
           classpath 'com.android.tools.build:gradle:3.6.3' 
       } 
   } 
    
   allprojects { 
       repositories { 
           google() 
           mavenCentral() 
           jcenter() 
           maven {
               url "https://artifact.bytedance.com/repository/Volcengine/" // 公共 Maven 儲存庫的 URL
           }
           maven {
               url "https://artifact.byteplus.com/repository/public/" // BytePlus 公共儲存庫的 URL
   }
           maven {
               url "https://artifact.bytedance.com/repository/thrall_base/" // 串流儲存庫的 URL
               credentials {
                   username = 'veVOS' // Username to access the streaming repository.請勿更改此值
                   password = 'KUC9TpKrqbryrxHz' // Password to access the streaming repository.無需更改
               }
               authentication {
                   digest(BasicAuthentication)
               }
           }
       } 
   } 
   ```
   

2. 開啟專案 `app` 目錄下的 `build.gradle` 檔案，並新增以下配置。

   ```Groovy
   android { 
       defaultConfig { 
           minSdkVersion 21 
           ndk { 
               abiFilters "armeabi-v7a","arm64-v8a" 
           } 
       } 
    
    
      // Enable DataBinding
       dataBinding { 
           enabled = true 
       } 
   } 
    
   // Import dependencies
   dependencies { 
    
       // Import the Viewer SDK.您可以使用 implementation "com.bytedance.bdlive:bdlive-pull:1.65.0.globalLite" 來優化 SDK 封包大小。優化後的 SDK 封包不包含超低延遲直播功能。
       implementation "com.bytedance.bdlive:bdlive-pull:1.65.0.globalFull"
    
       // Import the Glide library.若您先前已將 Glide 函式庫匯入專案，請參閱 Glide 版本相容性章節以確保 Glide 版本相容性
       implementation "com.github.bumptech.glide:glide:4.15.1"
   } 
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">自 SDK 1.54.0 版本起，   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">匯入包含所有功能的 Viewer SDK 時，SDK 版本後綴已從<code>pull-global:VersionNumber.external</code>變更為<code>pull:VersionNumber.globalFull</code>。例如，使用<code>com.bytedance.bdlive:bdlive-pull-global:1.53.0.external</code>匯入包含所有功能的 Viewer SDK 1.53.0，並使用<code>com.bytedance.bdlive:bdlive-pull:1.54.0.globalFull</code>匯入包含所有功能的 Viewer SDK 1.54.0。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">匯入不包含超低延遲直播功能的 Viewer SDK 時，SDK 版本後綴已從<code>pull-global-remove-rtc:VersionNumber.external</code>變更為<code>pull:VersionNumber.globalLite</code>。例如，使用<code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external</code>匯入不包含超低延遲直播功能的 Viewer SDK 1.53.0，並使用<code>com.bytedance.bdlive:bdlive-pull:1.54.0.globalLite</code>匯入不包含超低延遲直播功能的 Viewer SDK 1.54.0。   </div>
   


<span id="aca3bab7"></span>
#### Glide 版本相容性

自 1.10.6 版本起，Android Viewer SDK 的圖像函式庫元件已遷移至 Glide。

由於 Glide API 不同版本間差異顯著，您必須確保版本相容性，以避免應用程式崩潰。所需步驟取決於您的專案所使用的 Glide 版本。


* Glide 版本大於或等於 4.9.0：無需任何操作。

* Glide 版本為 4.x，但低於 4.9.0：開啟專案 `app` 目錄下的 `build.gradle` 檔案，並新增以下配置。

   ```Java
   // Import the Viewer SDK
   implementation("com.bytedance.bdlive:bdlive-pull:x.x.x.globalFull"){
       {
           // Remove the default bdlive-glide-v4 library
           exclude group:"com.bytedance.bdlive",module:"bdlive-glide-v4"
       }
   }
   
   // Import the bdlive-glide-adapt-v4 library
   implementation "com.bytedance.bdlive:bdlive-glide-adapt-v4:1.1.5"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Viewer SDK 不支援 Glide 3.x。建議您將 Glide 升級至最新版本。升級操作簡單，升級後無需額外操作即可確保 Glide 版本相容性。   </div>
   

<span id="006c7b9c"></span>
### Step 2: 新增權限

開啟 `AndroidManifest.xml` 檔案（位於 `app/src/main` 目錄），並新增以下權限。

```XML
<!-- 存取本地儲存 --> 
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


<span id="Adding manifest permissions"></span>
### Step 3: 新增混淆規則

開啟 `proguard-rules.pro` 檔案（位於 `app` 目錄），並新增以下混淆規則。

```XML
-keep class com.pandora.**{*;}
-keep class com.ss.**{*;} 
-keep class com.bytedance.**{*;}
-keep class com.pandora.ttlicense2.**{*;}
-keep class com.bytertc.**{*;}
-keep class org.webrtc.**{*;}
-keep class log.**{*;}
```


<span id="Implementing code obfuscation"></span>
### Step 4: 匯入授權檔案

在 `app/src/main` 目錄下建立 `assets/lic` 目錄，並將直播授權檔案 `liveLicense.lic` 及 VOD 授權檔案 `vodLicense.lic` 放入 `assets/lic` 目錄。檔案結構如下。

```Plain
app
|-- src
    |-- main
        |-- java
        |-- assets
            |-- lic
                |--  liveLicense.lic
                |--  vodLicense.lic
```


<span id="660b1619"></span>
### Step 5: 初始化 BDLive SDK

當您的應用程式初始化時，請呼叫 `BDLiveEnv.init` 以初始化 BDLive SDK（Viewer SDK）。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">初始化期間不會收集使用者個人資訊。</div>


```Java
private void initBDLiveEnv() {
    String assetsLicenseUri = "assets:///lic/example.lic"; // Replace assets:///lic/example.lic with the URI of the VOD license
    String assetsLicenseUri2 = "assets:///lic/example.lic"; // Replace assets:///lic/example.lic with the URI of the live streaming license
    BDLiveEnv.init(new BDLiveConfig.Builder()
        .setApplicationContext(this)
        .setAppId("APP_ID") // Replace APP_ID with the app ID returned after the successful license application.請聯絡 BytePlus Live 技術支援以取得 app ID。
        .setAppName("APP_NAME") // Replace APP_NAME with the app name used to apply for the license.請聯絡 BytePlus Live 技術支援以取得 app 名稱。
        .setAppChannel("CHANNEL_NAME") // 將 CHANNEL_NAME 替換為 下載 app 的渠道名稱。
        .setAppVersion("APP_VERSION") // Replace APP_VERSION with the app version.有效的版本號需包含兩個或以上分隔符，例如 1.3.2。
        .setAppRegion("REGION") // Replace REGION with the region used to apply for the license.此值請始終設為 'singapore'。
        .setVodLicenseUri(assetsLicenseUri) // URI of the VOD license
        .setLiveLicenseUri(assetsLicenseUri2) // URI of the live streaming license
        .setUseSecureInfoCollect(true) // 是否啟用安全資訊收集模式。true：啟用該模式。不會收集使用者個人資訊。false：停用該模式。會收集使用者個人資訊。預設值：true
        .build());
}
```


<span id="Entering the live room"></span>
### Step 6: 加入與離開直播間

以下範例程式碼展示如何加入與離開功能完整的直播間。

```Java
long activityId = ACTIVITY_ID; // Replace ACTIVITY_ID with the activity ID of the live room.
String token = "TOKEN"; // Replace TOKEN with the authorization token required to join the live room.
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC; // The authentication mode of the live room.本範例採用公開模式。觀眾可在未登入直播間的情況下觀看直播、查看評論及執行其他操作。
boolean isPortrait = true;// Whether the live room is in portrait mode.此處以直式模式為例。
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
// Leave the live room.
TVULiveRoom.leaveLiveRoom(context);
```


<span id="a90cb94f"></span>
## 優化 SDK 套件大小

自 SDK 1.54.0 版本起，您可以依照以下步驟優化 SDK 套件大小：


1. 開啟 `app` 目錄下的 `build.gradle` 檔案，並在 `dependencies` 區塊找到 Viewer SDK 依賴項。

   ```Groovy
   com.bytedance.bdlive:bdlive-pull:1.65.0.globalFull
   ```
   

2. 將 `globalFull` 替換為 `globalLite`。

   ```Groovy
   com.bytedance.bdlive:bdlive-pull:1.65.0.globalLite
   ```
   


優化後的 SDK 套件將不包含超低延遲直播功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若 SDK 版本低於 1.54.0，可將 SDK 依賴項從<code>com.bytedance.bdlive:bdlive-pull-global:VersionNumber.external</code>更換為<code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:VersionNumber.external</code>，以優化 SDK 套件大小。例如，將<code>com.bytedance.bdlive:bdlive-pull-global:1.53.0.external</code>更換為<code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external</code>。</div>


<span id="de28cb2c"></span>
## 套件大小

此處的套件大小指的是整合 SDK 後 APK 檔案（安裝包）的增量大小，計算方式為整合 SDK 後的 APK 檔案大小減去整合前的 APK 檔案大小。

以下數據基於應用程式僅支援 arm64\-v8a CPU 架構。

若您的應用程式支援多種 CPU 架構，套件大小將相應增加。


|版本 |類型 |依賴項 |增量套件大小 |
|---|---|---|---|
|1.58.0 \- 1.65.0（依賴項以 1.65.0 為例） |觀眾端 SDK |`com.bytedance.bdlive:bdlive-pull:1.65.0.globalFull` |約 31.2 MB |
||經優化套件大小的觀眾端 SDK |`com.bytedance.bdlive:bdlive-pull:1.65.0.globalLite` |約 19.4 MB |
||直播推流 SDK + 觀眾端 SDK |* `com.bytedance.bdlive:bdlive-push:1.65.0.globalFull`<br><br>* `com.bytedance.bdlive:bdlive-pull:1.65.0.globalFull` |約 34 MB |
||經優化套件大小的直播推流 SDK + 經優化套件大小的觀眾端 SDK |* `com.bytedance.bdlive:bdlive-push:1.65.0.globalLite`<br><br>* `com.bytedance.bdlive:bdlive-pull:1.65.0.globalLite` |約 28 MB |


優化封包大小的直播串流 SDK 不包含螢幕分享功能，而優化封包大小的 Viewer SDK 不包含超低延遲直播功能。如需有關新增依賴項的更多資訊，請參閱[Step 1: 設定 Gradle 配置](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-android-viewer-sdk-zh-TW#8a9e8a55)的第 2 步。
