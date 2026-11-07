---
title: "Android SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Android_SDK_Integration_Scenario_Practice"
---

<span id="6a0bcdc1"></span>
# SDK offline integration package description

<span id="c1a60b82"></span>
## Offline file description

Please go to the [Android SDK package download page ](https://github.com/volcengine/datarangers-sdk-packages)to get the corresponding version of the SDK package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Android offline package name is <code>All-cn-Android_ version number.zip</code>format. For example: <code>All-cn_Android_6.17.0.zip</code>, where 6.17.0 is the SDK version number.</div>


```Java
Mandatory dependence:
 - if_encryptor-xxx.aar（6.17.0 and before） / encryptor-xxx-private.aar: Encryption library related
 - RangersAppLog-All-cn-xxx.aar: DataFinder major function
 - RangersAppLog-Log-xxx.aar: DataFinder SDK internal log dependency
 - plugin-aggregation-xxx.aar: DataFinder SDK internal information aggregation module dependency

Optional dependence:
 - RangersAppLog-All-scheme-xxx.aar: Real-time event tracking monitoring and circle function
 - RangersAppLog-All-plugin-xxx.jar: SDK plugin, mainly supports full event tracking / h5 open up / blacklist filter / remove some privacy collection code
 - RangersAppLog-DevTools-xxx.aar: Visual event tracking debugging tool, which can be used to verify event tracking process
```


<span id="12403e20"></span>
## integration instructions

```Java
Integration methord 1, project already includes aar / jar of all libs:
//build.gradle in the app directory
implementation fileTree(dir: 'libs', include: ['*.jar','*.aar'])
//At this time, you can add the above required dependencies and some optional dependencies to the libs directory

Integration methord 2, integrate one by one:
//build.gradle in the app directory
implementation files('libs/encryptor-xxx-private.aar')
//6.17.1 and above removed if_encryptor -xxx
implementation files('libs/if_encryptor-xxx.aar')
implementation files('libs/RangersAppLog-All-cn-xxx.aar')
implementation files('libs/RangersAppLog-Log-xxx.aar')
implementation files('libs/plugin-aggregation-xxx.aar')
//The remainder is integrated on demand
//Note: The debugging tool recommends only debug mode
debugImplementation files('libs/RangersAppLog-DevTools-xxx.aar')

If use plugin offline, please refer to integration method below:
//build.gradle in the root directory
buildscript {
  dependencies {
    //gradle plugin required for growth marketing
    //If you put xxxdir in the app/libs directory, you can replace it with app/libs.
    classpath fileTree(include: ['*.jar'], dir: 'xxxdir/RangersAppLog-All-plugin-xxx.jar')
  }
}

offline package depend on confusion configuration:
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


<span id="6ff245df"></span>
# user_unique_id related

<span id="e7ec629e"></span>
## user login settings

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: The concept of user login status is a statement from a business perspective. The SDK itself does not have the concept of user login/login. The SDK only cares about whether the user_unique_id has been actively set.</div>


For example, the business has an account system and wants the SDK to synchronize user status. You can consider setting user_unique_id to the SDK immediately after the user logs in, and clearing the user_unique_id to the SDK immediately after the user logs out.

```TypeScript
//Set user_unique_id immediately after user login
AppLog.setUserUniqueID("your_USER_UNIQUE_ID");

//Clear user_unique_id immediately after user logs out
AppLog.setUserUniqueID(null);
```


<span id="86f883d2"></span>
## User caliber related processing

If you want to set the user aperture, you need to set the user_unique_id_type at the same time as setting the user_unique_id

```TypeScript
//Set user_unique_id and user_unique_id_type immediately after user login
AppLog.setUserUniqueID("your_USER_UNIQUE_ID", "your_USER_UNIQUE_ID_TYPE");

//clear user_unique_id and user_unique_id_type immediately after user logs out
AppLog.setUserUniqueID(null, null);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: user_unique_id_type values are pre\-made, ask your project manager or customer success manager.</div>


<span id="c45646a0"></span>
## Multi\-user aperture type processing

If you want to perform multi\-aperture binding, you need to call the bind method after setting the user_unique_id_type while setting the user_unique_id. Attention: Only in the SAAS cloud native, private support.

```TypeScript
//In the example, phone and cust_num are only examples, and the specific transmission is determined by the business
Map<String, String> ids = new HashMap<String, String>
ids.put("phone", "1230000000"); //The first parameter phone is an enumeration value of type id, the same as the id design scheme
ids.put("cust_num", "12345656788888"); //The first parameter cust_num the enumeration value of the id type, the same as the id design scheme
AppLog.bind(ids, new IDBindCallback() {
    void onSuccess(IDBindResult result) {
        //Request successful and set login status
        AppLog.setUserUniqueID("12345656788888" ,"cust_num");
    }
    void onFail(int code) {
        //binding request failed
    }
});
```


<span id="5a46ea81"></span>
# SDK plug\-in (full event tracking, H5 connection, sensitive field collection code removal)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to enable full event tracking, webview automatic injection, privacy field code removal and other functions.</div>


<span id="e768d9a0"></span>
## plugin dependency

<span id="7b26ba23"></span>
### plugin repository configuration

**Gradle below 7.0**

```Java
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


**Gradle 7.0 and above**

```Java
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


<span id="388f81ea"></span>
### plugin dependency

**Gradle below 7.0**

```Java
//Add the maven repository and SDK plugin to the repositories of buildscript in the project-level build.gradle
buildscript {
    //omit other
    dependencies {
        classpath 'com.bytedance.applog:RangersAppLog-All-plugin:6.17.4'
    }
}

//build.gradle at the app module level
//Default, put to the last declaration in the plugin list, if there is a conflict,
//you can adjust it to the first one after official plugins such as application/kotlin.
apply plugin: 'com.bytedance.std.tracker'
```


**Gradle 7.0 and above~ 8.0 and below**

```Java
//project-level build.gradle
buildscript {
    //omit other
    dependencies {
        classpath 'com.bytedance.applog:RangersAppLog-All-plugin:6.17.4'
    }
}

//build.gradle at the app module level
//Default, put to the last declaration in the plugin list, if there is a conflict,
//you can adjust it to the first one after official plugins such as application/kotlin.
plugins {
    //omit other plugins
    id 'com.bytedance.std.tracker'
}
```


**Gradle 8.0 and above**

```Java
//project-level build.gradle
buildscript {
    dependencies {
        //agp8 version uses the new version plugin
        classpath 'com.bytedance.applog:RangersAppLog-All-plugin-agp8:6.17.1'
    }
}

//build.gradle at the app module level
//Default, put to the last declaration in the plugin list, if there is a conflict,
//you can adjust it to the first one after official plugins such as application/kotlin.
plugins {
    //omit other plugins
    id 'com.bytedance.std.tracker'
}
```


<span id="a0789d0e"></span>
## Plugin usage example

Apply the plugin in the build.gradle file at the app module level.

**Gradle 8.0 or less**

```Java
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


**Gradle 8.0 and above**

```Java
//The new version of the plugin is adjusted to appLog.
appLog {
    //Automatically inject the docking bridge of the webview
    //The get-through function of agp8 needs to use 6.16.7 and above version
    autoInjectWebViewBridge = true

    //instrumentation blacklist, package path prefix, configure for some packages that do not want instrumentation, and benchmark the old plugin blackList
    //Example: ignoredInstrumentationPaths = ['dji.upgrade.internal', 'org.bouncycastle.jcajce']
    //From ['dji/upgrade/internal', 'org/bouncycastle/jcajce'] to ['dji.upgrade.internal', 'org.bouncycastle.jcajce']
    ignoredInstrumentationPaths = []

    //event tracking blacklist configuration, benchmarking the old plugin trackBlackList
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
    //Example of usage scenario: When you use the lite package, but you need to trackBlackList to remove part of the capture code, you can use this function
    disableAutoTrack = false
}
```


<span id="5dca8fbf"></span>
# H5 through the introduction

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your application integrates the Web/JS SDK and the Android SDK at the same time, by default, all H5 events will be reported through the Web/JS SDK. If you want the H5 event to be reported by the Android SDK, you can use the embedded H5 function to get through. At this time, the events generated on the H5 page will be reported through the Android SDK instead of the Web/JS SDK. This kind of takeover and reporting scenario will reuse the <code>user_unique_id</code>and public properties set by the Android side, but also supports the uuid/public properties on the web side setting/update end when getting through. Please pay attention to which side of the data is used when getting through. If it is completely subject to the end, you can remove the uuid on the web SDK side (if you need to support updating multi\-caliber from the web side, you need to use a new version of the SDK)/public attribute operation.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get through the function requires the Web/JS SDK and Android SDK to integrate and cooperate with each other at the same time, and the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, because the reporting is taken over by the Android SDK at this time. If you still want to collect H5 full event tracking, you need to check Section 5.7: Native collection of H5 full event tracking. Web/JS SDK Integration Refer to <a href="https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_">Web/JavaScript SDK Integration</a> and Section 3.4.</div>


<div data-tips="true" data-tips-type="warning">Lite does not support the function of packing and getting through. If you need to get through, please integrate All.</div>


```Java
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
    autotrack: After connecting, the old version becomes invalid (web sdk version before 5.1.10 will be invaild, version 5.1.10 and subsequent versions will be collected normally)
})
```


<span id="5be8ac7f"></span>
## Get through the whitelist pre\-work of the embedded H5 page

After the switch is turned on, the whitelist must be configured. Only the domain names configured in the whitelist take effect. The whitelist can be added by wild\-card, and `*`means wild\-card.

```Java
//Embedded H5 page whitelist configuration
//Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
config.setH5BridgeAllowlist(Arrays.asList("www.volcengine.com", "*.bytedance.*"));
//There are many whitelists for adaptation www.bytedance.com, please configure the whitelist according to the business scenario, for example:
//www.bytedance.com or * .bytedance. * or *.*.* , all supported. 
```


If you do not filter any domain names and local resource files, you can configure to allow all H5 pages to open. This configuration has a higher priority than `setH5BridgeAllowlist`.

```Java
//allow all h5 to open up
//This function only supports 6.9.7 and above versions
config.setH5BridgeAllowAll(true);
```


<span id="78a4a57f"></span>
## Get through the plug\-in injection attention item embedded in the H5 page

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Under normal circumstances, H5 requires you to integrate the AppLog plugin plugin first. At this time, the injection Bridge is completed by Plugin instrumentation, but in some scenarios, the instrumentation may not take effect (the scenarios where the insertion fails may be confused, overwritten, etc.). You can choose to manually turn off the automatic injection Bridge ability of the SDK, and then manually call the injection. At this time, you can add the configuration <code>autoInjectWebViewBridge = false</code>in the full event tracking plugin Plugin, and then manually inject the Bridge before the WebView that needs to get through loads H5.</div>



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


<span id="206d85f5"></span>
## Prohibit H5 from updating user information in the app (uuid) when opening the embedded H5 page

When getting through, the in\-terminal SDK user information is used by default, but it also supports the H5 side to update the in\-terminal SDK user information through the Web SDK.

Android 6.17.0 version is newly added to prohibit H5 from updating user information in the App when getting through the embedded H5 page, so as to avoid the difficulty of removing the relevant code for updating user information when using H5 in many places, thereby destroying the original user information of the SDK in the terminal when getting through.

```Java
//On by default, support off
config.setUseBridgeUpdateUUIDEnabled(true);
```


<span id="4d4bb581"></span>
# Finder SDK instance related

<span id="268e8477"></span>
## SDK default instance introduction

Android SDK provides a default global instance, by AppLog.xxx is equivalent to calling the default global instance.

```Java
AppLog.xxx equals AppLog.getInstance().xxx
```


<span id="d3ad2d12"></span>
## Multi\-instance introduction

Multi\-instance initialization means that the SDK supports event tracking to multiple applications (multiple appids) in apps with the same package name, and the event tracking data is isolated from each other, and each appid corresponds to a separate instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the multi\-instance scenario, the appid configured in the SDK is the application ID generated when creating each application in the DataFinder. You need to create corresponding multiple applications in the DataFinder, and obtain the application ID, and then configure the application ID into the SDK. See details <a href="https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration#8c5ac3ed">Step 2: Obtain the APPID/APP URL</a>.</div>


Usage scenarios such as:


* When the third\-party SDK relies on the **Growth Marketing Suite SDK** to do event tracking generated internally in the SDK;

* When you associate multiple event tracking apps (multiple appids) in the same app or system and share the **Growth Marketing Suite SDK**;


```Java
Core API, after use, the IAppLogInstance object is returned, and the developer needs to save the instance to ensure that the data is sent to the correct instance
AppLog.newInstance()
```


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
config1.setAutoTrackEnabled(true); //Full event tracking switch, true: on, false: off
config1.setLogEnable(true); //true: open log, set logger, false: close log
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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note: The app_id requirements for different instances cannot be the same.</div>


<span id="d795cda9"></span>
# Privacy compliance

<span id="18e6b6ed"></span>
## SDK can turn off captured sensitive fields

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The switch deals with whether sensitive field collection logic is reached when dynamically executable code during app execution.</div>



1. Disable MAC Address Acquisition


```Java
//After the switch is turned off, the relevant code does not run, and the attributes are not collected. Whether to upload depends on whether the customer has passed in the MAC from the outside.
config.setMacEnable(false);
```



2. Turn off device IMEI/MEID acquisition


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">OAID is important device tracking information. Turning off OAID will affect Tracer attribution. Please consider using Tracer with caution.</div>


```Java
//After the switch is turned off, the relevant code does not run, the attributes are not collected, and whether to upload depends on whether the customer has passed AppImei from the outside.
config.setImeiEnable(false);
```



3. Turn off OAID acquisition


```Java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
config.setOaidEnabled(false);
```



4. Turn off Android ID capture


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Closing the Android ID will affect the device_id generation logic, resulting in inconsistent device_id uninstall and reinstall.</div>


<div data-tips="true" data-tips-type="warning">Subsequent documentation will be abbreviated device_id did.</div>


```Java
//After the switch is closed, the relevant code will not run, and the attributes will not be collected. After closing, it will be randomly generated and saved in the local cache. Uninstall and reinstall will lose the cache.
config.setAndroidIdEnabled(false);
```



5. Turn off ICCID acquisition


```Java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.14.3 and above versions
config.setIccIdEnabled(false);
```



6. Turn off SN (hardware serial number) acquisition


```Java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.15.0 and above versions
config.setSerialNumberEnable(false);
```



7. Turn off GAID acquisition

   * 6.15.0 before cn (domestic version) and global (overseas version) were collected by default

   * 6.15.0 and after cn is closed by default, global is turned on by default


```Java
//After the switch is closed, the relevant code does not run, the attributes are not collected, and whether to upload depends on whether the customer has passed Gaid from the outside.
config.setGaidEnabled(false);
```



8. Turn off carrier information collection


```Java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
config.setOperatorInfoEnabled(false);
```



9. Close clipboard access


```Java
//client clipboard content will not be accessed after switch off
//Close through the corresponding applog instance
AppLog.setClipboardEnabled(false);
```



10. Turn off CPU architecture acquisition


```Java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.17.1 and above versions
config.setCPUAbiEnabled(false);
```



11. Turn off screen definition/screen density capture


```Java
//After the switch is closed, the relevant code does not run, and the attributes cannot be collected and sent.
//This function only supports 6.17.1 and above versions
config.setDisplayDensityAndDpiEnabled(false);
```


<span id="72b7a67d"></span>
## Static detection removes related code

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your app allows some sensitive fields to be stored in Apk, for example, compliance does not need to use the API of collecting sensitive fields when scanning Apk statically, then removing them during compilation through plugins can meet your requirements.</div>


<div data-tips="true" data-tips-type="tip">If you integrate plug\-ins, please refer to this article < SDK plug\-ins (full event tracking, H5 connection, sensitive field collection code removal) \>.</div>



1. Remove MAC address related code

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



2. Remove IMEI/MEID related codes

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



3. Remove OAID related code

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



4. Remove AndroidId related code

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



5. Remove operator information related code

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



6. Remove clipboard related code

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


<span id="5ab6ba03"></span>
# Full event tracking scenario

<span id="eb8c6394"></span>
## Custom page event properties

`The IPageMeta`interface class supports custom headers, paths, and properties. Implement the interface and corresponding functions on an Activity or Fragment, for example:

```Java
public class MyActivity extends Activity implements IPageMeta {
    @Override
    public String title() {
        return "自定义页面"; //custom page
    }
    
