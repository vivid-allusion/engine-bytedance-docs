---
title: "Integrating the Viewer SDK for Flutter"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-flutter"
---

To enable live streaming and VOD playback in your Flutter app, this guide provides step\-by\-step instructions for integrating the Viewer SDK. Follow these steps to add dependencies, configure platform\-specific settings for Android and iOS, and add the required license files to prepare your project for development.

<span id="60f21c26"></span>
## System requirements


* Flutter version: Flutter stable channel 3.0.0 or later

* Dart version: Dart 2.17.0 and above

* System versions:

   * iOS 12.0 and above

   * Android 5.0 (minSdkVersion: 21) and above

* Development tool: Visual Studio Code or Android Studio (recommended to use the latest version)


<span id="494cbce1"></span>
## Prerequisites

Contact BytePlus Live technical support to obtain your live streaming and Video on Demand (VOD) license files, the app name used for the license application, and the resulting app ID.

<span id="da55573e"></span>
## Project structure

The project structure of the Viewer SDK for Flutter is as follows.

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


The key directories and their corresponding descriptions are as follows.


|Directory |Description |Required |
|---|---|---|
|lib |A Flutter plugin layer built on the native SDK. |Yes |
|android |Native code for Android. |Yes |
|ios |Native code for iOS. |Yes |
|example |A full\-featured live room demo built with Flutter. |No |


<span id="f27e47f0"></span>
## Integration steps

<span id="a40a1392"></span>
### Step 1: Add dependencies

Currently, the Viewer SDK for Flutter only supports local dependencies.


1. Click [here](https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/release/flutter/1.65.0/bdlive-flutter-viewer.zip) to download the latest version of the SDK package to your local environment and unzip it.

2. Copy the SDK folder to your project directory.

3. In the `pubspec.yaml` file, add the `bdlive_flutter_viewer` dependency as follows.

   ```YAML
   dependencies:
       flutter:
           sdk: flutter
       # Replace <SDK_PATH> with the file path of the SDK in your project.
       bdlive_flutter_viewer: 
           path: <SDK_PATH>
   ```
   


<span id="c7fc6e43"></span>
### Step 2: Platform configuration

Configure the settings for Android and iOS.

<span id="43fb4df8"></span>
#### Android


1. Open the `build.gradle` file in the `app` directory and add the following configurations.

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
   

2. Open the `AndroidManifest.xml` file in the `app` directory and add the following permissions.

   ```XML
   <!-- Access local storage -->
   <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
   <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
   
   <!-- Network status -->
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
   <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/>
   <uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
   
   <!-- System alert window -->
   <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
   
   <!-- Calendar --> 
   <uses-permission android:name="android.permission.READ_CALENDAR"/> 
   <uses-permission android:name="android.permission.WRITE_CALENDAR"/>
   ```
   

3. Open the `proguard-rules.pro` file in the `app` directory and add the following obfuscation rules.

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


1. Open a terminal window and run the command `cd` to navigate to your iOS project's directory. Run the command `pod install` to install the dependencies.

2. In the app target of Xcode, complete the following steps:

   1. Open the `info.plist` file, add the parameter `SSAppID`, and set the parameter value to the app ID from your approved license application.

   2. In the `info.plist` file, add permissions in one of the following ways:

      * Click  **+**  to add the `NSPhotoLibraryAddUsageDescription` key (displayed as **Privacy \- Photo Library Additions Usage Description**) and the `NSCalendarsUsageDescription` key (displayed as **Privacy \- Calendars Usage Description**), select **String** as **Type**, and then enter the prompt message displayed in the system authorization dialog box as **Value**.

      * Open the `info.plist` file in source code mode and add the following keys and strings. You can customize the value of the string as the prompt message displayed in the system authorization dialog box.

         ```JavaScript
         <!-- Write access to photo library -->
         <key>NSPhotoLibraryAddUsageDescription</key> 
         <string>The app needs permission to save images to your photo library. 
         <!-- Write access to calendar -->
         <key>NSCalendarsUsageDescription</key>
         <string>Used to remind viewers before live stream starts</string>
         ```
         

