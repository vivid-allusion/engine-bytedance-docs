---
title: "Integrating VE SDK with UI—Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-android"
---

This guide demonstrates how to integrate BytePlus Video Editor SDK into your Android application. This UI\-inclusive integration method allows you to refer extensively to the UI packages in our CKOne sample code. Using this method, you will directly copy most of the sample code to your project without having to write the video editing UI logic by yourself.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus Video Editor SDK is also known as CKOne or CK within the SDK file and sample code.</div>


<span id="1. Prerequisites"></span>
# **Prerequisites**

Before you begin, ensure that the following requirements are met:


* Your application is intended for devices that are Android 5.0 or later.

* You have obtained a valid Video Editor SDK license, key, and token.

* You have obtained the account username and password required to access Video Editor SDK, which is stored in a Maven repository. For more information about obtaining these credentials, contact your technical support manager.


<span id="d1202df2"></span>
# Video Editor SDK architecture

BytePlus Video Editor SDK consists of the following SDKs: VESDK, and NLE SDK. The table below summarizes the main function of each SDK.


|**Name** |**Package** |**Description** |
|---|---|---|
|VESDK |com.bytedance.ugc.framework.libs:vesdk |A media\-editing SDK, responsible for media rendering. |
|NLE SDK |com.volcengine.ck.nle:NLEMediaPublic |A non\-linear editing middleware SDK comprised of a set of media\-editing APIs. It is not responsible for media rendering or on\-screen display. |
||com.volcengine.ck.nle:NLEProcessor |An NLE SDK module, responsible for features such as smooth speed. |


<span id="aa65277e"></span>
# **CKOne sample code**

The CKOne sample code is required for the UI\-inclusive integration method for Android. In this section, you will learn more about the sample code runtime environment and directory structure, which will help you understand how to integrate and use Video Editor SDK in your own application.

<span id="6f55850c"></span>
## **CKOne sample code runtime environment**

The runtime environment for the CKOne sample code is as follows:

