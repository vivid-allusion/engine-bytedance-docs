---
title: "Integrate the Android SDK into the application"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application"
---

This article introduces the detailed steps for integrating the Android SDK. After integrating the SDK and verifying that data reporting is successful, you can use relevant analysis features on the Application Performance Management Plus platform.

<span id="d6c3d406"></span>
## Precautions


* The Android SDK has a Chinese version and an overseas version; the features are the same, but the reporting addresses are different.

   * Applications released in China: Use the cn version and report within China.

   * Applications released overseas: Use the oversea version and report to Johor, Malaysia.

* Calling the SDK initialization interface does not collect user information, while calling the SDK start interface will begin collection of user information. Please ensure that you have obtained user authorization before collecting user information[SDK Privacy Policy](https://docs.byteplus.com/en/docs/apmplus/The_SDK_privacy_policy).


<span id=".RGVtb-ekuuS-iw=="></span>
## Demo description

[APMPlus_Android](https://github.com/volcengine/APMPlus_Android)


* Demo has already integrated all of ApmPlus's performance and stability monitoring capabilities.

* You can simulate some exception and performance data using the Demo.

* You can configure your own Appid, report data to the platform, and perform SDK feature testing.


<span id=".5q2l6aqk5LiA77ya6I635Y-WU0RL5YyF77yM5byV5YWl5L6d6LWW"></span>
## Step 1: Obtain the SDK package and add dependencies

The Android SDK for Application Performance Management Plus does not need to be downloaded; simply integrate it by following the initialization configuration instructions below.


1. In the project\-level `build.gradle` file, add the Maven address.

&nbsp;

   ```Java
   buildscript {
       repositories {
           maven {
               url "https://artifact.byteplus.com/repository/public/"
           }
       }
   }
   allprojects {
       repositories {
           maven {
               url "https://artifact.byteplus.com/repository/public/"
           }
       }
   }
   ```
   

2. Integrate Application Performance Management Plus.

   1. In the dependencies section of the `build.gradle` file at the project level, add the following code to integrate the plugin component for assisting with instrumentation. `apm_insight_plugin` The same version is used both domestically and internationally.

      ```Java
      classpath "com.volcengine:apm_insight_plugin:1.4.2"
      ```
      

   2. In the dependencies section of the `build.gradle` file in the app module, add the following code. Select one of the two versions below based on whether your application is for domestic or overseas use.

         * Overseas applications integrate with the overseas version and report to Johor, Malaysia. Use the following dependencies:

         ```Java
         implementation 'com.volcengine:apm_insight:1.5.26.byteplus'
         implementation 'com.volcengine:apm_insight_crash:1.5.18.byteplus'
         ```
         


<span id=".5q2l6aqk5LqM77ya5Yid5aeL5YyWU0RL"></span>
## Step 2: Initialize SDK and turn on monitoring

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">User personal information is not obtained during SDK initialization.</div>


<span id=".5bSp5rqD55u45YWz5Yqf6IO9"></span>
### Crash\-related features


1. In the onCreate method of Application, add the following code to initialize crash\-related features.

   ```Java
   MonitorCrash.Config config = MonitorCrash.Config.app({{AppId}})
                   .token({{AppToken}})// Set the authentication token, which can be obtained from the platform application information. If the token is incorrect, data cannot be reported.
   //              .versionCode(1)// Optional; by default, uses the versionCode from PackageInfo
   //              .versionName("1.0")// Optional; by default, uses the versionName from PackageInfo
   //              .channel("google play")// Optional. Set the app's download channel, which can be filtered on the platform. For example, the Google app store channel can be set to "Google Play."
   //              .url("www.xxx.com")// By default, this is not required; only configure the reporting address for private deployments
                   // Optional: you can set a custom did; if not set, the internal default will be used.
   //              .dynamicParams(new MonitorCrash.Config.IDynamicParams() {
   //                  @Override
   //                  public String getDid() {//If the return value is empty, the internal default did will be used.}
   //                      return null;
   //                  }
   //
   //                  @Override
   //                  public String getUserId() { //Optional.
   //                  } A unique identifier for the user, allowing users to define their own UserId to associate platform data with their own user. Each time it is used internally, the getUserId() function is called, and its return value can be assigned to a variable. When the user logs in and has a UserId, assign the UserId to this variable.
   //                      return null;
   //                  }
   //              })
                   // Optional: add custom business data in the crash details page, under On-site Data
   //              .customData(crashType -> {
   //                  HashMap<String, String> map = new HashMap<>();
   //                  map.put("app_custom", "app_value");
   //                  return map;
   //              })
                 .exitType(ExitType.EXCEPTION) // Optional. Report application exit cause. The EXCEPTION type will filter out the USER_REQUEST type.
                 .enableApmPlusLog(true) // Optional. Whether to write crash information and similar data to the APMPlus log. The default value is false.
   //              .crashProtect(true)  // Optional; whether to turn on crash protection. The default value is false.
   //              .enableOptimizer(true)  // Optional. Specifies whether to turn on the crash optimization solution. The default value is false.
                 .autoStart(false) // Optional. Specifies whether to automatically turn on Monitoring during initialization. The default value is true (if this method is not called, Monitoring is automatically turned on during initialization).
   //            .debugMode(true) // Optional. Log switch for offline use only; in production, do not call this method, or set it to false.
                // Optional: Add a custom tag to the pv event to filter the denominator data used for crash ratio calculation.
                //.pageViewTags(<<Map<String, String>>>)
                 .build();
           MonitorCrash monitorCrash = MonitorCrash.init(ApplicationContext, config);
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to pass ApplicationContext as the context.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Parameters must not be null; otherwise, initialization will fail.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">versionInt is a numeric version number, for example, 100; versionString is a string version number, for example, "1.0.0".   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The returned MonitorCrash instance serves as the entry point for subsequent configuration.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Avoid repeated calls to the initialization method, and perform a null pointer check on the object returned by init.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">aid can be obtained from the URL of the platform project browser.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the method to obtain AppID and AppToken, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken">How to query AppID and AppToken?</a>.   </div>
   

2. Start crash monitoring, begin collecting data.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only call the method to collect data after the user has agreed to the privacy policy.   </div>
   

   ```Java
   // Start monitoring. When initializing, if the autoStart parameter is set to false, monitoring will not start automatically and you need to call the start method at an appropriate location to start monitoring. If the autoStart parameter is not set during initialization or is set to true, monitoring will start automatically and you do not need to call the start method.
           if (monitorCrash != null) {
               monitorCrash.start();
           }
   ```
   


<span id=".5oCn6IO955u45YWz5Yqf6IO9"></span>
### Performance\-related features


1. In the onCreate method of the Application class, add the following code to initialize performance\-related features.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please add code for initializing performance\-related features in the main thread.   </div>
   

   ```Java
   //Must be placed in the onCreate method of Application; it will register a lifecycle listener and does not involve data collection or privacy compliance issues.
   ApmInsight.getInstance().init(application);
   //Initialize custom log and configure the maximum disk usage for the custom log. Typically, the internal configuration is set to 20, which means the maximum disk usage is 20 MB. This API has been available since version 1.4.1.
   VLog.init(this,20);
   ```
   

2. Start the performance monitor and begin collecting data.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Call the method to collect data only after the user has agreed to the privacy policy.   </div>
   

   ```Java
   //Call after agreeing to privacy compliance
   ApmInsightInitConfig.Builder builder = ApmInsightInitConfig.builder();
   //Set the allocated appid
   builder.aid({{app_id}});
   //Set the allocated AppToken
   builder.token({{AppToken}});
   // Whether to turn on the lag feature
   builder.blockDetect(true);
   //Whether to turn on the severe lag feature
   builder.seriousBlockDetect(true);
   //Whether to turn on smoothness and frame loss detection
   builder.fpsMonitor(true);
   //Control whether to enable WebView monitoring
   builder.enableHybridMonitor(true);
   //Control whether to enable memory monitoring
   builder.memoryMonitor(true);
   // Control whether to enable battery monitoring
   builder.batteryMonitor(true);
   //Controls whether to enable the CPU monitor
   builder.cpuMonitor(true);
   //Controls whether to enable the disk monitor
   builder.diskMonitor(true);
   //Control whether to enable the traffic monitor
   builder.trafficMonitor(true);
   //Control whether to enable monitoring of user session duration
   builder.operateMonitor(true);
   //Controls whether to enable monitoring. Enabling monitoring also requires configuring the apm-plugin.
   builder.startMonitor(true);
   //Controls whether to enable Activity duration monitoring for pages. Enabling this feature also requires configuration of the apm-plugin.
   builder.pageMonitor(true);
   //Controls whether to turn on network monitoring. Turning it on requires configuring the apm-plugin plugin at the same time.
   builder.netMonitor(true);
   // Whether to print logs. Note: For the production release, the configuration should be set to false.
   builder.debugMode(true);
   //No configuration is required by default; configuration of the data reporting domain name is only necessary for private deployments. (An internal default domain name is provided. For testing, setting http://www.xxx.com is supported. The default protocol is HTTPS.)
   //builder.defaultReportDomain("www.xxx.com");
   //Set channel. Interfaces added in version 1.3.16
   
   //Turn on leak detection and leak fallback detection capabilities. Leak detection and leak fallback detection each require separate sampling configuration on the platform.
   //builder.detectActivityLeak(new IActivityLeakListener() {
   //    @Override
   //    public void onActivityLeaked(Activity activity) {
   //        //callback for activity leak
   //   }
   //});
   
   // Optional: set the App download channel, and can be filtered on the platform. For example, the Google app store channel can be set to "google play".
   builder.channel("google play");
   // Enable the custom log recovery capability. New interfaces added in version 1.4.1
   builder.enableLogRecovery(true);
   //Enable APMPlus log capability to obtain APMPlus logs via recovery
   builder.enableAPMPlusLocalLog(true);
   // When setting data and integrating with Rangers Applog data, the device identifier "did" is required. Interfaces added in version 1.3.16
   builder.setDynamicParams(new IDynamicParams() {
       @Override
       public String getUserUniqueID() {
           // Optional. If AppLog is used, you can obtain the user unique ID through AppLog.getUserUniqueID(); otherwise, the method may return null.
           return null;
       }
   
       @Override
       public String getAbSdkVersion() {
           // Optional. If AppLog is a dependency, you can obtain it through AppLog.getAbSdkVersion(); otherwise, you can return null. getAbSdkVersion is a parameter of the callback class and can be set after initialization.
           return null;
       }
   
       @Override
       public String getSsid() {
           // Optional. If you rely on AppLog, you can obtain the ssid via AppLog.getSsid(); otherwise, the ssid may return null. getSsid is a parameter of the callback class and can be set after initialization.
           return null;
       }
   
       @Override
       public String getDid() {
           //Optional for version 1.4.0 and above; required for other versions. The unique identifier of the device. If you rely on AppLog, you can obtain it using AppLog.getDid(), or you can generate it yourself. getDid is a parameter of the callback class and can be set after initialization.
           return null;
       }
       
       @Override
       public String getUserId() {
            // Optional. A unique identifier for the user. The system supports user-defined user_id, allowing you to associate platform data with your own user accounts. Each time it is used internally, the getUserId() function is called, and its return value can be stored in a variable. When the user logs in and obtains a UserId, assign the UserId to the variable.
            return "userid";
       }
       
   });
   
   ApmInsight.getInstance().start(builder.build());
   ```
   

3. At the outermost level of the build.gradle file in the app module, add the following code to complete instrumentation.

   Instrumentation is intended to simplify the integration of network monitoring, start monitoring, and page monitoring, and is not related to other monitoring capabilities. We currently support up to AGP version 7.0.2. For solutions to compilation exceptions, refer to the documentation [Apmplus plugin compilation exception](https://docs.byteplus.com/en/docs/apmplus/Apmplus_plugin_compilation_error). If compilation conflicts and exceptions occur, you can also directly use the non\-instrumentation method for integration. For details, refer to [How to integrate Monitoring capabilities using the non-instrumentation method?](https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_monitoring_capability_based_on_a_non-instrumentation_approach).

   ```Java
   // Add at the beginning of the file
   apply plugin: 'apm-plugin'
   
   ApmPlugin {
       // Whether to perform instrumentation
       enable true
       // Whether to enable instrumentation in the Debug package; instrumentation is disabled by default
       enableInDebug true
       // DEBUG("DEBUG"), INFO("INFO"), WARN("WARN"), ERROR("ERROR");
       // The DEBUG level log aggregates all instrumented classes for view. Path: app/build/ByteX/ApmPlugin/ApmPlugin_log.txt
       logLevel "DEBUG"
       // Startup analytic switch: Monitoring app startup duration also requires turning on pageLoadSwitch
       startSwitch = true
       // Switch for monitoring Activity lifecycle time
       pageLoadSwitch = true
       // Network monitoring switch: Monitoring network requests made by okhttp3
       okHttp3Switch = true
       // Switch for displaying instrumentation of HttpUrlConnection network requests
       httpUrlConnectionSwitch = true
       // Important: To instrument packages under the allowlist, you must specify the package name where the class to be instrumented is located. Prefix configuration is supported, and by default, you can use 'com'.
       whiteList = [
               "com"
       ]
       // Classes in blocklist packages are not instrumented. You can configure package names and class names; if none are specified, these fields can be left blank.
       blackList = [
       ]
   }
   ```
   


<span id=".V2ViVmlld-mhtemdouebkeaOpw=="></span>
### WebView page monitoring

WebView initialization is typically performed within an Activity or a Fragment. Add the following code to wrap the WebView that needs to be monitored. Reported data will be displayed in the New H5 monitor module.

```Plain
// Set the WebChromeClient for the webView.
webView.setWebChromeClient(new WebChromeClient(){
    @Override
    public void onProgressChanged(WebView view, int newProgress) {
        super.onProgressChanged(view, newProgress);
        // Call the following function to control the new H5 monitoring of JS loading.
        HybridMonitorManager.getInstance().onProgressChanged(view,newProgress);
    }
});

// The following function needs to be called before the WebView loads the URL.
HybridMonitorManager.getInstance().onLoadUrl(webView,url);
webView.loadUrl(url);
```


<span id="82211ed6"></span>
### Optional configuration


* If privacy compliance requires you to turn off some data collection, please modify the following configuration before initializing the SDK.


```Plain
import com.apm.applog.AppLog;
// Disable the collection of the device's OAID (optional).
AppLog.setOAIdEnabled(false);
// Disable the collection of the device's GAID (optional).
AppLog.setGAIdEnabled(false);
// Disable the collection of the operating system information (optional).
AppLog.setEnableOsVersion(false);
// Disable the collection of the device model information (optional).
AppLog.setEnableDeviceModel(false);
// Disable the collection of the screen resolution information (optional).
AppLog.setEnableDisplay(false);
```



* The switch for the `SDK setting configuration` on the platform can control whether to turn on related capabilities and data collection and reporting. For example, disk monitor and memory optimization switches, as well as sampling controls, can be used to manage the collection and reporting of disk and memory data.

* Permission description: The following permissions are optional and do not require special business handling by default.


```Plain
// Optional permission. When you need to read disk monitoring - related data, the user needs to agree to enable the permission.
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
// Optional permission. When you need to save temporary data, the user needs to agree to enable the permission.
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```


<span id="49dce7df"></span>
## **Step 3: Upload symbol table**

The symbol table can parse the contents of a crash stack trace, converting the stack trace information in the log from a raw stack trace to a symbolized stack trace. The symbol table mainly supports two methods: manual upload and automatic upload.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also select to upload the symbol table using methods such as custom scripts. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_customize_uploading_a_symbol_table">How to customize symbol table upload</a>.</div>


<span id="45e40de8"></span>
### Manual upload

Manual upload is performed on the **symbol table management** page. For details, refer to [Android symbol table management](https://docs.byteplus.com/en/docs/apmplus/File_management#d0e32c8d).

<span id="851d6474"></span>
### **Automatic upload**


1. In the dependencies section of the project\-level `build.gradle` file, add the following code to integrate the plugin component.

   ```Java
   classpath "com.volcengine:apmplus_upload_plugin:0.0.12-byteplus"
   ```
   

2. In the `build.gradle` file of the application project, add the following code to configure automatic symbol table upload.

   ```Java
   apply plugin: 'apmplus-upload-plugin'
   ApmPlusUploadConfig {
           api_token = "" // From the platform, go to All features > Symbol table management > System selection, then select Android. The API key and API token will be displayed below. Alternatively, contact the development team to obtain a token for the corresponding appId; no setting is required for private deployment.
           api_key = 0 // From the platform's feature -> symbol table management -> operating system select Android -> the API key and API token can be viewed below. Alternatively, contact the development team to obtain a key for the corresponding appId; for private deployment, there is no need to set this.
           aid = 12345 // appid on Application Performance Management Plus
           // oversea = true // Set to true when uploading the symbol table for the overseas domain version. For the domestic platform, this setting is not required or should be set to false.
    //       updateVersionCode = -1 // By default, you do not need to write this line unless you manually specify a non-standard version code (or SDK version code) during initialization; the version code here must be consistent with the one used during initialization.
   //       mappingUrl = "https://www.xxx.com" // By default, you do not need to write this line. If you are using a private deployment, configure the private platform domain name here.
   }
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When integrating the SDK, the value of the <code>updateVersionCode</code> field must match the value passed during APMPlus initialization.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When integrating the App, configuration of <code>updateVersionCode</code> is not required. Please delete this line of code.   </div>
   


<span id="d885935f"></span>
## References


* After integrating the Android SDK into your application, if you need to verify data reporting for each module, refer to [Verify data reporting](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data_Android).

* After integrating the Android SDK, if you need to use advanced features, refer to [Use advanced features](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features_Android).
