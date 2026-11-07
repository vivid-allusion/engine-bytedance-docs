---
title: "Integration Guide (with UI) - Magic Template SDK - Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-magic-template-sdk-android-v.4.0.2"
---

This guide demonstrates integrating BytePlus Magic Template SDK into your Android application. This UI\-inclusive integration method allows you to extensively refer to the UI packages in our CKOne Demo App sample code. Using this method, you will directly copy most of the sample code to your project without having to write the UI logic by yourself.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The BytePlus Video Editor SDK is also known as <strong>CKOne</strong> or <strong>CK</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The BytePlus Magic Template SDK is also called <strong>cutsame</strong> or <strong>CutSame</strong>.</div>


* <div data-tips="true" data-tips-type="tip">These terms will be used interchangeably in this article.</div>



<span id="421f2d23"></span>
# **Prerequisites**

Before you begin, ensure that the following requirements are met:


* Your application is intended for devices that are Android 5.0 or later.

* You have obtained a valid Magic Template SDK license, audiotoken, and audioappkey.

* You have obtained the account username and password required to access Magic Template SDK, which is stored in a Maven repository. For more information about obtaining these credentials, contact your technical support manager.


<span id="9637c89c"></span>
# Magic Template SDK architecture

BytePlus Magic Template SDK consists of four SDKs, VESDK, NLE SDK, CutSame SDK, and CutSameConsumer. The table below summarizes the main function of each SDK.


|**Name** |**Package** |**Description** |
|---|---|---|
|VESDK |com.bytedance.ugc.framework.libs:vesdk |A media\-editing SDK, responsible for media rendering. |
|NLE SDK |com.volcengine.ck.nle:NLEMediaPublic |A non\-linear editing middleware SDK comprised of a set of media\-editing APIs. It is not responsible for media rendering or on\-screen display. |
|CutSame SDK |com.volcengine.ck.cutsame:CK\-CutSameIF |The Magic Template consumption SDK, responsible for template replay, update, and synthesis. |
|CutSameConsumer |com.volcengine.ck.cutsame:CutSameConsumer |The Magic Template protocol conversion SDK. |


<span id="cf0ea671"></span>
# **CKOne sample code**

The CKOne sample code is required for the UI\-inclusive integration method for Android. In this section, you will learn more about the runtime environment and directory structure of the Demo App, which will help you understand how to integrate and use Magic Template SDK in your own application.

<span id="92c14238"></span>
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


<span id="ceb290ab"></span>
## CKOne sample code directory structure

The directory structure of the CKOne project file demonstrates how the sample code is organized. You can refer to the project file to understand how to integrate and use Video Editor SDK in your own application.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d127809627c430282c17d0fcd5884ed~tplv-goo7wpa0wc-image.image" width="321px" /></div>


The CKOne project file consists of the following top\-level files and modules.

```Shell
.
├── app
├── business
├── editor-res                 (Built-in resources required by Video Editor SDK)
├── record-res                 (Built-in resources required by the recording page, including stickers, filters, and beauty effects resources)
├── draft                      (Draft box module)
├── gradle
├── gradle-config
│   ├── include_source.gradle  (Quickly includes all modules, configured in setting.gradle)
│   └── version.gradle         (Declares all dependency version numbers and forces the building of dependency version numbers)
├── module_api                 (API layer code for each module)
│   └── cutsame-api
├── module_business
│   ├── cutsame                (Sample code for Magic Template)
│       ├── CutSameUIIF        (UI sample code for Magic Template)
│       ├── data-convert       (Data conversion for Magic Template, which is not required if the recording page is not integrated)
│       └── small-window       (UI sample code for the Magic Template window on the recording page, which is not required if the recording page is not integrated)
│   ├── editor                 (Sample code for the editor)
│   └── recorder               (Sample code for the recording page)
├── build.gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── dependency-lock.json       (JSON file used to declare all modules)
├── settings.gradle
```


<span id="38c88fc2"></span>
### **Resource modules**

The resource modules contain built\-in resources for video editing. There are two resource modules, `editor-res` and `record-res`.

**editor\-res**

`editor-res` contains built\-in resources required by Video Editor SDK.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af81c637b4ab497fb62b1c1eb1f0705c~tplv-goo7wpa0wc-image.image" width="389px" /></div>


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

`record-res` contains built\-in resources required by the recording page, including stickers, filters, and beauty effects resources. These resources are not included with Magic Template SDK and need to be purchased separately.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/122be5b0a3da4a409506f6e4af733cf8~tplv-goo7wpa0wc-image.image" width="391px" /></div>


