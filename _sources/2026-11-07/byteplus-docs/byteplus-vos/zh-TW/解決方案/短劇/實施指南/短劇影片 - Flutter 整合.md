---
title: "短劇影片 - Flutter 整合"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-flutter-integration-zh-TW"
---

本文提供 BytePlus VideoOne Flutter 端整合短劇場景的方案概覽，並為您詳細介紹如何快速整合短劇 Demo。

<span id="整合方案概覽"></span>
## 整合方案概覽

BytePlus VideoOne 針對短劇場景提供整合方案。下表列出該解決方案的詳細資訊。


|**整合方案** |整合短劇 Demo |
|---|---|
|**方案說明** |基於短影片場景控制項，支援劇集切換、切換頁面無縫續播、付費內容解鎖播放等短劇場景特色功能。 |
|**適用客戶** |適用於開發新 App、可切換業務介面層邏輯的客戶。 |
|**開發工作** |僅需切換業務介面層邏輯和轉換資料結構。 |
|**上線時間** |最快一週上線 |
|**相關連結** |[VideoOneSolutions/Client/Flutter](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Flutter) |


<span id="整合短劇-demo"></span>
## 整合短劇 Demo

<span id="步驟-1：下載原始碼"></span>
### 步驟 1：下載原始碼

執行以下命令將原始碼下載至本機：

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions.git
```


<span id="步驟-2：拷貝程式碼"></span>
### 步驟 2：拷貝程式碼

將以下資料夾拷貝至您的專案根目錄下：

```Bash
# 短劇核心程式碼
lib/src/solutions/minidrama
# 靜態資源
assets/minidrama
```


<span id="步驟-3：設定憑證"></span>
### 步驟 3：設定憑證


1. 下載憑證，放在 `assets/minidrama/licenses` 目錄下：


```Bash
- assets/minidrama
    - licenses
        - ttsdk.lic
```



2. 在 `pubspec.yaml` 下設定對應的靜態資源路徑：


```YAML
 assets:
     # licenses
    - assets/minidrama/licenses/ttsdk.lic

    # other icon png
    - assets/minidrama
```



3. 開啟 `lib/src/solutions/minidrama/constants/common.dart` 檔案，修改 `APP_ID` 與 `LICENSE_PATH` 欄位：


```Dart
const APP_ID = "your app id"; // BytePlus 對應 app id
const LICENSE_PATH = 'assets/minidrama/licenses/ttsdk.lic'; // 對應憑證路徑
```


<span id="步驟-4：設定相依項"></span>
### 步驟 4：設定相依項


1. 在 `pubspec.yaml` 下設定對應的相依模組：


```YAML
dependencies:
  android_id: ^0.4.0
  byteplus_vod: ^1.44.2-1
  collection: ^1.18.0
  connectivity_plus: ^6.1.0
  crypto: ^3.0.6
  device_info_plus: ^11.1.1
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  flutter_screenutil: ^5.9.3
  fluttertoast: ^8.2.8
  http: ^1.2.2
  logger: ^2.5.0
  shared_preferences: ^2.3.3
  wakelock_plus: ^1.2.8
  carousel_slider: ^5.0.0
  lottie: ^3.2.0
  intl: ^0.20.2
  loader_overlay: ^4.0.4+1
  visibility_detector: ^0.4.0+2
  path_provider: ^2.1.5

byteplus_vod:
  sub_spec: premium
```



2. 設定 Android 相關相依項。詳情請參考[短劇影片 - Android 整合](https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-android-integration-zh-TW)。

   a. 增加以下倉庫設定。

   * 在 `android/settings.gradle` 檔案的 `pluginManagement.repositories` 中增加 Volcengine Maven 倉庫：

   ```Groovy
   maven { url "https://artifact.bytedance.com/repository/Volcengine/" }
   ```
   

   * 在 `android/build.gradle` 檔案的 `allprojects.repositories` 中增加 BytePlus 公共 Maven 倉庫：

   ```Groovy
   maven { url "https://artifact.byteplus.com/repository/public/" }
   ```
   

   b. 在 `android/app/build.gradle` 檔案中新增以下相依項：

   ```Groovy
   dependencies {
       implementation "com.squareup.okhttp3:okhttp:4.2.1"
   }
   ```
   

   c. 在專案的 `proguard-rules.pro` 檔案中新增 BytePlus VOD Player 所需的混淆規則：

   ```Bash
   -keep class com.ss.ttm.** {*;}
   -keep class com.ss.ttvideoengine.** {*;}
   -keep class com.ss.mediakit.** {*;}
   -keep class com.ss.texturerender.** {*;}
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.pandora.common.applog.**{*;}
   -keep class com.pandora.vod.VodSDK {*;}
   -keep class com.bytertc.volcbaselog.VolcBaseLogConfig{*;}
   -keep class com.bytertc.volcbaselog.VolcBaseLogNative{*;}
   ```
   

3. 設定 iOS 相關相依項。詳情請參考[短劇影片 - iOS 整合](https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-ios-integration-zh-TW)。在 `Podfile` 檔案中設定對應的來源：

   ```Ruby
   source 'https://github.com/volcengine/volcengine-specs.git'
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   


<span id="步驟-5：初始化播放器模組"></span>
### 步驟 5：初始化播放器模組

在 `lib/src/settings/settings_controller.dart` 中初始化 player：

```Dart
Future<void> loadSettings() async {
  _themeMode = await _settingsService.themeMode();

  // init byteplus_vod sdk
  await PlayerController.initTTSDK();

  // Important! Inform listeners a change has occurred.
  notifyListeners();
}
```


<span id="適配業務邏輯"></span>
## 適配業務邏輯

參考以下步驟快速將短劇 Demo 與您的業務邏輯進行適配：


