---
title: "Integrate the iOS SDK"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app"
---

The iOS SDK for Application Performance Management Plus is essentially non\-intrusive. After integrating the SDK, the app can perform crash analytic, error analytic, lag analytic, and analysis of various monitoring metrics to help optimize and identify issues. This document describes the detailed integration steps for products in the App form.

<span id="e1f12491"></span>
## Precautions


* The iOS SDK is available in two versions: one for mainland China (excluding the Hong Kong, Macau, and Taiwan regions) and one for overseas. Both versions have identical features, but use different reporting addresses.

   * Applications released in China use the CN sub\-library and report to servers in mainland China.

   * Applications released overseas that use the Global sub\-library and have an SDK version greater than or equal to 5.1.0 will report to the server in Johor, Malaysia.

* Calling the SDK initialization interface does not collect user information. Calling the SDK start interface will initiate collection of user information. Please ensure that user authorization has been obtained before collecting user information. For details, refer to [SDK Privacy Policy](https://docs.byteplus.com/en/docs/apmplus/The_SDK_privacy_policy).


<span id="f391c95d"></span>
## Demo descriptions

[APMPlus_iOS](https://github.com/volcengine/APMInsight_iOS)


* The demo has already integrated all capabilities of the SDK.

* You can generate some crash and performance data using Demo.

* You can modify the AppID and AppToken in the Demo, and report performance data to the console to view it.

* The Demo provides sub\-libraries for each feature module. The correspondence between sub\-libraries and modules is shown in the following table:

   
   |**Sub\-library** |**DescriptionS** |**Corresponding platform module** |**Supported since versions** |
   |---|---|---|---|
   |Crash |Crash monitoring: Capture CPP Exception, Mach Exception, NSException, and Signal Exception |crash analytic |0.0.5 |
   |WatchDog |Monitors when the main thread hangs for a long time and is forcefully terminated by the operating system watchdog |crash analytic |0.0.5 |
   |OOM |Out of memory monitoring |Crash analytic and memory optimization – OOM trend |0.0.5 |
   |LAG |Lag monitoring: Monitoring cases where the main thread fails to respond within a short time |lag analytic |0.0.5 |
   |UserException |Custom error; requires the business team to manually add tracking points. |Error analysis \- custom error |0.0.5 |
   |Monitors |Startup analytic: Fluency: |User experience \- startup analytic user experience \- page experience \- memory optimization \- OOM trend \- extended metrics |0.0.7 |
   |UITrackers |Page analysis: |User experience\-page experience\-page responsiveness |0.0.7 |
   |Hybrid |WKWebView HTML5 page monitoring |Page monitoring |0.0.8 |
   |MemoryGraph |Memory analysis: obtain the memory status of the app at a specific moment |memory optimization |0.0.8 |
   |Network |Network analysis: network errors, HTTP analysis, and DNS analysis |Network analytic error analysis \- network error |1.0.0 |
   |NetworkPro |Network analysis: network errors, HTTP analysis, and DNS analysis |Network analytic error analysis – network error |2.5.2 |
   |EventMonitor |Event analytics, custom event recording, and manual instrumentation are required. |event analytic |2.0.0 |
   |SessionTracker |PV/UV tracking. Data will be automatically reported after integration. |Exception rate, Exception Impacted Users rate, and more for each module |2.3.0 |
   |APMLog |APM log library that allows you to manually insert log points to record app runtime logs. |Crash analytic for log recovery \- crash details \- custom log |2.4.0 |
   |CrashProtector |crash protection |Exception protection \- crash protection |2.5.2 |
   |CPUException |CPU exception monitoring |CPU monitoring\-CPU anomaly |2.7.3 |
   |MetricKit |MetricKit stability |MetricKit\-stability |2.12.1 |
   ||The performance of MetricKit |MetricKit performance |3.5.3 |
   |Disk |disk monitor |disk monitor |3.0.0 |
   |GWPASan |GWPASan |crash analytic |3.1.0 |
   |Coredump |Coredump |crash analytic |3.2.0 |
   |BootingProtect |Continuous crash protection |\- |2.10.0 |
   |BootingProtectLite |Lite version of continuous crash protection (does not rely on OOM) |\- |2.10.0 |
   |Zombie |Online Zombie analyses |crash analytic |2.8.0 (does not support allowlist)<br><br>2.10.0 (supports allowlist) |
   |CloudCommand |Recovery features |Single point tracing recovery |3.5.3 |
   |HybridPro |Monitoring H5 pages in the new version of WKWebView |New H5 monitor |3.10.0 |
   


<span id="5c7778e3"></span>
## Step 1: Obtain the SDK package


1. In the Podfile, add the following example code to obtain the SDK package.

   ```Ruby
   platform :ios, '10.0'
   source 'https://github.com/volcengine/volcengine-specs.git'
   
   pod 'RangersAPM', '5.2.7', :subspecs => [
       'Crash',
       'WatchDog',
       'OOM',
       'LAG',
       'UserException',
       'Monitors',
       'UITrackers',
       'HybridPro',
       'MemoryGraph',
       'NetworkPro',
       'EventMonitor',
       'SessionTracker',
       'APMLog',
       'CrashProtector',
       'CPUException',
       'MetricKit',
       'Disk',
       'GWPASan',
       'Coredump',
       'CloudCommand',
       # 'CN'
       # 'Global'
   ]
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Adding the above code will import all features of the SDK. If you do not want to import all features, import submodules as needed. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app#f391c95d">Demo description</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Starting from version 3.10.0, APMPlus supports the <a href="https://developer.apple.com/news/?id=3d8a9yyh">Privacy manifest</a> feature required by Apple at WWDC 23.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">CN and Global are used to specify the domain name for data reporting. By default, you must use one and only one of them. If you have special requirements, refer to the <a href="https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features">reporting domain name configuration</a>.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Report to domestic servers   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Global: Report to overseas server   </div>
   

2. Run the following commands to install the SDK.

   ```PowerShell
   pod install
   ```
   


<span id="878f6178"></span>
## Step 2: Initialize SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">No personal user information is obtained during SDK initialization.</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to initialize the SDK in the <code>AppDelegate.m</code> file's <code>application didFinishLaunchingWithOptions:</code> method, or at an appropriate time after the user has agreed to the privacy policy.</div>



Add the following example code, and initialize the SDK.

```objectivec
#import <RangersAPM.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
    apmConfig.channel = @"App Store";
    /**
     During the first startup, since the configuration has not been obtained, it's impossible to determine which functional modules need to be enabled. You can configure this property to decide which functional modules should be enabled by default during the first startup. This setting only takes effect for the first startup. Once the configuration is fetched, the local cached configuration will be read first to make the decision for subsequent startups.
 
It is recommended to enable Crash Analysis (RangersAPMCrashMonitorSwitch), Launch Analysis (RangersAPMLaunchMonitorSwitch), and Network Analysis (RangersAPMNetworkMonitorSwitch) by default to avoid the loss of some data strongly related to the first startup.
After configuring the default - enabled modules, these modules will be opened by default when a new device starts up for the first time. There may be a situation where these modules are turned off on the platform, but data is still being reported, which may cause unexpected consumption of your event volume. Please configure it flexibly according to your application's situation.
To configure multiple modules, you can refer to this syntax: RangersAPMCrashMonitorSwitch | RangersAPMNetworkMonitorSwitch | RangersAPMLaunchMonitorSwitch
     */
    apmConfig.defaultMonitors = RangersAPMCrashMonitorSwitch;

    return YES;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>{{app_id}}</code> and <code>{{app_token}}</code> must be replaced with the AppID and AppToken corresponding to the application you have created. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken">How to query AppID and AppToken?</a>.</div>


<span id="d1e16317"></span>
## Step 3: Start the SDK and turn on data collection

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">It is recommended to call the startup code as early as possible; otherwise, crashes that occur during the startup phase (before the SDK startup code is called) may not be captured, or startup analytic data may be inaccurate.</div>


* <div data-tips="true" data-tips-type="warning">It is recommended to start the SDK in the <code>AppDelegate.m</code> file's <code>application didFinishLaunchingWithOptions:</code> method, or at an appropriate time after the user has agreed to the privacy policy.</div>



Add the following sample code, start the SDK, and turn on data collection.

```objectivec
#import <RangersAPM.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Start the SDK with the configuration obtained during the initialization phase.
    [RangersAPM startWithConfig:apmConfig];
    [RangersAPM setUserID:@"xxxx"];
    [RangersAPM setDeviceID:@"xxxx"]; 
    
    return YES;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to use a custom deviceID, you need to modify the relevant parameters in apmConfig. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features#4beda33f">Obtain device and user counts</a>.</div>


<span id="403a16c4"></span>
## Step 4: Upload a symbol table

The symbol table can parse the contents of a crash stack trace, converting the stack trace information in the log from a raw stack trace into a symbolicated, parsed stack trace. The symbol table supports manual upload and automatic upload.

<span id="163d3b5c"></span>
### Manual upload


1. Verify that the symbol table meets the following format.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/1f8fb8d3a37842ad9302dd9683df776d) </span>

2. Compress the symbol table into a zip file.

   When using zip on Mac, you need to run the following command to remove the `DS_Store__MACOSX` files generated by default.

   ```PowerShell
   zip -r test.app.dSYM.zip test.app.dSYM -x "*.DS_Store" -x "__MACOSX"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>test.app.dSYM.zip</code> and <code>test.app.dSYM</code> with your symbol table name.   </div>
   

3. Upload symbol table.

   * Upload the symbol table on the **symbol table management** page. For details, refer to [iOS symbol table management](https://docs.byteplus.com/en/docs/apmplus/File_management#47c37795).

   * Use the curl command to upload.

      ```PowerShell
      APMPlus_Upload_DSYM_Domain=""
      APMPlus_APPID=""
      APMPlus_Upload_DSYM_API_Key=""
      APMPlus_Upload_DSYM_API_Token=""
      APMPlus_DSYM_File_Path=""
      
      APMPlus_CURRENT_TIMESTAMP=$(date "+%s")000
      APMPlus_Signature=$(md5 -s "${APMPlus_CURRENT_TIMESTAMP}${APMPlus_Upload_DSYM_API_Token}" | cut -d ' ' -f1)
      curl ${APMPlus_Upload_DSYM_Domain}/apmplus_api/eue/guest/app/mapping/upload -F "file=@${APMPlus_DSYM_File_Path}" -F "type=Dwarf" -F "os=iOS" -F "aid=${APMPlus_APPID}" -F "script-version=3.0" -H "Content-Type: multipart/form-data" -H "X-OpenApi-Timestamp: ${APMPlus_CURRENT_TIMESTAMP}" -H "X-OpenApi-AppID: ${APMPlus_Upload_DSYM_API_Key}" -H "X-OpenApi-Token: ${APMPlus_Signature}" -H "x-app-ids: ${APMPlus_APPID}" -w %{http_code}
      ```
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Set the value of the <code>APMPlus_Upload_DSYM_Domain</code> variable to the domain name to which you want to report.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Domestic domain name: https://open.apmplus.cn\-beijing.volces.com. When accessing the CN subspec, please use this domain name.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Foreign domain name: <a href="https://open.apmplus.ap-southeast-1.volces.com/">https://open.apmplus.ap\-southeast\-1.volces.com</a>. When accessing Global subspec, please use this domain name.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Set the value of the <code>APMPlus_APPID</code> variable to your AppID.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Set the value of the variable <code>APMPlus_Upload_DSYM_API_Key</code> to the API Key. Go to Platform \> All features \> Symbol table management. Under Operating system, select iOS. The API Key will be displayed below.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Set the value of <code>APMPlus_Upload_DSYM_API_Token</code> to the API Token. From All Features in the platform, go to Symbol Table Management. In Operating System, select iOS. The API Token will be displayed below.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Set the value of the variable <code>APMPlus_DSYM_File_Path</code> to the path of the symbol table file to be uploaded.      </div>
      

      After execution is complete, if the following is returned, it indicates that the upload was successful.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/9ae88d9aa8fb4350a4d6351fa6088050) </span>


<span id="da36781e"></span>
### Automatic upload

By configuring Build Phases under the corresponding Target in Xcode and adding a Run Script, you can automatically upload the symbol table when packaging the app.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, the symbol table is not uploaded in Debug mode and when compiling for the simulator. If you need to upload a symbol table in these two situations, please refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app#163d3b5c">Manual upload</a>.</div>



1. Select **Build Settings \> Debug Information Format**, and check that the project configuration is set to generate a symbol table.

2. Select **Build Phases \> New Run Script Phase**, add Run Script.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/45d54ff0f38140cfaa8c9f3ca61dc2aa) </span>

3. Place the added Run Script at the end to prevent the script from running before the symbol table has been generated.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/54f5abee016f4ad5a4ab4f7b5891cea2.png) </span>

