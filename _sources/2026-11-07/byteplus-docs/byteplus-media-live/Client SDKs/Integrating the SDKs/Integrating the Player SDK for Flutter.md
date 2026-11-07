---
title: "Integrating the Player SDK for Flutter"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter"
---

This topic describes how to integrate the Player SDK for Flutter into your app.

<span id="c8bc54ac"></span>
## Development environment requirements


* Flutter version: Flutter stable channel 3.0.0 or later

* Dart version: Dart 2.17.0 or later

* System versions:

   * Physical devices running iOS 11.0 or later

   * Physical devices running Android 5.0 (minSdkVersion: 21) or later

* Development tool: Visual Studio Code or Android Studio (latest version recommended)


<span id="bcda95b5"></span>
## Prerequisites

You have created an SDK application and obtained the SDK license. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).

<span id="addbcbfe"></span>
## Integration steps

<span id="950f7a4d"></span>
### Step 1: Add dependencies


1. In the `pubspec.yaml` file, add the `byteplus_live` dependency as follows:

   ```YAML
   dependencies:
     flutter:
       sdk: flutter
     byteplus_live: x.x.x
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>x.x.x</code> with the specific SDK version. We recommend that you use the latest version. For more information about the version number, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-release-notes">Player SDK for Flutter release notes</a>.   </div>
   

2. Open a terminal window and run the command `cd` to navigate to your Flutter project directory. Run the command `flutter pub get` to get all required project dependencies and ensure successful compilation and execution.


<span id="0de5bfe2"></span>
### Step 2: Platform configuration

Configure the settings for Android and iOS.

<span id="22c08d7f"></span>
#### Android


1. Open the `AndroidManifest.xml` file in the `app` directory and declare the permissions required by the SDK.

   ```XML
   <!-- Camera -->
   <uses-permission android:name="android.permission.CAMERA" />
   <!-- Recording --> 
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   <!-- Network status -->
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   

2. Open the `proguard-rules.pro` file in the `app` directory and add the following obfuscation rules.

   ```XML
   -keep class com.pandora.**{*;}
   -keep class com.ss.**{*;} 
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.bytertc.**{*;}
   -keep class log.**{*;}
   ```
   


<span id="29b43fe9"></span>
#### iOS


1. Disable Bitcode in the app target of Xcode.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f0309bc1e2f428aa19208511b308682~tplv-goo7wpa0wc-image.image) </span>

   1. Click the **Build Settings** tab.

   2. In the **Build Options** section, set **Enable Bitcode** to **No**.

2. Open the `Podfile` file of your iOS project and add the following sources.

   ```YAML
   source 'https://github.com/cocoapods/Specs.git'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you use CocoaPods 1.11.0 or later. If your iOS project has not yet used CocoaPods, run the command <code>pod init && pod install</code> in the root directory of your iOS project to create the <code>Podfile</code> file.   </div>
   

3. Open a terminal window and run the command `cd` to navigate to your iOS project's directory. Then, run the command `pod install`.


<span id="8841c34f"></span>
### Step 3: Add the license file


1. Place the license file that you obtained into your Flutter project. The following example places the license file in the `assets` folder under the root directory of your project.

   ```YAML
   ├── assets
   │   └── live.lic
   ├── pubspec.yaml
   ```
   

2. In the `pubspec.yaml` file, add the path to the license file under `assets`.

   ```YAML
   assets:
     - assets/live.lic
   ```
   

3. When initializing the SDK, you must pass the path to the license file. For more information, see [Initializing the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter).


<span id="c2391fea"></span>
## Next steps

Initialize the Player SDK for Flutter. For more information, see [Initializing the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter).