```Plain
Gradle：6.7.1
Android Gradle Plugin：com.android.tools.build:gradle:4.1.3
kotlin: 1.5.30

minSdkVersion: 21
targetSdkVersion: 30
compileSdkVersion: 30
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each supported runtime environment in Video Editor SDK is different.</div>


<span id="67537322"></span>
## CKOne sample code directory structure

The directory structure of the CKOne project file demonstrates how the sample code is organized. You can refer to the project file to understand how to integrate and use Video Editor SDK in your own application.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfc81915132e40a7ba8205bec4925428~tplv-goo7wpa0wc-image.image" width="213px" /></div>


The CKOne project file consists of the following top\-level files and modules.

```Shell
.
├── capture_cut    (Application section)
├── gradle
├── gradle-config
│   └── version.gradle (Declares all dependency version numbers and forces the building of dependency version numbers)
├── module_business
│   ├── base              （This section contains fundamental module components.）
│   ├── editor            （Sample code for the editing section.）
│   ├── editor-resource   （Internal resources utilized in the core editing section.）
│   ├── record-resource   （Built-in resources for the recording section, including stickers, filters, and beauty assets. ）
│   └── recorder          （Sample code for the recording segment.）
├── build.gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── settings.gradle
```


<span id="47b4895d"></span>
### Resource modules

The resource modules contain built\-in resources for video editing. Before integrating the source code, it's necessary to configure the `version.gradle` file. This file serves to centrally define the dependencies used by the SampleCode. The `version.gradle` is located within the `gradle-config` directory.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64c059ab2e2146d7b7a6c1060f5a0bf6~tplv-goo7wpa0wc-image.image" width="666px" /></div>


There are two resource modules, `editor-res` and `record-res`.

**editor\-i18n\-res**

`editor-i18n-res` contains built\-in resources required by Video Editor SDK.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32532c0658024d76a38aa5fb506caa38~tplv-goo7wpa0wc-image.image" width="315px" /></div>


The table below describes the types of resources stored in `editor-i18n-res`.


|**Name** |**Description** |
|---|---|
|LocalResource |Built\-in default resources that come with the sample code. They are not encrypted and can be used at will. |
|resource |Resources required by all features in Video Editor SDK, such as text stickers, filters, effects, and masks. You need to change these resources with your purchased resources. |


The table below describes the resource bundles stored in `editor-i18n-res`.


|**Name** |**Description** |
|---|---|
|ModelResource.bundle |Algorithm model files required by features such as chroma key and image matting. |
|adjust.bundle |Resources required by **Adjust**. |
|bubble.bundle |Resources required by **Text** \> **Add Text** \> **Bubble**. |
|canvas.bundle |Resources required by **Canvas** \> **Canvas Style**. |
|chroma.bundle |Resources required by **Edit** \> **Chroma Key**. |
|curve_speed.bundle |Resources required by **Edit** \> **Speed** \> **Curve Speed**. |
|flower.bundle |Resources required by **Text** \> **Add Text** \> **Flourish**. |
|mix.bundle |Resources required by **Edit** \> **Mixing Mode**. |
|sticker.bundle |Resources required by **Sticker**. |
|sticker_animation.bundle |Resources required by **Sticker** \> **Animation**. |
|text_align.bundle |Resources required by **Unused**. |
|text_animation.bundle |Text resources required by **Text** \> **Add Text** \> **Animation**. |
|text_color.bundle |Text resources required by **Text** \> **Add Text** \> **Color**. |
|text_fonts.bundle |Text resources required by **Text** \> **Add Text** \> **Font**. |
|text_style.bundle |Text resources required by **Text** \> **Add Text** \> **Style**. |
|text_template.bundle |Text resources required by **Text** \> **Text Template**. |
|tone.bundle |Resources required by **Audio** \> **Voice Change**. |
|transitions.bundle |Resources required by **Transition**. |
|ve_effect.bundle |Resources required by **Effect**. |
|ve_filter.bundle |Resources required by **Filter**. |
|video_animation.bundle |Resources required by **Edit** \> **Animation**. |
|video_mask.bundle |Resources required by **Edit** \> **Mask**. |


**record\-res**

`record-res` contains built\-in resources required by the recording page, including stickers, filters, and beauty effects resources. These resources are not included with Video Editor SDK and need to be purchased separately.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/901659f6be4547bc91de459bce4116ce~tplv-goo7wpa0wc-image.image" width="330px" /></div>


The table below describes the resource bundles stored in `record-res`.


|**Name** |**Description** |
|---|---|
|ComposeMakeup.bundle |Beauty and makeup resources. |
|duet.bundle |Duet resources required by **Home** \> **Duet**. |
|FilterResource.bundle |Filter resources required by **Record** \> **Filter**. |
|ModelResource.bundle |Effects algorithm model file. |
|StickerResource.bundle |Sticker resources required by **Record** \> **Prop**. |


<span id="0fac1a4f"></span>
### **Sample code modules**

All business\-related code within the Demo is located in the `module_business` folder. Additionally, we have organized distinct folders within `module_business` based on different business categories.

If you intend to reuse our sample code, you must copy and reference the Base module. As for the `editor-i18n` and `recorder` modules, along with their respective resource modules, you can selectively copy them according to your needs.


|**Module** |**Description** |**Requirements** |
|---|---|---|
|base |Some basic modules in the Sample Code, currently only the album module. |Required |
|editor |Sample code for the basic editing SDK. |Use when necessary. |
|editor\-resource |Built\-in resources used by the basic editing SDK. ||
|recorder |Sample code for the recording SDK. |Use when necessary. |
|record\-resource |Built\-in resources used by the recording SDK. ||


<span id="cd06c3b3"></span>
### **gradle.properties**

`gradle.properties` in the CKOne project file contains the following properties:


|**Field** |**Description** |
|---|---|
|android.useAndroidX=true |Gradle configuration. AndroidX libraries are used instead of Support libraries. |
|android.enableJetifier=true |Gradle configuration. Third\-party libraries will use AndroidX dependencies. |
|NLE_VERSION |NLE SDK version number. |
|VESDK_VERSION |VESDK version number. |
|CUTSAME_IF_VERSION |Magic Template SDK version number, which can be ignored if Magic Template SDK is not integrated. |
|VERSION_CODE |CKOne version code, which can be ignored. |
|VERSION_NAME |CKOne version name, which can be ignored. |
|MAVEN_USER_NAME |Username for the Maven repository, which is required to access the SDK. |
|MAVEN_PASS_WORD |Password for the Maven repository, which is required to access the SDK. |


<span id="7f29229f"></span>
# Getting started with Video Editor SDK

Get started with Video Editor SDK by completing the following tasks:


1. Integrating CKone SDK.

2. Initializing Video Editor SDK.

3. Starting the UI interface.

4. (Optional) Adding obfuscation rules.


<span id="0caef57d"></span>
# Integrating CKone SDK

Integrate Video Editor SDK into your Android application by completing the following steps:


1. Adding the sample code.

2. Configuring Gradle scripts.

3. Adding `ck_repos_high_agp` Plugin for AGP 7.1.0 in `settings.gradle`.

4. Adding the ServiceManager plug\-in.

5. Adding dependencies.


<span id="5. CKOne integration"></span>
## Step 1: Adding the sample code

You can directly copy the CKOne sample code to your project without having to write the video editing UI logic by yourself.

**To add the sample code:** 


1. Copy the codes in`module_business`into your project.

2. Configure the settings in `settings.gradle`.

3. \*\*(\*\*Optional) Depending on your project requirements, copy the draft box module.

4. Copy the `version.gradle` script from the `gradle-config`folder into your project.

5. Copy the license authentication files to the following filepath of your module's assets: `resource/LicenseBag.bundle/yourLicenseFile`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f51c2ddec7949e5826ae52237d86b99~tplv-goo7wpa0wc-image.image" width="532px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After configuring, it's not possible to change the file path for the licenses. It's important to ensure that you store the licenses in the correct folder.</div>


<span id="810bc19f"></span>
## Step 2: Configuring Gradle scripts

Configure the Gradle scripts in your project to enable Video Editor SDK to run properly. Refer to the following file for an example:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c03cf3ca5cf4103a3637ac548e64676~tplv-goo7wpa0wc-image.image" name="settings.gradle">settings.gradle</Attachment>


&nbsp;

**To configure Gradle scripts:** 


1. In your project's root directory `build.gradle`, add the following configurations.


```Kotlin
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    // Add version.gradle (mandatory)
    apply from: rootProject.file("gradle-config/version.gradle")
    repositories {
        google()
        mavenCentral()
        // Fetch the ServiceManager plugin (mandatory)
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
    }
    dependencies {
        // Android Gradle Plugin, required for all Android projects
        classpath "com.android.tools.build:gradle:4.1.3"
        // Kotlin Gradle Plugin, used for building Kotlin code
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        // SPI framework for code decoupling
        classpath "com.bytedance.news.common:service-manager-plugin:1.1.0.5-alpha.0"
    }
}

