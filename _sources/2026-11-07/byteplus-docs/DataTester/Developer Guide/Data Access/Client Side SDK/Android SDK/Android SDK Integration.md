---
title: "Android SDK Integration"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Android-SDK-Integration"
---

<span id="一-概述"></span>
# Overview

The "A/B Testing" SDK used in the Android client is the Growth Marketing Suite SDK. There are two main interfaces related to A/B Testing:


* Experimental group shunt interface

* Event tracking report interface


<span id="230c5aad"></span>
# Notes before operation


* SDK version: The current SDK version is being released in continuous iterations. You can go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to view the SDK version of each end. The latest version of the SDK is recommended. The code examples in this article use a version number as an example. When you actually use it, you need to modify the version number according to the actual SDK version you are using.

* Download the SDK package: When integrating the SDK, if you need to manually import the SDK, you need to go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to download the corresponding version of the SDK package.


<span id="二-集成sdk"></span>
# 1. Integrated SDK


* If you have already integrated RangerAppLog\-lite/RangerAppLog\-all, you can skip this section.

* If not, please refer to the following:


<span id="c3228a73"></span>
## 1.1 Introduction to the warehouse

**Gradle 7.0 and below:** 

```groovy
//Add the maven repository to the build.gradle at the project level
//Add the maven repository to the repositories of allprojects
allprojects {
    repositories {
        maven {
            url 'https://artifact.bytedance.com/repository/Volcengine/'
        }
        //Other warehouses
    }
}
```


**Gradle 7.0 and above:** 

```typescript
//Add the maven repository in settings.gradle at the project level
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        //omit other
        maven{
            url 'https://artifact.bytedance.com/repository/Volcengine/'
        }
    }
}
```


<span id="55d488ef"></span>
## 1.2 Introduction of plug\-ins (optional)

If you need to enable full event tracking, webview automatic injection, privacy field code removal and other functions, please execute 1.2 to introduce plugins. Otherwise, this step can be skipped.

<span id="1e7ec1f2"></span>
### 1.2.3 Plugin repository

**Gradle 7.0 and below:** 

```groovy
//Add the maven repository and SDK plugin to the repositories of buildscript in the project-level build.gradle
buildscript {
    repositories {
        maven{
            url 'https://artifact.bytedance.com/repository/Volcengine/'
        }
        //omit other
    }
}
```


**Gradle 7.0 and above:** 

```typescript
//settings.gradle
pluginManagement {
    repositories {
        maven{
            url 'https://artifact.bytedance.com/repository/Volcengine/'
        }
        //omit other
    }
}
```


<span id="336888d0"></span>
### 1.2.2 Plugin dependencies


<Tabs>
<Tab zoneid="OZRS6dJlVh" title="Gradle below 7.0">
<TabTitle>Gradle below 7.0</TabTitle>

```Groovy
//Add the maven repository and SDK plugin to the repositories of buildscript in the project-level build.gradle
buildscript {
    //omit other
    dependencies {
        classpath 'com.bytedance.applog:RangersAppLog-All-plugin:6.16.10'
    }
}

//build.gradle at the app module level
//Default to the last declaration in the plugin list, if there is a conflict,
//You can adjust it to the first one after official plugins such as application/kotlin.
apply plugin: 'com.bytedance.std.tracker'
```



</Tab>
<Tab zoneid="MwF53UaK8G" title="Gradle above 7.0 to below 8.0">
<TabTitle>Gradle above 7.0 to below 8.0</TabTitle>

```Groovy
//project-level build.gradle
buildscript {
    //omit other
    dependencies {
        classpath 'com.bytedance.applog:RangersAppLog-All-plugin:6.16.7'
    }
}

//build.gradle at the app module level
//Default to the last declaration in the plugin list, if there is a conflict,
//You can adjust it to the first one after official plugins such as application/kotlin.
plugins {
    //omit other plugins
    id 'com.bytedance.std.tracker'
}
```



</Tab>
<Tab zoneid="FqtdvVDhVj" title="Gradle 8.0 and above">
<TabTitle>Gradle 8.0 and above</TabTitle>

```Groovy
//project-level build.gradle
buildscript {
    dependencies {
        //agp8 version uses the new version plugin
        classpath 'com.bytedance.applog:RangersAppLog-All-plugin-agp8:6.16.7'
    }
}

//build.gradle at the app module level
//Default to the last declaration in the plugin list, if there is a conflict,
//You can adjust it to the first one after official plugins such as application/kotlin.
plugins {
    //omit other plugins
    id 'com.bytedance.std.tracker'
}
```



</Tab>
</Tabs>


<span id="5abea567"></span>
### 1.2.3 Plugin usage example

Apply the plugin in the build.gradle file at the app module level.


<Tabs>
<Tab zoneid="pmz55HFBbd" title="Gradle 8.0 or less">
<TabTitle>Gradle 8.0 or less</TabTitle>