    @Override
    public String path() {
        return "/mypath";
    }
    
    @Override
    public JSONObject pageProperties() {
        JSONObject params = new JSONObject();
        try {
            params.put("key", "value");
        } catch (JSONException e) {
            
        }
        return params;
    }
}
```


<span id="3b07be8e"></span>
## Custom View Click Event Properties

In addition to the preset properties for each preset event, DataFinder also supports setting custom properties for click events (bav2b_click).

<span id="bc2ce99e"></span>
### Set the element ID of the View

Support setting an element ID for the specified View object, string is enough, example:

```Java
AppLog.setViewId(view, "myElementId");
```


<span id="441b72f8"></span>
### Set the properties of the View

Supports setting property values for the specified View object, example:

```Java
JSONObject props = new JSONObject();
try {
    props.put("key", "value");
} catch (Exception e) {
}
AppLog.setViewProperties(view, props);
```


<span id="86c5a63c"></span>
## Ignore full event tracking events

<span id="0a8d2edd"></span>
### Ignore specific page access events

Supports omitting full event tracking events for specific Activities or Fragments, example:

```Java
AppLog.ignoreAutoTrackPage(MyActivity.class, MyFragment.class);
```


<span id="ff57f25d"></span>
### Ignore Click Events for Specific Views


* Ignore the click event of the specified View object, example:


```Java
AppLog.ignoreAutoTrackClick(findViewById(R.id.button1));
```



* Ignore click events of the specified View type, example:


```Java
//Ignore click events for all Switch components
AppLog.ignoreAutoTrackClickByViewType(Switch.class);
```


<span id="c420ba45"></span>
## Manually capture full event tracking

<span id="36330ee1"></span>
### Manually capture page events

Supports manual collection of page events and properties for specific Activity and Fragment objects. Example:

```Java
JSONObject params = new JSONObject();
try {
    params.put("param1", "test");
} catch (JSONException e) {
}
AppLog.trackPage(MyActivity.this, params);
```


<span id="0adf71b0"></span>
### Manually Capture View Click Events

Supports manual collection of click events and properties for a specific View. Example:

```Java
JSONObject params = new JSONObject();
try {
    params.put("param1", "test");
} catch (JSONException e) {
}
AppLog.trackClick(myView, params);
```


<span id="1e9d6964"></span>
# Other Scenario Practices

<span id="b36c4ba7"></span>
## Native capture H5 full event tracking

When the H5 page is embedded in the native end, the H5 page full event tracking event can be collected from the native end by turning on the following switch.

There are generally two usage scenarios:


* Since the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, in order to ensure that the H5 page full event tracking function can still be retained after getting through.

* Independent use, in the case that H5 does not integrate Web/JS SDK, I want to enable the full event tracking function on the H5 page in the application.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature can be used independently without the need to integrate a Web/JavaScript SDK.</div>


* <div data-tips="true" data-tips-type="warning">This feature is available 6.14.4 version, and the current H5 full event tracking only supports page entry events and click events.</div>



```Java
//Note: This feature only supports native WebView and Tencent X5

