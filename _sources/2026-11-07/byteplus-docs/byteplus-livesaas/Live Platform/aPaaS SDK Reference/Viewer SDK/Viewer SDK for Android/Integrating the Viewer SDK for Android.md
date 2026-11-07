---
title: "Integrating the Viewer SDK for Android"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android"
---

To add interactive live streaming features—such as watching streams, sending comments, and engaging with hosts—to your Android app, you can integrate the Viewer SDK. This guide provides step\-by\-step instructions for the entire integration process, from setting up Gradle configurations to initializing the SDK and joining a live room.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To prevent troubleshooting complications, upgrade to version 1.54.2 or later.</div>


<span id="Prerequisites"></span>
## Prerequisites


* Android Studio 4.0 or later (recommended).

* Real devices running Android 5.0 (API level 21) and above.

* CPU architecture: armeabi\-v7a or arm64\-v8a.

* AndroidX library only.

* minSdkVersion: 21 (Android 5.0) and above.

* targetSdkVersion: minSdkVersion and above, up to 35 (Android 15).

* JDK version: 1.8.0 and above.

* Contact BytePlus Live technical support to obtain the following items: your license files (for live streaming and VOD), the app name used for the license application, and the corresponding app ID.


<span id="Integrating the SDK"></span>
## Integration steps

<span id="8a9e8a55"></span>
### Step 1: Set Gradle configurations


1. Open the `build.gradle` file in the root directory of your project and add the following configurations.

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
               url "https://artifact.bytedance.com/repository/Volcengine/" // URL of a public Maven repository
           }
           maven {
               url "https://artifact.byteplus.com/repository/public/" // URL of BytePlus's public repository
   }
           maven {
               url "https://artifact.bytedance.com/repository/thrall_base/" // URL of a streaming repository
               credentials {
                   username = 'veVOS' // Username to access the streaming repository. Do not change this value
                   password = 'KUC9TpKrqbryrxHz' // Password to access the streaming repository. No need to change
               }
               authentication {
                   digest(BasicAuthentication)
               }
           }
       } 
   } 
   ```
   

2. Open the `build.gradle` file in the `app` directory of your project and add the following configurations.

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
    
       // Import the Viewer SDK. You can use implementation "com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite" to optimize the SDK package size. The optimized SDK package excludes the feature of ultra-low latency live streaming.
       implementation "com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull"
    
       // Import the Glide library. If you have imported the Glide library into your project before, see the Glide version compatibility section to ensure Glide version compatibility
       implementation "com.github.bumptech.glide:glide:4.15.1"
   } 
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Starting from SDK version 1.54.0,   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">when importing the Viewer SDK with all features, the SDK version suffix has changed from <code>pull-global:VersionNumber.external</code> to <code>pull:VersionNumber.globalFull</code>. For example, use <code>com.bytedance.bdlive:bdlive-pull-global:1.53.0.external</code> to import the Viewer SDK 1.53.0 with all features, and use <code>com.bytedance.bdlive:bdlive-pull:1.54.0.globalFull</code> to import the Viewer SDK 1.54.0 with all features .   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">when importing the Viewer SDK excluding the feature of ultra\-low latency live streaming, the SDK version suffix has changed from <code>pull-global-remove-rtc:VersionNumber.external</code> to <code>pull:VersionNumber.globalLite</code>. For example, use <code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external</code> to import the Viewer SDK 1.53.0 excluding the feature of ultra\-low latency live streaming, and use <code>com.bytedance.bdlive:bdlive-pull:1.54.0.globalLite</code> to import the Viewer SDK 1.54.0 excluding the feature of ultra\-low latency live streaming.   </div>
   


<span id="aca3bab7"></span>
#### Glide version compatibility

Since version 1.10.6, the Viewer SDK for Android has migrated its image library component to Glide.

Because different versions of the Glide API have significant differences, you must ensure version compatibility to prevent app crashes. The required steps depend on the Glide version your project uses.


* Glide version is greater than or equal to 4.9.0: No action is required.

* Glide version 4.x, but less than version 4.9.0: Open the `build.gradle` file in the `app` directory of your project and add the following configurations.

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
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Viewer SDK does not support Glide 3.x. We recommend that you upgrade Glide to the latest version. Upgrading is straightforward, and no action is required after the upgrade to ensure Glide version compatibility.   </div>
   

<span id="006c7b9c"></span>
### Step 2: Add permissions

Open the `AndroidManifest.xml` file in the `app/src/main` directory and add the following permissions.

```XML
<!-- Access local storage --> 
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
 
<!-- Network status --> 
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" /> 
<uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/> 
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/> 

 <!-- System alert window --> 
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />

<!-- Calendar --> 
<uses-permission android:name="android.permission.READ_CALENDAR"/> 
<uses-permission android:name="android.permission.WRITE_CALENDAR"/>
```


<span id="Adding manifest permissions"></span>
### Step 3: Add obfuscation rules

Open the `proguard-rules.pro` file in the `app` directory and add the following obfuscation rules.

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
### Step 4: Import licenses

Create the `assets/lic` directory in the `app/src/main` directory and place the live streaming license file `liveLicense.lic` and VOD license file `vodLicense.lic` in the `assets/lic` directory. The file structure is as follows.

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
### Step 5: Initialize the BDLive SDK

When your application initializes, call `BDLiveEnv.init` to initialize the BDLive SDK (Viewer SDK).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Personal information of users is not collected during initialization.</div>


```Java
private void initBDLiveEnv() {
    String assetsLicenseUri = "assets:///lic/example.lic"; // Replace assets:///lic/example.lic with the URI of the VOD license
    String assetsLicenseUri2 = "assets:///lic/example.lic"; // Replace assets:///lic/example.lic with the URI of the live streaming license
    BDLiveEnv.init(new BDLiveConfig.Builder()
        .setApplicationContext(this)
        .setAppId("APP_ID") // Replace APP_ID with the app ID returned after the successful license application. Contact BytePlus Live technical support to obtain the app ID.
        .setAppName("APP_NAME") // Replace APP_NAME with the app name used to apply for the license. Contact BytePlus Live technical support to obtain the app name.
        .setAppChannel("CHANNEL_NAME") // Replace CHANNEL_NAME with the name of the channel through which to download the app.
        .setAppVersion("APP_VERSION") // Replace APP_VERSION with the app version. A valid version number should contain two or more separators, such as 1.3.2.
        .setAppRegion("REGION") // Replace REGION with the region used to apply for the license. Always set this value to 'singapore'.
        .setVodLicenseUri(assetsLicenseUri) // URI of the VOD license 
        .setLiveLicenseUri(assetsLicenseUri2) // URI of the live streaming license
        .setUseSecureInfoCollect(true) // Whether to enable the secure information collection mode. true: Enables the mode. Personal information of users is not collected. false: Disables the mode. Personal information of users is collected. Default value: true       
        .build());
}
```


<span id="Entering the live room"></span>
### Step 6: Join and leave a live room

The following sample code shows the methods to join and leave a full\-featured live room.

```Java
long activityId = ACTIVITY_ID; // Replace ACTIVITY_ID with the activity ID of the live room.
String token = "TOKEN"; // Replace TOKEN with the authorization token required to join the live room. 
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC; // The authentication mode of the live room. This example uses public mode. Viewers can watch live streams, view comments, and perform other operations without logging in to the live room.
boolean isPortrait = true;// Whether the live room is in portrait mode. Here take the portrait mode as an example.
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
// Leave the live room.
TVULiveRoom.leaveLiveRoom(context);
```


<span id="a90cb94f"></span>
## Optimizing the SDK package size

Starting from SDK version 1.54.0, you can optimize the SDK package size by following these steps:


1. Open the `build.gradle` file in the `app` directory, and locate the Viewer SDK dependency in the `dependencies` block.

   ```Groovy
   com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull
   ```
   

2. Replace `globalFull` with `globalLite`.

   ```Groovy
   com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite
   ```
   


The optimized SDK package excludes the feature of ultra\-low latency live streaming.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the SDK version is below 1.54.0, you can change the SDK dependency from <code>com.bytedance.bdlive:bdlive-pull-global:VersionNumber.external</code> to <code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:VersionNumber.external</code> to optimize the SDK package size. For example, change <code>com.bytedance.bdlive:bdlive-pull-global:1.53.0.external</code> to <code>com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external</code>.</div>


<span id="de28cb2c"></span>
## Package size

Here, the package size refers to the incremental APK file (installation package) size after integrating the SDK, calculated as the APK file size after SDK integration minus the APK file size before SDK integration.

The following data is based on the app supporting only the arm64\-v8a CPU architecture.

If your app supports multiple CPU architectures, the package size will increase accordingly.


|Version |Type |Dependency |Incremental Package Size |
|---|---|---|---|
|1.58.0 \- 1.66.3 (Use 1.66.3 as an example in the dependency) |Viewer SDK |`com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull` |About 31.2 MB |
||Viewer SDK with optimized package size |`com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite` |About 19.4 MB |
||Live Streaming SDK + Viewer SDK |* `com.bytedance.bdlive:bdlive-push:1.66.3.globalFull`<br><br>* `com.bytedance.bdlive:bdlive-pull:1.66.3.globalFull` |About 34 MB |
||Live Streaming SDK with optimized package size + Viewer SDK with optimized package size |* `com.bytedance.bdlive:bdlive-push:1.66.3.globalLite`<br><br>* `com.bytedance.bdlive:bdlive-pull:1.66.3.globalLite` |About 28 MB |


The Live Streaming SDK with optimized package size excludes the screen sharing feature, while the Viewer SDK with optimized package size excludes the ultra\-low latency live streaming feature. For more information on adding dependencies, see step 2 in [Step 1: Set Gradle configurations](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android#8a9e8a55).