1. 資料層適配，以快速接入短劇場景的核心功能。您需要：

   1. 替換業務介面：App 需要實作 `lib/src/solutions/minidrama/service` 中定義的 API。

   2. 轉換資料結構：App 將業務 AppServer 傳回的資料結構轉換成短劇 Demo 中定義的資料結構，以便快速複用 Demo 中的現有業務邏輯。

2. 適配付費內容解鎖播放等短劇場景特色功能。


<span id="短劇-demo-原始碼結構說明"></span>
### 短劇 Demo 原始碼結構說明

```Bash
├── android/                 # Android 平台特定程式碼
│   └── app/                 # Gradle 模組設定
│       └── build.gradle     # Android 建置設定
├── ios/                     # iOS 平台特定程式碼
│   ├── Runner.xcodeproj/    # Xcode 專案設定
│   └── Runner/              # iOS 應用主體
│       └── Runner.entitlements # 權限設定檔
├── lib/
│   ├── src/
│   │   ├── settings/        # 設定模組（當前核心元件）
│   │   │   ├── settings_controller.dart # 業務邏輯控制
│   │   │   └── settings_service.dart    # 資料持久層
│   │   ├── solutions/minidrama/ # 短劇專案入口
│   │   │   ├── constants/   # 常數設定項
│   │   │   ├── meta/        # 資料層
│   │   │   ├── pages/       # 短劇主頁面
│   │   │   ├── service/     # 短劇介面層
│   │   │   ├── utils/       # 短劇工具類
│   │   │   ├── video_sdk/   # 播放器 SDK
│   │   │   └── widgets/     # 短劇元件
│   └── main.dart            # 應用入口
├── assets/
│   ├── minidrama/
│   │   └── licenses/        # 憑證檔案
│   ├── images/              # 圖片資源
│   └── lotties/             # Lottie 動畫資源
└── pubspec.yaml             # 相依管理核心檔案
```


<span id="資料層適配"></span>
### 資料層適配

<span id="資料結構介紹"></span>
#### 資料結構介紹

為建構短劇業務邏輯，短劇 Demo 層定義了 `drama_meta`（短劇資訊）、`video_meta`（影片資訊）、`comment_meta`（評論）資料結構。您需要將自己的應用伺服器端傳回的資料結構轉換為上述資料結構。資料結構具體說明如下表所示。


|類 |欄位 |類型 |是否必須 |描述 |
|---|---|---|---|---|
|`drama_meta`<br><br>（短劇資訊） |`dramaId` |String |必需 |短劇 ID。 |
||`dramaTitle` |String |必需 |短劇名稱。 |
||`dramaCoverUrl` |String |必需 |短劇封面 URL。 |
||`dramaPlayTimes` |int |必需 |播放次數。 |
||`dramaVideoOrientation` |int |必需 |影片方向。<br><br>\- `0`：直式。<br><br>\- `1`：橫式。 |
||`dramaLength` |int |必需 |短劇總集數。 |
||`newRelease` |bool |可選 |是否展示 New 圖示，預設 `false`。<br><br>\- `true`：展示。<br><br>\- `false`：隱藏。 |
|`video_meta`<br><br>（單集影片資訊） |`vid` |String |必需 |影片 ID。 |
||`name` |String |可選 |影片標題。 |
||`duration` |double |必需 |影片時長（單位：秒）。 |
||`coverUrl` |String |必需 |封面地址。 |
||`playAuthToken` |String |可選 |影片資料源的 `PlayAuthToken`。AppServer 可使用 BytePlus VOD Server SDK 簽發。 |
||`subtitleAuthToken` |String |可選 |影片資料源取得字幕的 Token。AppServer 可使用 BytePlus VOD Server SDK 簽發。 |
||`videoModel` |String |可選 |影片資料源的 `VideoModel`。 |
||`playTimes` |int |可選 |播放次數。 |
||`caption` |String |可選 |影片標題文案。 |
||`subtitle` |String |可選 |影片副標題。 |
||`like` |int |可選 |影片喜歡次數。 |
||`comment` |int |可選 |影片評論次數。 |
||`height` |int |必需 |影片高度。 |
||`width` |int |必需 |影片寬度。 |
||`order` |int |必需 |影片在劇集中的次序。 |
||`uid` |int |可選 |上傳者使用者 ID。 |
||`vip` |bool |必需 |是否需要付費解鎖。 |
||`displayType` |int |必需 |在 For you 頁的短劇卡片展示類型。<br><br>\- `0`：TEXT，不帶封面圖。<br><br>\- `1`：COVER，帶封面圖。 |
|`comment_meta`<br><br>（評論） |`content` |String |可選 |評論內容。 |
||`name` |String |可選 |使用者名稱。 |
||`uid` |int |可選 |使用者 ID。 |
||`like` |int |可選 |按讚數量。 |
||`createTime` |String |可選 |建立時間。 |
||`liked` |bool |可選 |是否按讚。 |


<span id="介面替換"></span>
#### 介面替換


1. 在 `lib/src/solutions/minidrama/constants/api.dart` 檔案下，替換對應介面的路徑：


```Dart
// get feed if drama
const GET_DRAMA_FEED = "/videoone/drama/v1/getDramaFeed";

const GET_DRAMA_CHANNEL = '/videoone/drama/v1/getDramaChannel';
const GET_VIDEO_COMMENT = '/videoone/drama/v1/getVideoComments';

// get Recommend
const GET_DRAMA_LIST = "/videoone/drama/v1/getDramaList";
const UNLOCK_DRAMA  = "/videoone/drama/v1/getDramaDetail";
```



2. `lib/src/solutions/minidrama/service` 目錄下記錄了當前介面的呼叫，您可根據自己的業務進行取值替換。
