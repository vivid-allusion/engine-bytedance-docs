---
title: "Short drama videos - Flutter integration"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-flutter-integration"
---

This document provides an overview of the BytePlus VideoOne integration solution for short drama videos on Flutter, and walks you through integrating the short drama demo step by step.

<span id="overview-of-integration-solutions"></span>
## Overview of integration solutions

BytePlus VideoOne provides an integration solution for short drama videos. The table below summarizes this solution.


|**Integration solution** |Integrating the short drama demo |
|---|---|
|**Description** |Built on short video components. Supports short drama\-specific features such as episode switching, seamless resumed playback when switching pages, and unlocking paid content for playback. |
|**Target client** |Clients who are developing a new app and are able to replace the business API layer. |
|**Required development** |You only need to switch the business API layer logic and convert the data structures. |
|**Time to market** |As short as one week |
|**Related links** |[VideoOneSolutions/Client/Flutter](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Flutter) |


<span id="integrating-the-short-drama-demo"></span>
## Integrating the short drama demo

<span id="step-1-download-the-source-code"></span>
### Step 1: Download the source code

Run the following command to download the source code to your local device:

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions.git
```


<span id="step-2-copy-the-code"></span>
### Step 2: Copy the code

Copy the following folders to your project root directory:

```Bash
# Short drama core code
lib/src/solutions/minidrama
# Static assets
assets/minidrama
```


<span id="step-3-configure-the-license"></span>
### Step 3: Configure the license


1. Download the license file and place it in the `assets/minidrama/licenses` directory:


```Bash
- assets/minidrama
    - licenses
        - ttsdk.lic
```



2. Configure the corresponding asset path in `pubspec.yaml`:


```YAML
 assets:
     # licenses
    - assets/minidrama/licenses/ttsdk.lic

    # other icon png
    - assets/minidrama
```



3. Open the `lib/src/solutions/minidrama/constants/common.dart` file and modify the `APP_ID` and `LICENSE_PATH` fields:


```Dart
const APP_ID = "your app id"; // Your BytePlus app ID
const LICENSE_PATH = 'assets/minidrama/licenses/ttsdk.lic'; // The license file path
```


<span id="step-4-configure-dependencies"></span>
### Step 4: Configure dependencies


1. Configure the required dependencies in `pubspec.yaml`:


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



2. Configure the Android dependencies. For details, refer to [Short drama videos - Android integration](https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-android-integration).

   a. Add the following repositories.

   * In `android/settings.gradle`, add the Volcengine Maven repository to the `pluginManagement.repositories` block:

   ```Groovy
   maven { url "https://artifact.bytedance.com/repository/Volcengine/" }
   ```
   

   * In `android/build.gradle`, add the BytePlus public Maven repository to the `allprojects.repositories` block:

   ```Groovy
   maven { url "https://artifact.byteplus.com/repository/public/" }
   ```
   

   b. In `android/app/build.gradle`, add the following dependency:

   ```Groovy
   dependencies {
       implementation "com.squareup.okhttp3:okhttp:4.2.1"
   }
   ```
   

   c. Add the obfuscation rules required by BytePlus VOD Player to your `proguard-rules.pro` file:

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
   

3. Configure the iOS dependencies. For details, refer to [Short drama videos - iOS integration](https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-ios-integration). Configure the sources in your `Podfile`:

   ```Ruby
   source 'https://github.com/volcengine/volcengine-specs.git'
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   


<span id="step-5-initialize-the-player-module"></span>
### Step 5: Initialize the player module

Initialize the player in `lib/src/settings/settings_controller.dart`:

```Dart
Future<void> loadSettings() async {
  _themeMode = await _settingsService.themeMode();

  // init byteplus_vod sdk
  await PlayerController.initTTSDK();

  // Important! Inform listeners a change has occurred.
  notifyListeners();
}
```


<span id="adapting-to-your-business-logic"></span>
## Adapting to your business logic

Follow the steps below to quickly adapt the short drama demo to your business logic:


1. Adapt the data layer to quickly integrate the core features of the short drama scene. You need to:

   1. Replace the business APIs: Your app needs to implement the APIs defined in `lib/src/solutions/minidrama/service`.

   2. Convert the data structures: Convert the data structures returned by your business AppServer into the data structures defined in the short drama demo, so that you can quickly reuse the existing business logic in the demo.

2. Adapt short drama\-specific features such as unlocking paid content for playback.


<span id="short-drama-demo-source-structure"></span>
### Short drama demo source structure

