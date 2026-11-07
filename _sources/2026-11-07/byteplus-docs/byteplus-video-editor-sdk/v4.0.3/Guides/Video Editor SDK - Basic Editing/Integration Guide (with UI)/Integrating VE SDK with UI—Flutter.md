---
title: "Integrating VE SDK with UI—Flutter"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-flutter-ve-sdk"
---

This article demonstrates how to integrate BytePlus Video Editor SDK into your Flutter application, enabling you to develop cross\-platform applications for Android, iOS, Linux, macOS, and Windows. By utilizing this UI\-extensive integration method, you can use a variety of UI packages included in our CKOne sample code, and directly incorporate most of the sample code into your project.

<span id="6c6ee097"></span>
# **Prerequisites**

Before you begin, ensure that the following system requirements are met:


|**Name** |**Description** |
|---|---|
|**Flutter** |* Android Studio or VSCode.<br><br>* Supports Flutter SDK 2.0 and later. |
|**Android** |* Gradle: 6.7.1<br><br>* Android Gradle Plugin: com.android.tools.build:gradle:4.1.3<br><br>* kotlin: 1.5.30<br><br>* minSdkVersion: 21<br><br>* targetSdkVersion: 30<br><br>* compileSdkVersion: 30 |
|**iOS** |* Supports Xcode 9.0 and later.<br><br>* Supports iOS 9.0 and later, as well as iPhone 6s and later. |


<span id="c14d387f"></span>
# Flutter project structure

In this section, you will learn more about the integration process of Video Editor SDK within the Flutter framework and its sample code directory structure. This will help you understand how to integrate and use Video Editor SDK in your own application.

<span id="9de9a4ad"></span>
## Video Editor SDK Flutter framework

Here is a diagram that shows the integration process of Video Editor SDK within the Flutter framework.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4645dac8cd745bbbd0f5402217fb134~tplv-goo7wpa0wc-image.image" width="450px" /></div>


<span id="82c37587"></span>
## CKOne sample code directory structure

This section helps you learn more about CKOne sample code directory structure for Flutter, Android, and iOS applications.

<span id="f3a12679"></span>
### CKOne **Flutter** structure

The directory structure of the CKOne project file aligns with the standard Flutter structure. Major contents are located in the `android` and `ios`directory.

```Bash
├── README.md
├── analysis_options.yaml
├── android
├── build
├── ios
├── lib
├── pubspec.lock
├── pubspec.yaml
└── test
```


<span id="432c125f"></span>
### CKOne Android structure

The directory structure of the CKOne project file for Android is shown in the figure below.

```JSON
├── .gradle
├── app            (Modules that interact with flutter)
├── ck             (The directory where the BytePlus VE SDK is located)
│   ├── draft          (draft box module)
│   ├── editor-res    （Resources needed for the built-in VE SDK, in editing module）
│   ├── record-res    （Resources needed for the built-in VE SDK, in shooting/recording mo
│   ├── module_api    （Individual module API layer code）
│       └── cutsame-api
│   ├── module_business
│       ├── editor    （Editing module DemoCode）
│       └── recorder  （Shooting/recording module DemoCode）
├── gradle
├── gradle-config      (self-customized gradle configuration file directory)
    ├── version.gradle (Declare all dependency version numbers that will "force" at build time)
├── build.gradle       (Build configuration information for the main project)
├── gradle.properties  (SDK-related configuration information)
├── gradlew
├── gradlew.bat
└── settings.gradle  （The configuration introduced by each model in the SDK）
```


The CKOne demo project file for Android (directory name: `ck_flutter`) should be imported into the `app/src/main/java/com/example/ve_demo_for_flutter` directory. The directory structure of `ck_flutter` is shown in the figure below.

```JSON
├── CKApplication        (inherits from FlutterApplication, does pre-processing and initialization logic for copying resources)
├── CKChannelHelper      (core implementation of MethodChannel communication)
├── CKEntranceActivity   (inherited from FlutterFragmentActivity, business processing after MethodChannel communication)
├── CKHomeDelegate       (Wrapper class implemented by calling SDK interface, including permission request and local resource determination)
├── ICKHomeDelegate      (Definition of calling the SDK interface)
└── ICKMethodChannel     (Communication between CKChannelHelper and CKEntranceActivity)
```


<span id="24965400"></span>
### CKOne iOS structure

The directory structure of the CKOne project file for iOS is shown in the figure below.

```Bash
├── CK
│   ├── CKBaseKit-iOS 「Contains basic UI packages and Foundation」
│   ├── CKCommon-iOS 「Contains resources and sample service」
│   ├── CKEditor 「Contains configuration files for SDK initialization」
│   ├── CKRRecorder 「Recording and duet module」
│   ├── DVEAlbum-iOS 「Album」
│   ├── CKi18n 「Internationalization strings」
│   ├── DVEFoundationKit 「Contains some general basic classes」
│   ├── DVETrackKit「Track area in the editor」
│   └── NLEEditor-iOS 「Editor Module」
```


The detailed description of the `CK` directory is as follows:


|**Name** |**Description** |
|---|---|
|CKBaseKit\-iOS |Contains basic capacities and UI packages. |
|CKCommon\-iOS |Contains resource directory and sample service. |
|CKEditor |The entry point for Video Editor SDK initialization. |
|CKRRecorder |The module for recording and duet. |
|DVEAlbum\-iOS |Stores pictures. |
|CKi18n |Contains internationalization strings. |
|DVEFoundationKit |Contains some general basic classes. |
|DVETrackKitis |The track area for the editor. |
|NLEEditor\-iOS |The editor module. |


The CKOne demo project file for iOS (directory name: `CKFlutter`) contains demo project files to implement `MethodChannel` on iOS applications.

<span id="62b228b5"></span>
# Getting started with Video Editor SDK

Get started with Video Editor SDK by completing the following tasks:


