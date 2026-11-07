---
title: "Getting started with Android "
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-getting-started-with-android"
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

The following table shows the required versions of third\-party library dependencies for BytePlus Video Editor SDK.


* Business

   
   |**Category** |**Library** |**Version** |**License** |
   |---|---|---|---|
   |jetpack |androidx.appcompat:appcompat |1.3.0 |Apache 2.0 |
   ||androidx.annotation:annotation |1.3.0 |Apache 2.0 |
   ||androidx.core:core |1.5.0 |Apache 2.0 |
   ||androidx.exifinterface:exifinterface |1.2.0 |Apache 2.0 |
   ||androidx.constraintlayout:constraintlayout |2.1.4 |Apache 2.0 |
   ||androidx.recyclerview:recyclerview |1.2.1 |Apache 2.0 |
   ||androidx.lifecycle:lifecycle\-viewmodel |2.3.1 |Apache 2.0 |
   |material |com.google.android.material:material |1.3.0 |Apache 2.0 |
   |kotlin coroutines |org.jetbrains.kotlinx:kotlinx\-coroutines\-android |1.5.2 |Apache 2.0 |
   ||org.jetbrains.kotlinx:kotlinx\-coroutines\-core |1.5.2 |Apache 2.0 |
   |Status bar adaptation |com.geyifeng.immersionbar:immersionbar |3.2.2 |Apache 2.0 |
   ||com.geyifeng.immersionbar:immersionbar\-ktx |3.2.2 |Apache 2.0 |
   |Json parser |com.google.code.gson:gson |2.9.0 |Apache 2.0 |
   |Optional |com.github.bumptech.glide:glide |4.13.2 |BSD, part MIT and Apache 2.0 |
   ||com.squareup.okhttp3:okhttp |4.9.3 |Apache 2.0 |
   ||io.reactivex.rxjava2:rxjava |2.2.8 |Apache 2.0 |
   ||io.reactivex.rxjava2:rxandroid |2.1.0 |Apache 2.0 |
   ||io.reactivex.rxjava2:rxkotlin |2.3.0 |Apache 2.0 |
   ||io.github.jeremyliao:live\-event\-bus\-x |1.8.0 |Apache 2.0 |
   ||com.danikula:videocache |2.7.1 |Apache 2.0 |
   ||com.airbnb.android:lottie |5.2.0 |Apache 2.0 |
   ||com.google.android.exoplayer:exoplayer |2.18.1 |Apache 2.0 |
   

* Native

   
   |**Library** |**Version** |**License** |
   |---|---|---|
   |lua |5.1.5 |MIT |
   |nlohmann |3.11.2 |MIT |
   |lua_cjson |2.1.0 |MIT |
   |Eigen |3.3.3 |MPL 2.0, BSD, Apache |
   |libpng |1.6.37 |http://www.libpng.org/pub/png/src/libpng\-LICENSE.txt |
   |cJson |1.4 |MIT |
   |stb_image |2.22 |MIT |
   |icu |72.1 |MIT |
   |harfbuzz |2.2.0 |MIT |
   |freetype |2.10.0 |https://github.com/freetype/freetype/blob/master/LICENSE.TXT |
   |giflib |5.1.4 |https://github.com/rcancro/giflib/blob/5.0.4/COPYING |
   |yaml\-cpp |0.6.2 |MIT |
   |zip |1.15 |MIT |
   |ffmpeg |Customized based on version 3.x |LGPL v2.1 |
   |libyuv |1816 |https://chromium.googlesource.com/libyuv/libyuv.git/+/refs/heads/main/LICENSE |
   |RGBConverter | |https://github.com/ratkins/RGBConverter/blob/master/LICENSE.md |
   |xxtea\-c |1.0 |MIT |
   


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
