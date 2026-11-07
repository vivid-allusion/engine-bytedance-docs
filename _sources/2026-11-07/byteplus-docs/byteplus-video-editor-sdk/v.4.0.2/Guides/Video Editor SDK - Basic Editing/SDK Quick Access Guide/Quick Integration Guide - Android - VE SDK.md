---
title: "Quick Integration Guide - Android - VE SDK"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-quick-integration-guide-android-ve-sdk-v.4.0.2"
---

<span id="f0e7d13e"></span>
# Project settings

<span id="9dadfab9"></span>
### System requirements

Android 5.0 (API 21) or later

<span id="853dd680"></span>
### Development environment

minSdkVersion: 21

targetSdkVersion: 26

compileSdkVersion: 26

<span id="ccebd043"></span>
# Integrate the SDK

<span id="b9d7b757"></span>
### Step 1 Create an Android Studio project

Set **Minimum SDK to API 21: Android 5.0 (Lollipop)** .

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f8031c4171764626bab63d48a2a7e052~tplv-em5hxbkur4-noop.image) </span>

<span id="14e8fdf7"></span>
### Step 2 Install NDK of the required version

Install NDK of the 21.0.6113669 version. If any error occurs, change the NDK version as follows:


1. Open the project and go to **Tools \> SDK Manager**.

2. Click the **SDK Tools** tab.

3. Select the **Show Package Details** check box.

4. Click **NDK (Side by side)**  and select the NDKs you want to install. All of the selected NDKs will be installed to the **android/sdk/ndk/**  directory by Android Studio.


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5858a7631df846899b1db305bad30fcc~tplv-em5hxbkur4-noop.image) </span>


5. Click **OK**.

   A dialog box will be displayed, showing you the space occupied by the NDK packages.

6. Click **OK**.

7. Click **Finish** after the installation is complete.


<span id="e9228140"></span>
### Step 3 Import the SDK

Copy the **vesdk\-xxx.aar** and **nleeditor\-xxx.aar** files to the app/libs directory.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/acdd14720583404cae33f946eda89b89~tplv-em5hxbkur4-noop.image) </span>

<span id="c631bc20"></span>
### Step 4 Add build dependencies for the SDK

Add the following to the **app/build.gradle** file:

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9e4a901ca070401fbb058f30ea414a20~tplv-em5hxbkur4-noop.image) </span>

```Groovy
repositories {
    flatDir {
        dirs 'libs'
    }
}

implementation(name: 'Name of the VE SDK AAR file', ext: 'aar')
implementation(name: 'Name of the NLEEditor AAR file', ext: 'aar')
```


<span id="6f8a2b5c"></span>
### Step 5 Configure permissions

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/978ba9fb56b44498876d004eb97e4825~tplv-em5hxbkur4-noop.image) </span>

```XML
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```


<span id="fdc457ea"></span>
# Initialize the SDK

```Java
// Initialize the VE SDK environment.
VESDK.init(application, Environment.getExternalStorageDirectory().getAbsolutePath());

// Set whether the SDK reads model files from the asset directory using assetManager.
VESDK.setAssetManagerEnable(true);

// Set a local directory for saving algorithm models (for the recognition of faces, gestures, objects, and more). You can place required models in the local directory or deliver them from your server.
VESDK.setEffectResourceFinder(new FileResourceFinder("Local directory for saving model files"));

// Pass the path of the license file for authentication.
VEAuth.init(licenseFile.getAbsolutePath());
```


**Note**


* Call **VEAuth.init** only after you have called **VESDK.init**.

* Set the model directory before using the SDK because some effects such as beauty effects and body shaping can be implemented only under model support.

* Call **VEAuth.init** and **VESDK.init** before you use **VERecoder** or create **VEEditor**. Otherwise, the call is invalid.


<span id="d9b6980a"></span>
# Synchronize and run the project

If the following error occurs, click the link in blue to synchronize the project again.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/76bc953f2f004113a3d67f79efbda747~tplv-em5hxbkur4-noop.image) </span>