1. Downloading Flutter Demo project & BytePlus Video Editor SDK.

2. Running the demo project.

3. Integrating Video Editor SDK.

4. Initializing Video Editor SDK.


<span id="af58c8f1"></span>
## Step 1: Downloading Flutter Demo project & BytePlus Video Editor SDK

To download the Flutter demo project, contact the BytePlus Video Editor SDK team.

<span id="8c0f0aee"></span>
## Step 2: Running the demo project

Run the demo project for your Android or iOS application by following the steps below.

<span id="9d1b3005"></span>
### Android

**To run the demo project on an Android device**:


1. Open the demo project for Android with Android Studio.

2. In `gradle.properties`, configure the Maven account details.

   **EXAMPLE**

   ```JSON
   MAVEN_USER_NAME=your_user_name
   MAVEN_PASS_WORD=your_password
   ```
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18d77ceda2194cf6834e446770f8efbc~tplv-goo7wpa0wc-image.image" width="742px" />   </div>
   

3. (Optional) In `local.properties`, configure Android SDK and Flutter SDK path.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A running project automatically configures Android SDK and Flutter SDK path and generates the <code>local.properties</code> file according to the local environment. If you find the Android SDK and Flutter SDK path are not properly configured in your project, follow this step to modify the configuration.   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5121dc758b8e4775b8377393d48bc82c~tplv-goo7wpa0wc-image.image" width="720px" />   </div>
   

4. Select an Android device and click the play icon.

   The demo project now runs on your Android device.


<span id="d36680e1"></span>
### iOS

**To run the demo project on an iOS device**:


1. Open the CKFlutter demo project with Android Studio or VSCode.

2. Click **Tools** \> **Flutter**.

3. Select the following: **Flutter Clean**, **Flutter Pub Get**, and **Flutter Pub Upgrade**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dda9a060a71457a924856909247c06a~tplv-goo7wpa0wc-image.image" width="550px" />   </div>
   

4. At the same directory level as `Podfile`, run `pod update` by using the following code.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de549307bf374d3b8670d38ad7b54647~tplv-goo7wpa0wc-image.image" width="350px" />   </div>
   

   ```Bash
   cd ios
   pod update
   ```
   

   If you receive an error as shown in the figure below, return to the previous step and make sure that **Flutter Pub Get** is selected.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50aac46e01b44820aabbee70fe7197a6~tplv-goo7wpa0wc-image.image" width="620px" />   </div>
   

5. Enter your own developer certificate in the **Signing Certificate Apple Development** field.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1b3dcd3195a4148906dd2a9382d7040~tplv-goo7wpa0wc-image.image" width="632px" />   </div>
   

6. Select an iOS device and click the play icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67489025883244a7ac6d004f0e7e2fc3~tplv-goo7wpa0wc-image.image" width="1000px" />   </div>
   

   The demo project now runs on your iOS device.


<span id="94e9be87"></span>
## Step 3: Integrating Video Editor SDK

Integrate Video Editor SDK into your Android or iOS applications by following the steps below.

<span id="55d19099"></span>
### Integrating Video Editor SDK for Android

**To integrate Video Editor SDK into your Android applications**:


1. Under the `android` directory of the Flutter Demo project file, locate the the `ck` file and import it to the `android` directory of your project.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11fc237e91274dbd8278036f3c07b25c~tplv-goo7wpa0wc-image.image" width="656px" />   </div>
   

2. Import the `ck_flutter` to the `app/src/main/java/com/example/ve_demo_for_flutter` directory of your project.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8f4f2f708af4399b4e66c0a27272508~tplv-goo7wpa0wc-image.image" width="510px" />   </div>
   

3. In `CKApplication`, modify the path of the CKFlutter package.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d30c33137a94c9280765c3751cbd203~tplv-goo7wpa0wc-image.image" width="716px" />   </div>
   

4. In `AndroidManifest.xml`, import `xmlns:tools` files.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ced1d4424e0422895e89d19e8cad291~tplv-goo7wpa0wc-image.image" width="712px" />   </div>
   

5. In `AndroidManifest.xml`, modify the `application` and main `Activity` files.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you already have <code>application</code> and main <code>Activity</code> files, copy your corresponding business logic to the<code>application</code> and <code>Activity</code>field.   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d8ab88bcffb45a5915e764874309e24~tplv-goo7wpa0wc-image.image" width="748px" />   </div>
   

6. In `themes.xml`, modify the `style` file.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9f3b37ccbd743b3b33572d4f86ee228~tplv-goo7wpa0wc-image.image" width="742px" />   </div>
   

7. Under the `main` directory, create an `assets` folder and import the license files to the directory as shown in the figure below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The directory hierarchy must not be changed.   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b44a1279cd84708b251bc671ddbe732~tplv-goo7wpa0wc-image.image" width="350px" />   </div>
   

