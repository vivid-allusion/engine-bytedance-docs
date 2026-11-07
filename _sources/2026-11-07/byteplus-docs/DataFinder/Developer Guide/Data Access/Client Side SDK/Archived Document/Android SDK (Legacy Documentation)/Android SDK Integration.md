---
title: "Android SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Android_SDK_Integration_"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Android SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration">Android SDK Integration</a></div>


<span id="79ed9d7c"></span>
# Notes before operation


* SDK version: The current SDK version is being released in continuous iterations. You can go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to view the SDK version of each end. The latest version of the SDK is recommended. The code examples in this article use a version number as an example. When you actually use it, you need to modify the version number according to the actual SDK version you are using.

* Download the SDK package: When integrating the SDK, if you need to manually import the SDK, you need to go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to download the corresponding version of the SDK package.

* When using the Android SDK, you can first learn about the common data reporting policy ( [Data reporting strategy](https://docs.byteplus.com/docs/DataFinder/DataFinder_Data_Access_Overview#1e80ed67)), the supported preset events ( [Android-Side Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Android-Side_Preset_Events_and_Properties)), and the reporting process on the Android side ( [9. Reference: Data reporting process and trigger timing](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_#d366c09b)).


<span id="5257dfb2"></span>
# 1. Integrated Growth Marketing Suite SDK

<span id="_1-1-引入仓库"></span>
## 1.1 Introduction to the warehouse


* Gradle below 7.0

   ```Groovy
   // Add the maven repository to the build.gradle at the project level
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
   

* Gradle 7.0 and above

   ```Groovy
   //Add the maven repository in settings.gradle at the project level
   dependencyResolutionManagement {
       repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
       repositories {
           maven {
               url 'https://artifact.bytedance.com/repository/Volcengine/'
           }
           //Other warehouses
       }
   }
   ```
   


<span id="_1-2-引入插件-可选"></span>
## 1.2 Introduction of plug\-ins (optional)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to enable full event tracking, webview automatic injection, privacy field code removal and other functions, please execute 1.2 to introduce plugins. Otherwise, this step can be skipped.</div>


<span id="66c95b64"></span>
### 1.2.1 Plugin repository


* Gradle below 7.0

   ```Groovy
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
   

* Gradle 7.0 and above

   ```Groovy
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
   


<span id="52df70cd"></span>
### 1.2.2 Plugin dependencies


* Gradle below 7.0

   ```Groovy
   //Add the maven repository and SDK plugin to the repositories of buildscript in the project-level build.gradle
   buildscript {
       //omit other
       dependencies {
           classpath 'com.bytedance.applog:RangersAppLog-All-plugin:6.17.1'
       }
   }
   
   //build.gradle at the app module level
   //Default to the last declaration in the plugin list, if there is a conflict,
   //You can adjust it to the first one after official plugins such as application/kotlin.
   apply plugin: 'com.bytedance.std.tracker'
   ```
   

* Gradle 7.0 and above~ 8.0 and below

   ```Groovy
   //project-level build.gradle
   buildscript {
       //omit other
       dependencies {
           classpath 'com.bytedance.applog:RangersAppLog-All-plugin:6.17.1'
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
   

* Gradle 8.0 and above

   ```Groovy
   //project-level build.gradle
   buildscript {
       dependencies {
           //agp8 version uses the new version plugin
           classpath 'com.bytedance.applog:RangersAppLog-All-plugin-agp8:6.17.1'
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
   


<span id="fde4f1eb"></span>
### 1.2.3 Plugin usage example

Apply the plugin in the build.gradle file at the app module level.


* Gradle 8.0 or less

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
   

* Gradle 8.0 and above

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
   


<span id="53dca97a"></span>
## 1.3 Introduction of SDK

In the build.gradle file at the app module level, import the SDK in the dependencies.

The Growth Marketing Suite provides two versions of the SDK, please choose one to refer to according to your business needs.


* If you need to use the full SDK functionality, please integrate All versions:

   ```groovy
   //In the dependencies of the build.gradle file, introduce the SDK and integrate All versions. This version is recommended
   implementation 'com.bytedance.applog:RangersAppLog-All-cn:6.17.1'
   ```
   

* If you don't need full event tracking, circle selection, web connection and other functions, you only need to customize event tracking, which can be integrated with the Lite version:

   ```groovy
   //Introduce the SDK in the dependencies of the build.gradle file and integrate the Lite version .
   implementation 'com.bytedance.applog:RangersAppLog-Lite-cn:6.17.1'
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The above two versions only need to choose one of the two to integrate, otherwise it will cause an error in the compilation.</div>


<span id="3342f189"></span>
## 1.4 Introduction of Debugging Tools DevTools Component (optional)

> This section is supported after 6.12.0 +.


`DevTools`is a component that assists developers or testers in the Debug environment to verify in\-app event tracking and troubleshoot SDK access issues. In the build.gradle file at the app module level, import `DevTools`in the dependencies. For detailed access documentation, please refer to: [Android event tracking power builder ](https://www.volcengine.com/docs/76880/1033614).

```java
//It is recommended to debug only under debug or testing suite
//Dependent DevTools components in the debugging or testing suite
debugImplementation 'com.bytedance.applog:RangersAppLog-DevTools:3.4.7'
```


<span id="_1-5-实时埋点检测和圈选功能-可选"></span>
## 1.5 Real\-time event tracking and circling (optional)

If you need [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification), execute Section 1.5 to import the scheme package, otherwise you can skip this step.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please make sure to remove the scheme package before the official launch and only use it during debugging to avoid compliance risks.</div>


```groovy
//Add dependencies to the build.gradle file
implementation 'com.bytedance.applog:RangersAppLog-All-scheme:6.17.1'
```


<span id="_1-7-kotlin相关依赖-可选"></span>
## 1.6 Kotlin\-related dependencies (optional)

If you are writing a project in Kotlin, please follow Section 1.7 to confirm the introduction of the Kotlin dependencies, otherwise you can skip this step.

```groovy
//example version
implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.3.61'
```


<span id="_1-8-手动引入须知"></span>
## 1.7 Manual introduction instructions

It is recommended that you import the SDK remotely. If special circumstances require manual introduction, please read this section.

Please go to the [Android SDK package download page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main/Android)to get the corresponding version of the SDK package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Android offline package name is <code><em>All-cn-Android_ version number</em></code><code>.zip</code>format. For example: <code>All-cn_Android_6.16.6.zip</code>, where 6.16.6 is the SDK version number.</div>


```Plain
Mandatory dependency:
 - if_encryptor-xxx.aar（6.17.0 and versions before） / encryptor-xxx-private.aar: Encryption library related
 - RangersAppLog-All-cn-xxx.aar: DataFinder main module
 - RangersAppLog-Log-xxx.aar: DataFinder SDK internal log dependency
 - plugin-aggregation-xxx.aar: DataFinder SDK internal information aggregation module dependency

Optional dependency:
 - RangersAppLog-All-scheme-xxx.aar: Real-time event tracking detection and circle selection function, please refer to 1.5 for exploration
 - RangersAppLog-All-metasec-cn-xxx.aar: anti cheating risk control sub library, please refer to 1.6 for exploration
 - RangersAppLog-All-plugin-xxx.jar: SDK plugin, mainly provides full event tracking / h5 open up / blacklist filter  / remove some privacy collection code functions
 - RangersAppLog-DevTools-xxx.aar: Visual event tracking debugging tool, which can be used for verifying the event tracking process


Integration method one, the project already includes all aar/jar files under libs:
// build.gradle under app directory
implementation fileTree(dir: 'libs', include: ['*.jar','*.aar'])
// At this point, you can add the necessary dependencies and some optional dependencies to the libs directory

Integration method two, integrate one by one:
// build.gradle under app directory
implementation files('libs/encryptor-xxx-private.aar')
// if_encryptor-xxx is removed in 6.17.1 and later versions
implementation files('libs/if_encryptor-xxx.aar')
implementation files('libs/RangersAppLog-All-cn-xxx.aar')
implementation files('libs/RangersAppLog-Log-xxx.aar')
implementation files('libs/plugin-aggregation-xxx.aar')
// The remaining parts are integrated as needed
// Note: Debugging tools are recommended to only debug mode
debugImplementation files('libs/RangersAppLog-DevTools-xxx.aar')

If you use plugin offline, please refer to integration method below:
// build.gradle under root directory
buildscript {
  dependencies {
    // the gradle plugin needed by DataFinder
    // If it is put under app/libs directory, xxxdir below can be replaced with app/libs.
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


<span id="_2-初始化增长营销套件sdk"></span>
# 2. Initialize the Growth Marketing Suite SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended that you initialize the SDK after the user agrees to the Privacy Policy in your app; before the user agrees to the Privacy Policy, you should avoid dynamically applying for sensitive device permissions involving the user's personal information, and you should avoid privately collecting and reporting personal information. When your app does not provide services to users, do not request services related to the SDK.</div>


<span id="_2-1-获取appid"></span>
## 2.1 Get the appid.


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-获取数据上送地址"></span>
## 2.2 Obtain the data upload address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="b22723a0"></span>
### SaaS\-cloud\-native


|End type |SaaS\-cloud native environment<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|Android |* https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* You need to use the overseas package: 'com.bytedance.applog: RangersAppLog\-All\-global: xxx' |* No configuration required, report to SG by default<br><br>* Need to use with overseas package: `'com.bytedance.applog: RangersAppLog-All-global: xxx'` |


<span id="a69737ab"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk"></span>
## 2.3 Initializing the SDK

<span id="9c525a3e"></span>
## 2.4 Multi\-instance initialization (optional)

Multi\-instance initialization means that the SDK supports event tracking to multiple applications (multiple appids) in apps with the same package name, and the event tracking data is isolated from each other, and each appid corresponds to a separate instance. Usage scenarios such as:


* When the third\-party SDK relies on the **Growth Marketing Suite SDK** to do event tracking generated internally in the SDK;

* When you associate multiple event tracking apps (multiple appids) in the same app or system and share the **Growth Marketing Suite SDK** ;


The example code is as follows.


* Java

   ```Java
   /* Multi-instance initialization of SDK instance 1 */
   final InitConfig config1 = new InitConfig("yourAPPID1", "yourCHANNEL1");
   //Create an instance
   IAppLogInstance appLogInst1 = AppLog.newInstance();
   //Set the data upload address
   config1.setUriConfig(UriConstants.DEFAULT);
   //Whether to automatically start after init can be changed to false, and please call start to start collection after user authorization
   config1.setAutoStart(false);
   //Open the upload of the full event tracking event
   config1.setAutoTrackEnabled(true); //Full event tracking switch, true on, false off
   config1.setLogEnable(true); //true: turn on the log, refer to Section 4.3 to set the logger, false: turn off the log
   appLogInst1.setEncryptAndCompress(true); //Encryption switch, true on, false off
   //Initialize once
   //It is recommended to use this method for initialization in Applition
   appLogInst1.init(this, config1);
   //It is recommended to use this method for initialization in Activity
   appLogInst1.init(this, config1, activity);
   
   //Example 2
   final InitConfig config2 = new InitConfig("yourAPPID2", "yourCHANNEL2");
   IAppLogInstance appLogInst2 = AppLog.newInstance();
   config2.setUriConfig(UriConstants.DEFAULT);
   //Whether to automatically start after init can be changed to false, and please call start to start collection after user authorization
   config2.setAutoStart(false);
   config2.setAutoTrackEnabled(true);
   config2.setLogEnable(true); //true: turn on the log, refer to Section 4.3 to set the logger, false: turn off the log
   appLogInst2.setEncryptAndCompress(true); //Encryption switch, true on, false off
   //Initialize once
   //It is recommended to use this method for initialization in Applition
   appLogInst2.init(this, config2);
   //It is recommended to use this method for initialization in Activity
   appLogInst2.init(this, config2, activity);
   
   //Please call the following method after user authorization to start the actual collection of user information + reporting:
   appLogInst1.start();
   appLogInst2.start();
   ```
   

* Kotlin

   ```Kotlin
   /* Initialize the SDK */
   //The first parameter APPID: refer to Section 2.1 to obtain
   //The second parameter CHANNEL: fill in the channel information, please note that it cannot be empty
   val appLogInst1 = AppLog.newInstance()
   val config1 = InitConfig("yourAPPID1", "yourCHANNEL1").apply {
       //Set the data upload address
       uriConfig = UriConfig.createByDomain("https://gator.volces.com", null)
       //Whether to automatically start after init can be changed to false, and please call start to start collection after user authorization
       setAutoStart(false)
       //Full event tracking switch, true on, false off
       isAutoTrackEnabled = true
       //true: turn on the log, refer to Section 4.3 to set the logger, false: turn off the log
       isLogEnable = false
   }
   //Encryption switch, true on, false off
   appLogInst1.encryptAndCompress = true
   //Initialize once
   //It is recommended to use this method for initialization in Applition
   appLogInst1.init(this, config1)
   //It is recommended to use this method for initialization in Activity
   appLogInst1.init(this, config1, activity)
   
   val appLogInst2 = AppLog.newInstance()
   val config2 = InitConfig("yourAPPID2", "yourCHANNEL2").apply {
       //Set the data upload address
       uriConfig = UriConfig.createByDomain("https://gator.volces.com", null)
       //Whether to automatically start after init can be changed to false, and please call start to start collection after user authorization
       setAutoStart(false)
       //Full event tracking switch, true on, false off
       isAutoTrackEnabled = true
       //true: turn on the log, refer to Section 4.3 to set the logger, false: turn off the log
       isLogEnable = false
   }
   //Encryption switch, true on, false off
   appLogInst2.encryptAndCompress = true
   appLogInst2.init(context, config2)
   //Initialize once
   //It is recommended to use this method for initialization in Applition
   appLogInst2.init(this, config2)
   //It is recommended to use this method for initialization in Activity
   appLogInst2.init(this, config2, activity)
           
   //Please call the following method after user authorization to start the actual collection of user information + reporting:
   appLogInst1.start();
   appLogInst2.start();
   ```
   


<span id="_3-延迟初始化与敏感信息采集"></span>
# 3. Delayed initialization and sensitive information collection

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SaaS\-cloud native and privatized 4.4.0 versions and above also support turning off sensitive field collection in the DataFinder console. You can turn off sensitive field collection in Project Management \> SDK Settings <a href="https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings">Project Management \- SDK Settings</a>.</div>


<span id="_3-1-延迟初始化"></span>
## 3.1 Delayed initialization

To ensure compliance, it is recommended that you initialize the SDK after obtaining user authorization, enable functions according to the scenario, and obtain personal information. If you use the above recommended delayed initialization SDK, to compensate for the data impact of delayed initialization on the startup event, please modify the initialization init method:

```java
/* Initialize the SDK */
//... other configurations remain unchanged
Modify the init method to add a third parameter to the current Activity object
AppLog.init(this, mConfig, XXXActivity.this);
```


In order to avoid the impact of delayed data acquisition on SDK services, it is recommended to turn on event tracking collection as soon as possible after initialization, and we provide you with an automatic start collection switch. If you want to control the timing of turning on event tracking collection, you can turn off the automatic start collection switch, but because the event between the initialization and the user authorization will not be able to collect the device number, it will affect the attribution of advertising effect and other analysis.

```Java
//Application does not automatically start acquisition through configuration adjustment
config.setAutoStart(false);
AppLog.init(this, config);


//After the user authorizes, call the following method
AppLog.start()；
```


<span id="212af5b8"></span>
## 3.2 Oaid acquisition configuration

> After 6.16.10, 360 Oaid collection is supported. If you want to collect, please configure it in the AndroidManifest.xml of the App:


```Plain
<queries>
    <!--    qiku 360 OAID acquire and add    -->
    <package android:name="com.qiku.id"/>
</queries>
```


<span id="f49462f1"></span>
## 3.3 Custom Oaid Collection

> If you integrate an OAID acquisition SDK such as MSA, you can change the Oaid acquisition logic built into AppLog to the application\-side acquisition logic.


```Plain
// newly-added in 6.16.11 version
/* Initialize the SDK */
final InitConfig config = new InitConfig("yourAPPID", "yourCHANNEL");
// Key point: Ensure that user information collection begins only after the start
config.setAutoStart(false);
// Key point: set custom Oaid, custom configure callback
config.setCustomOaidCallback(new DynamicValueCallback<String>() {
    @Override
    public String get() {
        // Custom retrieval logic, if no callback is set or callback returns ""/null, follow the built-in Oaid collection logic
        return getCustomOaid();
    }
});
// omit other SDK configuration
// initialize once is sufficient
// It is recommended to use this method for initialization in Application
AppLog.init(this, config);
// It is recommended to use this method for initialization in Activity
AppLog.init(this, config, activity);

// Key point: Since setAutoStart is set to false, the SDK needs to be manually triggered by calling start. Please call it after obtaining the oaid.
// start begins to collect user information and report:
AppLog.start()；
```


<span id="_3-2-关闭mac地址采集"></span>
## 3.4 Turn off MAC address acquisition

The following is the initialization basic configuration of sensitive field collection, `config`refers to the `InitConfig`at initialization.

The device's MAC address acquisition is enabled by default. To close:

```java
//After the switch is turned off, the relevant code does not run, and the attributes are not collected. Whether to upload depends on whether the customer has passed in the MAC from the outside.
config.setMacEnable(false);
```


To remove the relevant code for MAC address collection, you can configure it in the full event tracking plugin:


* Gradle 8.0 or less

   ```Groovy
   //This function only supports 6.9.0 and above versions
   teaExtension {
       // ... Other configurations
       trackBlackList = ["MAC_ADDRESS"]
   
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   

* Gradle 8.0 and above

   ```Groovy
   //This function only supports 6.9.0 and above versions
   //AGP8 version plugin 6.16.3 support
   appLog {
       // ... Other configurations
       sensitiveFieldsBlocklist = ["MAC_ADDRESS"]
     
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   


<span id="_3-3-关闭设备imei-meid采集"></span>
## 3.5 Turn off device IMEI/MEID acquisition

The device's IMEI address collection is enabled by default. To close:

```java
//After the switch is turned off, the relevant code does not run, the attributes are not collected, and whether to upload depends on whether the customer has passed AppImei from the outside.
config.setImeiEnable(false);
```


To remove the relevant code for IMEI and MEID collection, you can configure it in the full event tracking Plugin:


* Gradle 8.0 or less

   ```Groovy
   //This function only supports 6.9.0 and above versions
   teaExtension {
       // ... Other configurations
       trackBlackList = ["IMEI_MEID"]
   
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   

* Gradle 8.0 and above

   ```Groovy
   //This function only supports 6.9.0 and above versions
   //AGP8 version plugin 6.16.3 support
   appLog {
       // ... Other configurations
       sensitiveFieldsBlocklist = ["IMEI_MEID"]
     
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   


<span id="6cde3dfe"></span>
## 3.6 Turn off OAID acquisition

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">OAID is important device tracking information. Turning off OAID will affect Tracer attribution. Please consider using Tracer with caution.</div>


The device's OAID information collection is turned on by default. To close:

```java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
config.setOaidEnabled(false);
```


To remove the relevant code for OAID collection, you can configure it in the full event tracking Plugin:


* Gradle 8.0 or less

   ```Groovy
   //This function only supports 6.9.0 and above versions
   teaExtension {
       // ... Other configurations
       trackBlackList = ["OAID"]
   
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   

* Gradle 8.0 and above

   ```Groovy
   //This function only supports 6.9.0 and above versions
   //AGP8 version plugin 6.16.3 support
   appLog {
       // ... Other configurations
       sensitiveFieldsBlocklist = ["OAID"]
     
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   


<span id="fc4316e2"></span>
## 3.7 Turn off Android ID collection

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Closing the Android ID will affect the device_id generation logic, resulting in inconsistent device_id uninstall and reinstall.</div>


<div data-tips="true" data-tips-type="warning">Subsequent documentation will be abbreviated device_id did.</div>


The Android ID collection of the device is turned on by default, if you need to turn it off:

```java
//After the switch is turned off, the relevant code will not run, and the properties will not be collected. It will be randomly generated after closing.
config.setAndroidIdEnabled(false);
```


To remove the Android ID capture code, you can configure it in the Full event tracking Plugin:


* Gradle 8.0 or less

   ```Groovy
   //This function only supports 6.10.1 and above versions
   teaExtension {
       // ... Other configurations
       trackBlackList = ["ANDROIDID"]
   
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   

* Gradle 8.0 and above

   ```Groovy
   //This function only supports 6.10.1 and above versions
   //AGP8 version plugin 6.16.3 support
   appLog {
       // ... Other configurations
       sensitiveFieldsBlocklist = ["ANDROIDID"]
     
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   


<span id="62555027"></span>
## 3.8 Turn off ICCID acquisition

The ICCID collection of the device is turned on by default, if you need to turn it off:

```java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.14.3 and above versions
config.setIccIdEnabled(false);
```


ICCID does not currently support removing capture code via plug\-ins.

<span id="10614427"></span>
## 3.9 Turn off SN (hardware serial number) acquisition

The SN acquisition of the device is turned on by default, if you need to turn it off:

```java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.15.0 and above versions
config.setSerialNumberEnable(false);
```


SN does not currently support removing capture code through plug\-ins.

<span id="c05aeff1"></span>
## 3.10 Turn off GAID collection

Device GAID acquisition default scheme:


* 6.15.0 before cn (domestic version) and global (overseas version) are collected by default.

* 6.15.0 and after cn is closed by default, global is turned on by default.


To close:

```java
//After the switch is closed, the relevant code does not run, the attributes are not collected, and whether to upload depends on whether the customer has passed Gaid from the outside.
config.setGaidEnabled(false);
```


⚠️Please note that since the switch is turned on by default before the 6.15.0 version of the SDK package at home and abroad, it may cause third parties in the domestic application package to try to obtain GAID after integrating Google Service, and GAID is time\-consuming, which may have ANR problems in some models or affect the response time of device registration requests.

```java
//The collection timeout time control is provided for the Gaid acquisition time-consuming SDK. If the collection time has not been exceeded, it will be returned to empty directly.
//Default time 2s timeout, method parameter ms
//The method 6.15.0 provided
config.setGaidTimeOutMilliSeconds(2000)
```


⚠️Please note that since the switch is turned on by default in both domestic and foreign SDK packages, it may cause third parties in domestic application packages to try to obtain GAID after integrating Google Service, and GAID is time\-consuming, which may have ANR problems in some models or affect the response time of device registration requests.

<span id="69c893aa"></span>
## 3.11 Turn off operator information collection

The operator information of the device is collected by default, if you need to turn it off:

```java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
config.setOperatorInfoEnabled(false);
```


To remove the carrier information collection code, you can configure it in the full event tracking Plugin:


* Gradle 8.0 or less

   ```Groovy
   //This function only supports 6.10.1 and above versions
   teaExtension {
       // ... Other configurations
       trackBlackList = ["OPERATOR"]
   
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   

* Gradle 8.0 and above

   ```Groovy
   //This function only supports 6.10.1 and above versions
   //AGP8 version plugin 6.16.3 support
   appLog {
       // ... Other configurations
       sensitiveFieldsBlocklist = ["OPERATOR"]
     
       //You are using the Lite package and need to remove the collection related code.
       //You need to add this configuration in the new version to avoid the flash back caused by the uneven content of the Lite package. It is provided from 6.14.3
       disableAutoTrack = true
   }
   ```
   


<span id="45bd0dad"></span>
## 3.12 Remove clipboard access code

Cut version access is currently used for ad monitoring and is turned off by default.

```Plain
// The content in user's clipboard will not be accessed after you turn the switch off.
// turn off by corresponding applog instance
AppLog.setClipboardEnabled(false);
```


To remove the clipboard access code, you can configure it in the full event tracking Plugin:


* Gradle 8.0 or less

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
   

* Gradle 8.0 and above

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
   


<span id="d963c887"></span>
## 3.13 Turn off CPU architecture acquisition

The CPU architecture acquisition of the device is turned on by default, if you need to turn it off:

```java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.17.1 and above versions
config.setCPUAbiEnabled(false);
```


<span id="a780444b"></span>
## 3.14 Turn off screen definition/screen density capture

The screen definition/screen density capture of the device is turned on by default, if you need to turn it off:

```java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.17.1 and above versions
config.setDisplayDensityAndDpiEnabled(false);
```


<span id="_4-配置scheme-可选"></span>
# 4. Configuration Scheme (optional)

To use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification), configure Scheme, otherwise you can skip this step.

<span id="_4-1-获取url-scheme"></span>
## 4.1 Obtaining URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98d05204fc4f4380a07e0f2e1238c9d2~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-添加url-scheme"></span>
## 4.2 Adding URL Schemes

Add URL Scheme to build.gradle at the app module level.

```groovy
//Add defaultConfig in android
manifestPlaceholders.put("APPLOG_SCHEME", "yourURL_SCHEME".toLowerCase())
```


<span id="_5-初始化基本配置"></span>
# 5. Initialize the basic configuration

The following are common initialization basic configuration, `config`refers to the initialization of `InitConfig`.

<span id="_5-1-全埋点设置开关"></span>
## 5.1 Full event tracking settings switch

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The full event tracking switch is on by default. After enabling full event tracking in the SDK, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.</div>



* <div data-tips="true" data-tips-type="warning">SaaS\-cloud native and privatization scenarios: Go to Project Center \> Project Management \> SDK Settings and make sure the full event tracking switch is turned on.</div>



```java
//Open the upload of the full event tracking event
config.setAutoTrackEnabled(true); //true: enable full event tracking, false: turn off full event tracking
```


Page view events in full event tracking, default for Activity pages. To turn on the bav2b_page event acquisition for Fragment, in addition to the above switch, the Fragment acquisition switch needs to be turned on additionally.

```java
//Enable Fragment full event tracking event collection
config.setAutoTrackFragmentEnabled(true);
```


<span id="_5-2-开启圈选埋点"></span>
## 5.2 Turn on event tracking

Circle event tracking is off by default.

```java
//Turn on the event tracking function. To use this function, you need to turn on full event tracking first.
config.setPicker(new Picker(this, config));

//If you want to turn on the circle selection for the h5 embedded in the App, please turn on the js injection switch:
config.setH5CollectEnable(true);
//Note: h5 circle selection only supports native WebView and Tencent X5
```


<span id="_5-3-查看日志打印"></span>
## 5.3 View log printing

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Log printing is turned off by default, and it is recommended that the online production package be turned off.</div>



* Current instance log print

   ```Java
   //Output logs in the console, which can be used to observe user behavior log reports. It is recommended to close it when online
   config.setLogEnable(true); //true: open log, false: close log
   config.setLogger(new ILogger() {
       @Override
       public void log(String s, Throwable throwable) {
           Log.d("AppLog------->: ", "" + s);
       }
   });
   ```
   

* Unified printing of multiple instance logs

   ```Java
   //If you need to print the logs of all instances, you can refer to the following configuration:
   //Only 6.12.0 + versions are supported
   LogProcessorHolder.addProcessor(
       new ILogProcessor() {
           @Override
           public void onLog(LogInfo log) {
               Log.d("AppLog------->: ", log.toLiteString());
           }
   });
   ```
   


<span id="_5-4-加密设置开关"></span>
## 5.4 Encryption setting switch

Encryption settings are enabled by default. You can turn off encryption during the debug phase to facilitate joint debugging.

```java
//Encryption setting switch, it is recommended to turn on the online version.
AppLog.setEncryptAndCompress(true); //true: open encryption, false: close encryption
```


<span id="_5-5-设置app-language-和-app-region"></span>
## 5.5 Set APP Language and APP Region

```java
//Modify language and region, set APP Language and APP Region
config.setLanguage(...); //Set APP Language, such as zh-cn
config.setRegion(...); //Set the APP Region, such as cn
```


<span id="_5-6-打通内嵌-h5-页"></span>
## 5.6 Open the embedded H5 page

If your application integrates the Web/JS SDK and the Android SDK at the same time, by default, all H5 events will be reported through the Web/JS SDK. If you want the H5 event to be reported by the Android SDK, you can use the embedded H5 function to get through. At this time, the events generated on the H5 page will be reported through the Android SDK instead of the Web/JS SDK. This kind of takeover and reporting scenario will reuse the `user_unique_id`and public properties set by the Android side, but also supports the uuid/public properties on the web side setting/update end when getting through. Please pay attention to which side of the data is used when getting through. If it is completely subject to the end, you can Remove the uuid on the web SDK side (if you need to support updating multi\-caliber from the web side, you need to use a new version of the SDK)/public attribute operation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get through the function requires the Web/JS SDK and Android SDK to integrate and cooperate with each other at the same time, and the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, because the reporting is taken over by the Android SDK at this time. If you still want to collect H5 full event tracking, you need to check Section 5.7: Native collection of H5 full event tracking. Web/JS SDK integration please refer to <a href="https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_">Web/JavaScript SDK Integration</a>section 3.4.</div>


<div data-tips="true" data-tips-type="warning">Lite does not support the function of packing and getting through. If you need to get through, please integrate All.</div>


```java
//Note: This feature only supports native WebView and Tencent X5

//The following configurations need to be enabled at the same time. If the following two are not satisfied at the same time, the H5 event will continue to be reported by the Web/JS SDK:
//Android SDK turn on the embedded H5 open switch
config.setH5BridgeEnable(true);
//Web/JS SDK set H5 to be embedded in the native side and get through
window.collectEvent('init', {
    // ...... Other initialization configurations
    enable_native: true 
    //5.1.3 the following version parameters are Native,
    //5.1.3 the above version is changed to enable_native, but still compatible with Native settings
})

//Supplement: After opening and getting through, the full event tracking configuration of the original web sdk of the old version will be invalid.
//After the old version before 5.1.10 gets through, the Web/JS SDK blocks the full event tracking function of H5, so the full event tracking setting switch of the Web/JS SDK will fail.
//If you want to keep the H5 full event tracking function in the old version of web sdk, please check section 4.7 or recommend upgrading to a new version
window.collectEvent('init', {
    //Full event tracking setting switch
    autotrack: the old versions will be invalid (the former version before web sdk 5.1.10 will be invalid, versions after 5.1.10 will collect normally)
})
```


<span id="_5-6-1-打通内嵌-h5-页的白名单前置工作"></span>
### 5.6.1 get through the whitelist front work of the embedded H5 page

After the switch is turned on, the whitelist must be configured. Only the domain names configured in the whitelist take effect. The whitelist can be added by wild\-card, and `*`means wild\-card.

```java
//Embedded H5 page whitelist configuration
//Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
config.setH5BridgeAllowlist(Arrays.asList("www.volcengine.com", "*.bytedance.*"));
//There are many whitelists for adaptation www.bytedance.com, please configure the whitelist according to the business scenario, for example:
//www.bytedance.com or * .bytedance. * or *.*.* .
```


If you do not filter any domain names and local resource files, you can configure to allow all H5 pages to open. This configuration has a higher priority than `setH5BridgeAllowlist`.

```java
//allow all h5 to get through
//This function only supports 6.9.7 and above versions
config.setH5BridgeAllowAll(true);
```


<span id="_5-6-2-打通内嵌-h5-页的插件注入注意项"></span>
### 5.6.2 through the embedded H5 page plug\-in injection note

Under normal circumstances, H5 to get through requires you to refer to Section 1.2 integrated plugin plugin, at this time the injection Bridge is completed by Plugin instrumentation, but in some scenarios, instrumentation may not take effect (the scene of plug failure may be confused, overwritten, etc.), you can choose to manually turn off the SDK's automatic injection Bridge ability, and then manually call injection, at this time you can add configuration in the full event tracking plugin Plugin `autoInjectWebViewBridge = false`, and then manually inject Bridge before the WebView that needs to get through loads H5.


* Gradle 8.0 or below turns off automatic injection of plugins

   ```Groovy
   //Turn off automatic injection through plugins
   teaExtension {
       //Close the docking bridge that automatically injects webview
       autoInjectWebViewBridge = false
       //Omit other uses of plugins
   }
   ```
   

* Gradle 8.0 and above turn off automatic injection of plugins

   ```Groovy
   //AGP8 version plugin 6.16.3 support
   appLog {
       //Close the docking bridge that automatically injects webview
       autoInjectWebViewBridge = false
       //Omit other uses of plugins
   }
   ```
   


```Java
//This function only supports 6.13.0 and above versions
WebView myWebView = findViewById(R.id.webview);
//Inject Bridge before loadUrl
AppLog.initWebViewBridge(myWebView, url);
myWebView.loadUrl(url);
```


<span id="7489fca5"></span>
### 5.6.3 Stop H5 from updating user information in the app when opening the embedded H5 page (uuid)

When getting through, the in\-terminal SDK user information is used by default, but it also supports the H5 side to update the in\-terminal SDK user information through the Web SDK.

Android 6.17.0 version is newly added to prohibit H5 from updating user information in the App when getting through the embedded H5 page, so as to avoid the difficulty of removing the relevant code for updating user information when using H5 in many places, thereby destroying the original user information of the SDK in the terminal when getting through.

```java
//On by default, support off
config.setUseBridgeUpdateUUIDEnabled(true);
```


<span id="_5-7-原生端采集h5全埋点"></span>
## 5.7 Native acquisition H5 full event tracking

When the H5 page is embedded in the native end, the H5 page full event tracking event can be collected from the native end by turning on the following switch.

There are generally two usage scenarios:


* Since the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, in order to ensure that the H5 page full event tracking function can still be retained after getting through.

* Independent use, in the case that H5 does not integrate Web/JS SDK, I want to enable the full event tracking function on the H5 page in the application.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature can be used independently without the need to integrate a Web/JavaScript SDK.</div>


* <div data-tips="true" data-tips-type="warning">This feature is available 6.14.4 version, and the current H5 full event tracking only supports page entry events and click events.</div>



```java
//Note: This feature only supports native WebView and Tencent X5

//Embedded H5 page full event tracking event
config.setH5CollectEnable(true); //true: turn on h5 full event tracking event, false: turn off h5 full event tracking event

//Supplement, this function is also injected by plug-in by default. When the plug-in fails or you want to inject it manually,
//You can refer to 4.6.2 subsection, 4.6, 4.7 although the function is independent, but through the unified method of injection control,
//However, you can configure whether to turn it on through the respective switches.
```


<span id="_5-8-全埋点事件采集"></span>
## 5.8 Full event tracking

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


<span id="_5-9-设置gps坐标"></span>
## 5.9 Setting GPS Coordinates

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


<span id="_5-10-开启崩溃采集"></span>
## 5.10 Turn on crash acquisition

By default, the application crash event `$crash`is not collected. To enable:

```java
//Currently only supports capturing Java crashes
//This function only supports 6.13.0 and above versions
config.setTrackCrashType(AppCrashType.JAVA);
```


<span id="_5-11-开启fragment页面事件采集"></span>
## 5.11 Open Fragment Page Event Collection

Default Fragment page event collection is turned off, after turning on the switch, each Fragment access will also record a page access event ($bav2b_page). To open:

```java
//This function only supports 6.13.0 and above versions
config.setAutoTrackFragmentEnabled(true);
```


<span id="_5-12-是否区分鸿蒙设备"></span>
## 5.12 Whether to distinguish Hongmeng equipment

The data collection report will distinguish whether it is Hongmeng system:

```java
//This function only supports 6.14.3 and above versions
config.setHarmonyEnable(true);
```


<span id="_6-常用回调介绍"></span>
# 6. Introduction to common callbacks

<span id="_6-1-如何正确获取-did-等参数"></span>
## 6.1 How to correctly obtain parameters such as DID

Due to the possible delay in obtaining parameters, methods such as Applog.getDid () may not be able to obtain the corresponding parameters at the first time, so it is recommended to obtain them through callbacks, and after the callback, methods such as Applog.getDid () can ensure that they are obtained.

```typescript
//step1: Add dataset observation callback, this refers to the class that implements IDataObserver
AppLog.addDataObserver(this);
//step2: Use it after getting the data through onIdLoaded or onRemoteIdGet of IDataObserver or use the following methods to obtain it:
Default instance: Applog.getDid() / Use multiple instances: IAppLogInstance.getDid()


//IDataObserver main function introduction and parameter introduction:
//- did, iid, ssid can all be obtained through this callback
//- server level configuration fetch
//- ab experiment configuration acquisition
public interface IDataObserver {
    /**     * Local ID data loading result notification     *@param did device id     *@param iid install id     *@param Ssid number says id     */
    void onIdLoaded(@NonNull String did, @NonNull String iid, @NonNull String ssid);

    /**     Notify registration results and ID changes     Only the main process will be called     *@param Changed whether it is different from the local cache     *@param oldDid Local old oldDid, possibly empty     *@param newDid server returns new device id     *@param newIid server returns the new install id     *@param newSsid server returns the new ID     */
    void onRemoteIdGet(boolean changed, @Nullable String oldDid, @NonNull String newDid,
                       @NonNull String oldIid, @NonNull String newIid, 
                       @NonNull String oldSsid, @NonNull String newSsid);

    /**     * Config pulls data, and notifies changes compared with local data     Only the main process will be called     *@param Changed whether it is different from the local cache     *@param Config server returns new config content     */
    void onRemoteConfigGet(boolean changed, @Nullable JSONObject config);

    /**     * The server pulls AbConfig data and notifies changes compared with local data     Only the main process will be called     *@param Changed whether it is different from the local cache     *@param abConfig server returns new abConfig content     */
    void onRemoteAbConfigGet(boolean changed, @NonNull JSONObject abConfig);

    /**     * Notification of client side ab exposure vid collection changes     *@param Vids client side ab experiment exposure vid collection     *@param extVids external vid collection of external settings     */
    void onAbVidsChange(@NonNull String vids, @NonNull String extVids);
}
```


<span id="_6-2-事件过滤以及自定义参数补齐"></span>
## 6.2 Event filtering and custom parameter padding

For event filtering or event custom parameter padding, the following callbacks can be used:


* 6.16.1 and above

   ```Groovy
   AppLog.setEventHandler(new IEventHandler() {
       Return the acceptable event type
       @Override
       public int acceptType() {
           return EventType.EVENT_ALL;
       }
   
       //Do event filtering for single events, or custom parameters for additional processing
       @Override
       public EventPolicy onReceive(
               int eventType,
               @NonNull String eventName,
               @NonNull JSONObject properties,
               //Add basic event information
               @NonNull EventBasicData basicData) {
           //user attributes are not processed
           if (eventName.startsWith("__profile_")) {
               return EventPolicy.ACCEPT;
           }
           Filter the xx event
           if ("xx".equals(eventName)) {
               return EventPolicy.DENY;
           }
           //Add custom properties
           try {
               properties.put("eventHandlerProps", "12345");
           } catch (JSONException ignored) {
   
           }
           //Other events are reported normally
           return EventPolicy.ACCEPT;
       }
   });
   ```
   

* 6.16.1 the following versions

   ```Groovy
   //Set event handling callback
   AppLog.setEventHandler(new IEventHandler() {
       Return the acceptable event type
       @Override
       public int acceptType() {
           return EventType.EVENT_ALL;
       }
   
       //Do event filtering for single events, or custom parameters for additional processing
       @Override
       public EventPolicy onReceive(
               int eventType,
               @NonNull String eventName,
               @NonNull JSONObject properties) {
           //user attributes are not processed
           if (eventName.startsWith("__profile_")) {
               return EventPolicy.ACCEPT;
           }
           Filter the xx event
           if ("xx".equals(eventName)) {
               return EventPolicy.DENY;
           }
           //Add custom properties
           try {
               properties.put("eventHandlerProps", "12345");
           } catch (JSONException ignored) {
   
           }
           //Other events are reported normally
           return EventPolicy.ACCEPT;
       }
   });
   ```
   


<span id="_6-3-请求自定义加密"></span>
## 6.3 Request custom encryption

The privatized version V4.4.0 supports the request encryption of the national secret SM2 algorithm, and the SDK provides a custom encryption interface. If the privatized version supports other encryption protocols in the future, you can use the custom encryption interface to request encryption.


* Java

   ```Java
   //sm2 encryption
   Sm2Helper sm2Helper = new Sm2Helper(yourPublicKey);
   config.setEncryptor(new IEncryptor() {
       @Override
       public byte[] encrypt(byte[] data, int size) {
           //Convert the original data to encrypted data
           return sm2Helper.encrypt(data, size);
       }
       //The encryption type will be put into Content-Type, which needs to be agreed with the private deployment.
   }, sm2Helper.encryptorType());
   
   //Custom encryption
   //The encryption mode of the custom protocol with the private deployment can be realized through the custom encryption interface
   config.setEncryptor(new IEncryptor() {
       @Override
       public byte[] encrypt(byte[] data, int size) {
           //Convert the original data to encrypted data
           return yourEncryptMethod(data, size);
       }
       //The encryption type will be put into Content-Type, which needs to be agreed with the private deployment.
   }, "yourEncryptType");
   ```
   

* Kotlin

   ```Kotlin
   //sm2 encryption
   val sm2Helper = Sm2Helper(yourPublicKey)
   config.setEncryptor({ data, size -> 
           //Convert the original data to encrypted data
           sm2Helper.encrypt(data, size)
       }, 
       //The encryption type will be put into Content-Type, which needs to be agreed with the private deployment.
       sm2Helper.encryptorType()
   )
   
   //Custom encryption
   //The encryption mode of the custom protocol with the private deployment can be realized through the custom encryption interface
   config.setEncryptor({ data, size -> 
           //Convert the original data to encrypted data
           yourEncryptMethod(data, size)
       }, 
       //The encryption type will be put into Content-Type, which needs to be agreed with the private deployment.
       "yourEncryptType"
   )
   ```
   


<span id="_7-其他功能介绍"></span>
# 7. Introduction to other functions

<span id="_7-1-私有化云控能力"></span>
## 7.1 Cloud control capabilities

Note: This function is only SaaS cloud native version or privatization V4.4.0 or above, and the SDK 6.15.0 above version support;

DataFinder supports sending SDK settings through the server level, including reporting timing, full event tracking switch, etc. [Project Management - SDK Settings](https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings).

<span id="_8-权限说明"></span>
# 8. Permissions Description

Growth Marketing Suite Android SDK Permissions List:


|**Permission** |**Explain** |**Use scenario and purpose** |
|---|---|---|
|android.permission.READ_PHONE_STATE |Read IMEI and other device information as device identification |Device registration: initialize reading, generate a unique device identifier, and calculate the number of devices |
|android.permission.ACCESS_WIFI_STATE |Get network status (wifi) |Device registration and event tracking data collection: collect device network (wifi) information |
|android.permission.ACCESS_NETWORK_STATE |Get network status |Device registration and event tracking data collection: collect device network information |
|android.permission.INTERNET |Send a network request |Register, report event tracking, attribution, activation, etc.: report event tracking data to a remote server |
|com.asus.msa.SupplementaryDID.ACCESS |Read oaid |Device registration and deep linking: Identifying devices across apps |


<span id="d366c09b"></span>
# 9. Reference: Data reporting process and trigger timing

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SaaS\-cloud native, privatized environment supports setting the basic settings of Android, iOS, web, and Mini Program platform SDKs in the DataFinder console, including whether to enable full event tracking, event tracking report timing, and so on. The following is the default reporting process and mechanism on the device, you can also configure and adjust in the DataFinder console <a href="https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings">Project Management \- SDK Settings</a>.</div>


<span id="21ba8411"></span>
## Data reporting prerequisites

The precondition for data reporting is to complete the SDK initialization. Before reporting, it will check whether setAutoStart (false) is configured in the config initialized by the SDK:


* If not configured, data will be reported regularly after init.

* If configured, it will wait for the developer to call start and start reporting data regularly.


<span id="1e54cb1c"></span>
## Data reporting process and logic

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMzI1cHgiIGhlaWdodD0iNDg1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMzI1IDQ4NSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gODIgMTIyIEwgMTE1LjYzIDEyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDEyMC44OCAxMjIgTCAxMTMuODggMTI1LjUgTCAxMTUuNjMgMTIyIEwgMTEzLjg4IDExOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTAyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+U0RLIFN0YXJ0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDIwMiAxMjIgTCAyMzUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjQwLjg4IDEyMiBMIDIzMy44OCAxMjUuNSBMIDIzNS42MyAxMjIgTCAyMzMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDE2MiAxNjIgTCAxNjIgMTk1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTYyIDIwMC44OCBMIDE1OC41IDE5My44OCBMIDE2MiAxOTUuNjMgTCAxNjUuNSAxOTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDE2MiA4MiBMIDIwMiAxMjIgTCAxNjIgMTYyIEwgMTIyIDEyMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAxMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+SXMgaXQgbWFpbiBwcm9jZXNzPzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTA3IiB5PSIyMDIiIHdpZHRoPSIxMTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjIycHg7IG1hcmdpbi1sZWZ0OiAxMDhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+U3VicHJvY2VzcyBkb2Vzbid0IHNlbmQgYW55IHJlcXVlc3Q8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzMyIDEyMiBMIDM2NS42MyAxMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzNzAuODggMTIyIEwgMzYzLjg4IDEyNS41IEwgMzY1LjYzIDEyMiBMIDM2My44OCAxMTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjI0MiIgeT0iODIiIHdpZHRoPSI5MCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAyNDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VHJpZ2dlcmluZyB0aW1lPGJyIC8+PGJyIC8+U2NoZWR1bGVyKHNlbmQgb25jZSBldmVyeSA2MHMpPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDQ5MiAxMjIgTCA1MjUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTMwLjg4IDEyMiBMIDUyMy44OCAxMjUuNSBMIDUyNS42MyAxMjIgTCA1MjMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQzMiAxNjIgTCA0MzIgMTkyIEwgMjg3IDE5MiBMIDI4NyAxNjguMzciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyODcgMTYzLjEyIEwgMjkwLjUgMTcwLjEyIEwgMjg3IDE2OC4zNyBMIDI4My41IDE3MC4xMiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDMyIDgyIEwgNDkyIDEyMiBMIDQzMiAxNjIgTCAzNzIgMTIyIFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAzNzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2hlY2sgaWYgdGhlIGRldmljZSBoYXMgYmVlbiBzdWNjZXNzZnVsbHkgcmVnaXN0ZXJlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1OTIgMTYyIEwgNTkyIDI0MiBMIDI4NyAyNDIgTCAyODcgMTY4LjM3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjg3IDE2My4xMiBMIDI5MC41IDE3MC4xMiBMIDI4NyAxNjguMzcgTCAyODMuNSAxNzAuMTIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY1MiAxMjIgTCA2ODUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjkwLjg4IDEyMiBMIDY4My44OCAxMjUuNSBMIDY4NS42MyAxMjIgTCA2ODMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDU5MiA4MiBMIDY1MiAxMjIgTCA1OTIgMTYyIEwgNTMyIDEyMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogNTMzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNoZWNrIGlmIGZyZXF1ZW5jeSBjb250cm9sIHJlc3RyaWN0aW9uIGlzIHRyaWdnZXJlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3NzIgMTIyIEwgODA1LjYzIDEyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDgxMC44OCAxMjIgTCA4MDMuODggMTI1LjUgTCA4MDUuNjMgMTIyIEwgODAzLjg4IDExOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA3MTIgMTQyIEwgNzEyIDM1MiBMIDM1OC4zNyAzNTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzNTMuMTIgMzUyIEwgMzYwLjEyIDM0OC41IEwgMzU4LjM3IDM1MiBMIDM2MC4xMiAzNTUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjY5MiIgeT0iMTAyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMjJweDsgbWFyZ2luLWxlZnQ6IDY5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EYXRhIHBhY2thZ2luZzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA5NDIgMTIyIEwgOTc1LjYzIDEyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4MC44OCAxMjIgTCA5NzMuODggMTI1LjUgTCA5NzUuNjMgMTIyIEwgOTczLjg4IDExOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iODEyIiB5PSIxMDIiIHdpZHRoPSIxMzAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiA4MTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Rmlyc3QgcmVxdWVzdCBwYWNrPGJyIC8+TWF4IGV2ZW50IGFtb3VudDogMjAwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDEwNjIgMTIyIEwgMTA5NS42MyAxMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMTAwLjg4IDEyMiBMIDEwOTMuODggMTI1LjUgTCAxMDk1LjYzIDEyMiBMIDEwOTMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI5ODIiIHk9IjEwMiIgd2lkdGg9IjgwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiA5ODNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGF0YSB1cGxvYWRpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTE4MiAxMjIgTCAxMjM1LjYzIDEyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDEyNDAuODggMTIyIEwgMTIzMy44OCAxMjUuNSBMIDEyMzUuNjMgMTIyIEwgMTIzMy44OCAxMTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTE0MiA4MiBMIDExNDIgNDguMzciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMTQyIDQzLjEyIEwgMTE0NS41IDUwLjEyIEwgMTE0MiA0OC4zNyBMIDExMzguNSA1MC4xMiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTE4MiAxMjIgTCAxMjEyIDEyMiBMIDEyMTIgMTgyIEwgMTIzNS42MyAxODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMjQwLjg4IDE4MiBMIDEyMzMuODggMTg1LjUgTCAxMjM1LjYzIDE4MiBMIDEyMzMuODggMTc4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDExODIgMTIyIEwgMTIxMiAxMjIgTCAxMjEyIDI0MiBMIDEyMzUuNjMgMjQyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTI0MC44OCAyNDIgTCAxMjMzLjg4IDI0NS41IEwgMTIzNS42MyAyNDIgTCAxMjMzLjg4IDIzOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxMTgyIDEyMiBMIDEyMDIgMTIyIEwgMTIwMiAyMjIgTCAxMTEzLjM3IDIyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExMDguMTIgMjIyIEwgMTExNS4xMiAyMTguNSBMIDExMTMuMzcgMjIyIEwgMTExNS4xMiAyMjUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTE0MiA4MiBMIDExODIgMTIyIEwgMTE0MiAxNjIgTCAxMTAyIDEyMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAxMTAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJlc3BvbnNlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMDk3IiB5PSIyIiB3aWR0aD0iOTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMTA5OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5yZXRyeS8gZGVjcmVhc2UgZnJlcXVlbmN5PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMjQyIiB5PSIxMDIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogMTI0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EZWxldGUgY2FjaGU8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjEyNDIiIHk9IjE2MiIgd2lkdGg9IjgwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTgycHg7IG1hcmdpbi1sZWZ0OiAxMjQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlVwZGF0ZSBjb25maWc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjEyNDIiIHk9IjIyMiIgd2lkdGg9IjgwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjQycHg7IG1hcmdpbi1sZWZ0OiAxMjQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJlcXVlc3QgZm9yIGluY3JlYXNpbmcgZnJlcXVlbmN5PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDEwMjIgMjYyIEwgMTAyMiAyOTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMDIyIDMwMC44OCBMIDEwMTguNSAyOTMuODggTCAxMDIyIDI5NS42MyBMIDEwMjUuNSAyOTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDEwMjIgMTgyIEwgMTAyMiAxNDguMzciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMDIyIDE0My4xMiBMIDEwMjUuNSAxNTAuMTIgTCAxMDIyIDE0OC4zNyBMIDEwMTguNSAxNTAuMTIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI5MzciIHk9IjE4MiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyMnB4OyBtYXJnaW4tbGVmdDogOTM4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlN1YnNlcXVlbnQgcmVxdWVzdCBwYWNrPGJyIC8+TWF4IGV2ZW50IGFtb3VudDogMjAwPGJyIC8+VXAgdG8gOCBwYWNrcyBpbiBzaW5nbGUgc2VuZCB3aXRoaW4gMSBtaW51dGU8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijk4MiIgeT0iMzAyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMjJweDsgbWFyZ2luLWxlZnQ6IDk4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5ObyBldmVudCBlbmQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gODIgMzYyIEwgMTE1LjYzIDM2MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDEyMC44OCAzNjIgTCAxMTMuODggMzY1LjUgTCAxMTUuNjMgMzYyIEwgMTEzLjg4IDM1OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMzQyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+R2VuZXJhdGUgZXZlbnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjAyIDM2MiBMIDIzNS42MyAzNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNDAuODggMzYyIEwgMjMzLjg4IDM2NS41IEwgMjM1LjYzIDM2MiBMIDIzMy44OCAzNTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTYyIDQwMiBMIDE2MiA0MzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNjIgNDQwLjg4IEwgMTU4LjUgNDMzLjg4IEwgMTYyIDQzNS42MyBMIDE2NS41IDQzMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTYyIDMyMiBMIDIwMiAzNjIgTCAxNjIgNDAyIEwgMTIyIDM2MiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzYycHg7IG1hcmdpbi1sZWZ0OiAxMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+SXMgaXQgbWFpbiBwcm9jZXNzPzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTA3IiB5PSI0NDIiIHdpZHRoPSIxMTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDYycHg7IG1hcmdpbi1sZWZ0OiAxMDhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UGFzc2luZyBldmVudHMgYWNyb3NzIHByb2Nlc3NlcyB0byB0aGUgbWFpbiBwcm9jZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM1MiAzNzIgTCA3NTIgMzcyIEwgNzUyIDE0OC4zNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc1MiAxNDMuMTIgTCA3NTUuNSAxNTAuMTIgTCA3NTIgMTQ4LjM3IEwgNzQ4LjUgMTUwLjEyIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjQyIiB5PSIzNDIiIHdpZHRoPSIxMTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzYycHg7IG1hcmdpbi1sZWZ0OiAyNDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGF0YSBzdG9yZWQgaW4gQVBQIGRhdGFiYXNlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxNjIiIHk9IjE3MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4MnB4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5vPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxOTkiIHk9IjEwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDExMnB4OyBtYXJnaW4tbGVmdDogMjAwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDkyIiB5PSIxMDIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMTJweDsgbWFyZ2luLWxlZnQ6IDQ5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5ZZXM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjM1NyIgeT0iMTYyIiB3aWR0aD0iMTUwIiBoZWlnaHQ9IjMwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNzdweDsgbWFyZ2luLWxlZnQ6IDM1OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Obywgc2VuZCBhZnRlciBkZXZpY2UgcmVnaXN0ZXJlZCBzdWNjZXNzZnVsbHk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQ4MiIgeT0iMzIyIiB3aWR0aD0iMTUwIiBoZWlnaHQ9IjMwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMzdweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5RdWVyeSBkYXRhIGluIGRhdGFiYXNlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTIiIHk9IjEwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDExMnB4OyBtYXJnaW4tbGVmdDogNjUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5vPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMTQyIiB5PSI1MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDYycHg7IG1hcmdpbi1sZWZ0OiAxMTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZhaWw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjExODciIHk9IjEwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDExMnB4OyBtYXJnaW4tbGVmdDogMTE4OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TdWNjZWVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxNjIiIHk9IjQxMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQyMnB4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5vPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxOTkiIHk9IjM0MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM1MnB4OyBtYXJnaW4tbGVmdDogMjAwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDQyIiB5PSIyMTIiIHdpZHRoPSIxNTAiIGhlaWdodD0iMzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyN3B4OyBtYXJnaW4tbGVmdDogNDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlllcywgc2VuZCBhZnRlciBtZWV0IHRoZSBmcmVxdWVuY3kgY29udHJvbDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDgyIiB5PSIzNzIiIHdpZHRoPSIxNTAiIGhlaWdodD0iMzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM4N3B4OyBtYXJnaW4tbGVmdDogNDgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBhY2thZ2luZyBkYXRhPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" />


1. **SDK initialization:** 

   After the SDK is initialized, it will detect the current process. If it is the main process, it will start to create regular reporting tasks, and the child process will not handle it.

2. **Trigger timing:** 

   * Start the regular sending task, the default reporting interval is 1min, and check whether the next reporting is triggered every 5s. Privatization supports cloud control configuration to shorten the reporting interval.

   * If the detection has reached the reporting time, the reporting will be triggered, otherwise the next detection will be delayed for 5s.

3. **Test before reporting:** 

   * Detect whether the device registration is successful, because the pre\-reporting requires the did and ssid returned by the device registration (the event needs to be properly bound to ssid, so for events that do not have ssid when generated, ssid will be added before reporting), and continue if it has been successful.

   * Before reporting, it will also detect whether the frequency control limit is met. If the frequency control is not currently triggered, the reporting process will continue. If the frequency control is triggered, it will be judged whether the current reporting can be done according to the frequency control.

   1. The main purpose of frequency control is to limit the frequency of reporting requests on the end when the server level is unavailable, so as to avoid more pressure when the server level is unavailable.

4. **Data packaging and reporting:** 

   * First, the data stored in the APP database is queried and packaged for reporting data (the reporting data unit is pack, pack is data packet, each data packet contains up to 200 events, and the queried events are packaged into a pack for reporting). The source is divided into two parts:

      * Last failed pack

      * New pack of local events aggregation

   * After querying the packs to be sent according to different versions of the query strategy, report them separately for each pack.

      * After 6.15.0, query up to 8 packs each time (you can roughly understand that up to 200 \* 8 = 1600 events are reported per minute).

      * Before 6.15.0, a maximum of 1 pack was queried at a time (it can be roughly understood that a maximum of 200 \* 1 = 200 events are reported per minute).

5. **Data reporting post\-processing:** 

   After each pack is reported, the following processing will be done:

   * The report is successful, delete the corresponding pack reported, and upgrade the frequency control.

   * Report the failure, record the failure information to the corresponding pack, and wait for the next retransmission. If the error returned by the server level this time is 5xx, the frequency control downgrade process will be performed.

6. After sending the queried pack, this sending is over, go back to step 2, and wait for the next trigger to report.
