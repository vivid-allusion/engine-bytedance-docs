---
title: "Integrating VE SDK with UI—Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-android-v.4.0.2"
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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Debugging using an emulator is currently not supported.</div>


<span id="d1202df2"></span>
# Video Editor SDK architecture

BytePlus Video Editor SDK consists of two SDKs, VESDK and NLE SDK. The table below summarizes the main function of each SDK.


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
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cf53540f5fe4b068bf3db120551c2af~tplv-goo7wpa0wc-image.image" width="202px" /></div>


The CKOne project file consists of the following top\-level files and modules.

```Shell
.
├── app
├── editor-res         (Built-in resources required by Video Editor SDK)
├── record-res         (Built-in resources required by the recording page, including stickers, filters, and beauty effects resources)
├── draft              (Draft box module)
├── gradle
├── gradle-config
│   └── version.gradle (Declares all dependency version numbers and forces the building of dependency version numbers)
├── module_api         (API layer code for each module)
│   └── cutsame-api
├── module_business
│   ├── cutsame        (Sample code for Magic Template)
│   ├── editor         (Sample code for the editor)
│   └── recorder       (Sample code for the recording page)
├── build.gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── settings.gradle
```


<span id="47b4895d"></span>
### Resource modules

The resource modules contain built\-in resources for video editing. There are two resource modules, `editor-res` and `record-res`.

**editor\-res**

`editor-res` contains built\-in resources required by Video Editor SDK.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8663b522a7541a490e3244f85b2a2a5~tplv-goo7wpa0wc-image.image" width="389px" /></div>


The table below describes the types of resources stored in `editor-res`.


|**Name** |**Description** |
|---|---|
|LocalResource |Built\-in default resources that come with the sample code. They are not encrypted and can be used at will. |
|resource |Resources required by all features in Video Editor SDK, such as text stickers, filters, effects, and masks. You need to change these resources with your purchased resources. |


The table below describes the resource bundles stored in `resource`.


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
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/901659f6be4547bc91de459bce4116ce~tplv-goo7wpa0wc-image.image" width="391px" /></div>


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

The sample code for each module consists of one API layer module and several business modules. The API layer module contains only the interface definitions, while the business modules contain the actual business logic.

To reuse the sample code in your project, all API layer modules in`module_api` must be copied, while the business modules in `module_business` can be copied at your own discretion.

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


1. Integrating Video Editor SDK.

2. Initializing Video Editor SDK.

3. Starting the UI interface.


<span id="0caef57d"></span>
# Integrating Video Editor SDK

Integrate Video Editor SDK into your Android application by completing the following steps:


1. Managing dependencies.

2. Adding the sample code.

3. Configuring Gradle scripts.

4. Adding the ServiceManager plug\-in.

5. Adding dependencies.


<span id="e1da198c"></span>
## Step 1: Managing dependencies

Before you begin integrating the sample code, configure `version.gradle` to uniformly define the version numbers for the dependencies used in your project.

**To manage dependencies:** 


1. Copy `version.gradle` in `gradle-config` from the CKOne sample code to your project.

2. Configure `version.gradle` as needed.

3. In your project's root directory`build.gradle`, add the following configuration to `buildscript{}`.


```Kotlin
buildscript {
    // Required. Add version.gradle.
    apply from: rootProject.file("gradle-config/version.gradle")
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76a51ca026bf48229f9f6caedbe0246a~tplv-goo7wpa0wc-image.image) </span>

<span id="5. CKOne integration"></span>
## Step 2: Adding the sample code

You can directly copy the CKOne sample code to your project without having to write the video editing UI logic by yourself.

**To add the sample code:** 


1. Depending on your project, copy the code in `module_api` and `module_business` as needed.

2. Copy `editor-res` and `recorder-res` and replace the resources with your own resources.

3. (Optional) Depending on your project requirements, copy the draft box module.

4. Copy the license files to the following filepath of any module: `\src\main\assets\resource.LicenseBag.bundle`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f52d33f4dc95424d8bf356ee207635b1~tplv-goo7wpa0wc-image.image" width="721px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once set, you cannot modify the file path for the licenses. Make sure to store the licenses in the appropriate folder.</div>


<span id="810bc19f"></span>
## Step 3: Configuring Gradle scripts

Configure the Gradle scripts in your project to enable Video Editor SDK to run properly.

**To configure Gradle scripts:** 


1. Depending on which `module_api` and `module_business` code segments were copied, configure `settings.gradle` as needed.


**EXAMPLE: CKOne sample code**

```Kotlin
rootProject.name = "CKOne"