8. Under the`app` directory, locate the `build.gradle`file and modify it with the following code.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9808df5ceaf7422abd94028a8b1df943~tplv-goo7wpa0wc-image.image" width="350px" />   </div>
   

   **EXAMPLE**

   ```JSON
   plugins {
       id 'com.android.application'
       id 'kotlin-android'
       id 'kotlin-android-extensions'
       id 'kotlin-kapt'
       id 'com.bytedance.news.common.service-manager'
   }
   android {
       ndkVersion rootProject.ext.ndkVersion
       compileSdkVersion rootProject.ext.compileSdkVersion
   
       compileOptions {
           sourceCompatibility JavaVersion.VERSION_1_8
           targetCompatibility JavaVersion.VERSION_1_8
       }
       
       defaultConfig {
           configurations.all {
               resolutionStrategy { force 'androidx.window:window-java:1.0.0-alpha10' }
           }
           applicationId "com.bytedance.solution.ck"
           minSdkVersion rootProject.ext.minSdkVersion
           targetSdkVersion rootProject.ext.targetSdkVersion
           versionCode flutterVersionCode.toInteger()
           versionName flutterVersionName
       
           ndk {
               abiFilters "armeabi-v7a", "arm64-v8a"
           }
           addBuildConfig("PRODUCT_TYPE")
       }
       
       kotlinOptions {
           jvmTarget = '1.8'
       }
       lintOptions {
           checkReleaseBuilds false
           abortOnError false
       }
       
       packagingOptions {
           pickFirst 'lib/arm64-v8a/libc++_shared.so'
           pickFirst 'lib/armeabi-v7a/libc++_shared.so'
           pickFirst 'lib/arm64-v8a/libNLEEditorJni.so'
           pickFirst 'lib/armeabi-v7a/libNLEEditorJni.so'
           pickFirst 'lib/arm64-v8a/libNLETemplateModelJni.so'
           pickFirst 'lib/armeabi-v7a/libNLETemplateModelJni.so'
           pickFirst 'lib/arm64-v8a/libDavinciResourceJni.so'
           pickFirst 'lib/armeabi-v7a/libDavinciResourceJni.so'
           pickFirst 'lib/arm64-v8a/libNLEResourcesDAVJni.so'
           pickFirst 'lib/armeabi-v7a/libNLEResourcesDAVJni.so'
           pickFirst 'lib/armeabi-v7a/libNLEMediaJni.so'
       
           pickFirst 'lib/arm64-v8a/libGamePlayJni.so'
           pickFirst 'lib/armeabi-v7a/libGamePlayJni.so'
       
           pickFirst 'lib/arm64-v8a/libMediaDelegatesJni.so'
           pickFirst 'lib/armeabi-v7a/libMediaDelegatesJni.so'
       
           pickFirst 'lib/armeabi-v7a/libThreeDVideoJni.so'
           pickFirst 'lib/arm64-v8a/libThreeDVideoJni.so'
       
           pickFirst 'lib/armeabi-v7a/libCutSameConsumerJni.so'
           pickFirst 'lib/arm64-v8a/libCutSameConsumerJni.so'
       }
   }
   
   dependencies {
       api rootProject.ext.libs["media-picker"]
       implementation project(':editor-res')
       implementation project(':record-res')
       implementation project(':draft')
       implementation project(":cutsame-api")
       implementation project(":verecorder")
       implementation project(":editor-main")
       kapt "com.bytedance.news.common:service-manager-processor:1.0.9"
   }
   
   def addBuildConfig(String key) {
       def value = project.findProperty(key)
       if (value instanceof String && !((String) value).isEmpty()) {
           project.android.defaultConfig.buildConfigField("String", key, "\"${value}\"")
       }
   }
   ```
   

9. Under the `android`directory, locate the `build.gradle` file and add the following configurations.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbb128e2f050460c89ac57ee73cebc71~tplv-goo7wpa0wc-image.image" width="726px" /></div>



10. In the `gradle.properties` file, add SDK\-related configurations as shown in example below.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fafedb4ff6a24f219af07dbde848b9f3~tplv-goo7wpa0wc-image.image" width="350px" /></div>


**EXAMPLE**

```JSON
org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8
kotlin.code.style=official
android.useAndroidX=true
android.enableJetifier=true

NLE_VERSION=4.0.0
VESDK_VERSION=11.8.1.16-release-tob
CUTSAME_IF_VERSION=0.0.0.3
VERSION_CODE=400000
VERSION_NAME=4.0.0
ENABLE_CUTSAME=false
USE_LOCAL_RES=true
PRODUCT_TYPE=Lite
MAVEN_USER_NAME=your_user_name
MAVEN_PASS_WORD=your_password
```



11. In the `settings.gradle` file, add references to Video Editor SDK.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4a79eca1ea8448aaa66252ae0fe95cb~tplv-goo7wpa0wc-image.image" width="350px" /></div>


**EXAMPLE**

```JSON
include ':app'
include ':editor-res'
project(":editor-res").projectDir = new File(rootDir, "ck/editor-res")

include ':record-res'
project(":record-res").projectDir = new File(rootDir, "ck/record-res")

include ':draft'
project(":draft").projectDir = new File(rootDir, "ck/draft")

include ':editor-main'
project(":editor-main").projectDir = new File(rootDir, "ck/module_business/editor/editor-main")

include ':editor-components'
project(":editor-components").projectDir = new File(rootDir, "ck/module_business/editor/editor-components")

include ':editor-core'
project(":editor-core").projectDir = new File(rootDir, "ck/module_business/editor/editor-core")

include ':editor-btmpanel'
project(":editor-btmpanel").projectDir = new File(rootDir, "ck/module_business/editor/editor-btmpanel")

include ':editor-preview'
project(":editor-preview").projectDir = new File(rootDir, "ck/module_business/editor/editor-preview")

include ':editor-trackpanel'
project(":editor-trackpanel").projectDir = new File(rootDir, "ck/module_business/editor/editor-trackpanel")

include ':editor-uibase'
project(":editor-uibase").projectDir = new File(rootDir, "ck/module_business/editor/editor-uibase")

include ':res-manager'
project(":res-manager").projectDir = new File(rootDir, "ck/module_business/recorder/res-manager")

include ':verecorder'
project(":verecorder").projectDir = new File(rootDir, "ck/module_business/recorder/verecorder")

include ':cutsame-api'
project(":cutsame-api").projectDir = new File(rootDir, "ck/module_api/cutsame-api")
```



12. Import the `gradle-config` folder which contains the `version.gradle` file into your `android` directory.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63399f5f40ed4b2dbb85bdf8683881d4~tplv-goo7wpa0wc-image.image" width="350px" /></div>



13. In `gradle.properties`, modify the `MAVEN_USER_NAME` and `MAVEN_PASS_WORD` as well as the `PRODUCT_TYPE`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b957b37a4a249e6a66931a85422f76d~tplv-goo7wpa0wc-image.image" width="704px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88241a7500c7437a99b2f0c315b4007b~tplv-goo7wpa0wc-image.image" width="712px" /></div>