The table below describes the resource bundles stored in `record-res`.


|**Name** |**Description** |
|---|---|
|ComposeMakeup.bundle |Beauty and makeup resources. |
|duet.bundle |Duet resources required by **Home** \> **Duet**. |
|FilterResource.bundle |Filter resources required by **Record** \> **Filter**. |
|ModelResource.bundle |Effects algorithm model file. |
|StickerResource.bundle |Sticker resources required by **Record** \> **Prop**. |


<span id="c1210190"></span>
### **Sample code modules**

The sample code for each module consists of one API layer module and several business modules. The API layer module contains only the interface definitions, while the business modules contain the actual business logic.

To reuse the sample code in your project, all API layer modules in`module_api` must be copied, while the business modules in `module_business` can be copied at your own discretion.

<span id="e79c4a82"></span>
### **gradle.properties**

`gradle.properties` in the CKOne project file contains the following properties:


|**Field** |**Description** |
|---|---|
|android.useAndroidX=true |Gradle configuration. AndroidX libraries are used instead of Support libraries. |
|android.enableJetifier=true |Gradle configuration. Third\-party libraries will use AndroidX dependencies. |
|NLE_VERSION |NLE SDK version number. |
|VESDK_VERSION |VESDK version number. |
|CUTSAME_IF_VERSION |Magic Template SDK version number. |
|VERSION_CODE |CKOne version code, which can be ignored. |
|VERSION_NAME |CKOne version name, which can be ignored. |
|MAVEN_USER_NAME |Username for the Maven repository, which is required to access the SDK. |
|MAVEN_PASS_WORD |Password for the Maven repository, which is required to access the SDK. |


<span id="8010715b"></span>
# Getting started with Magic Template SDK

Get started with Magic Template SDK by completing the following tasks:


1. Integrating Magic Template SDK.

2. Initializing Magic Template SDK.

3. Starting the UI interface.


<span id="832d3739"></span>
## Integrating Magic Template SDK

Integrate Magic Template SDK into your Android application by completing the following steps:


1. Managing dependencies.

2. Adding the sample code.

3. Configuring Gradle scripts.

4. Adding dependencies.


<span id="95f506ee"></span>
### Step 1: Managing dependencies

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


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1b95dcef5f04708b489f8bc29606e8d~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<span id="4940ff5d"></span>
### Step 2: Adding the sample code

You can directly copy the CKOne sample code to your project without having to write the UI logic by yourself.

**To add the sample code:** 


1. Copy the `cutsame` module from `module_business`.

2. (Optional) If asset selection in your application does not involve recording, delete the code in `data-convert` and `small-window`.

3. (Optional) If asset selection in your application involves recording, copy the `recorder` module from `module_business`.

4. Copy the code in `module_api`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When copying code from <code>module_business</code> and <code>module_api</code>, ensure that the resulting filepath in your project file is the same as in the sample code.</div>



5. (Optional) If asset selection in your application involves recording, copy `recorder-res` and replace the resources with your own resources.

6. Copy the Magic Template license file to the following filepath of any module: `\src\main\assets\resource.LicenseBag.bundle`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4efc753bfe45fd81653ad654c416ef~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Magic Template license file is the one containing "union" in its name. Ensure that the correct license is stored in the correct folder, as the ThrallCutSameInit class will search for the license in this path during initialization.</div>


<span id="323d3a6c"></span>
### Step 3: Configuring Gradle scripts

Configure the Gradle scripts in your project to enable Magic Template SDK to run properly.

**To configure Gradle scripts:** 


1. Depending on which `module_api` and `module_business` code segments were copied, configure `settings.gradle` as needed.


**EXAMPLE: CKOne sample code**

```Kotlin
rootProject.name = "CKOne"

include ':app'
include ':record-res'

include ':res-manager'
project(":res-manager").projectDir = new File(rootDir, "module_business/recorder/res-manager")

include ':verecorder'
project(":verecorder").projectDir = new File(rootDir, "module_business/recorder/verecorder")

include ':CutSameUIIF'
project(":CutSameUIIF").projectDir = new File(rootDir, "module_business/cutsame/CutSameUIIF")

include ':cutsame-api'
project(":cutsame-api").projectDir = new File(rootDir, "module_api/cutsame-api")

include ':data-convert'
project(":data-convert").projectDir = new File(rootDir, "module_business/cutsame/data-convert")

include ':small-window'
project(":small-window").projectDir = new File(rootDir, "module_business/cutsame/small-window")
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



3. In `gradle.properties`, configure the following properties.


```Properties
# Configure the account username and password for the Maven repository to access the SDK. No quotation marks are needed for the account and password.
MAVEN_USER_NAME=your user_name
MAVEN_PASS_WORD=your password

