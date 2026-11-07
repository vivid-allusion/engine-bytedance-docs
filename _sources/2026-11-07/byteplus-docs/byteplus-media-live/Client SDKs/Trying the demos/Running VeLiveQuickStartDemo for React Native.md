---
title: "Running VeLiveQuickStartDemo for React Native"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-rn"
---

MediaLive VeLiveQuickStartDemo is designed to help you get started with developing a mobile app using the React Native SDK.

This article provides a comprehensive guide on how to run VeLiveQuickStartDemo.

<span id="a21722ee"></span>
## System requirements


* A development provisioning profile

* React Native 0.73.0 and above

* Android

   * Android 5.0 (SDK API Level 21) or higher

   * Android Studio 4.0 or higher

   * A physical Android device running Android 5.0 or higher

   * Ensure that the CPU architecture that you use is armeabi\-v7a or arm64\-v8a

* iOS

   * Xcode 14.0 or higher

   * CocoaPods 1.11.3 or higher

   * A physical iOS device running iOS 11.0 or higher


<span id="ed62ded1"></span>
## Prerequisites

Complete the following tasks before you start:


* Sign up for a BytePlus account. For detailed instructions, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Activate the BytePlus MediaLive service and add domain names for pull streaming and push streaming through the console. Refer to [Getting started with BytePlus MediaLive](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started) for detailed instructions.


<span id="073dc5e5"></span>
## Preparations

You need to prepare an SDK license, an App ID, and token information before you run the demo.

<span id="ba69c964"></span>
### **Downloading a MediaLive SDK license**

Follow the instructions in [SDK management](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) to create an SDK application and then download the corresponding SDK license. Note down the App ID and bundle ID as you will need them in future steps.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bea7ca3024e46998c225be78e7dff60~tplv-goo7wpa0wc-image.image) </span>

<span id="ec13e57b"></span>
## Running the demo

This section introduces the detailed steps for setting up and running the demo.

<span id="9dde0df8"></span>
### Downloading the source code

Please contact technical support by [creating a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to obtain the Demo source code.

<span id="bb219e9f"></span>
### Integrating the SDK license


1. Rename the downloaded MediaLive SDK license file to `ttsdk.lic`.

2. Replace the original `ttsdk.lic` file in the `android/app/src/main/assets/` and `ios` directory with your own SDK license.

   * Android

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_044c1ec77126f9426239e8b66c25c310.jpg) </span>

   * iOS

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_837d406299865f1c08b552e8cdece2ce.jpg) </span>


<span id="0212a64a"></span>
### Gradle sync


1. Open `Android/VeLiveQuickStartDemo` in Android Studio.

2. Click **Sync Project with Gradle Files** to sync the project with the Gradle files.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cc7b8c264de379a8e295f701c75bee2.png) </span>


<span id="80b9feb1"></span>
### Updating the Cocoapods repository


1. Open Terminal and change the current directory to `ios`.

2. Run `pod install --repo-update` to update the local Cocoapods repository clone and install the project dependencies.


<span id="6e21bd77"></span>
### Configuring pull streaming and push streaming

Enter the App ID, AppName, AppChannel, AppVersion, and LicenseUri for live streaming.


* When you integrate both push and pull streaming, or only push streaming, you need to open the `src/store/push/pusher.ts` file and make the following modifications.

   ```JavaScript
   // Using push or both push and pull streaming
   import {initEnv} from '@byteplus/react-native-live-push';
   
   initEnv({
     AppID: 'appId', // App ID, get it on the SDK management page of the MediaLive console.
     // Set the iOS App Bundle ID and Android App Packagename 
     AppName: 'xxx'
     })
   
     // The channel through which to download the app. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging.
     AppChannel: Platform.select({
         android: 'GoogleStore',
         ios: 'AppStore',
         default: ''
     }),
   
     // The version number of your Android app. A valid version number should contain two or more separators, such as "1.3.2".
     AppVersion: '1.0.0',
     
     // License name. If you replace the license file, modify the file name accordingly. If you do SDK quick verification, you can directly replace the content of the original License file (ttsdk.lic).
     LicenseUri: {
       android: 'assets:///ttsdk.lic', 
       ios: 'ttsdk.lic'
     },
     UserUniqueID: 'VeLiveQuickStartDemo',
   });
   ```
   

* When you only integrate pull\-streaming, you need to open the `src/store/pull/player.ts` file and make the following modifications.

   ```JavaScript
   // Only use pull streaming
   import {initEnv} from '@byteplus/react-native-live-pull';
   
   initEnv({
     AppID: 'appId', // App ID, get it on the SDK management page of the MediaLive console.
     // Set the iOS App Bundle ID and Android App Packagename 
     AppName: Platform.select({
         android: 'xxx', 
         ios: 'xxx'
     })
   
     // The channel through which to download the app. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging.
     AppChannel: Platform.select({
         android: 'GoogleStore',
         ios: 'AppStore',
         default: ''
     }),
   
     // The version number of your Android app. A valid version number should contain two or more separators, such as "1.3.2".
     AppVersion: '1.0.0',
     
     // The License name.If you replace the License file, you need to modify the file name synchronously. If you do SDK quick verification, you can directly replace the content of the original License file (ttsdk.lic).
     LicenseUri: {
       android: 'assets:///ttsdk.lic', 
       ios: 'ttsdk.lic'
     },
     UserUniqueID: 'VeLiveQuickStartDemo',
   });
   ```
   


<span id="266db972"></span>
### Compiling Demo App

Refer to [React Native Document](https://reactnative.dev/docs/running-on-device).
