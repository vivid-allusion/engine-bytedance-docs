---
title: "Use custom logs"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_custom_logs"
---

This article describes the detailed steps for integrating your application with iOS, configuring custom data, and obtaining custom log data.

<span id="5c7778e3"></span>
## Step 1: Obtain the SDK package


1. In the Podfile, add the following sample code to obtain the SDK package.

   ```Ruby
   platform :ios, '10.0'
   source 'https://github.com/volcengine/volcengine-specs.git'
   
   pod 'RangersAPM', '5.1.3', :subspecs => [
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
       'CN'      # Only one of # and Global can be selected
       'Global'  # Only one of this and CN can be selected
   ]
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Adding the above code will import all SDK features. If you do not want to import all features, you can selectively import submodules as needed. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app#f391c95d">Demo description</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Starting from version 3.10.0, APMPlus supports the <a href="https://developer.apple.com/news/?id=3d8a9yyh">Privacy manifest</a> feature required by Apple at WWDC 23.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">CN and Global are used to specify the domain names for data reporting.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">CN: Report to the domestic server.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Global: Report to foreign servers   </div>
   

2. Run the following command to install the SDK.

   ```PowerShell
   pod install
   ```
   


<span id="878f6178"></span>
## Step 2: Initialize the SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">During SDK initialization, user personal information is not obtained.</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to perform SDK initialization actions in the <code>AppDelegate.m</code> <code>application didFinishLaunchingWithOptions:</code> method, or at an appropriate time after the user has agreed to the privacy policy.</div>



Add the following sample code, and initialize the SDK.

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


<div data-tips="true" data-tips-type="tip"><code>{{app_id}}</code> and <code>{{app_token}}</code> must be replaced with the AppID and AppToken corresponding to the application you create. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken">How to query AppID and AppToken?</a>.</div>


<span id="d1e16317"></span>
## Step 3: Start SDK and turn on data collection

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">It is recommended to invoke the start code as early as possible; otherwise, crashes that occur during the start phase (before the start SDK code is called) may not be captured, or startup analytic data may be inaccurate.</div>


* <div data-tips="true" data-tips-type="warning">It is recommended to complete the start of the SDK in the <code>AppDelegate.m</code> <code>application didFinishLaunchingWithOptions:</code> method, or at an appropriate time after the user has agreed to the privacy policy.</div>



Add the following example code, start the SDK, and turn on data collection.

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


<div data-tips="true" data-tips-type="tip">If you need to use a custom deviceID, you need to modify the relevant parameters of apmConfig. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features#4beda33f">Obtain device and user counts</a>.</div>


<span id="7114a5f2"></span>
## Step 4: Write a custom log

To implement custom log functionality, you need to import the APMLog sub\-library. By using the interfaces provided by the SDK to log events, you can record logs generated during the app runtime. Custom log types are divided into user\-defined logs and APMPlus logs.


* Custom log: Log data generated by users based on business events.

* APMPlus log: Exception, performance, network, event, and other log data collected by the built\-in instrumentation of the APMPlus SDK.



<Tabs>
<Tab zoneid="r4tlO7fi15" title="User-defined log">
<TabTitle>User-defined log</TabTitle>

A custom log is log data defined by users by marking business events.

Example code:

```C
//No matter which type of interface is used, you must first call the following interface to turn on the Alog feature. //Caution: Call this only once when the app starts. #import "RangersAPM+ALog.h"

[RangersAPM setALogEnabled];  //Enable Alog
[RangersAPM enableConsoleLog];  //Also outputs logs to the console //Objective-C can use the following interface for logging #import "RangersAPM+ALog.h" //The first parameter identifies the business, scenario, and other information for the current log; //The second parameter is the specific log information, which can use the format type. If format is used, you must also pass in the corresponding parameters
RANGERSAPM_ALOG_DEBUG(@"Business", @"version : %@", [self version]);  //Debug class log
RANGERSAPM_ALOG_INFO(@"Business", @"version : %@", [self version]);   // Info type log
RANGERSAPM_ALOG_WARN(@"Business", @"version : %@", [self version]);   //Warn log
RANGERSAPM_ALOG_ERROR(@"Business", @"version : %@", [self version]);   //Error type log //In C/C++, you can use the following interface for log tracking #import "RangersAPM_ALog.h" //The first parameter identifies the business or scenario information for the current log; //The second parameter is the specific log information, which can use the format type. If you use format, you need to provide the corresponding parameters.
 RANGERSAPM_ALOG_DEBUG_C("Business", "version : %s", version());
 RANGERSAPM_ALOG_INFO_C("Business", "version : %s", version());
 RANGERSAPM_ALOG_WARN_C("Business", "version : %s", version());
 RANGERSAPM_ALOG_ERROR_C("Business", "version : %s", version());
 
