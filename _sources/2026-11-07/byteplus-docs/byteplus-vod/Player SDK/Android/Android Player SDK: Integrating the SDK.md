---
title: "Android Player SDK: Integrating the SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android"
---

To begin using the BytePlus Player SDK in your Android application, you must first integrate it into your project. This guide provides step\-by\-step instructions for completing the initial setup, including adding dependencies, declaring permissions, and configuring obfuscation rules, ensuring your project is ready for video playback.

<span id="563ceed9"></span>
## Prerequisites


* Android Studio. We recommend using the latest version.

* Ensure your app targets Android API level 16 or higher.

* Ensure your CPU architecture is armv7 or arm64.

* Complete the following on the [SDK management](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console:

   * Create an app and get the app ID and the app name. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management).

   * Register for the app, and purchase and download a license for the Player SDK. For details, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you test your app, use the trail license. The validity period of the trail license is one month and cannot be extended. After the trail license expires, the SDK fails in authentication, and you must apply for a new one. Therefore, do not use the trail license in your online environment.   </div>
   

<span id="83b73e1a"></span>
## Procedure

<span id="79e0fb2f"></span>
### Step 1: Add the Maven repositories

In your project's `build.gradle` file, specify [Maven Central](https://search.maven.org/) repository and BytePlus's Maven repository as repository locations, as shown below:

```Groovy
allprojects {
    repositories {
        google()
        jcenter()
        // Maven central repository
        mavenCentral()
        maven {
            // BytePlus's Maven repository
            url "https://artifact.byteplus.com/repository/public/"
        }
    }
}
```


<span id="ec0f7133"></span>
### Step 2: Integrate the SDK

To integrate the SDK into your project, add the required libraries to your module's `build.gradle` file. BytePlus VOD provides two editions of the Player SDK: Standard and Premium. Add the libraries for your chosen edition as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Replace <code>x.x.x.x</code> with the version number. To get the latest version number, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-android-player-sdk-release-notes">Android Player SDK: Release notes</a>.</div>



<Tabs>
<Tab zoneid="F4nsIcBWYr" title="Standard">
<TabTitle>Standard</TabTitle>

```Groovy
dependencies {
    implementation "com.bytedanceapi:ttsdk-player_standard:x.x.x.x"
    // Add the following code if you integrate a version earlier than 1.40.200.3
    // implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.15.4'
    implementation 'com.squareup.okhttp3:okhttp:4.2.1'
}
```



</Tab>
<Tab zoneid="ouLKNJDFUi" title="Premium">
<TabTitle>Premium</TabTitle>

```Groovy
dependencies {
    implementation "com.bytedanceapi:ttsdk-player_premium:x.x.x.x" 
    // Add the following code if you integrate a version earlier than 1.40.200.3
    // implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.15.4'
    implementation 'com.squareup.okhttp3:okhttp:4.2.1'
}
```



</Tab>
</Tabs>


<span id="86378372"></span>
### Step 3: Configure your project to use Java 8

The SDK depends on Java 8, so you must add the following code to your module's `build.gradle` file:

```Groovy
android {
  // ...
  compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
```


<span id="5b4618aa"></span>
### Step 4: Declare app permissions

Declare the permissions required by the SDK in `AndroidManifest.xml`.

```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>WRITE_EXTERNAL_STORAGE</code> is an optional permission that can be configured based on your specific requirements:</div>



* <div data-tips="true" data-tips-type="tip">If you do not need to play audio and video files from external storage or save downloaded videos to external storage, this permission is not necessary. By default, video download cache files are stored in the internal storage of the application.</div>


* <div data-tips="true" data-tips-type="tip">If you do require the <code>WRITE_EXTERNAL_STORAGE</code> permission, please refer to <a href="https://developer.android.com/training/data-storage/use-cases">Android storage use cases and best practices</a>.</div>



<span id="fb66a4b1"></span>
### Step 5: Add obfuscation rules

To prevent SDK\-related classes from being obfuscated, add the following rules to `proguard-rules.pro`.

```Plain
# For the VOD module
-keep class com.ss.ttm.** {*;} 
-keep class com.ss.ttvideoengine.** {*;} 
-keep class com.ss.mediakit.** {*;} 
-keep class com.ss.texturerender.** {*;}
-keep class com.ss.vcbkit.** {*;}
-keep class com.bytedance.**{*;}
-keep class com.pandora.ttlicense2.**{*;}
-keep class com.pandora.common.applog.**{*;}
-keep class com.pandora.vod.VodSDK {*;}
-keep class com.bytertc.volcbaselog.VolcBaseLogConfig{*;}
-keep class com.bytertc.volcbaselog.VolcBaseLogNative{*;}
```


<span id="7fb74d07"></span>
## Next step

You can proceed to use the Player SDK to play videos. For details, please refer to [Android Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk).