// This script line is necessary. If the codebase is located in settings.gradle, no need to apply this plugin. See details: High AGP Configuration
apply from: 'https://ve-vos.volccdn.com/ckone/ckone_integration.gradle'

allprojects {
    repositories {
        google()
        mavenCentral()
        maven { url "https://maven.aliyun.com/repository/public" }
    }
}
```



2. In `gradle.properties`, configure the username and password for the Maven repository to access the SDK.


```Properties
# Configure the account username and password for the Maven repository to access the SDK. No quotation marks are needed for the account and password.
MAVEN_USER_NAME=your user_name
MAVEN_PASS_WORD=your password
```


<span id="76981bcc"></span>
## Step 3: Adding `ck_repos_high_agp` Plugin for AGP 7.1.0 in `settings.gradle`

This step is for projects that use a codebase configured within the `settings.gradle` file and are utilizing Android Gradle Plugin (AGP) version 7.1.0. To enable the project to fetch the SDK, you need to add the `ck_repos_high_agp` plugin to the `settings.gradle` file. This plugin facilitates the process of retrieving the necessary SDK components for the project.

Add the following configurations:

```Kotlin
//settings.gradle
pluginManagement {
    repositories {
        // Add your repositories here
    }
}
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        // Add your repositories here
    }
}

// This script line is necessary (mandatory)
apply from: 'https://ve-vos.volccdn.com/ckone/ck_repos_high_agp.gradle'
xxxxx
```


<span id="6e12a1a6"></span>
## Step 4: Adding the ServiceManager plug\-in

The `ServiceManager` plug\-in helps to decouple dependencies.

**To add the ServiceManager plug\-in:** 


1. In your modules, add the following configurations.


```Groovy
plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
    // Mandatory: Add the ServiceManager Plugin.
    id 'com.bytedance.news.common.service-manager'
}
```


<span id="dd4f07fa"></span>
## **Step 5: Adding dependencies**

In your modules' `build.gradle`, add the following configurations.

```Groovy
// Add basic editing dependencies
implementation project(":editor-main")
// Basic editing resource module
implementation project(":editor-res")
// Basic editing draft module
implementation project(":editor-draft")