14. In `CKApplication`, set `veLicensePath` to the actual filepath.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/787f0f13238c4b44989142d384c5ff36~tplv-goo7wpa0wc-image.image" width="714px" /></div>



15. In the top navigation bar, click the play icon to run your entire programme.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63cf806d01454d7c8af6c3e0cbee6b3b~tplv-goo7wpa0wc-image.image" width="1000px" /></div>


<span id="525362fc"></span>
### Integrating Video Editor SDK for iOS

**To integrate Video Editor SDK into your iOS applications**:


1. Import the BytePlus Video SDK file (directory name: `CK`) into your Flutter\-generated iOS project directory.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Video Editor SDK file to be imported is located at the same directory level as the<code>Podfile</code>.   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2198ef9bd31c4a3e96ec7c3e07ae446b~tplv-goo7wpa0wc-image.image" width="704px" />   </div>
   

2. Under the `ios` directory of the Flutter Demo project file, open the `Podfile`.

   If you don't have a `Podfile`, import `fluttertoast: ^8.1.2` to `pubspec.yaml`. After `Flutter Pub Upgrade` is selected successfully, delete `fluttertoast: ^8.1.2`.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d6aa6827571480e82ed4f36764b1515~tplv-goo7wpa0wc-image.image" width="508px" />   </div>
   

3. Modify the `Podfile` using the following configurations.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the sample code below, the content between the <strong>Begin</strong> and <strong>End</strong> sections represents newly added content.   </div>
   

   **EXAMPLE**

   ```Ruby
   # Uncomment this line to define a global platform for your project
   # platform :ios, '11.0'
   
   # CocoaPods analytics sends network stats synchronously affecting flutter build latency.
   ENV['COCOAPODS_DISABLE_STATS'] = 'true'
   
   project 'Runner', {
     'Debug' => :debug,
     'Profile' => :release,
     'Release' => :release,
   }
   
   def flutter_root
     generated_xcode_build_settings_path = File.expand_path(File.join('..', 'Flutter', 'Generated.xcconfig'), __FILE__)
     unless File.exist?(generated_xcode_build_settings_path)
       raise "#{generated_xcode_build_settings_path} must exist. If you're running pod install manually, make sure flutter pub get is executed first"
     end
   
     File.foreach(generated_xcode_build_settings_path) do |line|
       matches = line.match(/FLUTTER_ROOT\=(.*)/)
       return matches[1].strip if matches
     end
     raise "FLUTTER_ROOT not found in #{generated_xcode_build_settings_path}. Try deleting Generated.xcconfig, then run flutter pub get"
   end
   
   require File.expand_path(File.join('packages', 'flutter_tools', 'bin', 'podhelper'), flutter_root)
   
   flutter_ios_podfile_setup
   
   ##################################### Begin #####################################
   def base_pods
     pod 'TTVideoEditor', '11.8.1.43-D',:source => 'https://github.com/volcengine/volcengine-specs.git'
     pod 'NLEPlatform', '0.5.4', :source => 'https://github.com/volcengine/volcengine-specs.git'
     pod 'DVEInject', '0.0.5', :source => 'https://github.com/volcengine/volcengine-specs.git'
     # support international
     pod 'CKi18n', :path => 'CK/CKi18n'
     pod 'CKBaseKit', :subspecs => ['UI'], :path => 'CK/CKBaseKit-iOS'
     pod 'DVEAlbum', :path => 'CK/DVEAlbum-iOS'
   end
   
   # Edit
   def editor_pods
     base_pods
     
     pod 'NLEEditor', :subspecs => ['CK'], :path => 'CK/NLEEditor-iOS'
     pod 'DVETrackKit', :subspecs => ['CK'], :path => 'CK/DVETrackKit'
     pod 'DVEFoundationKit', :path => 'CK/DVEFoundationKit'
     pod 'CKEditor', :path => 'CK/CKEditor', :subspecs => ['Arch']
   
     ############# public pods #############
     pod 'SGPagingView', '~> 1.7.1'
     pod 'KVOController','~> 1.2.0'
     pod 'Masonry','~> 1.1.0'
     pod 'ReactiveObjC', '~> 3.1.1'
     pod 'YYWebImage', '~> 1.0.5'
     pod 'YYImage', '~> 1.0.4'
     pod 'YYModel', '~> 1.0.4'
     pod 'MBProgressHUD', '~> 1.2.0'
     pod 'lottie-ios', '~> 2.5.3'
     pod 'SDWebImage', '~> 5.11.1'
     pod 'Toast', '~> 4.0.0'
     pod 'MJExtension', '~> 3.4.1'
     pod 'MJRefresh', '~> 3.6.1'
     pod 'PocketSVG', '~> 2.7.0'
     pod 'IGListKit', '~> 4.0.0'
     pod 'IGListDiffKit', '~> 4.0.0'
     pod 'FileMD5Hash', '~> 2.0.0'
   end
   
   # Record
   def recorder_pods
       base_pods
       pod 'CKRRecorder', :subspecs => ['Base','Duet'], :path => 'CK/CKRRecorder'
   end
   
   target 'Runner' do
     pod 'CKService', :subspecs => ['WebImageImpl','AlertImpl'], :path => 'CK/CKCommon-iOS'
     # resource
     pod 'CKResource', :subspecs => ['Editor'], :path => 'CK/CKCommon-iOS'
     editor_pods
     recorder_pods
   
     flutter_install_all_ios_pods File.dirname(File.realpath(__FILE__))
   end
   
   
   post_install do |installer|
     installer.pods_project.targets.each do |target|
       flutter_additional_ios_build_settings(target)
     end
   
     installer.generated_projects.each do |project|
       project.targets.each do |target|
         target.build_configurations.each do |config|
           # [Xcode 14 build failed with manual code sign and app resource bundles](https://github.com/CocoaPods/CocoaPods/issues/11402)
           config.build_settings['CODE_SIGN_IDENTITY'] = '-'
           config.build_settings['CODE_SIGN_ENTITLEMENTS'] = '-'
           config.build_settings['CODE_SIGNING_REQUIRED'] = 'NO'
           config.build_settings['CODE_SIGNING_ALLOWED'] = 'NO'
         end
       end
       # Configure warning notifications 
       project.build_configurations.each do |config|
         config.build_settings['CLANG_WARN_DOCUMENTATION_COMMENTS'] = 'NO'
   
         config.build_settings['WARNING_CFLAGS'] = '-Wno-strict-prototypes -Wno-swift-name-attribute -Wno-comment -Wno-shorten-64-to-32 -Wno-unused-function -Wno-unused-variable -Wno-nullability -Wno-nullability-completeness -Wno-documentation -Wno-documentation-html -Wno-incomplete-umbrella'
   
         if project.targets.first.name.start_with?("NLEPlatform")
           config.build_settings['GCC_WARN_INHIBIT_ALL_WARNINGS'] = "YES"
         end
   
         if project.targets.first.name.start_with?("NLEEditor") || project.targets.first.name.start_with?("DVETrackKit")
           config.build_settings['WARNING_CFLAGS'] = '-Wno-strict-prototypes -Wno-swift-name-attribute -Wno-comment -Wno-shorten-64-to-32 -Wno-unused-function -Wno-unused-variable -Wno-nullability -Wno-nullability-completeness -Wno-documentation -Wno-documentation-html -Wno-ambiguous-macro'
         end
       end
     end
   end
   
   ##################################### End #####################################
   ```
   

