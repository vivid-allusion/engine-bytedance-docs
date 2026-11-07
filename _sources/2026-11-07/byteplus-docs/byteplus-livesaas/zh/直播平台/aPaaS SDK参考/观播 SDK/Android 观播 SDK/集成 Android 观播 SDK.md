---
title: "集成 Android 观播 SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android-zh-CN"
---

要为你的 Android 应用添加互动直播功能，例如观看流、发送评论以及与主播互动，你可以集成 Android 观播 SDK。本指南为整个集成流程提供分步说明，包括配置 Gradle、初始化 SDK 以及加入直播间。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">为避免排查问题时出现复杂情况，请升级至1.54.2或更高版本。</div>


<span id="Prerequisites"></span>
## 前提条件


* 建议使用 Android Studio 4.0 或更高版本。

* 运行 Android 5.0（API 级别 21）及以上的真实设备。

* CPU 架构：armeabi\-v7a 或 arm64\-v8a。

* 仅支持 AndroidX 库。

* minSdkVersion：21（Android 5.0）及以上。

* targetSdkVersion：不低于 minSdkVersion，最高支持 35（Android 15）。

* JDK 版本：1.8.0 及以上。

* 请联系 BytePlus Live 技术支持获取以下内容：你的直播和点播授权文件、用于申请授权的应用名称，以及对应的应用 ID。


<span id="Integrating the SDK"></span>
## 集成步骤

<span id="8a9e8a55"></span>
### Step 1: 设置 Gradle 配置


1. 打开项目根目录下的 `build.gradle` 文件，添加以下配置。

   ```Groovy
   buildscript { 
       repositories { 
           google() 
           mavenCentral() 
       } 
       dependencies { 
           // We recommend that you use version 3.6.3 or later.
           classpath 'com.android.tools.build:gradle:3.6.3' 
       } 
   } 
    
   allprojects { 
       repositories { 
           google() 
           mavenCentral() 
           jcenter() 
           maven {
               url "https://artifact.bytedance.com/repository/Volcengine/" // 公共Maven仓库的URL
           }
           maven {
               url "https://artifact.byteplus.com/repository/public/" // BytePlus公共仓库的URL
   }
           maven {
               url "https://artifact.bytedance.com/repository/thrall_base/" // 流媒体仓库的URL
               credentials {
                   username = 'veVOS' // Username to access the streaming repository.请勿更改此值
                   password = 'KUC9TpKrqbryrxHz' // Password to access the streaming repository.无需更改
               }
               authentication {
                   digest(BasicAuthentication)
               }
           }
       } 
   } 
   ```
   