```Groovy
teaExtension {
    //Automatically inject the docking bridge of the webview
    autoInjectWebViewBridge = true

    //instrumentation blacklist, package path prefix, configure for some packages that do not want instrumentation
    //You need to put the. Replace with/, configurable multiple, by, split
    //Example: blackList = ['dji/upgrade/internal', 'org/bouncycastle/jcajce']
    blackList = []

    //event tracking blacklist configuration
    //Only the following configurations are supported:
    //'MAC_ADDRESS': mac address
    //'IMEI_MEID': imei and meid
    // 'OAID'： oaid
    // 'ANDROIDID': android id
     // 'OPERATOR': carrier、mcc_mnc
    //'CLIPBOARD': clipboard related code
    //Example: trackBlackList = ['MAC_ADDRESS', 'IMEI_MEID', 'OPERATOR']
    trackBlackList = []
  
    //6.14.3 new features
    //Turn off the interface/class automatic tracking function
    //Example of usage scenario: When you use the lite package, but you need to trackBlackList to remove part of the capture code, you can use this function
    disableAutoTrack = false
}
```



</Tab>
<Tab zoneid="RdG0sbLjIr" title="Gradle 8.0 and above">
<TabTitle>Gradle 8.0 and above</TabTitle>

```Groovy
// The new version of the plug-in is adjusted to appLo g
appLog {
    //Automatically inject the docking bridge of the webview
    //The get-through function of agp8 needs to use 6.16.7 and above version
    autoInjectWebViewBridge = true

    //instrumentation blacklist, package path prefix, configure for some packages that do not want instrumentation , benchmark the old plugin blackList
    //Example: ignoredInstrumentationPaths = ['dji.upgrade.internal', 'org.bouncycastle.jcajce']
    //From ['dji/upgrade/internal', 'org/bouncycastle/jcajce'] to ['dji.upgrade.internal', 'org.bouncycastle.jcajce']
    ignoredInstrumentationPaths = []

    //event tracking blacklist configuration , benchmark the old plugin trackBlackList
    //Only the following configurations are supported:
    //'MAC_ADDRESS': mac address
    //'IMEI_MEID': imei and meid
    // 'OAID'： oaid
    // 'ANDROIDID': android id
    // 'OPERATOR': carrier、mcc_mnc
    //'CLIPBOARD': clipboard related code
    //Example: sensitiveFieldsBlocklist = ['MAC_ADDRESS', 'IMEI_MEID', 'OPERATOR']
    sensitiveFieldsBlocklist = []
  
    //6.14.3 new features
    //Turn off the interface/class automatic tracking function
    / /Example of usage scenario: When you use the lite package, but need trackBlackList to remove part of the capture code, you can use this function
    disableAutoTrack = false
}
```



</Tab>
</Tabs>


<span id="d48ad9e9"></span>
## 1.3 Introduction of SDK

In the build.gradle file at the app module level, import the SDK in the dependencies.

Currently, two versions of the SDK are available. Please choose one to refer to according to your business needs.

If you need to use the full SDK functionality, please integrate All versions:

```groovy
//Introduce the SDK in the dependencies of the build.gradle file, integrate All versions, this version is recommended
implementation 'com.bytedance.applog:RangersAppLog-All-cn:6.16.10'
```


If you don't need full event tracking collection and circling functions, you only need custom event tracking, which can integrate the Lite version:

```groovy
//Introduce the SDK in the dependencies of the build.gradle file and integrate the Lite version
implementation 'com.bytedance.applog:RangersAppLog-Lite-cn:6.16.10'
```


Please note that the above two versions only need to be integrated by choosing one of the two, otherwise it will cause an error in the compilation.

<span id="_1-4-引入调试工具-devtools组件-可选"></span>
## 1.4 Introducing Debugging Tools \- DevTools Component (Optional)

> This section is supported after 6.12.0 +.