4. (Optional) If your project is in Swift language, perform the following steps to ensure that the Video Editor SDK runs properly on your application:

   1. In `Podfile`, replace `use_frameworks!` with `use_modular_headers!`.

   2. Set `:modular_headers` to false for all provided components.

      **EXAMPLE**

   ```Ruby
   use_modular_headers!
   
   target 'Runner' do
   pod 'NLEEditor', :subspecs => ['CK'], :path => 'CK/NLEEditor-iOS', :modular_headers => false
   pod 'DVETrackKit', :subspecs => ['CK'], :path => 'CK/DVETrackKit', :modular_headers => false
   pod 'DVEFoundationKit', :subspecs => ['CK'], :path => 'CK/DVEFoundationKit', :modular_headers => false
   pod 'CKEditor', :path => 'CK/CKEditor', :modular_headers => false
   pod 'CKi18n', :path => 'CK/CKi18n', :modular_headers => false
   pod 'CKRRecorder', :subspecs => ['Arch'], :path => 'CK/CKRRecorder', :modular_headers => false
   # ...
   end
   ```
   

5. At the same directory level as `Podfile`, run `pod update`.

6. In Xcode, click **TARGETS** \> **Project Name** \> **Build Setting** \> **Build Options**.

7. Select the **All** information tab and search for **bitcode** in the search field.

8. Set Enable Bitcode to **No**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/177475f4e4c6451eb2f2b368ca9d4ab1~tplv-goo7wpa0wc-image.image" width="550px" />   </div>
   

9. Import the `CKFlutter` demo file project into your Xcode project.

   1. Drag and drop `CKFlutter` file into your project.

      
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7c1299b779b437a8d5477a4c99c34bc~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffce0ccd67aa483f92a44257b9f0c8eb~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02b73cef68dc4242bf4a1c5bfca0d685~tplv-goo7wpa0wc-image.image) </span> |
      |---|---|---|
      

   2. Open `AppDelegate`and add the following code.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edb990bf856647d4871f9ce9f82377a0~tplv-goo7wpa0wc-image.image" width="628px" />      </div>
      

      **EXAMPLE**

      ```objectivec
      #import "CKChannelHelper.h"
      
      // add channel
      NSObject<FlutterPluginRegistrar>* registrar = [self registrarForPlugin:@"ve"];
      [CKChannelHelper registerWithRegistrar:registrar];
      ```
      

10. Add permission descriptions.

11. Locate the `Info.plist` file of your project.

12. Add relevant permission descriptions.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/780a44a7073948e088f7e36ee0d17161~tplv-goo7wpa0wc-image.image" width="638px" />   </div>
   

   **EXAMPLE**

   ```JavaScript
   <key>NSCameraUsageDescription</key>
   <string>Use Camera</string>
   <key>NSMicrophoneUsageDescription</key>
   <string>Use Microphone</string>
   <key>NSPhotoLibraryAddUsageDescription</key>
   <string>Use Photo Libary</string>
   <key>NSPhotoLibraryUsageDescription</key>
   <string>Use Photo Library</string>
   ```
   

13. Modify the Bundle Identifier.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each SDK license is bound to the application's Bundle ID. If your Bundle Identifier does not start with <code>com.bytedance.solution.ck</code>, contact the Video Editor SDK team and change the license.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2505bdbf0ec4f4a907fe5525d7bdf64~tplv-goo7wpa0wc-image.image" width="506px" /></div>



12. Select an iOS device and click the play icon to run the project.

* **Android Studio**

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f04bcea9991f478d9fbfa4a30c045c44~tplv-goo7wpa0wc-image.image" width="1000px" />   </div>
   

* **Xcode**

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/253b09243ea34631b3416912e481126e~tplv-goo7wpa0wc-image.image" width="714px" />   </div>
   


<span id="1fa874af"></span>
## Step 4: Initializing Video Editor SDK

Call the `setupEngine` API to initialize Video Editor SDK.


* **API name**: \*\*\*\* setupEngine.

* **Interface description**: \*\*\*\* Initialization.