2. 打开项目 `app` 目录下的 `build.gradle` 文件，添加以下配置。

   ```Groovy
   android { 
       defaultConfig { 
           minSdkVersion 21 
           ndk { 
               abiFilters "armeabi-v7a","arm64-v8a" 
           } 
       } 
    
    
      // Enable DataBinding
       dataBinding { 
           enabled = true 
       } 
   } 
    
   // Import dependencies
   dependencies { 
    
       // Import the Viewer SDK.您可以使用 implementation "com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite" 来优化SDK包体大小。优化后的SDK包体不包含超低延时直播功能。
       implementation "com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull"
    
       // Import the Glide library.如果您之前已在项目中导入Glide库，请参见Glide版本兼容性部分以确保Glide版本兼容
       implementation "com.github.bumptech.glide:glide:4.15.1"
   } 
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">从SDK版本1.54.0开始，   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">导入包含全部功能的观众SDK时，SDK版本后缀已从<code>pull-global:VersionNumber.external</code>变更为<code>pull:VersionNumber.globalFull</code>。例如，使用<code>com.bytedance.bdlive:bdlive-pull-global:1.53.0.external</code>导入包含全部功能的观众SDK 1.53.0，使用<code>com.bytedance.bdlive:bdlive-pull:1.54.0.globalFull</code>导入包含全部功能的观众SDK 1.54.0。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">导入不包含超低延时直播功能的观众SDK时，SDK版本后缀已从<code>pull-global-remove-rtc:VersionNumber.external</code>变更为<code>pull:VersionNumber.globalLite</code>。例如，使用<code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external</code>导入不包含超低延时直播功能的观众SDK 1.53.0，使用<code>com.bytedance.bdlive:bdlive-pull:1.54.0.globalLite</code>导入不包含超低延时直播功能的观众SDK 1.54.0。   </div>
   


<span id="aca3bab7"></span>
#### Glide 版本兼容性

自 1.10.6 版本起，Android 观播 SDK 的图片库组件已迁移至 Glide。

由于 Glide API 的不同版本差异较大，你必须确保版本兼容性，以防止应用崩溃。所需操作步骤取决于你的项目所使用的 Glide 版本。


* Glide 版本大于等于 4.9.0：无需操作。

* Glide 版本为 4.x 且低于 4.9.0：打开项目 `app` 目录下的 `build.gradle` 文件，添加以下配置。

   ```Java
   // Import the Viewer SDK
   implementation("com.bytedance.bdlive:bdlive-pull:x.x.x.globalFull"){
       {
           // Remove the default bdlive-glide-v4 library
           exclude group:"com.bytedance.bdlive",module:"bdlive-glide-v4"
       }
   }
   
   // Import the bdlive-glide-adapt-v4 library
   implementation "com.bytedance.bdlive:bdlive-glide-adapt-v4:1.1.5"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">观众SDK不支持Glide 3.x。建议您将Glide升级到最新版本。升级操作简单，升级后无需额外操作即可确保Glide版本兼容性。   </div>
   

<span id="006c7b9c"></span>
### Step 2: 添加权限

打开 `AndroidManifest.xml` 文件（位于 `app/src/main` 目录），添加以下权限。

```XML
<!-- 访问本地存储 --> 
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
 
<!-- 网络状态 --> 
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" /> 
<uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/> 
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/> 

 <!-- 系统提示窗口 --> 
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />

<!-- 日历 --> 
<uses-permission android:name="android.permission.READ_CALENDAR"/> 
<uses-permission android:name="android.permission.WRITE_CALENDAR"/>
```


<span id="Adding manifest permissions"></span>
### Step 3: 添加混淆规则

打开 `proguard-rules.pro` 文件（位于 `app` 目录），添加以下混淆规则。

```XML
-keep class com.pandora.**{*;}
-keep class com.ss.**{*;} 
-keep class com.bytedance.**{*;}
-keep class com.pandora.ttlicense2.**{*;}
-keep class com.bytertc.**{*;}
-keep class org.webrtc.**{*;}
-keep class log.**{*;}
```


<span id="Implementing code obfuscation"></span>
### Step 4: 导入授权文件

在 `app/src/main` 目录下创建 `assets/lic` 文件夹，并将直播授权文件 `liveLicense.lic` 和点播授权文件 `vodLicense.lic` 放入 `assets/lic` 文件夹。文件结构如下。

```Plain
app
|-- src
    |-- main
        |-- java
        |-- assets
            |-- lic
                |--  liveLicense.lic
                |--  vodLicense.lic
```


<span id="660b1619"></span>
### Step 5: 初始化 BDLive SDK

应用初始化时，调用 `BDLiveEnv.init` 方法以初始化 BDLive SDK（Android 观播 SDK）。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">初始化过程中不会收集用户个人信息。</div>