//Embedded H5 page full event tracking event
config.setH5CollectEnable(true); //true: turn on h5 full event tracking event, false: turn off h5 full event tracking event
//Supplement, this function is also injected by plug-in by default, when the plug-in fails or you want to manually inject it yourself
```


<span id="8aad8f2e"></span>
## How to correctly obtain parameters such as DID

Since did/ssid is returned through a device service request, there may be a certain delay in obtaining it. Methods such as Applog.getDid () may not be able to obtain the corresponding parameters at the first time. Therefore, it is recommended to obtain it through a callback, and after the callback, Applog.getDid () and other methods can ensure a certain acquisition.

```Java
//step1: Add dataset observation callback, this refers to the class that implements IDataObserver
AppLog.addDataObserver(this);
//step2: Use it after getting the data through onIdLoaded or onRemoteIdGet of IDataObserver or use the following methods to obtain it:
Default instance: Applog.getDid() / use multiple instances: IAppLogInstance.getDid()


//IDataObserver main function introduction and parameter introduction:
//- did, iid, ssid can all be obtained through this callback
//- server level configuration fetch
//- ab experiment configuration acquisition
public interface IDataObserver {
    /**
     * Local ID data loading result notification
     *@param did device id
     *@param iid install id
     *@param Ssid number says id
     */
    void onIdLoaded(@NonNull String did, @NonNull String iid, @NonNull String ssid);

