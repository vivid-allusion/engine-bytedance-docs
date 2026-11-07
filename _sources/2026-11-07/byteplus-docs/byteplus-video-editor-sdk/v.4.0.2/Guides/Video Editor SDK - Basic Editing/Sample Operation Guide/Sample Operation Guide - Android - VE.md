---
title: "Sample Operation Guide - Android - VE"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sample-operation-guide-android-ve-v.4.0.2"
---

<span id="ffed0667"></span>
# Procedure

<span id="c7f1fb76"></span>
### Step 1 Decompress the sample package

Decompress the **CK\-Sample\-x.x.zip** file.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/fba6702df0b84f5a9fd32d98dbda7e88~tplv-em5hxbkur4-noop.image) </span>

<span id="7f66265f"></span>
### Step 2 Open the sample project in Android Studio

Go to **File \> Open**. Select the decompressed **CK\-Sample\-x.x** directory, and click **Open**.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/0d41ffd3336448d49e3c46f8ea1a81bb~tplv-em5hxbkur4-noop.image) </span>

<span id="7fdec5f1"></span>
### Step 3 Run the sample project

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/766a238fa4584ad4adb9eab7e7c5110e~tplv-em5hxbkur4-noop.image) </span>

<span id="d41a4f5f"></span>
# Precautions

<span id="d449515d"></span>
### 1. Do not change the Gradle version

Do not change the Gradle version of the sample package. Otherwise, problems like NDK incompatibility may occur.

<span id="d1ae1451"></span>
### 2. Do not change applicationId


* Ensure that **applicationId** matches the license file that is generated based on the app ID. Otherwise, you cannot be authorized to use the functions of the sample.

* To test your own license file, change **applicationId** in the app\-level **build.gradle** file based on your app ID and license file, and change LICENSE_NAME in the **BaseModuleInit.java** file.


<span id="3f6570da"></span>
### 3. Pay attention to the authorization period

If the time on your mobile is not within the authorization period, the sample cannot run on the mobile.

You can obtain the authorization period from the value of **com.vesdk.vebase.app# LICENSE_NAME**.

For example, **ve_test_20201108_20210228_com.ss.android.vesdk.vedemo_v2.0.2.licbag** indicates that the authorization period is from 2020\-11\-08 to 2021\-02\-28.