```Java
private void initBDLiveEnv() {
    String assetsLicenseUri = "assets:///lic/example.lic"; // Replace assets:///lic/example.lic with the URI of the VOD license
    String assetsLicenseUri2 = "assets:///lic/example.lic"; // Replace assets:///lic/example.lic with the URI of the live streaming license
    BDLiveEnv.init(new BDLiveConfig.Builder()
        .setApplicationContext(this)
        .setAppId("APP_ID") // Replace APP_ID with the app ID returned after the successful license application.请联系 BytePlus Live 技术支持获取应用ID。
        .setAppName("APP_NAME") // Replace APP_NAME with the app name used to apply for the license.请联系 BytePlus Live 技术支持获取应用名称。
        .setAppChannel("CHANNEL_NAME") // 将 CHANNEL_NAME 替换为下载应用的渠道名称。
        .setAppVersion("APP_VERSION") // Replace APP_VERSION with the app version.有效的版本号应包含两个或以上分隔符，例如1.3.2。
        .setAppRegion("REGION") // Replace REGION with the region used to apply for the license.此值始终设置为“singapore”。
        .setVodLicenseUri(assetsLicenseUri) // URI of the VOD license
        .setLiveLicenseUri(assetsLicenseUri2) // URI of the live streaming license
        .setUseSecureInfoCollect(true) // 是否启用安全信息收集模式。true：启用该模式。不会收集用户个人信息。false：禁用该模式。会收集用户个人信息。默认值：true
        .build());
}
```


<span id="Entering the live room"></span>
### Step 6: 加入和退出直播间

以下示例代码展示了如何加入和退出完整直播间的方法。

```Java
long activityId = ACTIVITY_ID; // Replace ACTIVITY_ID with the activity ID of the live room.
String token = "TOKEN"; // Replace TOKEN with the authorization token required to join the live room.
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC; // The authentication mode of the live room.本示例使用公开模式。观众无需登录直播间即可观看在线流、查看评论及执行其他操作。
boolean isPortrait = true;// Whether the live room is in portrait mode.此处以竖屏模式为例。
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
// Leave the live room.
TVULiveRoom.leaveLiveRoom(context);
```


<span id="a90cb94f"></span>
## 优化 SDK 包体积

从 SDK 1.54.0 版本开始，你可以通过以下步骤优化 SDK 包体积：


1. 打开 `app` 目录下的 `build.gradle` 文件，在 `dependencies` 块中找到 Android 观播 SDK 依赖项。

   ```Groovy
   com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull
   ```
   

2. 将 `globalFull` 替换为 `globalLite`。

   ```Groovy
   com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite
   ```
   


优化后的 SDK 包体积不包含超低延时直播功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果 SDK 版本低于 1.54.0，可以将 SDK 依赖项从<code>com.bytedance.bdlive:bdlive-pull-global:VersionNumber.external</code>更改为<code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:VersionNumber.external</code>，以优化 SDK 包体大小。例如，将<code>com.bytedance.bdlive:bdlive-pull-global:1.53.0.external</code>更改为<code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external</code>。</div>


<span id="de28cb2c"></span>
## 包体积

此处的包体积指集成 SDK 后 APK 文件（安装包）的增量体积，即集成 SDK 后的 APK 文件大小减去集成前的 APK 文件大小。

以下数据基于应用仅支持 arm64\-v8a CPU 架构。

如果你的应用支持多种 CPU 架构，包体积会相应增加。


|版本 |类型 |依赖项 |增量包体大小 |
|---|---|---|---|
|1.58.0 \- 1.66.3（依赖项以 1.66.3 为例） |观众 SDK |`com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull` |约 31.2 MB |
||优化包体大小的观众 SDK |`com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite` |约 19.4 MB |
||直播推流 SDK + 观众 SDK |* `com.bytedance.bdlive:bdlive-push:1.66.3.globalFull`<br><br>* `com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull` |约 34 MB |
||优化包体大小的直播推流 SDK + 优化包体大小的观众 SDK |* `com.bytedance.bdlive:bdlive-push:1.66.3.globalLite`<br><br>* `com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite` |约 28 MB |


优化包体大小的直播SDK不包含屏幕共享功能，优化包体大小的观众SDK不包含超低延时直播功能。有关添加依赖项的更多信息，请参见[Step 1: 设置 Gradle 配置](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android-zh-CN#8a9e8a55)的第2步。