`DevTools`is a component that assists developers or testers in the Debug environment to verify in\-app event tracking and troubleshoot SDK access issues. In the build.gradle file at the app module level, import `DevTools`into the dependencies. For detailed access documentation, please refer to [DevTools-Android Quick Access](https://www.volcengine.com/docs/76880/1033614).

```java
//Dependent DevTools components in the debugging or testing suite
debugImplementation 'com.bytedance.applog:RangersAppLog-DevTools:3.4.6'
//Release dependent DevTools-No-Op components
releaseImplementation 'com.bytedance.applog:RangersAppLog-DevTools-No-Op:3.4.6'
```


<span id="_1-5-实时埋点检测和圈选功能-可选"></span>
### 1.5 Real\-time event tracking and circling (optional)

To use the [real-time event tracking detection ](https://www.volcengine.com/docs/6285/66054)or [circling event feature](https://www.volcengine.com/docs/6285/66197), import the scheme package and configure it according to Chapter 3. Otherwise, this step can be skipped.

⚠️ Please make sure to remove the scheme package before the official launch and only use it during debugging to avoid compliance risks.

```groovy
//Add dependencies to the build.gradle file
implementation 'com.bytedance.applog:RangersAppLog-All-scheme:6.15.4'
```


<span id="_1-6-反作弊风控子库-可选"></span>
### 1.6 Anti\-cheat risk control sublibrary (optional)

If you want to use the ad monitoring function, in order to make its anti\-cheat identification more accurate, please execute Section 1.5 to introduce the risk control sublibrary. Otherwise, this step can be skipped.

```groovy
//Add dependencies to the build.gradle file
implementation 'com.volcengine:metasec_ml:4.3.4'
implementation 'com.bytedance.applog:RangersAppLog-All-metasec-cn:6.15.4'
```


<span id="_1-7-kotlin相关依赖-可选"></span>
### 1.7 Kotlin\-related dependencies (optional)

If you are writing a project in the Kotlin language, follow Section 1.6 to confirm the introduction of the Kotlin dependency. Otherwise, this step can be skipped.

```groovy
implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.3.61'
```


<span id="_1-8-手动引入须知"></span>
### 1.8 Manual introduction instructions

It is recommended that you import the SDK remotely. If special circumstances require manual introduction, please read this section.

Please go to the [Android SDK package download page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main/Android)to get the corresponding version of the SDK package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Android offline package name is <code><em>All-cn-Android_ version number</em></code><code>.zip</code>format. For example: <code>All-cn_Android_6.16.10.zip</code>, where 6.16.10 is the SDK version number.</div>


```groovy
Mandatory dependency:
 - if_encryptor-xxx.aar / encryptor-xxx-private.aar: encryption library related
 - RangersAppLog-All-cn-xxx.aar: Growth Marketing main sector
 - RangersAppLog-Log-xxx.aar: Growth Marketing SDK internal log dependency
 - plugin-aggregation-xxx.aar: Growth Marketing SDK internal information Integrated sectors dependency

Optional dependency:
 - RangersAppLog-All-scheme-xxx.aar: Real-time event tracking detection and circle feature, please refer to chapter 1.5
 - RangersAppLog-All-plugin-xxx.jar: SDK plugin, mainly provide full event tracking / h5 connection / blacklist filter / remove some privacy collection code functions
 - RangersAppLog-DevTools-xxx.aar: Visualization event tracking debugging tool, which can be used  for event tracking process verification


Integration method one, the project already includes all aar/jar files under libs:
//build.gradle in the app directory
implementation fileTree(dir: 'libs', include: ['*.jar','*.aar'])
//At this time, you can add the above required dependencies and some optional dependencies to the libs directory

Integration method two, integrate one by one
//build.gradle in the app directory
implementation files('libs/encryptor-xxx-private.aar')
implementation files('libs/if_encryptor-xxx.aar')
implementation files('libs/RangersAppLog-All-cn-xxx.aar')
implementation files('libs/RangersAppLog-Log-xxx.aar')
implementation files('libs/plugin-aggregation-xxx.aar')
//The remainder is integrated on demand
//Note: The debugging tool recommends only debug mode
debugImplementation files('libs/RangersAppLog-DevTools-xxx.aar')

If using plugins offline, please refer to the following integration methods:
//build.gradle in the root directory
buildscript {
  dependencies {
    //gradle plugin required for growth marketing
    //If you put xxxdir in the app/libs directory, you can replace it with app/libs.
    classpath fileTree(include: ['*.jar'], dir: 'xxxdir/RangersAppLog-All-plugin-xxx.jar')
  }
}

Offline package dependency obfuscation configuration:
-keep class com.bytedance.applog.picker.DomSender { public *; }
-keep class com.bytedance.applog.tracker.WebViewUtil { public *; }
-keep class com.bytedance.applog.metasec.AppLogSecHelper { *; }

-keepclassmembers class * {
    public void loadUrl(java.lang.String);
    public void loadUrl(java.lang.String, java.util.Map);
    public void loadData(java.lang.String, java.lang.String, java.lang.String);
    public void loadDataWithBaseURL(java.lang.String, java.lang.String, java.lang.String, java.lang.String, java.lang.String);
}
```


<span id="_2-初始化sdk"></span>
# 2. Initialize the SDK

The SDK will collect user information during initialization. Please ensure that you have obtained user authorization before collecting user information.

The compliance recommendations are as follows:

After the user authorizes, the SDK is initialized. All information will not be collected before the user authorizes, and the preset events will not be collected.

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_2-2-获取数据上送地址"></span>
## 2.2 Obtain the data upload address

The private deployment version needs to get the data upload address.

If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk"></span>
## 2.3 Initializing the SDK

<span id="4c0ef702"></span>
### Privatized version

If you use the private deployment version, please refer to the following code to initialize the SDK.

```java
public class TheApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        /* Initialize the SDK to start */
        //The first parameter APPID: refer to Section 2.1 to obtain
        //The second parameter CHANNEL: fill in the channel, please note that it cannot be empty
        final InitConfig config = new InitConfig("{{APPID}}", "{{CHANNEL}}");
        //Set the private deployment data upload address, refer to Section 2.2 to obtain, {{REPORT_URL}} For example https://yourdomain.com, be careful not to add "/" after the domain name
        config.setUriConfig(UriConfig.createByDomain("{{REPORT_URL}}", null));
        //Whether to automatically start after init can be changed to false, and please call start to start collection after user authorization
        config.setAutoStart(false);
        
        config.setAbEnable(true); //Start AB test
        config.setAutoTrackEnabled(true); //Full event tracking switch, true on, false off
        config.clearABCacheOnUserChange(true); //Default true, switch user to clear AB version information
        config.setLogEnable(false); //true: turn on the log, refer to Section 4.3 to set the logger, false: turn off the log
        AppLog.setEncryptAndCompress(true); //Encryption switch, true on, false off
        //Initialize once
        //It is recommended to use this method if initializing in the application
        AppLog.init(this, config);
        //It is recommended to use this method if initializing in an activity
        AppLog.init(this, config, activity);
        /* End of initialization SDK */
        
        //Please call the following method after user authorization to start the actual collection of user information + reporting:
        AppLog.start()
    }
}
```


<span id="86f7c305"></span>
### 2.3.4 Multi\-instance initialization (optional)

Multi\-instance initialization means that the SDK supports event tracking to multiple applications (multiple appids) in apps with the same package name, and the event tracking data is isolated from each other, and each appid corresponds to a separate instance. Usage scenarios such as:


* When the third\-party SDK relies on the growth marketing suite SDK to do event tracking generated within the SDK;

* In the same app or system, associate multiple event tracking apps (multiple appids), share, and grow the marketing suite SDK.


```java
//@Since 6.8.0, to use the functions in this section, you need to upgrade the Growth Marketing Suite SDK to 6.8.0 and above
public class TheApplication extends Application {
    
    @Override
    public void onCreate() {
        super.onCreate();
        /* Multi-instance initialization SDK starts, instance 1 */
        final InitConfig config1 = new InitConfig("APPID1", "CHANNEL1");        
        //Create an instance
        IAppLogInstance appLogInst1 = AppLog.newInstance();       
        //Set the data upload address
        config1.setUriConfig(UriConstants.DEFAULT);        
       //Open the upload of the full event tracking event
        config1.setAutoTrackEnabled(true); //Full event tracking switch, true on, false off
        config1.setLogEnable(true); //true: turn on the log, refer to Section 4.3 to set the logger, false: turn off the log
        appLogInst1.setEncryptAndCompress(true); //Encryption switch, true on, false off
        appLogInst1.init(this, config1);
        
        //Example 2
       final InitConfig config2 = new InitConfig("APPID2", "CHANNEL1");
       IAppLogInstance appLogInst2 = AppLog.newInstance();
       config2.setUriConfig(UriConstants.DEFAULT);
       config2.setAutoTrackEnabled(true);
       config2.setLogEnable(true); //true: turn on the log, refer to Section 4.3 to set the logger, false: turn off the log
       appLogInst2.setEncryptAndCompress(true); //Encryption switch, true on, false off
       appLogInst2.init(this, config2);
        /* End of initialization SDK */

      }
   }
```


<span id="b550b8ee"></span>
# 3. Delayed initialization and sensitive information collection

<span id="_3-1-延迟初始化"></span>
## 3.1 Delayed initialization

To ensure compliance, after integrating the SDK, the SDK will be initialized and start collecting information after obtaining user authorization. Please ensure that you have been authorized by the user before collecting user information. If you need to delay initializing the SDK, to compensate for the data impact of the delay on the startup event, please modify the initialization `init`method:

```java
/* Initialize the SDK */
//... other configurations remain unchanged
Modify the init method to add a third parameter to the current Activity object
AppLog.init(this, mConfig, XXXActivity.this);
```


If you still want to initialize as soon as possible, but turn on event tracking collection after user authorization, you can turn off automatic start collection, but because the event between initialization and user authorization will not be able to collect the device number, it will affect the attribution of advertising effect and other analysis.

```kotlin
//Application does not automatically start acquisition through configuration adjustment
config.setAutoStart(false);
AppLog.init(this, config);

//After the user authorizes, call the following method
AppLog.start()；
```


<span id="_3-2-关闭mac地址采集"></span>
## 3.2 Oaid acquisition configuration

> After 6.16.10, self\-sustaining 360 Oaid collection, if you need to collect, please configure it in the Android Manifest.xml of the App:


```Plain
<queries>
    <!--    qiku 360 OAID obtain and add    -->
    <package android:name="com.qiku.id"/>
</queries>
```


<span id="7cf0d17e"></span>
## 3.3 Turn off MAC address acquisition

The following is the initialization basic configuration of sensitive field collection, `config`refers to the `InitConfig` at initialization. The device's Mac address acquisition is enabled by default. To close:

```java
//After the switch is turned off, the relevant code does not run, and the attributes are not collected. Whether to upload depends on whether the customer has passed in the MAC from the outside.
config.setMacEnable(false);
```


To remove the relevant code for MAC address collection, you can configure it in the full event tracking plugin:

```groovy
//This function only supports 6.9.0 and above versions
teaExtension {
    // ... Other configurations
    trackBlackList = ["MAC_ADDRESS"]

                //You are using the Lite package and need to remove the collection related code.
    //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
    disableAutoTrack = true
}
```


<span id="_3-3-关闭设备imei-meid采集"></span>
## 3.4 Turn off device IMEI/MEID acquisition

The device's IMEI address collection is enabled by default. To close:

```java
//After the switch is turned off, the relevant code does not run, the attributes are not collected, and whether to upload depends on whether the customer has passed AppImei from the outside.
config.setImeiEnable(false);
```


To remove the relevant code for IMEI and MEID collection, you can configure it in the full event tracking Plugin:

```groovy
//This function only supports 6.9.0 and above versions
teaExtension {
    // ... Other configurations
    trackBlackList = ["IMEI_MEID"]

    //You are using the Lite package and need to remove the collection related code.
    //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
    disableAutoTrack = true
}
```


<span id="_3-4-关闭oaid采集"></span>
## 3.5 Turn off OAID acquisition

The device's OAID information collection is turned on by default. To close:

```java
//After the switch is turned off, the relevant code does not run, and the attributes cannot be collected and sent.
config.setOaidEnabled(false);
```


To remove the relevant code for OAID collection, you can configure it in the full event tracking Plugin:

```groovy
//This function only supports 6.10.1 and above versions
teaExtension {
    // ... Other configurations
    trackBlackList = [ "OAID" ]

    //You are using the Lite package and need to remove the collection related code.
    //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
    disableAutoTrack = true
}
groovy
```


<span id="_3-5-关闭android-id采集"></span>
## 3.6 Turn off Android ID collection

Attention

Turning off Android ID will affect the uninstall and reinstall consistency, please close it carefully.

The Android ID collection of the device is turned on by default, if you need to turn it off:

```java
//After the switch is turned off, the relevant code will not run, and the properties will not be collected. It will be randomly generated after closing.
config.setAndroidIdEnabled(false);
```


To remove the Android ID capture code, you can configure it in the Full event tracking Plugin:

```groovy
//This function only supports 6.10.1 and above versions
teaExtension {
    // ... Other configurations
    trackBlackList = [ "ANDROIDID" ]

    //You are using the Lite package and need to remove the collection related code.
    //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
    disableAutoTrack = true
}
```


<span id="_3-6-关闭-iccid-采集"></span>
## 3.7 Turn off ICCID collection

The ICCID collection of the device is turned on by default, if you need to turn it off:

```java
//After the switch is closed, the relevant code does not run, and the attributes are not collected and cannot be sent//This function only supports 6.14.3 and above versions
config.setIccIdEnabled(false);
```


ICCID does not currently support removing capture code via plug\-ins.

<span id="_3-7-关闭-sn（硬件序列号）-采集"></span>
## 3.8 Turn off SN (hardware serial number) acquisition

The SN acquisition of the device is turned on by default, if you need to turn it off:

```java
//After the switch is closed, the relevant code does not run, and the attributes are not collected and cannot be sent//This function only supports 6.16.1 and above versions
config.setSerialNumberEnable(false);
```


SN does not currently support removing capture code through plug\-ins.

<span id="_3-8-关闭-gaid-采集"></span>
## 3.9 Turn off GAID collection

Device GAID acquisition default scheme:


* 6.16.1 before cn (domestic version) and global (overseas version) are collected by default.

* 6.16.1 and after cn is closed by default, global is turned on by default.


To close:

```java
//After the switch is closed, the relevant code does not run, the attributes are not collected, and whether to upload depends on whether the customer has passed Gaid from the outside.
config.setGaidEnabled(false);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">⚠️Please note that since the switch is turned on by default before the 6.16.1 version of the SDK package at home and abroad, it may cause third parties in the domestic application package to try to obtain GAID after integrating Google Service, and GAID is time\-consuming, which may have ANR problems in some models or affect the response time of device registration requests.</div>


```java
//The acquisition timeout time control is provided for the Gaid acquisition time-consuming SDK. If the acquisition time is not collected, it will directly return to empty//The default time is 2s timeout, and the method parameter ms//The method 6.16.1 provided
config.setGaidTimeOutMilliSeconds(2000)
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">⚠️Please note that since the switch is turned on by default in both domestic and foreign SDK packages, it may cause third parties in domestic application packages to try to obtain GAID after integrating Google Service, and GAID is time\-consuming, which may have ANR problems in some models or affect the response time of device registration requests.</div>


<span id="_3-9-关闭运营商信息采集"></span>
## **3.10 Turn off operator information collection**

The operator information of the device is collected by default, if you need to turn it off:

```java
//After the switch is turned off, the relevant code does not run, and the attributes cannot be collected and sent.
config.setOperatorInfoEnabled(false);
```


To remove the carrier information collection code, you can configure it in the full event tracking Plugin:

```java
//This function only supports 6.10.1 and above versions
teaExtension {
    // ... Other configurations
    trackBlackList = [ "OPERATOR" ]

    //You are using the Lite package, and you need to remove the collection-related code.//You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. Provide from 6.14.3
    disableAutoTrack = true
}
```


<span id="281582fa"></span>
## 3.11 Remove clipboard access code

Cut version access is currently used for advertising monitoring is turned off by default, if you need to open it, you can refer to: [Open clipboard](https://www.volcengine.com/docs/6285/116319#_1-2-4-%E5%BC%80%E5%90%AF%E5%89%AA%E5%88%87%E6%9D%BF)

To remove the clipboard access code, you can configure it in the full event tracking Plugin:


<Tabs>
<Tab zoneid="HzuhFmnE3r" title="Gradle 8.0 or less">
<TabTitle>Gradle 8.0 or less</TabTitle>

```Groovy
//This function only supports 6.16.3 and above versions
teaExtension {
    // ... Other configurations
    trackBlackList = ["CLIPBOARD"]

    //You are using the Lite package and need to remove the collection related code.
    //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
    disableAutoTrack = true
}
```



</Tab>
<Tab zoneid="vUz1D52gEw" title="Gradle 8.0 and above">
<TabTitle>Gradle 8.0 and above</TabTitle>

```Groovy
//This function only supports 6.16.3 and above versions
//AGP8 version plugin 6.16.3 support
appLog {
    // ... Other configurations
    sensitiveFieldsBlocklist = ["CLIPBOARD"]
  
    //You are using the Lite package and need to remove the collection related code.
    //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
    disableAutoTrack = true
}
```



</Tab>
</Tabs>


<span id="_4-配置scheme-可选"></span>
# 4. Configuration Scheme (optional)

To use [real-time event tracking detection ](https://www.volcengine.com/docs/6285/66054)or [circling features ](https://www.volcengine.com/docs/6287/101834), configure Scheme. Otherwise, this step can be skipped.

<span id="_4-1-获取url-scheme"></span>
## 4.1 Obtaining URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3fc47667b264d36bad9a4f9df2f3863~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-添加url-scheme"></span>
## 4.2 Adding URL Schemes

Add URL Scheme to build.gradle at the app module level.

```groovy
//Add defaultConfig in android
manifestPlaceholders.put("APPLOG_SCHEME", "{{URL_SCHEME}}".toLowerCase())
```


<span id="_5-初始化基本配置"></span>
# 5. Initialize the basic configuration

The following are common initialization basic configuration, `config`refers to the initialization of `InitConfig`.

<span id="_5-1-全埋点采集开关"></span>
## 5.1 Full event tracking acquisition switch

The default full event tracking switch is on, if you want to turn it off:

```java
//Open the upload of the full event tracking event
config.setAutoTrackEnabled(true); //true: enable full event tracking, false: turn off full event tracking
```


After turning on full event tracking, page events and click events will be collected by default. If you need to customize full event tracking collection, the configuration method is as follows:

```java
//Default: AutoTrackEventType.PAGE | AutoTrackEventType.CLICK
//AutoTrackEventType. ALL: All events tracking
//AutoTrackEventType.PAGE: full event tracking page event, turned on by default
//AutoTrackEventType.CLICK: All buried point click event, turned on by default
//AutoTrackEventType.PAGE_LEAVE: Full event tracking page duration event, off by default//This function only supports 6.11.0 and above versions
config.setAutoTrackEventType(AutoTrackEventType.PAGE | AutoTrackEventType.CLICK | AutoTrackEventType.PAGE_LEAVE);
```


Page view events in full event tracking, default for Activity pages. To turn on the bav2b_page event acquisition for Fragment, in addition to the above switch, the Fragment acquisition switch needs to be turned on additionally.

```java
//Enable Fragment full event tracking event collection
config.setAutoTrackFragmentEnabled(true);
```


<span id="a617d106"></span>
## 5.2 Turn on event tracking

Circle event tracking is off by default.

```java
//Turn on the event tracking function. To use this function, you need to turn on full event tracking first.
config.setPicker(new Picker(this, config));

//If you want to turn on the circle selection for the h5 embedded in the App, please turn on the js injection switch:
config.setH5CollectEnable(true);
//Note: h5 circle selection only supports native WebView and Tencent X5
```


<span id="83d1ccde"></span>
## 5.3 AB function switch

```plain
config.setAbEnable(true); // enable AB testing
```


<span id="5d717d83"></span>
## 5.4 View log printing

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">⚠️ Please note that log printing is turned off by default, and it is recommended that production packages be turned off online.</div>


```java
//Output logs in the console, which can be used to observe user behavior log reports. It is recommended to close it when online
config.setLogEnable(true); //true: open log, false: close log
config.setLogger(new ILogger() {
    @Override
    public void log(String s, Throwable throwable) {
        Log.d("AppLog------->: ", "" + s);
    }
});
```


<span id="1127b8e9"></span>
## 5.5 Switch the user to clear the AB information switch

The switch is turned on by default. When switching users, empty the AB information hit in the cache; if the switching user does not want to empty the cache, it can be changed to false.

```json
config.clearABCacheOnUserChange(true); //Default true, switch user to clear AB version information
```


<span id="eb4d4af6"></span>
## 5.6 Encryption setting switch

Encryption settings are enabled by default. You can turn off encryption during the debug phase to facilitate joint debugging.

```java
//Encryption setting switch, it is recommended to turn on the online version.
AppLog.setEncryptAndCompress(true); //true: open encryption, false: close encryption
```


<span id="27a49291"></span>
## 5.7 Setting APP Language and APP Region

```java
//Modify language and region, set APP Language and APP Region
config.setLanguage(...); //Set APP Language, such as zh-cn
config.setRegion(...); //Set the APP Region, such as cn
```


<span id="85544f18"></span>
## 5.8 Open the embedded H5 page

If your application integrates the Web/JS SDK and the Android SDK at the same time, by default, all H5 events will be reported through the Web/JS SDK. If you want the H5 event to be reported by the Android SDK, you can use the embedded H5 function. At this time, the events generated on the H5 page will be reported through the Android SDK instead of the Web/JS SDK. This takeover reporting scenario will reuse the `user_unique_id`and public properties set by the Android side.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get through the function requires the Web/JS SDK and Android SDK to integrate and cooperate with each other at the same time, and the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, because the reporting is taken over by the Android SDK at this time. If you still want to collect H5 full event tracking, you need to check Section 5.9: Native collection of H5 full event tracking. Web/JS SDK Integration Refer to <strong>Web/JS SDK Integration</strong> and Section 3.6.</div>


```java
//Note: This function only supports native WebView and Tencent X5//The following configurations need to be turned on at the same time. If the following two are not satisfied at the same time, the H5 event will continue to be reported to the Web/JS SDK://Android SDK turns on the embedded H5 open switch
config.setH5BridgeEnable(true);
//Web/JS SDK set H5 to be embedded in the native side and get through
window.collectEvent('init', {
    // ...... Other initialization configurations
    enable_native: true 
    //5.1.3 the following version parameters are Native,//5.1.3 the above version is modified to enable_native, but still compatible with Native settings
})

//Supplement: Since the Web/JS SDK blocks the full event tracking function of H5 at this time,//the full event tracking setting switch of the Web/JS SDK is invalid.//If you want to still maintain the full event tracking function of H5, please check the 4.7 section
window.collectEvent('init', {
    //Full event tracking setting switch
    autotrack: invalid
})
```


<span id="7239f9ce"></span>
### 5.8.1 get through the whitelist front work of the embedded H5 page

After the switch is turned on, the whitelist must be configured. Only the domain names configured in the whitelist take effect. The whitelist can be added by wild\-card, and `*`means wild\-card.

```java
//Embedded H5 page whitelist configuration//Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
config.setH5BridgeAllowlist(Arrays.asList("www.volcengine.com", "*.bytedance.*"));
//There are many whitelists for www.bytedance.com, please configure the whitelist according to the business scenario, for example://www.bytedance.com or.bytedance. Or *.*.* can be achieved.
```


If you don't filter any domain names and local resource files, you can configure to allow all H5 pages to open. This configuration has a higher priority than `setH5BridgeAllowlist`.

```java
//Allow all h5 to get through//This function only supports 6.9.7 and above versions
config.setH5BridgeAllowAll(true);
```


<span id="c5ff0dca"></span>
### 5.8.2 through the embedded H5 page plug\-in injection note

Under normal circumstances, H5 to get through requires you to refer to Section 1.2 integrated plugin plugin, at this time, the injection Bridge is completed by Plugin instrumentation, but in some scenarios, instrumentation may not take effect (the scene of plug failure may be confused, overwritten, etc.), you can choose to manually turn off the SDK's automatic injection Bridge ability, and then manually call injection, at this time, you can add configuration in the full event tracking plugin `autoInjectWebViewBridge = false`, and then manually inject Bridge before the WebView that needs to get through loads H5.


<Tabs>
<Tab zoneid="K5WSNcDLpX" title="Gradle 8.0 or below turns off automatic injection of plugins">
<TabTitle>Gradle 8.0 or below turns off automatic injection of plugins</TabTitle>

```Groovy
//Turn off automatic injection through plugins
teaExtension {
    //Close the docking bridge that automatically injects webview
    autoInjectWebViewBridge = false
    //Omit other uses of plugins
}
```



</Tab>
<Tab zoneid="l1ERqTfvhl" title="Gradle 8.0 and above turn off automatic injection of plugins">
<TabTitle>Gradle 8.0 and above turn off automatic injection of plugins</TabTitle>

```Groovy
//AGP8 version plugin 6.16.3 support
appLog {
    //Close the docking bridge that automatically injects webview
    autoInjectWebViewBridge = false
    //Omit other uses of plugins
}
```



</Tab>
</Tabs>


```Java
//This function only supports 6.13.0 and above versions
WebView myWebView = findViewById(R.id.webview);
//Inject Bridge before loadUrl
AppLog.initWebViewBridge(myWebView, url);
myWebView.loadUrl(url);
```


<span id="b030e245"></span>
## 5.9 Native acquisition H5 full event tracking

When the H5 page is embedded in the native end, the H5 page full event tracking event can be collected from the native end by turning on the following switch.

There are generally two usage scenarios:


* Since the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, in order to ensure that the H5 page full event tracking function can still be retained after getting through.

* Independent use, in the case that H5 does not integrate Web/JS SDK, I want to enable the full event tracking function on the H5 page in the application


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature can be used independently without the need to integrate a Web/JavaScript SDK.</div>


* <div data-tips="true" data-tips-type="warning">This feature is available 6.14.4 version, and the current H5 full event tracking only supports page entry events and click events.</div>



```java
//Note: This feature only supports native WebView and Tencent X5

//Embedded H5 page full event tracking event
config.setH5CollectEnable(true); //true: turn on h5 full event tracking event, false: turn off h5 full event tracking event

//Supplement, this function is also injected by plug-in by default. When the plug-in fails or you want to inject it manually,
//You can refer to 4.6.2 subsection, 4.6, 4.7 although the function is independent but through the unified method of injection control,
//However, you can configure whether to turn it on through the respective switches.
```


<span id="0b04d016"></span>
## 5.10 Full event tracking

The default full event tracking switch is on, if you want to turn it off:

```java
config.setAutoTrackEnabled(false);
```


After turning on full event tracking, page events and click events will be collected by default. If you need to customize full event tracking collection, the configuration method is as follows:

```java
//Default: AutoTrackEventType.PAGE | AutoTrackEventType.CLICK
//
//AutoTrackEventType. ALL: All events tracking
//AutoTrackEventType.PAGE: full event tracking page event, turned on by default
//AutoTrackEventType.CLICK: All buried point click event, turned on by default
//AutoTrackEventType.PAGE_LEAVE: full event tracking page duration event, off by default
//This function only supports 6.11.0 and above versions
config.setAutoTrackEventType(AutoTrackEventType.PAGE | AutoTrackEventType.CLICK | AutoTrackEventType.PAGE_LEAVE);
```


<span id="5816557c"></span>
## 5.11 Setting GPS Coordinates

GPS coordinates are not collected by default. If you need to collect, you need to manually set the GPS coordinate information. Example:

```java
//GeoCoordinateSystemConst is a static class of coordinate system
//WGS84 Earth coordinate system
//GCJ02 Mars coordinate system
//BD09 Baidu coordinate system
//BDCS Beidou coordinate system
//This function only supports 6.10.1 and above versions
AppLog.setGPSLocation(18.00f, 18.00f, GeoCoordinateSystemConst.WGS84);
```


<span id="e6ddf288"></span>
## 5.12 Turn on crash acquisition

By default, the application crash event `$crash`is not collected. To enable:

```java
//Currently only supports capturing Java crashes
//This function only supports 6.13.0 and above versions
config.setTrackCrashType(AppCrashType.JAVA);
```


<span id="bdbdc20e"></span>
## 5.13 Open Fragment Page Event Collection

Default Fragment page event collection is turned off, after turning on the switch, each Fragment access will also record a page access event ($bav2b_page). To open:

```java
//This function only supports 6.13.0 and above versions
config.setAutoTrackFragmentEnabled(true);
```


<span id="96e82ec7"></span>
## 5.14 Whether to distinguish Hongmeng equipment

The data collection report will distinguish whether it is Hongmeng system:

```java
//This function only supports 6.14.3 and above versions
config.setHarmonyEnable(true);
```


<span id="4b10ba33"></span>
# 6. Permissions Description

Growth Marketing Suite Android SDK Permissions List:


|**Permission** |**Description** |**Use scenario and purpose** |
|---|---|---|
|android.permission.READ_PHONE_STATE |Read IMEI and other device information as device identification |Device registration: initialize reading, generate a unique device identifier, and calculate the number of devices |
|android.permission.ACCESS_WIFI_STATE |Get network status (wifi) |Device registration and event tracking data collection: collect device network (wifi) information |
|android.permission.ACCESS_NETWORK_STATE |Get network status |Device registration and event tracking data collection: collect device network information |
|android.permission.INTERNET |Send a network request |Register, report event tracking, attribution, activation, etc.: report event tracking data to a remote server |
|com.asus.msa.SupplementaryDID.ACCESS |Read oaid |Device registration and deep linking: Identifying devices across apps |


&nbsp;