The following table contains a detailed description of each parameter required for initialization:


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|veAppKey |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |Video Editor SDK App Key. |
|veToken |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |Video Editor SDK Token. |
|subtitleAppId |String |No |AppKey for features such as text\-to\-speech (TTS) and text recognition. |
|subtitleToken |String |No |Token for features such as text\-to\-speech (TTS) and text recognition. |
|volcAccessKey |String |No |Access key for the music beat feature. |
|volcSecretKey |String |No |Secret key for the music beat feature. |


**EXAMPLE**

```Dart
MethodChannel _channel = const MethodChannel('ve');
//  setup sdk before jumping
var setupArguments = {
  "veAppKey" : "iiWwiXvXhlN",
   "veToken" : "cJ75jX6c9m8eObgQif7okMgb3U2398MrE1DCr1LH1neWx3x4BkL5hIqlRwbrC1Hf6aVQRcvSWrFuXbf8ROmHIHTz1X5daYyh6Gmb+J/cI1deUayXIgmE2KUIlYyjMgDHL0gbyUNl6+XJhspB1nZP6tHyDfBhSISdQ5Aq6/1zqilrPYJSjo547IkdVg2xfuhDACrbgs1iu9LqI7pHDc+JEOSTYuHA3Fe5aVyVkwBRqBNf1EgrsgMtZ1W1U2GAZpLMQke7DUvB7WDaAb+GdZSAcovLM8WjGzZiIV4Cj6YTFYBtNH3WfM15954YRcS1rOeYhPmZN7/N6yYmBBz3OZKx/sD8OyFk5cY6Q9PdaqDF14qPhUIy0rqX79tqxNwyOLnKYWR+e/8nrG2N8NDef9BZ7dDSREVkgiDl8ELmDgKYzraUxyy5MOV1hbITl6nieiuI/oeVu0z3snytsDt4yMyOdsaT3acngkJJhHX3tz2dh+R5v2diJW6+VsybE6166eJm5swVLAxqdn1wcQuPX64hKHXuc6SssjwddRKqMgKrCzHrGdW5IJKQC25lOdY4ENMnSV8HwRUaaEZQJPBIyC605H6VQCDwUTHGL4VKu5enIA/itdoYJY8lJ9YQ7ZSWFZO21gTaAPhEj1JuuToYg6wh9xIPgFhKbpLknJzweKKxyzgtM3Ndf6Z4czyFrCKhJgZm+yEkl5/CplXWJ/MZT2tH9yIjnZlySfUHZFwJtB78MNdrxd3p+ux/me2CK70uvSBAB7pXautnEEpQdkQ3TDSJEgMvMN1QGZ09LaDPOINWjH2xl2aNCFMkB7Q5p1AqJFu69tZjzwRorFvLETwJNpBXZSP9M660/86y5MRPhvbFgWIrZwhM6/sf66/3MoRyz5cmwQ9fiYNheTCPLs+TVAkvKulQFZnSF2PgcuEBgqFCR03pcS2wn6C/QjMbIIa8B26aImgPzBzi9WqEjZjoVrb1OxkkSsJZFpvLWXr1YQslRut4sR9zldy1BijVN2AJdKnP2D1Zu9za/HodeX7dskbe2tiTX4xbfNCFPbAvubtI9UlOMsTOTdmnG7GRPykSsEO1fPmIEx0YeSlf6M1whjRzPQhhhqs3cnn8QbhDcpRj/Big3+PWeNf7c+vPjPBSYbXIYS2cNE5grP56/1Pv+VqftNMQP5dHIQJ7A1iXPabP0VPsgrlpH5KnBe/bX4jDLgP4FUWG4jl/YroGO0ETSwUWboldc6ia45pgcOCibQ9Gx/PmGdP2JzYx6QyImo3TwbDrhWhCMqYtKgwpPo+UD9lh4Q=="};
_channel.invokeMethod<void>("setupEngine", setupArguments);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To make the most of the Video Editor SDK, we ensure that <code>veAppKey</code>, <code>veToken</code>, and <code>Bundle ID</code> are linked together. This way, you don't need different bundle IDs when starting the VE SDK on different platforms.</div>


<span id="376a443e"></span>
# Starting the UI interface

Once Video Editor SDK has been initialized, you can start the UI interface and begin using its functions. This section provides sample code for calling the editing, recording, and draft box pages as well as the callback after exporting video.

<span id="f7058377"></span>
## Editing page


* **API name**: \*\*\*\* toEditor.

* **Interface description**: \*\*\*\* Jump to the editor page.


**EXAMPLE**

```Dart
MethodChannel _channel = const MethodChannel('ve');

_channel.invokeMethod<void>("toEditor");
```


<span id="c8f0eb36"></span>
## Recording page


* **API name**: \*\*\*\* toRecord.

* **Interface description**: \*\*\*\* Jump to the recording page.


**EXAMPLE**

```Dart
MethodChannel _channel = const MethodChannel('ve');

_channel.invokeMethod<void>("toRecord");
```


<span id="9ed80ac0"></span>
## Draft box page


* **API name**: \*\*\*\* toDraft.

* **Interface description**: \*\*\*\* Jump to the draft box page.


**EXAMPLE**

```Dart
MethodChannel _channel = const MethodChannel('ve');

_channel.invokeMethod<void>("toDraft");
```


<span id="0ec3bf1c"></span>
## Callback after exporting video


* **API name**: \*\*\*\* exportVideoCallback.

* **Interface description**: \*\*\*\* Callback after exporting video.


**EXAMPLE**

```Dart
MethodChannel _channel = const MethodChannel('ve');

_channel.setMethodCallHandler((call) async {
  print("callback with method: " + call.method);
  var arguments = call.arguments;
  if (call.method == 'exportVideoCallback') {
    var result = arguments["result"];
    var videoPath = arguments["videoPath"];
    if (result == true && videoPath != null) {
      print("exportVideo success with video path " + videoPath.toString());
      return Future.value(true);
    }
  }
  return Future.value(false);
});
```


<span id="696f4b67"></span>
## UI testing full sample code

Refer to the full sample code below to learn how to validate the features supported by Video Editor SDK through UI interface.

```Dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

