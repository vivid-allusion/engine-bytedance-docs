---
title: "Integrating the Player SDK for Android"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android"
---

This topic describes how to integrate the Player SDK for Android.

## System requirements

* Android 5.0 (API 21) or higher.

* CPU architecture: armeabi\-v7a or arm64\-v8a

## Prerequisites

You have created an SDK application and obtained the SDK license. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).

> **Note**

> For features supported by each license type, see [Client SDK: SDK overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction). For pricing, see [SDK licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses).

## Integrating the SDK

You can integrate the SDK through one of the following methods:

* Automatic integration (recommended): Use Gradle to download the SDK package automatically.

* Manual integration: Manually download the AAR file and import it into your project. [Contact technical support](https://console.byteplus.com/workorder/create) for detailed instructions.

This section describes how to automatically integrate the SDK.

### Step 1: Configure Maven repositories

To integrate the SDK, configure multiple Maven repositories to ensure all necessary dependencies are downloaded correctly. Follow these steps:

1. Open the `build.gradle` file in the root directory.

2. Set the primary repository URL to `https://artifact.byteplus.com/repository/public`. The following sample code shows the configuration:

   ```Groovy
   allprojects {
       repositories {
           google()
           mavenCentral()
           maven {
               url "https://artifact.byteplus.com/repository/public" // BytePlus public Maven repo
           }
       }
   }
   ```

3. Configure additional Maven repositories for components not in the primary repository:

   * **For AGP versions below 7.1**: Add this line to the root `build.gradle`:

      ```Groovy
      apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
      ```

   * **For AGP 7.1 and above**: Copy the Maven configuration from `https://ve-vos.volccdn.com/script/vevos-repo-base.gradle` into the `dependencyResolutionManagement` block of `settings.gradle`.

### Step 2: Configure the environment and dependencies

1. Open the `app/build.gradle` file and add the following configuration:

   * Configure the CPU architecture used by the app in `defaultConfig`. The SDK supports armeabi\-v7a and arm64\-v8a.

   * Add the dependencies in `dependencies`.

   ```Groovy
   android {
      defaultConfig {
          ndk {
              // Set the SO (Shared Object) library architecture to support armeabi-v7a or arm64-v8a.
              abiFilters 'armeabi-v7a', 'arm64-v8a'
           }
      }
   }
   
   dependencies {
      // ...
      // For version 1.49.100.2 or later, add this dependency to use basic stream-pulling features.
      implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:x.x.x.x' 
   }
   ```

   * For version 1.51.300.2 or later, add both `implementation 'com.bytedanceapi:ttsdk-ttbmf:x.x.x.x'` and `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'` to use the super\-resolution (SR) and video sharpening features.

   * For version 1.49.100.2 or later, replace `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:x.x.x.x'` with `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'` to use features supported by the premium license.

   * For version 1.49.100.2 or later, add both `implementation 'com.bytedanceapi:ttsdk-ttquic:x.x.x.x'` and `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'` to pull streams over QUIC.

   * For version 1.49.100.2 or later, add both `implementation 'com.bytedanceapi:ttsdk-ttcmaf:x.x.x.x'` and `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'` to play CMAF streams.

   > **Note**

   * > Replace `x.x.x.x` with the SDK version you want to integrate. We recommend that you use the latest version. For available versions, see [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes).

   * > For version 1.48.200.2:

      * > To use basic stream\-pulling features, add `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`.

      * > To pull streams over QUIC, add both `implementation 'com.bytedanceapi:ttsdk-ttquic:1.48.200.2'` and `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`.

      * > To pull streams over RTM, add `implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:1.48.200.2'`.

      * > To play CMAF streams, add both `implementation 'com.bytedanceapi:ttsdk-ttcmaf:1.48.200.2'` and `implementation 'com.bytedanceapi:ttsdk-ttlivepull_standard:1.48.200.2'`.

   * > For version 1.48.100.103 or earlier:

      * > To use basic stream\-pulling features, including pulling streams over QUIC and playing CMAF streams, add `implementation 'com.bytedanceapi:ttsdk-ttlivepull:x.x.x.x'`.

      * > To pull streams over RTM, add `implementation 'com.bytedanceapi:ttsdk-ttlivepull_rtc:x.x.x.x'`.

2. Click **Sync Project with Gradle Files** to synchronize the SDK. The SDK will be automatically downloaded and integrated into the project. If the integration fails, check your network connection to the Maven repositories.

## Configuring permissions

Declare the permissions required by the Player SDK in the `AndroidManifest.xml` file.

```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

## Adding a license

Copy the license file obtained by following [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) to your project directory. For example, copy the `License2_test.lic` file to the `assets` directory, as shown in the following screenshot. Take note of the path to the license file because you will use it when initializing the SDK.

![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0c295cb-file_path2.png)

## Implementing code obfuscation

Add the following lines to the `proguard-rules.pro` file to exclude SDK\-related classes from obfuscation.

```Plain
-keep class com.pandora.**{*;}
-keep class com.ss.**{*;}
-keep class com.bytedance.**{*;}
-keep class com.pandora.ttlicense2.**{*;}
-keep class com.bytertc.**{*;}
-keep class log.**{*;}
```

If you are integrating the RTC SDK, you also need to configure obfuscation rules for the RTC SDK. See [Obfuscating your code for Android Apps](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-78295) for details.
