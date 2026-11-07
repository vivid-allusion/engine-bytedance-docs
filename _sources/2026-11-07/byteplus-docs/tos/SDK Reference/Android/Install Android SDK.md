---
title: "Install Android SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-the-android-sdk"
---

This article provides the download address and installation method for the TOS Android SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Before installing the TOS Android SDK, ensure that JDK version 1.8 or later is installed.

* Please ensure that your Android application targets API level 21 (Android 5.0) or higher.


<span id=".c2RrLeS4i-i9veWcsOWdgOWPiuS_ruiuouiusOW9lQ=="></span>
## SDK Download Link and Revision History


* [Latest source code URL](https://github.com/volcengine/ve-tos-java-sdk)

* [Revision History](https://github.com/volcengine/ve-tos-java-sdk/blob/main/CHANGELOG.md)


<span id=".5a6J6KOF5pa55byP"></span>
## Installation Method

<span id=".6YCa6L-HLWdyYWRsZS3lvJXlhaU="></span>
### Integration via Gradle

Configure the `build.gradle` file as follows, and add dependencies in `dependencies`.

```apache
implementation 'com.volcengine:ve-tos-android-sdk:2.6.0'
```


Open the AndroidManifest.xml file and insert the following code snippet to configure the permissions required by the SDK.

```xml
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The minimum supported minSDK version for the TOS Android SDK is API 21 (Android 5.0).

* For Android applications with a minSDK version of API 21 to 26, the following additional settings are required to ensure proper operation.


**Relevant Dependencies**


* Gradle version 6.1.1 or later.

* Android Gradle Plugin version 4.0.0 or higher.


Add the following code to the build.gradle file of your Android application module (typically located in the app directory):

```groovy
android {
    compileOptions {
        coreLibraryDesugaringEnabled true
        
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

dependencies {
    coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:1.1.5'
}
```


For more details, see [Using Java 8 language features and API](https://developer.android.com/studio/write/java8-support).