include ':app'
include ':editor-res'
include ':record-res'
include ':draft'

include ':editor-main'
project(":editor-main").projectDir = new File(rootDir, "module_business/editor/editor-main")

include ':editor-components'
project(":editor-components").projectDir = new File(rootDir, "module_business/editor/editor-components")

include ':editor-core'
project(":editor-core").projectDir = new File(rootDir, "module_business/editor/editor-core")

include ':editor-btmpanel'
project(":editor-btmpanel").projectDir = new File(rootDir, "module_business/editor/editor-btmpanel")

include ':editor-preview'
project(":editor-preview").projectDir = new File(rootDir, "module_business/editor/editor-preview")

include ':editor-trackpanel'
project(":editor-trackpanel").projectDir = new File(rootDir, "module_business/editor/editor-trackpanel")

include ':editor-uibase'
project(":editor-uibase").projectDir = new File(rootDir, "module_business/editor/editor-uibase")

include ':res-manager'
project(":res-manager").projectDir = new File(rootDir, "module_business/recorder/res-manager")

include ':verecorder'
project(":verecorder").projectDir = new File(rootDir, "module_business/recorder/verecorder")

include ':cutsame-api'
project(":cutsame-api").projectDir = new File(rootDir, "module_api/cutsame-api")
```



2. In your project's root directory `build.gradle`, add the following configurations.


```Kotlin
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    // Required. Add version.gradle.
    apply from: rootProject.file("gradle-config/version.gradle")
    repositories {
        google()
        mavenCentral()
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
    }
    dependencies {
        classpath "com.android.tools.build:gradle:4.1.3"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        classpath "com.bytedance.news.common:service-manager-plugin:1.1.0.5-alpha.0"
    }
}

// Required. This row of scripts must be added.
apply from: 'https://ve-vos.volccdn.com/ckone/ckone_integration.gradle'

allprojects {
    repositories {
        google()
        mavenCentral()
        maven { url "https://maven.aliyun.com/repository/public" }
    }
}
```



3. In `gradle.properties`, configure the username and password for the Maven repository to access the SDK.


```Properties
# Configure the account username and password for the Maven repository to access the SDK. No quotation marks are needed for the account and password.
MAVEN_USER_NAME=your user_name
MAVEN_PASS_WORD=your password
```


<span id="6e12a1a6"></span>
## Step 4: Adding the ServiceManager plug\-in

The ServiceManager plug\-in helps to decouple dependencies.

**To add the ServiceManager plug\-in:** 


1. In your modules, add the following configurations.


```Groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-kapt'
    // Required. Apply the ServiceManager plug-in.
    id 'com.bytedance.news.common.service-manager'
}

dependencies {
    // Required. Add the ServiceManager comment processor.
    kapt "com.bytedance.news.common:service-manager-processor:1.0.9"
}
```


<span id="dd4f07fa"></span>
## **Step 5: Adding dependencies**

In your modules' `build.gradle`, add the following configurations.

```Groovy
// Basic editing resource module.
implementation project(':editor-res')
// Recording resource module.
implementation project(':record-res')
// Draft module.
implementation project(':draft')

implementation project(':cutsame-api')