3. (Optional) If you need the app to continue playing audio when running in the background or need to use the picture\-in\-picture (PiP) feature, complete the following steps:

   1. Click  **+ Capability** under the **Signing & Capabilities** tab, and double\-click to add **Background Modes**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acd720b361e33d38cd9d34fa8778bc0c.png) </span>

   2. In the **Background Modes** section, select the **Audio, AirPlay, and Picture in Picture** checkbox.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7fd45366e83df22b9d668b0df54fb16.png) </span>

4. (Optional) If your iOS project is using Bitcode, you need to disable Bitcode.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b66610c96ad455dbc270fdfb55f28a6~tplv-goo7wpa0wc-image.image) </span>

   1. Click the **Build Settings** tab.

   2. In the **Build Options** section, set **Enable Bitcode** to **No**.

5. Configure the screen orientation supported when playing live streams, previews, or playbacks in full\-screen mode.

   1. Click the **General** tab.

   2. In the **Deployment Info** section, select the **Portrait** and **Landscape Right** checkboxes for **iPhone Orientation** and **iPad Orientation**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d945974cbdbe4e50b94b1d69391ea5b0~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the screen to auto\-rotate between landscape orientations in full\-screen mode, the following conditions must be met:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The portrait orientation lock of the viewer's device is turned off. For how to turn off the portrait orientation lock, see the <a href="https://support.apple.com/en-us/118226">official Apple documentation</a>.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Both <strong>Landscape Left</strong> and <strong>Landscape Right</strong> checkboxes are selected in the <strong>Deployment Info</strong> section.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To prevent display issues with the full\-screen animation when viewers tap the full\-screen button, make sure to select the <strong>Landscape Right</strong> checkbox.   </div>
   


<span id="c6ec173e"></span>
### Step 3: Add license files


1. Place the live streaming license file and VOD license file that you obtained into your Flutter project. The following example places the files in the `assets` folder under the root directory of your project.

   ```YAML
   ├── assets
   │   ├── live.lic
   │   └── vod.lic
   ├── pubspec.yaml
   ```
   

2. In the `pubspec.yaml` file, add the paths to the license files under `assets`.

   ```YAML
    assets:
     - assets/live.lic
     - assets/vod.lic
   ```
   

3. When initializing the SDK, you must pass the paths to the license files. For more information, see [Initializing the SDK](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#a4ab4a00).


<span id="77ab57b8"></span>
## Package size


* iOS

   For iOS, the package size refers to:

   * The increase in the compressed IPA file size after integration. This is the difference between the file size before and after integrating the SDK.

   * The increase in the uncompressed IPA file size after integration. This is the difference between the file size before and after integrating the SDK.

      The compressed IPA file size represents the download size of your app, while the uncompressed IPA file size corresponds to the size of the installed app on the device.

      The actual uncompressed IPA file size on devices is smaller than the size listed in the following table, as only the resources applicable to the current device are kept during installation.

   
   |Version |Incremental compressed IPA file size |Incremental uncompressed IPA file size |
   |---|---|---|
   |1.58.0\-1 |About 30.8 MB |About 64.7 MB |
   

* Android

   For Android, this refers to the increase in the APK file size after integrating the SDK. It is the difference between the APK size before and after integration.

   The following data is based on the app supporting only the arm64\-v8a CPU architecture.

   If your app supports multiple CPU architectures, the package size will increase accordingly.

   
   |Version |Incremental package size |
   |---|---|
   |1.58.0\-1 |About 19.4 MB |
   


<span id="fbb6c796"></span>
## Next steps

For more information on how to use the Viewer SDK for Flutter, such as joining and leaving a live room, see [Feature implementation](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation).