    /**
     Notify registration results and ID changes
     Only the main process will be called
     *@param Changed whether it is different from the local cache
     *@param oldDid Local old oldDid, possibly empty
     *@param newDid server returns new device id
     *@param newIid server returns the new install id
     *@param newSsid server returns the new ID
     */
    void onRemoteIdGet(boolean changed, @Nullable String oldDid, @NonNull String newDid,
                       @NonNull String oldIid, @NonNull String newIid, 
                       @NonNull String oldSsid, @NonNull String newSsid);

    /**
     * Config pulls data, and notifies changes compared with local data
     Only the main process will be called
     *@param Changed whether it is different from the local cache
     *@param Config server returns new config content
     */
    void onRemoteConfigGet(boolean changed, @Nullable JSONObject config);

    /**
     * The server pulls AbConfig data and notifies changes compared with local data
     Only the main process will be called
     *@param Changed whether it is different from the local cache
     *@param abConfig server returns new abConfig content
     */
    void onRemoteAbConfigGet(boolean changed, @NonNull JSONObject abConfig);

    /**
     * Notification of client side ab exposure vid collection changes
     *@param Vids client side ab experiment exposure vid collection
     *@param extVids external vid collection of external settings
     */
    void onAbVidsChange(@NonNull String vids, @NonNull String extVids);
}
```


<span id="b6eb421c"></span>
## Event filtering and custom parameter padding

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


<span id="8e37711a"></span>
## event public property

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="c097e3bb"></span>
### Set public properties

```Java
/*
 * Example: Set a custom public property with the property name key_public and the property value value_public
 * Please note about customizing "public properties":
 * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute.
 *    Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail;
 * 2. High-frequency modifications are not recommended, such as once per second.
 */
 Map<String,Object> headerMap = new HashMap<String, Object>();
 headerMap.put("key_public", "value_public");
 AppLog.setHeaderInfo((HashMap<String, Object>)headerMap);