// Dependencies for recording & duet module
implementation project(":verecorder")
// Resources for recording & duet
implementation project(":record-res")
```


<span id="254cef2d"></span>
# Initializing CKOne SDK

Once Video Editor SDK has been integrated, you can initialize it to begin using its functions. Initialize Video Editor SDK by completing the following steps:


1. Configuring parameters.

2. Initializing the SDK.


<span id="7ec74349"></span>
## Step 1: Configuring parameters

Configure your SDK parameters, such as the SDK type and credentials.

**To configure the parameters:** 


1. Configure the following parameters in `CKAppConfig`.


**Parameters:** 


|**Name** ||**Data Type** |**Required** |**Description** |
|---|---|---|---|---|
|CKAppConfig |isOverSea |Boolean |Yes |Indicates whether the SDK is for users outside Mainland China. Valid values include:<br><br><br>* true—for users outside Mainland China.<br><br>* false—for users inside Mainland China. |
||productType |String |Yes |SDK type. Valid values include:<br><br><br>* Standard<br><br>* Lite |
||showOverSeaResource |Boolean |Yes |Whether overseas resources should be displayed. |


**EXAMPLE**

```Kotlin
CKAppConfig.apply{
    isOverSea = true or false
    productType = "Standard"
    it.showOverSeaResource = true or false
}
```



2. Configure the following parameters in `CKOneConstant`.


**Parameters:** 


|**Name** ||**Data Type** |**Required** |**Description** |
|---|---|---|---|---|
|CKGlobalConstant |appName |String |Optional |Application name. Default value is default. |
||veLicensePath |String |Required |License file name. |
||veAppKey |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |License key. |
||veToken |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |License token. |
||volcAccessKey |String |Optional |Access key for the music beat feature. |
||volcSecretKey |String |Optional |Secret key for the music beat feature. |
||subtitleAppId |String |Optional |AppKey for features such as text\-to\-speech (TTS) and text recognition. |
||subtitleToken |String |Optional |Token for features such as text\-to\-speech (TTS) and text recognition. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the credentials for volcAccessKey, volcSecretKey, subtitleAppId, and subtitleToken are not available, you do not need to assign any values. However, you can only use their features if the credentials have been assigned.</div>


**EXAMPLE**

```Kotlin
CKGlobalConstant.apply {
 
    appName = "CaptureCut"

    veLicensePath = CKBuildConfigUtil.getBuildConfigVeLicensePath()

    veAppKey = CKBuildConfigUtil.VE_APP_KEY
    veToken = AppConfigUtils.VE_TOKEN

    volcAccessKey = BuildConfig.volcAccessKey
    volcSecretKey = BuildConfig.volcSecretKey

    subtitleAppId = AppConfigUtils.subtitleAppId()
    subtitleToken = AppConfigUtils.subtitleToken()
}
```


<span id="4b5edd0d"></span>
## Step 2: Initializing SDKs

Initialize your SDK and resources.

**To initialize:** 


1. Initialize `AppSingleton`.


```Kotlin
AppSingleton.bindInstance(this)
```



2. Copy built\-in resources to the local storage.


```Kotlin
ResInitHelper.copyResourceToLocal(null)
```



3. Initialize VESDK.


```Kotlin
VEInit.init(context)
```



4. Initialize Video Editor SDK.


```Kotlin
CKEditorInitializer.init(context)
```


<span id="2eb963da"></span>
## SDK initialization sample code

Refer to the full sample code below to learn how to initialize Video Editor SDK for Android.

```Kotlin
// Configure CKAppConfig
CKAppConfig.apply {
    isOverSea = true // Set to true or false
    productType = "Standard"
    it.showOverSeaResource = true // Set to true or false
}