/// home page
class HomePage extends StatefulWidget {
  const HomePage({Key? key}) : super(key: key);
  @override
  State<StatefulWidget> createState() => _HomeState();
}

class _HomeState extends State<HomePage> {

  late MethodChannel _channel;
  @override
  void initState() {
    super.initState();
    _channel = const MethodChannel('ve');
    //  setup sdk before jumping
    var setupArguments = {
      "veAppKey" : "iiWwiXvXhlN",
      "veToken" : "cJ75jX6c9m8eObgQif7okMgb3U2398MrE1DCr1LH1neWx3x4BkL5hIqlRwbrC1Hf6aVQRcvSWrFuXbf8ROmHIHTz1X5daYyh6Gmb+J/cI1deUayXIgmE2KUIlYyjMgDHL0gbyUNl6+XJhspB1nZP6tHyDfBhSISdQ5Aq6/1zqilrPYJSjo547IkdVg2xfuhDACrbgs1iu9LqI7pHDc+JEOSTYuHA3Fe5aVyVkwBRqBNf1EgrsgMtZ1W1U2GAZpLMQke7DUvB7WDaAb+GdZSAcovLM8WjGzZiIV4Cj6YTFYBtNH3WfM15954YRcS1rOeYhPmZN7/N6yYmBBz3OZKx/sD8OyFk5cY6Q9PdaqDF14qPhUIy0rqX79tqxNwyOLnKYWR+e/8nrG2N8NDef9BZ7dDSREVkgiDl8ELmDgKYzraUxyy5MOV1hbITl6nieiuI/oeVu0z3snytsDt4yMyOdsaT3acngkJJhHX3tz2dh+R5v2diJW6+VsybE6166eJm5swVLAxqdn1wcQuPX64hKHXuc6SssjwddRKqMgKrCzHrGdW5IJKQC25lOdY4ENMnSV8HwRUaaEZQJPBIyC605H6VQCDwUTHGL4VKu5enIA/itdoYJY8lJ9YQ7ZSWFZO21gTaAPhEj1JuuToYg6wh9xIPgFhKbpLknJzweKKxyzgtM3Ndf6Z4czyFrCKhJgZm+yEkl5/CplXWJ/MZT2tH9yIjnZlySfUHZFwJtB78MNdrxd3p+ux/me2CK70uvSBAB7pXautnEEpQdkQ3TDSJEgMvMN1QGZ09LaDPOINWjH2xl2aNCFMkB7Q5p1AqJFu69tZjzwRorFvLETwJNpBXZSP9M660/86y5MRPhvbFgWIrZwhM6/sf66/3MoRyz5cmwQ9fiYNheTCPLs+TVAkvKulQFZnSF2PgcuEBgqFCR03pcS2wn6C/QjMbIIa8B26aImgPzBzi9WqEjZjoVrb1OxkkSsJZFpvLWXr1YQslRut4sR9zldy1BijVN2AJdKnP2D1Zu9za/HodeX7dskbe2tiTX4xbfNCFPbAvubtI9UlOMsTOTdmnG7GRPykSsEO1fPmIEx0YeSlf6M1whjRzPQhhhqs3cnn8QbhDcpRj/Big3+PWeNf7c+vPjPBSYbXIYS2cNE5grP56/1Pv+VqftNMQP5dHIQJ7A1iXPabP0VPsgrlpH5KnBe/bX4jDLgP4FUWG4jl/YroGO0ETSwUWboldc6ia45pgcOCibQ9Gx/PmGdP2JzYx6QyImo3TwbDrhWhCMqYtKgwpPo+UD9lh4Q=="};
    _channel.invokeMethod<void>("setupEngine", setupArguments);

    _channel.setMethodCallHandler((call) async {
      print("callback with method: " + call.method);
      var arguments = call.arguments;
      if (call.method == 'exportVideoCallback') {
        var result = arguments["result"];
        var videoPath = arguments["videoPath"];
        if (result == true && videoPath != null) {
          print("exportVideo success with video path " + videoPath.toString());
          return Future.value(true);
        }
      }
      return Future.value(false);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        crossAxisAlignment: CrossAxisAlignment.stretch,
        children: [
          TextButton(onPressed: () => _clickToEditor(),
              child: const Text('Gallery')),
          TextButton(onPressed: () => _clickToRecord(),
              child: const Text('Video')),
          TextButton(onPressed: () => _clickToDraft(),
              child: const Text('Draft')),
        ],
      ),
    );
  }

  void _clickToEditor() {
    _channel.invokeMethod<void>("toEditor");
  }

  void _clickToRecord() {
    _channel.invokeMethod<void>("toRecord");
  }