```


<span id="edbd5bdb"></span>
### Remove public attributes

```Java
//Example: Remove a public property named key_public
AppLog.removeHeaderInfo("key_public");

//Remove all set public properties by passing null
AppLog.setHeaderInfo(null);
```


<span id="6e433eae"></span>
## Get platform ID and notifications

<span id="669f2f3b"></span>
### Get the platform generation ID

```Java
//It is recommended to refer to "How to obtain parameters such as DID" for the correct acquisition time.
String ssid = AppLog.getSsid(); //Get SSID
String did = AppLog.getDid(); //get device bddid
```


<span id="2d2b5c6e"></span>
### Get the SDK version number

```Java
//The SDK version number format is X.X.X
String sdkVersion = AppLog.getSdkVersion();
```


<span id="217b2674"></span>
## acquisition duration event

> This section is supported after 6.10.1 +.


Events with time attributes can use the duration event capture interface, such as capturing video playback duration events. Example:

```Java
//Called when the video starts playing
AppLog.startDurationEvent("play");

//Called when the video is paused
AppLog.pauseDurationEvent("play");

//Called when the video continues to play
AppLog.resumeDurationEvent("play");

//Called at the end of playback, a play event will be reported at this time, with a $event_duration attribute (the playback time is recorded, in milliseconds)
JsonObject params = new JsonObject() 
//You can fill in your own custom parameters in params
AppLog.stopDurationEvent("play", params);
//After 6.16.10, the event name of the self-contained custom duration event, the default event name is the first parameter of the method
AppLog.stopDurationEvent("play", params, "custom_play");
```


<span id="ed6151e2"></span>
## Configure Scheme (optional)

If you need to use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification) or [Circle Event](https://docs.byteplus.com/docs/DataFinder/Circle_Event), please configure Scheme, because H5 needs to wake up the app through Scheme after scanning the code. If you find that the scan code is successful but the app does not jump, you can manually switch back. In a few scenarios, there is no automatic jump.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please make sure to remove the scheme package before the official launch and only use it during debugging to avoid compliance risks.</div>


<span id="8fcf1585"></span>
### Get URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/380b7a6cec9c4b8b9b461fa7bf8334a3~tplv-goo7wpa0wc-image.image) </span>

<span id="0ee95b78"></span>
### Add URL Scheme

Add URL Scheme to build.gradle at the app module level.

```Groovy
//Add defaultConfig in android
manifestPlaceholders.put("APPLOG_SCHEME", "yourURL_SCHEME".toLowerCase())
```
