---
title: "SDKs"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75707"
---

This document provides methods to integrate the RTC SDK on various platforms, allowing you to obtain the development kit via package managers or by manual download.

## Integrate RTC SDK Using Dependency Management Tools

### Android

To integrate the RTC SDK using Maven, follow these steps:

1. Include the following Maven configuration in the `build.gradle` file in your project's root directory:

   ```java
   allprojects {
       repositories {
           maven { url "https://artifact.byteplus.com/repository/public/" }
           google()
       }
   }
   ```

2. Include the following Maven configuration in `app/build.gradle`. We recommend that you specify a version number:

   ```java
   dependencies {
       ...
     implementation 'com.byteplus:BytePlusRTC:3.xx.x.xxx'
   }
   ```

   > **说明**

   > See [Download SDK](https://docs.byteplus.com/en/docs/12/14013#download-sdk) for the latest version. For previous versions, contact our technical support team.

3. Optional. You can remove any `.so` file that you don't need after integrating BytePlusRTC\-Release.aar. For example, the `libbytertc_ffmpeg_audio_extension.so` file is used for in\-memory playback and playing various audio file formats. If your application does not require these features, you can remove this extension to prevent unnecessary package growth.

   ```java
   android {
   ...
   packagingOptions {
           exclude 'lib/arm64-v8a/libbytertc_ffmpeg_audio_extension.so'
       }
   }
   ```

### iOS

To integrate the RTC SDK using CocoaPods, you can use the following configuration:

To integrate the specified version (Recommended):

```Plain
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
target '<YOUR_TARGET_NAME>' do
  pod 'BytePlusRTC', '3.xx.x.xxx'
end
```

Replace `<YOUR_TARGET_NAME>` with your actual iOS project target name.

> **说明**

> See [Download SDK](https://docs.byteplus.com/en/docs/12/14013#download-sdk) for the latest version. For previous versions, contact our technical support team.

### Flutter

You can integrate the Flutter plugin as a dependency. Go to the root directory of your project in the terminal, and run the command below.

```Plain
flutter pub add byteplus_rtc
```

This adds a dependency for the SDK to your project's `pubspec.yaml` file, as shown below:

```Plain
dependencies:
  byteplus_rtc: ^3.xx.x
```

> **说明**

> See [Download SDK](https://docs.byteplus.com/en/docs/12/14013#download-sdk) for the latest version. For previous versions, contact our technical support team.

If needed, run the following command to update the plugin to the latest version:

```Plain
flutter pub upgrade
```

When developing iOS applications using CocoaPods, add the following lines to your `Podfile`:

```Plain
target 'your target' do
  pod 'BytePlusRTC'
end
```

### Web

You can integrate the SDK by [npm](https://www.npmjs.com/package/@byteplus/rtc?activeTab=readme):

```powershell
npm install @byteplus/rtc --save
```

If you have an older version installed, you can update it to the latest version by running the following command:

```powershell
npm update @byteplus/rtc --save
```

### Electron

You can integrate the SDK by [npm](https://www.npmjs.com/package/@byteplus/byteplus-electron-sdk):

```powershell
npm install @byteplus/byteplus-electron-sdk --save
```

If you have an older version installed, you can update it to the latest version by running the following command:

```powershell
npm update @byteplus/byteplus-electron-sdk --save
```

### React Native

* Integrate the SDK by [npm](https://www.npmjs.com/package/@byteplus/react-native-rtc):

   ```powershell
   npm i @byteplus/react-native-rtc
   ```

* Integrate the SDK by [yarn](https://classic.yarnpkg.com/en/package/@byteplus/react-native-rtc):

   ```powershell
   yarn add @byteplus/react-native-rtc
   ```

## Download SDK

This documentation provides the latest version of RTC SDK. If you need older versions, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000762).

|Platform |SDK File |
|---|---|
|**Android** |[BytePlusRTC_Android_3.60.108.300.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261102060034-1115147221963.zip)<br> |
|**iOS** |[BytePlusRTC_iOS_3.60.108.700.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261102060110-1757152537654.zip)<br> |
|**macOS** |x86<br><br>[BytePlusRTC_macOS_x86_3.60.107.400.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260918072121-709274639120.zip)<br><br><br>ARM<br><br>[BytePlusRTC_macOS_arm_3.60.107.300.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260918072149-1363177027589.zip)<br> |
|**Windows** |Windows x86\-32<br><br>[VolcEngineRTC_Windows_3.60.107.2100_Win32.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260918072304-1200473807098.zip)<br><br><br>Windows x86\-64<br><br>[BytePlusRTC_Windows_3.60.107.2000_x64.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260918072330-1256183018330.zip)<br> |
|**Linux** |[BytePlusRTC_Linux_3.60.107.100_x86_64.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260918072349-1147752691625.zip)<br> |
|**Web** |[BytePlusRTC_Web_4.69.2_index.min.js](https://demo.volcvideo.com/exampleCenter/dynamicMarkdownManage/sourceFixedLink?queryType=sdk_version_source&amp;amp;reference_sdk_id=97&amp;amp;reference_sdkversion_id=4747)<br> |
|**Flutter** |[BytePlusRTC_Flutter_3.60.3](https://pub.dev/packages/byteplus_rtc/versions) |
|**Electron** |* macOS ARM64<br><br>   [BytePlusRTC_Electron_3.60.1_macOS_arm64.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261009020338-129030417405.zip)<br>   <br><br>* macOS x86\-64<br><br>   [BytePlusRTC_Electron_3.60.1_macOS_x86_64.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261009020431-1566680843365.zip)<br>   <br><br>* Windows x86\-64<br><br>   [BytePlusRTC_Electron_3.60.1_Windows_x86_64.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261009020617-1540269085639.zip)<br>   <br><br>* Windows x86\-32<br><br>   [BytePlusRTC_Electron_3.60.1_Windows_ia32.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261009020628-656305923813.zip)<br>    |
|**Unity** |[BytePlusRTC_Unity_3.58.1.unitypackage](https://demo.volcvideo.com/exampleCenter/dynamicMarkdownManage/sourceFixedLink?queryType=sdk_version_source&reference_sdk_id=133&reference_sdkversion_id=2230) |
|**React** |[React Native_1.2.0.zip](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2a1320699f140d98e85920ab0f8175b1.zip)<br> |