// Configure CKOneConstant
CKGlobalConstant.apply {
 
    appName = "CaptureCut"

    veLicensePath = CKBuildConfigUtil.getBuildConfigVeLicensePath()

    veAppKey = CKBuildConfigUtil.VE_APP_KEY
    veToken = AppConfigUtils.VE_TOKEN

    volcAccessKey = BuildConfig.volcAccessKey
    volcSecretKey = BuildConfig.volcSecretKey

    subtitleAppId = AppConfigUtils.subtitleAppId()
    subtitleToken = AppConfigUtils.subtitleToken()
}

// Initialize AppSingleton
AppSingleton.bindInstance(this)

// Copy internal resources to SD card
ResInitHelper.copyResourceToLocal(null)

// Initialize VESDK
VEInit.init(context)

// Initialize basic editing SDK
CKEditorInitializer.init(context)
```


<span id="c8cbec45"></span>
# Starting the UI interface

Once Video Editor SDK has been initialized, you can start the UI interface and begin using its functions. Refer to the sample code below to learn how to call the recording and editing pages and how to obtain the video URL.

```Kotlin
// Navigate to the recording page
uiHelper.check {
    RecordHelper.startRecord(this)
}

// Navigate to the basic editing page
uiHelper.check {
    EditorHelper.startEditor(this)
}

// Navigate to the draft page
uiHelper.check {
    DraftHelper.startDraft(this)
}

// Navigate to the duet page
uiHelper.check {
    DuetUtils.startDuet(this)
}

// Register BroadcastReceiver to retrieve the path of the composed video
// You can refer to the implementation of CompileLocalReceiver in the Demo
class CompileLocalReceiver : BroadcastReceiver() {

    companion object {
        private const val TAG = "CompileLocalReceiver"
    }

    override fun onReceive(context: Context, intent: Intent) {
        // Get the path of the composed video
        val editCompileVideoPath = intent.getStringExtra(ExtraConstants.EXTRA_COMPILE_VIDEO_PATH) ?: ""
        if (editCompileVideoPath.isEmpty()) {
            return
        }
        Log.d(TAG, "compile video path: $editCompileVideoPath")
        context.sendBroadcast(Intent(Intent.ACTION_MEDIA_SCANNER_SCAN_FILE).apply {
            data = Uri.fromFile(File(editCompileVideoPath))
        })
        // Use local preview for playback
        PreviewUtils.previewExportVideo(context, editCompileVideoPath)
    }
}
```


<span id="b699fd44"></span>
# Adding obfuscation rules

If your business enables obfuscation for release builds, it's important to incorporate the following obfuscation rules:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/767a737b96ce49cbbfe01ff38af260f9~tplv-goo7wpa0wc-image.image" name="proguard-rules.pro">proguard-rules.pro</Attachment>
