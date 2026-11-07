---
title: "Integrating the Player SDK for React Native"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn"
---

This topic introduces how to integrate the Player SDK for React Native.

<span id="b1be2e82"></span>
## System requirements


* React Native 0.70 or later

* Node v16 or later

* Android:

   * Android 4.3 or later

   * CPU architecture: armeabi\-v7a or arm64\-v8a

* iOS & macOS:

   * Physical devices running iOS 11.0 or later

   * Xcode 14.1 or later

* Please ensure that your project has a valid developer signature.

* For instructions on setting up your environment, see the [official documentation](https://reactnative.dev/docs/environment-setup).


<span id="23566c94"></span>
## Prerequisites

You have created an SDK application and obtained the SDK license. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).

<span id="33c06caa"></span>
## Integrating the SDK

Use the following npm packages to install the SDK.

```Plain
npm i @byteplus/react-native-live-pull
```


<span id="c7fa4b6f"></span>
### Step 1: Configuring the Maven repository


1. Open the `build.gradle` file in the Android root directory.

2. Define the Maven repositories and configure the repository URLs.

   ```Plain
   allprojects {
       repositories {
           google()
           mavenCentral()
           maven {
               url "https://artifact.bytedance.com/repository/Volcengine/"
           }
           maven {
               url "https://artifact.byteplus.com/repository/public/"
           }
       }
   }
   
   apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
   ```
   


<span id="75d013a7"></span>
### Step 2: Adding dependencies

Add the dependencies to your iOS Podfile.

```Plain
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
source 'https://cdn.cocoapods.org/'
```


<span id="db904c49"></span>
## Configuring permissions

<span id="07327795"></span>
### Android

Declare the permissions required by the app in the `AndroidManifest.xml` file:

```Plain
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.INTERNET" />
```


<span id="22b41bb8"></span>
## Adding the license file

Copy the license file to your project directory and note down the path to the license file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure the bundle ID and app ID associated with the license file are the same as those of your project. Otherwise, the license authentication will fail.</div>