4. Add the following commands to the script. The symbol table will not be uploaded when compiling in Debug mode and on the simulator.

   ```PowerShell
   /bin/sh ${PODS_ROOT}/RangersAPM/RangersAPM/Core/APMPlus_DSYMUploader_v3.sh "APMPlus_APPID" "APMPlus_Upload_DSYM_API_Key" "APMPlus_Upload_DSYM_API_Token" "APMPlus_Upload_DSYM_Domain"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>APMPlus_APPID</code> must be replaced with the AppID corresponding to the application you created. For details, please refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken">How to query AppID and AppToken?</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Set the value of <code>APMPlus_Upload_DSYM_API_Key</code> in the command to API Key. Go to All features \> symbol table management \> select operating system iOS. The API Key will be displayed below.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Set the value of <code>APMPlus_Upload_DSYM_API_Token</code> in the command to the API Token. From the platform, go to All features \> Symbol table management \> select the operating system iOS. The API Token will be displayed below.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Set the value of <code>APMPlus_Upload_DSYM_Domain</code> in the command to the domain name you want to upload to.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Domestic domain name: https://open.apmplus.cn\-beijing.volces.com. When accessing the CN subspec, please use this domain name.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Foreign domain name: <a href="https://open.apmplus.ap-southeast-1.volces.com/">https://open.apmplus.ap\-southeast\-1.volces.com</a>. When integrating Global subspec, please use this domain name.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The SDK version for integration must be greater than or equal to 5.1.6. If you are integrating an earlier version of the SDK, please use the solution in Step 5.   </div>
   

5. (Optional) Modify script content.

   If you are using a lower version of the SDK and do not wish to upgrade to a higher version, or if automatic symbol table upload requires Debug mode and emulator compilation, please perform the following actions:

   1. Download the script file.

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb1d051c792b4be9b7cbc03072bcfe1b~tplv-goo7wpa0wc-image.image" name="APMPlus_DSYMUploader_v3.sh">APMPlus_DSYMUploader_v3.sh</Attachment>
      

   2. Copy the contents of the downloaded script file into Run Script.

   3. Replace the variable `APMPlus_APPID` with your AppID.

   4. Setting the variable `APMPlus_Upload_DSYM_API_Key` to the API Key.

   5. Set the variable `APMPlus_Upload_DSYM_API_Token` to API Token.

   6. Change `APMPlus_UPLOAD_DOMAIN` to the domain name to which you want to upload data.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Domestic domain name: https://open.apmplus.cn\-beijing.volces.com. When integrating CN subspec, please use this domain name.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Foreign domain name: <a href="https://open.apmplus.ap-southeast-1.volces.com/">https://open.apmplus.ap\-southeast\-1.volces.com</a>. When integrating with Global subspec, please use this domain name.      </div>
      

      ```C
      #!/bin/sh
      ################################################################################
      # Custom Configuration
      ###############################################################################
      # Whether to upload during Debug mode compilation. 1 = Upload, 0 = Do not upload. Default is not to upload.
      UPLOAD_DEBUG_SYMBOLS=0
      
      # Whether to upload during simulator compilation. 1 = Upload, 0 = Do not upload. Default is not to upload.
      UPLOAD_SIMULATOR_SYMBOLS=0
      
      # APMPlusID：The ID of the application on the APMPlus platform.
      APMPlus_APP_ID="XXX"
      
      # APMPlusUploadDSYMAPIKey：You can find the API Key under All Features -> Symbol Table Management -> Select iOS in the platform.
      APMPlus_Upload_DSYM_API_Key="XXX"
      
      # APMPlusUploadDSYMAPIToken：You can find the API Token under All Features -> Symbol Table Management -> Select iOS in the platform.
      APMPlus_Upload_DSYM_API_Token="XXX"
      
      # APMPlusUploadDomain：The domain name for application reporting. 
      APMPlus_UPLOAD_DOMAIN="XXX"
      ```
      

   7. Modify the `UPLOAD_DEBUG_SYMBOLS` and `UPLOAD_SIMULATOR_SYMBOLS` fields in the script as needed.

      
      |Parameters |DescriptionS |
      |---|---|
      |UPLOAD_DEBUG_SYMBOLS |Whether to upload during Debug mode compilation<br><br><br>* Step 1: Upload<br><br>* 0 (default): Do not upload |
      |UPLOAD_SIMULATOR_SYMBOLS |Upload emulator compilation?<br><br><br>* 1: Upload<br><br>* 0 (default): Do not upload |
      


<span id="c68e410d"></span>
## References


* After integrating the iOS SDK into your application, if you need to verify data reporting for each module, refer to [Verify data reporting](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data).

* After integrating the iOS SDK into your application, if you need to use the SDK's advanced features, refer to [Use advanced features](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features).
