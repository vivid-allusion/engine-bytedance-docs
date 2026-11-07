---
title: "Getting started with Android "
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-getting-started-with-android"
---

Get started with the Video Editor (VE) Android SDK by exploring integration requirements and running the sample code. This guide provides an overview of essential setup steps and practical examples to help you quickly integrate and test your Android applications.

<span id="8ff74eb5"></span>
# Integration requirements overview

Learn about the integration overview of BytePlus Video Editor SDK that you must fulfill before you integrate it into your Android project.

<span id="13ddd4bf"></span>
## Development environment

The following table shows the required development environment for BytePlus Video Editor SDK:


|**Development Environment** |**Version** |
|---|---|
|Gradle |7.5.1 |
|Android Gradle Plugin |7.3.1 |
|kotlin |1.5.30 |
|minSdk |21 |
|targetSdk |33 |
|compileSdk |33 |
|Java Version |11 |


<span id="293b9023"></span>
## Third\-party library dependencies

The following table shows the required versions of third\-party library dependencies for BytePlus Video Editor SDK:


|**Library** |**dependency** |**Version** |
|---|---|---|
|Jetpack |androidx.appcompat:appcompat |1.3.0 |
||androidx.lifecycle:lifecycle\-viewmodel |2.3.1 |
|Material |com.google.android.material:material |1.2.0 |
|kotlinx.coroutines |org.jetbrains.kotlinx:kotlinx\-coroutines\-android |1.5.2 |
||org.jetbrains.kotlinx:kotlinx\-coroutines\-core |1.5.2 |
|StatusBar |com.geyifeng.immersionbar:immersionbar |3.2.2 |
||com.geyifeng.immersionbar:immersionbar\-ktx |3.2.2 |
|JSON resolution |com.google.code.gson:gson |2.9.0 |


<span id="384499c0"></span>
## Available languages

Chinese and English are supported. More languages can be added as needed.

<span id="e26583f8"></span>
## Obtaining a license

To obtain a trial or official license of BytePlus Video Editor SDK, contact the BytePlus Video Editor SDK team.

<span id="cfee56b4"></span>
## Supported media formats

These are the supported media formats in BytePlus Video Editor SDK:


|**Type** ||**Video** |**Image** |**Audio** |
|---|---|---|---|---|
|Input |* File Types<br><br>* Container Formats |* .mp4<br><br>* .mov |* .jpg<br><br>* .png<br><br>* .gif |* .mp3<br><br>* .aac<br><br>* .wav |
||Format |* H.264<br><br>* H.265 |N/A |N/A |
|Output |* File Types<br><br>* Container Formats |.mp4 |N/A |N/A |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to support other media formats in your project, reach out to the BytePlus Video Editor SDK team for more information.</div>


<span id="43f5cc8f"></span>
## SDK package sizes

These are the SDK packages offered in Video Editor SDK and their sizes:


|**SDK** |**Total Size** |**Class Size** |**arm64\-v8a** |**armeabi\-v7a** |
|---|---|---|---|---|
|EffectSDK |25.4 MB |140 KB |13.8 MB |11.5 MB |
|VESDK |21.2 MB |1.03 MB |10.6 MB |9.56 MB |
|NLESDK |2.69 MB |326 KB |1.32 MB |1.04 MB |
|Camera and editor |1.38 MB |845 KB |1.38 MB |1.38 MB |
|Total |50.67 MB |2.34 MB |27.1 MB |23.48 MB |


<span id="f1e9f848"></span>
## Runtime Permissions

You have to request for the following permissions:


* Camera.

* Microphone.

* Photos and videos

* Music and audio.


For more information, refer to [Request runtime permissions](https://developer.android.com/training/permissions/requesting).

<span id="1112a3d4"></span>
# Running the sample code

Get hands\-on with the BytePlus Video Editor SDK by downloading our sample project and running it in an Android environment. Dive into the SDK's functionality and explore seamless integration possibilities. You can proceed to run the sample code in your iOS project by following the steps below.

**To run the sample code in Android:** 


1. Download and decompress EffectOneSample.zip from the deliverables list.

2. Start Android Studio.

3. In Android Studio, select **File** \> **New** \> **Import Project**.

4. Navigate to the location where you extracted the project.

5. Select the project folder.

6. Click **OK** to import the project.