  void _clickToDraft() {
    _channel.invokeMethod<void>("toDraft");
  }
}
```


<span id="dadf4448"></span>
# Troubleshooting

This section helps you to learn more about how to troubleshoot and resolve problems you have encountered in Flutter, Android and iOS applications.

<span id="5d43ac4f"></span>
## Flutter

When debugging a Flutter project on a Mac environment, if you encounter a pop\-up box as shown in the figure below, you need to "trust the developer" , otherwise there will be a white screen on the home page.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d34af1cb8b9646229aa7a4c1d26ef2a8~tplv-goo7wpa0wc-image.image" width="350px" /></div>


**Trust the developer by completing the steps below**:


1. Click **System Preferences** \> **Privacy and Security**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f0cfa531242413f8a73876e51b3ac25~tplv-goo7wpa0wc-image.image" width="450px" /></div>



2. In the Security pane, grant permission to the iproxy application.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f142876007df42f194ee45bfa6ecc7c8~tplv-goo7wpa0wc-image.image" width="522px" />   </div>
   

3. In Android Studio, open the iproxy application again.

4. A pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57341b48724b4be88769a55999f6db30~tplv-goo7wpa0wc-image.image" width="280px" />   </div>
   

5. At the prompt, select **Open**.


When you need to switch platforms for debugging, it is recommended to execute `Flutter Clean` to clean up the environment and avoid abnormal problems. For example, after you complete debugging with an Android device, run `Flutter Clean` first and then proceed to debugging with an iOS device.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76cd6836d5aa4a8c898dca9dab7f58e0~tplv-goo7wpa0wc-image.image" width="638px" /></div>


<span id="d13e3989"></span>
## Android

This section provides solutions to resolve problems in your Android project, including invalid authentication after starting up, unavailable materials or assets, default setting configuration, and more. In this section, you will learn more about how to debug Android applications using Video Editor SDK.

<span id="98c8b5fd"></span>
### What should I do if the invalid authentication prompt appears after starting up?

**To fix the problem**:


1. In `FlutterPlugin.java`, check whether the token data is correct.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/891984e092a44d9da37aad6fdadfda57~tplv-goo7wpa0wc-image.image" width="686px" />   </div>
   

2. Under the `LicenseBag_bundel`directory, open the license file and check whether your SDK license corresponds with the`applicationId`.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b837ffe8ffb43d7901f1806a83cc347~tplv-goo7wpa0wc-image.image" width="704px" />   </div>
   

3. In`CKApplication`, check whether the path of the license file is correct.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27cce33d48c9431a886d52e2fa5b3f69~tplv-goo7wpa0wc-image.image" width="700px" />   </div>
   


<span id="e0417418"></span>
### What should I do if the materials or assets do not work?

**To fix the problem**:


* Prioritize the inspection of authentication files. For additional information on how to inspect the license files, refer to the previous solution.

* Check whether the imported clips and short videos match with the license file and `applicationId`.

* If all the above solutions do not work, send the console log the BytePlus Video Editor team.


<span id="46062f4a"></span>
### A conflict appears when I set my application's Target and Complie SDK version to 30. What should I do?

**To fix the problem**:

Configure the default setting of your application using the following code.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dcda632b8404ad8b1d05f20db75bf70~tplv-goo7wpa0wc-image.image" width="696px" /></div>


<span id="1942860b"></span>
### How do I replace assets?

You can integrate the editing and recording assets into the corresponding directory paths as shown in the figure below.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88fd2ec365ed4d12b036207585440d23~tplv-goo7wpa0wc-image.image" width="320px" /></div>


<span id="86064c0d"></span>
## iOS

This section provides solutions to resolve problems in your iOS project, including pod update execution failure, errors in Android Studio, logging, and more. In this section, you will learn more about how to debug iOS applications using Video Editor SDK.

<span id="20b3f871"></span>
### What should I do if the pod update or installation fails?

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adbc31a1d59f4cad8cfb84920af6c9e6~tplv-goo7wpa0wc-image.image" width="686px" /></div>


**To fix the problem**:


1. In Android Studio, click **Tools** \> **Flutter**.

2. Select the following: **Flutter Clean**, **Flutter Pub Get**, and **Flutter Pub Upgrade**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7e89dfce45a4d9085018d0977d3d7cc~tplv-goo7wpa0wc-image.image" width="472px" />   </div>
   


<span id="e85d5a3a"></span>
### What should I do if errors appear in Android Studio?

```C++
lib/main.dart:1
Automatically signing iOS for device deployment using specified development team in Xcode project: xxxxxx
Warning: CocoaPods not installed. Skipping pod install.
  CocoaPods is used to retrieve the iOS and macOS platform side's plugin code that responds to your plugin usage on the Dart side.
  Without CocoaPods, plugins will not work on iOS or macOS.
  For more info, see https://flutter.dev/platform-plugins
To install see https://guides.cocoapods.org/using/getting-started.html#installation for instructions.

Exception: CocoaPods not installed or not in valid state.
Exited (sigterm)
```


**To fix the problem**:


* Run `flutter run` in terminal.

* Close Android Studio and run `open /Applications/Android\ Studio.app` in terminal.


<span id="b675eb06"></span>
### How do I implement my own logging function?

When debugging, you can use NSLog by default or implement your own logging function. To facilitate troubleshooting, it is recommended to implement your own logging function that will write logs to the logging platform used by your application.

To implement your own logging function, refer to the logging section of troubleshooting in [Integrating VE SDK with UI—iOS](https://docs.byteplus.com/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-ios-ve-sdk-v.4.0.2). You can also modify the configuration in the `CKChannelHelper` file.

<span id="d377b17d"></span>
### How do I modify the SDK license?

You can modify the SDK license using the following methods:


*  **[Recommended]Method 1:**  Replace the default license with your own license. For details, refer to the license section of troubleshooting in [Integrating VE SDK with UI—iOS](https://docs.byteplus.com/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-ios-ve-sdk-v.4.0.2).

* **Method 2**: Modify the code of `VEChannelHelper` and pass the specific path using `veLicensePath`.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31f94fde071045e680355c546a8bb2a9~tplv-goo7wpa0wc-image.image" width="464px" />   </div>
   


<span id="98795325"></span>
### How do I replace resources?

For details, refer to the resource section of troubleshooting in [Integrating VE SDK with UI—iOS](https://docs.byteplus.com/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-ios-ve-sdk-v.4.0.2).

<span id="2df06e52"></span>
### What should I do if I fail to load the contents of the file list?

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78da145109f54fab89cdcdeeb5ff9225~tplv-goo7wpa0wc-image.image" width="640px" /></div>


**To fix the problem**:


1. In Android Studio, click **Tools** \> **Flutter**.

2. Select the following: **Flutter Clean** and **Flutter Pub Get**.
