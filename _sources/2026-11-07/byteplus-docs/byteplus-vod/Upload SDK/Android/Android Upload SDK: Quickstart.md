---
title: "Android Upload SDK: Quickstart"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-android_1"
---

To get started with the Android Upload SDK, follow this guide to integrate it into your Android project. This document walks you through adding the required repositories and dependencies, declaring app permissions, and configuring obfuscation rules.

<span id="1da61574"></span>
## Prerequisites


* Android Studio. We recommend using the latest version.

* Ensure that your app targets Android API level 16 or higher.

* Ensure that the CPU architecture is armv7 or arm64.


<span id="5236922a"></span>
## Procedure

<span id="8bd1ec29"></span>
### Step 1: Add the Maven repositories

In your project's build.gradle file, add the [Maven Central](https://search.maven.org/) and BytePlus's Maven repositories, as shown below:

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


<span id="8ce2bb55"></span>
### Step 2: Integrate the SDK

To integrate the SDK into your project, add the required libraries to your module's `build.gradle` file:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Replace x.x.x.x with the version number. To get the latest version number, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-android-upload-sdk-changelog">Android Upload SDK: Release notes</a>.</div>


```Groovy
dependencies {
    ...
    implementation "com.bytedanceapi:ttsdk-ttuploader:x.x.x.x"
    implementation "com.bytedanceapi:ttsdk-ttcommon:x.x.x.x"
    // Add the following code if you are using a version earlier than 1.40.200.3
    // implementation "com.bytedance.applog:RangersAppLog-Lite-global:6.10.1"
}
```


<span id="ececd89c"></span>
### Step 3: Declare app permissions

Declare the permissions required by the SDK in your AndroidManifest.xml file.

```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```


<span id="b182d510"></span>
### Step 4: Add obfuscation rules

To prevent SDK\-related classes from being obfuscated, add the following rules to your proguard\-rules.pro file.

```Plain
# For the upload module
-keep class com.pandora.common.applog.**{*;}
-keep class com.pandora.ttuploader2.** {*;}
-keep class com.ss.bduploader.** {*;}
```