# Configure the version number of relevant SDKs as required.
NLE_VERSION=4.0.0
VESDK_VERSION=11.8.1.16-release-tob
CUTSAME_IF_VERSION=4.0.0

# Configure your license file name, which the ThrallCutSameInit class uses to search for the license file during initialization.
cutSameLicenseName="xxxxxxxxxunion.licbag"
```


<span id="14f96a06"></span>
### Step 4: Adding dependencies

In your modules' `build.gradle`, add the following configurations.

```Groovy
implementation project(':cutsame-api')
// Optional. Resource recording module.
implementation project(':record-res')
// Optional. Dependency for recording.
implementation project(':verecorder')
// Dependency for Magic Template SDK.
implementation project(':CutSameUIIF')
// retrofit2, used in Magic Template SDK.
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
```


<span id="429d58eb"></span>
## Initializing Magic Template SDK

Once Magic Template SDK has been integrated, you can initialize it to begin using its functions.

**To initialize Magic Template SDK:** 


1. Modify the relevant configurations in `ThrallCutSameInit.initCutSame()`.

2. In the `CutsameExternalServiceImpl.initCutSame` method, call `ThrallCutSameInit.initCutSame()`.


```Kotlin
// Modify the related configurations in ThrallCutSameInit.initCutSame()

// Default log object.
val logWrapper = LogWrapper().apply {
    val logWrapper = LogWrapper().apply {
    init(
        logConfig = LogConfig.Builder()
            .logcatLevel(LogIF.LOG_LEVER.DEBUG) // Console output level.
            .localLevel(LogIF.LOG_LEVER.WARNING) // Local file output level.
            .toLocal(true) // Local file output switch.
            .toLogcat(true) // Console output switch.
            .showThreadInfo(true) // Displays thread information.
            .localPath(Environment.getExternalStorageDirectory().absolutePath) // Path of the local output.
            .build()
    )
}
}
// Sets the log interface. The LogIF interface can be implemented by yourself. 
CutSameSolution.setLogIf(logWrapper)
CutSameSolution.init(
    context = this,
    // authorityConfig: License configuration.
    authorityConfig = AuthorityConfig.Builder()
        .licensePath(getLicenseFilePath()) // Local path of the license.
        .audioAppKey("xxxx") // Key of audio license.
        .audioToken("xxxx")  // Token of audio license.
        .authorityListener(object : AuthorityConfig.AuthorityListener {
            override fun onError(errorCode: Int, errorMsg: String) {
                Log.d(TAG, "onError $errorCode $errorMsg")
            }
        }).build(),
    // templateFetcherConfig: Template pulling configuration. It needs to be configured only when CutSameSDK is used to pull template data. 
    templateFetcherConfig = TemplateFetcherConfig.Builder()
        .host("http://xx.xxxx.net")
        .build(),
    // effectFetcherConfig: Effects pulling configuration.
    effectFetcherConfig = EffectFetcherConfig.Builder()
        .host("http://xx.xxxx.net")
        .effectLitPath("/xxx/xxxx")
        .localModelPath("xxxxxx") // Absolute path of the local algorithm model. It is required by recording-related props and intelligent image matting.
        .build()
)
```



3. At the entry point of your application or of the Magic Template feature, use the following code to complete initialization.


```Kotlin
// Use CutsameExternalServiceImpl, an ICutSameExternalService implementation method, to complete initialization.
ServiceManager.getService(ICutSameExternalService::class.java)?.initCutSame(AppSingleton.instance as Application)。
```


<span id="d86ad760"></span>
## Starting the UI interface

Once Magic Template SDK has been initialized, you can start the UI interface and begin using its functions. Refer to the sample code below to learn how to call the template list page.

```Kotlin
// Call the template list and obtain Intent.
ServiceManager.getService(ICutSameExternalService::class.java)?.getTemplateUIIntent(context)
```


<span id="7f80820e"></span>
# **Adding obfuscation rules**

If obfuscation is enabled for the enterprise release package, you need to add the following obfuscation rules:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/793f8419a3534ab3b39d74a36fe46f4d~tplv-goo7wpa0wc-image.image" name="consumer-rules.pro">consumer-rules.pro</Attachment>