//Swift can use the following interface for logging events
#import "RangersAPM+ALog.h"
//The first parameter is the specific log information
//tag identifies the business, scenario, or other details for the current log
//fileName is the name of the current file; you can refer to the example and pass #file
//funcName is the name of the current method; you can refer to the example and pass #function
//line is the line number in the current file; you can refer to the example and pass #line
RangersAPM.debugALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
RangersAPM.infoALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
RangersAPM.warnALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
RangersAPM.errorALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
```



</Tab>
<Tab zoneid="ef7Lr0BDFh" title="APMPlus logs">
<TabTitle>APMPlus logs</TabTitle>

APMPlus logs are exception, performance, network, event, and other log data generated by built\-in instrumentation in the APMPlus SDK. After integrating the APMLog sub\-library, when the SDK records monitoring logs, it also writes a copy to Alog. If some data is missing for a user because sampling was not hit, you can use recovery Alog to troubleshoot the issue.


</Tab>
</Tabs>


<span id="0e4c17d7"></span>
## Step 5: Obtain custom log

You can report custom logs to the server side using the following different methods.

<span id="257d4807"></span>
### Report at crash


1. The switch for reporting crashes configured on the **SDK setting** page. For specific operations, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).



<Tabs>
<Tab zoneid="nwHh4wQVhX" title="User custom log">
<TabTitle>User custom log</TabTitle>

1. Change the parameter  **"Whether to report custom log"**  under the **crash analytic** module to Yes.

2. When **whether to upload custom log** is matched, upload user custom logs within N seconds of the crash time.


</Tab>
<Tab zoneid="mfxW9eyYjC" title="APMPlus logs">
<TabTitle>APMPlus logs</TabTitle>

1. Set the parameter **whether to report custom log** in the **crash analytic** module to Yes.

2. Change the **APMPlus crash log report sampling rate** to the sampling rate required by your business.

3. Modify the APMPlus log sampling rate parameter under the custom log module to the sampling rate required by the business.

4. When **whether to upload custom log** is triggered and **APMPlus log crash reporting sampling rate** is also triggered, sampling reporting is performed.


</Tab>
</Tabs>



2. View custom log

   * Method 1: On the corresponding issue **crash details** page, filter by log type to view the results.

   * Method 2: On the **custom log** page, filter by event type **reported with exception crash** to view.


<span id="649c541a"></span>
### Client active reporting


1. Configure the switch for active reporting on the **SDK setting** page. For specific operations, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

2. Call the method for proactive reporting in the business code.



<Tabs>
<Tab zoneid="QuMurtQD2R" title="User-defined log">
<TabTitle>User-defined log</TabTitle>

Call method one or method two, passing logtype asRangersAPMALogTypeCustom.


* Method 1

* Method 2


</Tab>
<Tab zoneid="Q1O9hOgWVF" title="APMPlus log">
<TabTitle>APMPlus log</TabTitle>

Call the method and pass logtype as`RangersAPMALogTypeCusto`


</Tab>
</Tabs>



3. On the **custom log** page, view and review custom logs after filtering by event type **active reporting**.


<span id="88188dae"></span>
### recovery


1. Create a recovery task.



<Tabs>
<Tab zoneid="JZm0PpJ1jj" title="User-defined log">
<TabTitle>User-defined log</TabTitle>

Before recovering a custom log, you first need to create a recovery task for it.


1. Click **App Monitoring** under the target application.

2. In the upper left corner of the console, select **All features \> Recovery**.

3. In the filter area, click **iOS**, then click **create task**.

4. On the **Create Task** page, complete the following configuration, and then click **Save**.


</Tab>
<Tab zoneid="jlcecC4evq" title="APMPlus logs">
<TabTitle>APMPlus logs</TabTitle>

Before log recovery, you need to first create a recovery task for APMPlus logs.


1. Click **App Monitoring** under the target application.

2. In the upper left corner of the console, select **All features \> Recovery**.

3. In the filter area, click the **iOS** operating system, then click **Create task**.

4. On the **Create task** page, complete the following configuration, and then click **Save**.


</Tab>
</Tabs>



2. On the **recovery** page, filter by time or operating system, or enter the task name and creator to search for recovery tasks, then view the recovery log.
