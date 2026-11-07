---
title: "Integrate Plugins on Demand to Reduce the Size of the Application"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/1108726"
---

To meet diverse user scenarios while considering the size of the App, starting from version **3.50**, the RTC SDK will gradually be split into a **main library + plugins** format. The main library is a required integration for implementing basic RTC functionalities; plugins are optional and can be integrated on demand based on actual application scenarios and usage methods to reduce the App's size.

This article provides a detailed introduction to the functions of each plugin, application scenarios, and integration methods, with data based on version 3.58.

<span id="android"></span>
# Android

<span id="plugin-details"></span>
## Plugin Details


|Library/Plugin Name |Starting Version |Library/Plugin Function |Description |Architecture |Required |
|---|---|---|---|---|---|
|BytePlusRTC\-lite.aar + libbyteplusrtc.so |ALL |Main Library |The main library of the RTC SDK, used to implement basic audio and video calling functions. |arm64\-v8a |Yes |
| | | | |armeabi\-v7a | |
| | | | |x86 | |
| | | | |x86_64 | |
|libbytertc_ffmpeg_audio_extension.so |v3.54 |Audio Decoder Plugin |This audio decoder plugin is based on [FFmpeg](https://www.ffmpeg.org/). It supports the SDK's audio memory playback feature and decodes various audio formats (mp3, mp4, aac, m4a, 3gp, wav, ogg, ts, wma), providing better compatibility for audio file playback functions. |arm64\-v8a |No |
| | | |If you need to use memory playback functionality or encounter compatibility issues when playing audio files, you can choose to integrate this plugin. After integration, the SDK will use the ffmpeg audio plugin for decoding by default, without the need for additional settings; if you do not integrate this plugin, the SDK will use the system library for decoding by default. |armeabi\-v7a | |
| | | | |x86 | |
| | | | |x86_64 | |
|libbdaudioeffect.so |v3.56 |Audio Technology Plugin |Audio technology (Speech, Audio & Music Intelligence, referred to as SAMI), mainly dedicated to the research and application of voice synthesis, audio understanding and processing, music understanding and editing, music generation, and other technologies. |arm64\-v8a |No |
| | | |To use the voice changer and karaoke scoring features, you must integrate this plugin. After integration, you can call [setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70080#setvoicechangertype) to use the voice change feature; call getSingScoringManager and ISingScoringManager class methods to use karaoke scoring related features |armeabi\-v7a | |
| | | | |x86 | |
| | | | |x86_64 | |
|effectAAR\-release_V4.4.3Lite.aar |ALL |Video Effects Library |The intelligent beautification effects SDK, developed by BytePlus, adds beautification effects, filters, stickers, and other effects to locally captured videos. After integration, you can call interfaces such as enableVideoEffect to use video effects related functions. For integration instructions, see [Intelligent Beautification Effects](https://docs.byteplus.com/en/docs/12/docs-114717). |arm64\-v8a |No |
| | | | |armeabi\-v7a | |


<span id="integration-method"></span>
## Integration Method

<span id="maven-integration"></span>
### Maven Integration

The RTC SDK feature plugins and the main library are published together using the BytePlusRTC\-lite.aar file to Maven. You can delete unnecessary plugins after integration. The specific steps are as follows:


1. Switch the project view to **Project** mode in the upper left corner of Android Studio, and configure the Maven repository address in the `settings.gradle` file in the project's root directory.

   ```groovy
   dependencyResolutionManagement {
       repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
       repositories {
           ...
           maven { url 'https://artifact.byteplus.com/repository/public/' }
       }
   }
   ```
   

   ::tip

   If your Android Gradle Plugin version is below v7.1.0, you should configure the Maven repository address in the build.gradle file in the project's root directory.

   ```groovy
   allprojects {
       repositories {
           ...
           maven { url 'https://artifact.byteplus.com/repository/public/' }
       }
   }
   ```
   

   :::

2. Add the RTC SDK dependency in the App's build.gradle file.

   You need to replace '3.x.y.z' with the specific version number. For the latest version number, refer to the SDK download page.

   ```groovy
   dependencies {
      ...
      implementation 'com.byteplus:BytePlusRTC:3.xx.x.xxx' // 填写需要接入的 RTC SDK 版本号
   }
   ```
   

3. After integrating the RTC SDK, remove the unnecessary plugins. For example, to exclude libbdaudioeffect.so:

   ```groovy
   android {
      ...
      packagingOptions {
         exclude 'lib/arm64-v8a/libbdaudioeffect.so'
      }
   }
   ```
   

   * Some plugins have dependencies on each other. If you want to remove unnecessary plugins, please consult the technical support team to avoid accidentally deleting plugins that may cause related functions to not work properly.

   * The video effects library effectAAR\-release_V4.X.XLite.aar is not currently supported for online Maven integration. If you need to use it, please download and unzip the Android SDK package, then manually drag it into the main project. For integration instructions, see Intelligent Beautification Effects.


<span id="offline-integration"></span>
### Offline Integration

<span id="method-1-delete-plugins"></span>
#### Method 1: Delete Plugins

Starting from version 3.57, when [manually integrating the SDK](https://docs.byteplus.com/en/docs/12/docs-70134), you can directly delete the **optional** and **unnecessary** plugin files.

At this point, you can ignore errors about missing `.so` files, such as `dlopen failed: library "libbdaudioeffect.so" not found`.

<span id="method-2-dynamic-loading"></span>
#### Method 2: Dynamic Loading

Starting from version 3.57, the RTC SDK supports dynamic loading of all libraries.

The SDK provides a `nativeLoadPath` property in the `EngineConfig` class, which allows dynamic loading of the required `.so` files from a specified private directory during App runtime, thereby reducing the size of the App's installation package. Follow these steps to implement this feature:


1. Download and unzip the [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707) file.

2. Switch the project view to **Project** mode in the upper left corner of Android Studio, and place the unzipped `BytePlusRTC-lite.aar` and `libbyteplusrtc.so` in the `app/libs` directory.

3. Upload all architecture `.so` files to your server and ensure that the App can download the `.so` files for the target architecture via the network.

4. When the App is running, check for the existence of the `.so` file for the target architecture. If it does not exist, download the `.so` file for the corresponding architecture via the network and save it to the App's private directory.

5. Call [RTCEngine::createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70080#creatertcengine), and set `config.nativeLoadPath` to the App's private directory where the `.so` files are saved. The SDK will automatically load the `.so` files based on the specified path.


<span id="ios"></span>
# iOS

<span id="plugin-details"></span>
## Plugin Details


|Library/Plugin Name |Starting Version |Library/Plugin Function |Description |Required |
|---|---|---|---|---|
|BytePlusRTC.xcframework |ALL |Main Library |The main library of the RTC SDK, used to implement basic audio and video calling functions. |Yes |
|RealXBase.xcframework |v3.57 |Main Library | |Yes |
|effect\-sdk.framework |ALL |Video Effects Library |The intelligent beautification effects SDK independently developed by BytePlus, which can add beauty, filters, stickers, and other effects to locally captured videos. After integration, you can call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCVideoEffect-enablevideoeffect) and other interfaces to use video effects related functions. Integration guide see [Intelligent Beautification Effects](https://docs.byteplus.com/en/docs/12/docs-114717). |No |
|BytePlusRTCScreenCapturer.xcframework |ALL |Screen Capture Plugin |This plugin is for use cases that require screen sharing. After integration, you can call [startScreenCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startscreencapture-bundleid) and other interfaces to use screen sharing related functions. See [iOS Screen Sharing](https://docs.byteplus.com/en/docs/12/docs-124177). |No |
|RTCFFmpeg.xcframework |v3.54 |Video/Image Decoding |FFmpeg is an open\-source multimedia processing library for handling audio, video, and other multimedia data. RTCFFmpeg.xcframework is based on the open\-source FFmpeg source code with some modifications, such as removing unused features. |No |
|ByteRTCFFmpegAudioExtension.xcframework |v3.54 |Audio Decoder Plugin |An audio decoder plugin compiled based on [FFmpeg](https://www.ffmpeg.org/), supporting SDK audio memory playback functionality, capable of decoding audio files in mp3, mp4, aac, m4a, 3gp, wav, ogg, ts, wma formats, and providing better compatibility for audio file playback functions. |No |
| | | |If you need to use memory playback functionality, or encounter compatibility issues when playing audio files, you can choose to integrate this plugin. After integration, the SDK will use the ffmpeg audio plugin for decoding by default, without the need for additional settings; if you do not integrate this plugin, the SDK will use the system library for decoding by default. | |
|bdaudioeffect.framework |v3.56 |Audio Technology Plugin |Audio technology (Speech, Audio & Music Intelligence, referred to as SAMI), mainly dedicated to the research and application of voice synthesis, audio understanding and processing, music understanding and editing, music generation, and other technologies. |No |
| | | |To use voice change and K\-song scoring features, you need to integrate this plugin. After integration, you can call [setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70086#setvoicechangertype) to use the voice change feature; call getSingScoringManager and ByteRTCSingScoringManager class methods to use K\-song scoring related functions. | |


`RealXBase.xcframework` was separated from the main library in version 3.57 and is required. Please pay attention to the changes in the [Integration Methods](https://docs.byteplus.com/6uofwzl3/25046).

<span id="integration-methods"></span>
## Integration Methods

<span id="cocoapods-integration"></span>
### CocoaPods Integration

When integrating the RTC SDK online with CocoaPods, you can specify the plugins you need to integrate in the `Podfile` using the `subspecs` field.


|Library/Plugin Name |Required |Starting Version |Corresponding `subspecs` Field |
|---|---|---|---|
|BytePlusRTC.xcframework |Yes |ALL |Core |
|RealXBase.xcframework |Yes |v3.57 |RealXBase |
|BytePlusRTCScreenCapturer.xcframework |No |ALL |ScreenCapture |
|RTCFFmpeg.xcframework |No |v3.54 |RTCFFmpeg |
|ByteRTCFFmpegAudioExtension.xcframework |No |v3.54 |ByteRTCFFmpegAudioExtension |


> The video effects library `effect-sdk.framework` is not supported for online CocoaPods integration. For usage, please refer to the [Intelligent Beautification Effects](https://docs.byteplus.com/en/docs/12/docs-114717) iOS integration method.


For specific configuration of the Podfile, see the examples below. Please replace `your target` with your actual target name and `3.x.y.z` with the specific version number:

```ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git' 

# Example 1:
# Integrate main library + default plugins
target 'your target' do
  pod 'BytePlusRTC', '3.x.y.z'
end

# Example 2:
# Integrate only the main library
target 'your target' do
  use_frameworks!
  pod 'BytePlusRTC', '3.x.y.z', :subspecs => ['Core', 'RealXBase']
end

# Example 3:
# Integrate main library + screen capture plugin
target 'ScreenShareExtension' do
  use_frameworks!
  pod 'BytePlusRTC', '3.x.y.z', :subspecs => ['Core', 'RealXBase', 'ScreenCapture']
end
```


<span id="offline-integration"></span>
### Offline Integration

Download and unzip [iOS SDK](https://docs.byteplus.com/en/docs/12/docs-75707), then drag the main library and the required plugin files into the main project. Configure the Embed property of the selected library in the project to `Embed & Sign`.

<span id="windows"></span>
# Windows

<span id="plugin-details"></span>
## Plugin Details


|Library/Plugin Name |Starting Version |Required |Library/Plugin Function |Description | |
|---|---|---|---|---|---|
|BytePlusRTC.dll |ALL |Yes |Main Library |The main library of the RTC SDK, used to implement basic audio and video calling functions. | |
|libEGL.dll |ALL |Yes |Video Rendering |libEGL.dll is an important component of the OpenGL ES interface specification, used to implement cross\-platform graphics processing. It includes a library of functions for creating and managing graphics contexts, surfaces, and other resources with EGL (Embedded System Graphics Library), enabling communication between the system and graphics hardware, and is an important part of OpenGL ES. | |
|libGLESv2.dll |ALL |Yes |Video Rendering |libGLESv2.dll is part of the OpenGL ES 2.0 graphics library. This file contains functions for rendering 2D and 3D graphics and is necessary for many applications that use OpenGL ES 2.0 for graphics development. | |
|openh264\-4.dll |ALL |Yes |Video H.264 Soft Encoding |OpenH264\-4.dll is a dynamic link library file that provides video encoding and decoding functionality. It is part of the OpenH264 open\-source video encoder, used for encoding and decoding video content. | |
|pthreadVC2.dll |ALL |Yes |Thread Library |pthreadVC2.dll is a dynamic link library file for the Windows operating system, providing an implementation of the POSIX thread library, commonly used in C/C++ program development on the Windows platform. It provides functions and tools for creating, managing, and synchronizing threads, allowing programs to perform multiple tasks simultaneously and more efficiently utilize system resources. | |
|RTCFFmpeg.dll |ALL |Yes |Video/Image Decoding |FFmpeg is an open\-source multimedia processing library for handling audio, video, and other multimedia data. RTCFFmpeg.dll is based on the open\-source FFmpeg source code with some modifications, such as feature pruning. | |
|effect.dll |ALL |No |Video Effects Library |The intelligent beautification effects SDK independently developed by BytePlus, which can add beauty, filters, stickers, and other effects to locally captured videos. After integration, you can call `enableVideoEffect` and other interfaces to use video effects related functions. | |
|bytertc_nico_extension.dll |v3.52 |No |Audio Codec Plugin |The RTC self\-developed audio codec plugin. The NICO audio codec algorithm offers better resilience to poor network conditions than the native Opus audio codec and is fully compatible with Opus. Suitable for application scenarios with strong demands for low stutter and low latency in voice calls. If you need to use this feature, please contact technical support. | |
|bytertc_ffmpeg_audio_extension.dll |v3.54 |No |Audio Decoder Plugin |An audio decoder plugin compiled based on FFmpeg, supporting SDK audio memory playback functionality, capable of decoding audio files in mp3, mp4, aac, m4a, 3gp, wav, ogg, ts, wma formats, and providing better compatibility for audio file playback functions. | |
| | | | |If you need to use memory playback functionality, or encounter compatibility issues when playing audio files, you can choose to integrate this plugin. After integration, the SDK will use the ffmpeg audio plugin for decoding by default, without the need for additional settings; if you do not integrate this plugin, the SDK will use the system library for decoding by default. | |
|bdaudioeffect\-mt.dll |v3.56 |No |Audio Technology Plugin |Audio technology (Speech, Audio & Music Intelligence, referred to as SAMI), mainly dedicated to the research and application of voice synthesis, audio understanding and processing, music understanding and editing, music generation, and other technologies. | |
| | | | |To use voice change and K\-song scoring features, you need to integrate this plugin. After integration, you can call [setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70095#setvoicechangertype) to use the voice change feature; call getSingScoringManager and ISingScoringManager class methods to use K\-song scoring related functions. | |


<span id="integration-method"></span>
## Integration Method

Integrate using your build tool based on the provided header files and dynamic libraries.

<span id="macos"></span>
# macOS

<span id="plugin-details"></span>
## Plugin Details


|Library/Plugin Name |Starting Version |Required |Library/Plugin Function |Description | |
|---|---|---|---|---|---|
|BytePlusRTC.framework |ALL |Yes |Main Library |The main library of the RTC SDK, used to implement basic audio and video calling functions. | |
|RTCFFmpeg.framework |ALL |Yes |Video/Image Decoding |FFmpeg is an open\-source multimedia processing library used for handling audio, video, and other multimedia data. RTCFFmpeg.framework is based on the open\-source FFmpeg source code with some modifications, such as feature pruning. | |
|libbytenn.dylib |v3.50 |Yes |AI Engine Plugin |The high\-performance heterogeneous inference engine framework bytenn, independently developed by BytePlus, provides unified multi\-platform rapid deployment capabilities for AI businesses. Suitable for AI noise reduction, music scene detection, video super\-resolution, denoising, HDR, MOS, and other application scenarios. | |
|libeffect.dylib |ALL |No |Video Effects Library |The intelligent beautification effects SDK independently developed by BytePlus, which can add beauty, filters, stickers, and other effects to locally captured videos. After integration, you can call enableVideoEffect and other interfaces to use video effects related functions. | |
|ByteRTCNICOExtension.framework |v3.52 |No |Audio Codec Plugin |The RTC self\-developed audio codec plugin. The NICO audio codec algorithm has stronger anti\-weak network capabilities compared to the native Opus audio codec and is fully compatible with Opus. Suitable for application scenarios with strong demands for low stutter and low latency in voice calls. If you need to use this feature, please contact technical support. | |
|ByteRTCFFmpegAudioExtension.framework |v3.54 |No |Audio Decoder Plugin |An audio decoder plugin compiled based on FFmpeg, supporting SDK audio memory playback functionality, capable of decoding audio files in mp3, mp4, aac, m4a, 3gp, wav, ogg, ts, wma formats, and providing better compatibility for audio file playback functions. | |
| | | | |If you need to use memory playback functionality, or encounter compatibility issues when playing audio files, you can choose to integrate this plugin. After integration, the SDK will use the ffmpeg audio plugin for decoding by default, without the need for additional settings; if you do not integrate this plugin, the SDK will use the system library for decoding by default. | |
|libbdaudioeffect.dylib |v3.56 |No |Audio Technology Plugin |Audio technology (Speech, Audio & Music Intelligence, referred to as SAMI), mainly dedicated to the research and application of voice synthesis, audio understanding and processing, music understanding and editing, music generation, and other technologies. | |
| | | | |To use voice change and K\-song scoring features, you need to integrate this plugin. After integration, you can call [setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70092#setvoicechangertype) to use the voice change feature; call getSingScoringManager and ByteRTCSingScoringManager class methods to use K\-song scoring related functions. | |


<span id="integration-method"></span>
## Integration Method

Download and unzip the [macOS SDK package](https://docs.byteplus.com/en/docs/12/docs-75707), then drag the main library and the required plugin files into the main project. Configure the Embed property of the selected library in the project to `Embed & Sign`.

<span id="linux"></span>
# Linux

<span id="plugin-details"></span>
## Plugin Details


|Library/Plugin Name |Starting Version |Required |Library/Plugin Function |Description |
|---|---|---|---|---|
|libbytenn.so |v3.52 |Yes |AI Engine Plugin |The high\-performance heterogeneous inference engine framework bytenn, independently developed by BytePlus, provides unified multi\-platform rapid deployment capabilities for AI services. Suitable for AI noise reduction, music scene detection, video super\-resolution, denoising, HDR, MOS, and other application scenarios. |
|libbytertc_ffmpeg_audio_extension.so |v3.54 |No |Audio Decoder Plugin |An audio decoder plugin compiled based on FFmpeg, supporting SDK audio memory playback functionality, capable of decoding audio files in mp3, mp4, aac, m4a, 3gp, wav, ogg, ts, wma formats, and providing better compatibility for audio file playback functions. If you need to use memory playback functionality, or encounter compatibility issues when playing audio files, you can choose to integrate this plugin. |
|libbytertc_nico_extension.so |v3.52 |No |Audio Codec Plugin |The RTC self\-developed audio codec plugin. The NICO audio codec algorithm has stronger anti\-weak network capabilities compared to the native Opus audio codec and is fully compatible with Opus. Suitable for application scenarios with strong demands for low stutter and low latency in voice calls. If you need to use this feature, please contact technical support. |
|libbytevc1enc.so |v3.57 |No |Video Codec Plugin |It is a dynamic link library file that provides video encoding and decoding functionality. This file is part of the VC1 video encoder, used for encoding and decoding video content. If you need to use this feature, please contact technical support. |
|libRTCFFmpeg.so |ALL |Yes |Video/Image Decoding |FFmpeg is an open\-source multimedia processing library used for handling audio, video, and other multimedia data. libRTCFFmpeg.so is based on the open\-source FFmpeg source code with some modifications, such as feature pruning. |
|libBytePlusRTC.so |ALL |Yes |Main Library |The main library of the RTC SDK, used to implement basic audio and video calling functions. |


<span id="integration-method"></span>
## Integration Method

Integrate using your build tool based on the provided header files and dynamic libraries.