// Dependency for recording.
implementation project(':verecorder')
// Dependency for basic editing.
implementation project(':editor-main')
// Optional. Dependency for Magic Template SDK.
implementation project(':CutSameUIIF')
```


<span id="254cef2d"></span>
# Initializing Video Editor SDK

Once Video Editor SDK has been integrated, you can initialize it to begin using its functions. Initialize Video Editor SDK by completing the following steps:


1. Configuring parameters.

2. Initializing.


<span id="7ec74349"></span>
## Step 1: Configuring parameters

Configure your SDK parameters, such as the SDK type and credentials.

**To configure the parameters:** 


1. Configure the following parameters in `CKAppConfig`.


**Parameters:** 


|**Name** |**Description** |
|---|---|
|isOverSea |Indicates whether the SDK is for users outside Mainland China. Valid values include:<br><br><br>* true—for users outside Mainland China.<br><br>* false—for users inside Mainland China. |
|productType |SDK type. Valid values include:<br><br><br>* Standard<br><br>* Lite |


**EXAMPLE**

```Kotlin
CKAppConfig.apply{
    isOverSea = false
    productType = "Standard"
}
```



2. Configure the following parameters in `CKOneConstant`.


**Parameters:** 


|**Name** |**Description** |
|---|---|
|appName |Optional. Application name. Default value is default. |
|veLicensePath |Required. License file name. |
|veAppKey |Required. License key. |
|veToken |Required. License token. |
|volcAccessKey |Optional. Access key for the music beat feature. |
|volcSecretKey |Optional. Secret key for the music beat feature. |
|subtitleAppId |Optional. AppKey for features such as text\-to\-speech (TTS) and text recognition. |
|subtitleToken |Optional. Token for features such as text\-to\-speech (TTS) and text recognition. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the credentials for volcAccessKey, volcSecretKey, subtitleAppId, and subtitleToken are not available, you do not need to assign any values. However, you can only use their features if the credentials have been assigned.</div>


**EXAMPLE**

```Kotlin
CKOneConstant.apply {
 
    appName = "CKOne"

    veLicensePath = "labcv_test_20220929_20221231_com.bytedance.solution.ck_4.2.6.5.licbag"

    veAppKey = "iWwiXvXhlN"
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
VEInit.init()
```



4. Initialize Video Editor SDK.


```Kotlin
CKEditorInitializer.init(this)
```


<span id="2eb963da"></span>
## SDK initialization sample code

Refer to the full sample code below to learn how to initialize Video Editor SDK for Android.

```Kotlin
// Step 1: Configure CKAppConfig.
CKAppConfig.apply{
    isOverSea = false
    productType = "Standard"
}
// Step 2: Configure CKOneConstant.
CKOneConstant.apply {
 
    appName = "CKOne"

    veLicensePath = "labcv_test_20220929_20221231_com.bytedance.solution.ck_4.2.6.5.licbag"

    veAppKey = "iWwiXvXhlN"
    veToken = AppConfigUtils.VE_TOKEN

    volcAccessKey = BuildConfig.volcAccessKey
    volcSecretKey = BuildConfig.volcSecretKey

    subtitleAppId = AppConfigUtils.subtitleAppId()
    subtitleToken = AppConfigUtils.subtitleToken()
}

// Step 3: Initialize AppSingleton.
AppSingleton.bindInstance(this)

// Step 4: Copy built-in resources to the SD card.
ResInitHelper.copyResourceToLocal(null)

// Step 5: Initialize VESDK.
VEInit.init()

// Step 6: Initialize the basic editing SDK.
CKEditorInitializer.init(this)
```


<span id="c8cbec45"></span>
# Starting the UI interface

Once Video Editor SDK has been initialized, you can start the UI interface and begin using its functions. Refer to the sample code below to learn how to call the recording and editing pages and how to obtain the video URL.

```Kotlin
// Call the recording page.
checkAuth {
    checkPermissions {
        checkResourceReady {
            PreviewActivity.startPreviewActivity(activity, null)
        }
    }
}
// Call the basic editing page.
checkAuth {
    checkPermissions {
        checkResourceReady {
            EditorHelper.startEditor(activity)
        }
    }
}
// Obtain the URL of the synthesized video from onActivityResult.
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
    when (requestCode) {
    ActivityRequestCode.CKEDITOR_ACTIVITY -> {
        // Obtain the video synthesized on the editing page.
        if (resultCode == Activity.RESULT_OK) {
            val editCompileVideoPath = data.getStringExtra(ExtraConstants.EXTRA_COMPILE_VIDEO_PATH) ?: ""
            LogKit.d(TAG, "compile video path: $editCompileVideoPath")
        }
    }
}
```


For more information about the implementation logic, refer to the CKHomeDelegate implementation in the CKOne sample code.