```Bash
├── android/                 # Android platform-specific code
│   └── app/                 # Gradle module configuration
│       └── build.gradle     # Android build configuration
├── ios/                     # iOS platform-specific code
│   ├── Runner.xcodeproj/    # Xcode project configuration
│   └── Runner/              # iOS app main body
│       └── Runner.entitlements # Entitlements configuration file
├── lib/
│   ├── src/
│   │   ├── settings/        # Settings module (current core component)
│   │   │   ├── settings_controller.dart # Business logic control
│   │   │   └── settings_service.dart    # Data persistence layer
│   │   ├── solutions/minidrama/ # Short drama entry
│   │   │   ├── constants/   # Constant configuration
│   │   │   ├── meta/        # Data layer
│   │   │   ├── pages/       # Short drama main pages
│   │   │   ├── service/     # Short drama API layer
│   │   │   ├── utils/       # Short drama utilities
│   │   │   ├── video_sdk/   # Player SDK
│   │   │   └── widgets/     # Short drama widgets
│   └── main.dart            # App entry point
├── assets/
│   ├── minidrama/
│   │   └── licenses/        # License files
│   ├── images/              # Image assets
│   └── lotties/             # Lottie animation assets
└── pubspec.yaml             # Dependency management core file
```


<span id="adapting-the-data-layer"></span>
### Adapting the data layer

<span id="data-structures"></span>
#### Data structures

To build the short drama business logic, the short drama demo layer defines the data structures `drama_meta` (short drama information), `video_meta` (episode information), and `comment_meta` (comments). You need to convert the data structures returned by your app server into these data structures. The details are described in the table below.


|Class |Field |Type |Required |Description |
|---|---|---|---|---|
|`drama_meta`<br><br>(short drama information) |`dramaId` |String |Required |Short drama ID. |
||`dramaTitle` |String |Required |Short drama name. |
||`dramaCoverUrl` |String |Required |Short drama cover URL. |
||`dramaPlayTimes` |int |Required |Playback count. |
||`dramaVideoOrientation` |int |Required |Video orientation.<br><br>\- `0`: portrait.<br><br>\- `1`: landscape. |
||`dramaLength` |int |Required |Total number of episodes. |
||`newRelease` |bool |Optional |Whether to display the New label. Defaults to `false`.<br><br>\- `true`: display.<br><br>\- `false`: hide. |
|`video_meta`<br><br>(episode information) |`vid` |String |Required |Video ID. |
||`name` |String |Optional |Video title. |
||`duration` |double |Required |Video duration, in seconds. |
||`coverUrl` |String |Required |Cover URL. |
||`playAuthToken` |String |Optional |The `PlayAuthToken` of the video data source. It can be issued by the AppServer using the BytePlus VOD Server SDK. |
||`subtitleAuthToken` |String |Optional |The token used to obtain subtitles for the video data source. It can be issued by the AppServer using the BytePlus VOD Server SDK. |
||`videoModel` |String |Optional |The `VideoModel` of the video data source. |
||`playTimes` |int |Optional |Playback count. |
||`caption` |String |Optional |Video caption. |
||`subtitle` |String |Optional |Video subtitle. |
||`like` |int |Optional |Number of likes on the video. |
||`comment` |int |Optional |Number of comments on the video. |
||`height` |int |Required |Video height. |
||`width` |int |Required |Video width. |
||`order` |int |Required |Video position in the episode list. |
||`uid` |int |Optional |Uploader user ID. |
||`vip` |bool |Required |Whether payment is required to unlock the episode. |
||`displayType` |int |Required |Display type of the short drama card on the For you page.<br><br>\- `0`: TEXT, without cover image.<br><br>\- `1`: COVER, with cover image. |
|`comment_meta`<br><br>(comments) |`content` |String |Optional |Comment content. |
||`name` |String |Optional |User name. |
||`uid` |int |Optional |User ID. |
||`like` |int |Optional |Number of likes. |
||`createTime` |String |Optional |Creation time. |
||`liked` |bool |Optional |Whether the comment is liked. |


<span id="replacing-the-apis"></span>
#### Replacing the APIs


1. In the `lib/src/solutions/minidrama/constants/api.dart` file, replace the paths of the corresponding APIs:


```Dart
// get feed if drama
const GET_DRAMA_FEED = "/videoone/drama/v1/getDramaFeed";

const GET_DRAMA_CHANNEL = '/videoone/drama/v1/getDramaChannel';
const GET_VIDEO_COMMENT = '/videoone/drama/v1/getVideoComments';

// get Recommend
const GET_DRAMA_LIST = "/videoone/drama/v1/getDramaList";
const UNLOCK_DRAMA  = "/videoone/drama/v1/getDramaDetail";
```



2. In the `lib/src/solutions/minidrama/service` directory, the current API calls are recorded. You can replace the values according to your own business.
