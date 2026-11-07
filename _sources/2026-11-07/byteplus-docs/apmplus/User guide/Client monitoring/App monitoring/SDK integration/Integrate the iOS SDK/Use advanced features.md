---
title: "Use advanced features"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features"
---

In addition to common features such as crash analytic, error analytic, and lag analytic, the SDK also supports some enhanced features. You can use these features after importing the relevant sub\-libraries based on your business requirements.

<span id="79df71df"></span>
## Notification

When certain events occur, the SDK sends notifications. You can listen for these notifications to implement custom responses.

Taking the lag scenario as an example, you can register notifications using the following method. If the LAG sub\-library is introduced, when a lag scenario occurs, the SDK will send a notification, thereby triggering lagHandler.

```objectivec
#import <RangersAPMNotifications.h>
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(lagHandler) name:APMLagTimeOutNotification object:nil];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In addition to lag notification, the SDK also supports other notifications such as memory threshold notification. For details, view the header file <code>RangersAPMNotifications.h</code>.</div>


* <div data-tips="true" data-tips-type="tip">SDK version must be greater than 1.5.4.</div>



<span id="22d29442"></span>
## Calibrate startup analytic time

<span id="1fb4462c"></span>
### The start phase of default monitoring

Startup analytic default monitoring of four start phases:


1. from_exec_to_load

2. from_load_to_didFinishLaunching

3. from_didFinishLaunching_to_first_render_time

4. from_vc_loadView_to_didAppear


Time node descriptions for each stage


|**Milestone** |**DescriptionS** |
|---|---|
|exec |The app process start time |
|load |RangersAPM's +load call time |
|didFinishLaunching |The initialization time of RangersAPM |
|first_render_time |The time of the first CoreAnimation submit |
|vc_loadView |Time when the first ViewController's loadView is called |
|didAppear |The time when the viewDidAppear method of the first ViewController occurs |


<span id="34af3571"></span>
### Custom tracking points

If you need to additionally record certain nodes during the start process, please refer to the following two tracking solutions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following two tracking methods can only be used during the app startup phase; calling them after app startup is complete is invalid.</div>



* Add tracking points at the start and end of the node, respectively.

   ```objectivec
   #import <RangersAPM+PerformanceAPI.h>
   
     RangersAPMConfig *config = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
     [RangersAPM startWithConfig:config];
   
     [RangersAPM beginLaunchSpan:@"business" callback:^(NSError * _Nullable error) {
         if (error.code == RangersAPMStartDetectorErrorTypeDuplicateSpanName) {
             //do something
         }
     }];
   
     //business
   
     [RangersAPM endLaunchSpan:@"business" callback:^(NSError * _Nullable error) {
         if (error.code == RangersAPMStartDetectorErrorTypeDuplicateSpanName) {
             //do something
         }
     }];
   ```
   

* Record the start time and end time of the node, and log an event when the node ends.

   ```objectivec
   #import <RangersAPM+PerformanceAPI.h>
   
       RangersAPMConfig *config = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
       [RangersAPM startWithConfig:config];
   
       NSTimeInterval startTime = [[NSDate date] timeIntervalSince1970] * 1000;
       //business
       NSTimeInterval endTime = [[NSDate date] timeIntervalSince1970] * 1000;
   
       [RangersAPM addSpan:@"business" startTimeMs:startTime endTimeMs:endTime callback:^(NSError * _Nullable error) {
           if (error.code == RangersAPMStartDetectorErrorTypeDuplicateSpanName) {
               //do something
           }
       }];
   ```
   


<span id="e833f418"></span>
### Custom endpoint

If you want to customize the endpoint of the start trace, you need to set the `customFinishStartTrace` parameter of RangersAPMConfig to `YES`. After the SDK has been initialized, that is, after `[RangersAPM startWithConfig:]`, call the `[RangersAPM finishLaunchTrace]` method at an appropriate time to end the start trace.

Example code:

```objectivec
#import <RangersAPM.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
    RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
    apmConfig.customFinishStartTrace = YES;
    apmConfig.channel = @"App Store";
    
    [RangersAPM startWithConfig:apmConfig];
    
    [RangersAPM finishLaunchTrace];
      
    return YES;
}
```


<span id="26d239d6"></span>
### iOS Prewarm

On iOS 15 and later operating systems, the Prewarm policy causes part of the application's startup process to occur in advance, resulting in the platform recording an overestimated startup time.

In this case, the platform adopts the following approach: if Prewarm is triggered, the platform calibrates the measured startup time by ignoring a portion of the startup time. As a result, the reported startup time will be slightly less than the actual time, and the reported startup Trace may lack execToLoad or loadToDidFinishLaunching time.

If you want to obtain a more accurate startup time, upgrade the SDK to version 2.11.1 or later and perform the following actions: Call `[RangersAPM prewarmCheckStart]` in the main method. Also, call `[RangersAPM prewarmCheckEnd]` in the `application:willFinishLaunchingWithOptions:` method. If your main method or the `application:willFinishLaunchingWithOptions:` method contains complex logic, these Actions are not recommended.

<span id="7b546c70"></span>
### Deferred initialization

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This method is used to obtain the timestamps of key points during the application start phase and does not involve personal information. If you need to call this method before the user confirms the privacy popup, please ensure, in accordance with your application's compliance requirements, whether the SDK is permitted to execute code logic before initialization.</div>


We recommend starting the SDK at the very beginning of `application:didFinishLaunchingWithOptions:` to obtain a more accurate startup time. If, due to special reasons, you cannot start too early, please first call `[RangersAPM applicationDidFinishLaunching]` in `application:didFinishLaunchingWithOptions:`.

<span id="d6c25c00"></span>
## Custom data

By using the following interface, you can add custom environment or business information, such as user email, location information, business scenario, and more. These details will be reported together with the SDK's log to help you troubleshoot issues.

```objectivec
[RangersAPM setCustomContextValue:@"customKeyDemoTest" forKey:@"customValueDemoTest"];
```


After a successful add, you can view these custom data on the console **log details** page.

<span id="e50c2e3c"></span>
## custom dimension

By using the following interface, you can add custom dimensions as custom filter options to filter logs under specific circumstances.

```objectivec
[RangersAPM setCustomFilterValue:@"filterValueDemooTest" forKey:@"filterKeyDemoTest"];
```


After a successful add, you can view these custom dimensions under **custom dimension** in the filter list.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In modules where only statistical data is available and log details are not provided, it is not possible to view these custom data and custom dimensions, such as fluency, HTTP, and so on.</div>


<span id="67a52cdd"></span>
## PV custom dimension

By using the following interface, you can add some custom dimensions to PV, which can serve as custom filter options for filtering PV data. Currently, PV data does not have a dedicated consumption scenario on the platform and is often used in combination with crash and lag data to calculate crash ratio and other metrics.

```objectivec
RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
apmConfig.PVFilters = @{@"key1": @"value1"};
[RangersAPM startWithConfig:apmConfig];
```


After a successful addition, you can view these data under the PV custom dimension in the filter list.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Since PV is reported immediately after a cold start or a warm start, the configuration of PVFilters will only take effect for the current PV data if it is performed during SDK initialization in a cold start, or before the application enters the Foreground in a warm start. At the same time, we also recommend using only data that does not change frequently as PV custom dimensions, because PV data represents a lifecycle. Using data that may change during the lifecycle as a PV dimension can result in ambiguous data meaning.</div>


2. <div data-tips="true" data-tips-type="warning">"Custom dimension" and "PV custom dimension" data are not interoperable. If you need to add the same dimension to both, please configure them separately on the client.</div>



<span id="cbb494be"></span>
## page tracking

No additional embedding code is required. By introducing the UITrackers sub\-library, you can view **page tracking** under the **on\-site data** tab on the **crash details** page, and see the user's page visit path before the crash occurred. Lag details also support page tracking.

<span id="f70b1408"></span>
## Continuous crash protection

Continuous crash protection can perform certain local actions when the application experiences consecutive crashes, for example, clearing cache, deleting files, and so on. Continuous crash protection requires integrating the BootingProtect module from the SDK.

```objectivec
#import <RangersAPM+BootingProtect.h>

    [RangersAPM startProtectWithBootingThreshold:10 bootingCrashHandler:^(RangersAPMBootingInfo * _Nonnull info) {
        /**
         Implement protection strategies for scenarios with consecutive exceptions. The demo here only outputs some logs. You can perform operations such as local cache cleaning or other strategies in your own application. Different strategies can be formulated according to different numbers of exception occurrences.
         */
        if (info.consecutiveExceptionTimes >= 1) {
            NSLog(@"⚠️Consecutive exception 1 time");
        } else if (info.consecutiveExceptionTimes >= 3) {
            NSAssert(NO, @"⚠️Consecutive exception 3 times !!!");
        }
        
        /**
         In addition to protecting against consecutive exceptions, you can also execute different protection strategies for different types of exceptions.
         */
        if (info.crashTimes >= 1) {
            NSLog(@"⚠️Consecutive crash 1 time");
        }
        if (info.watchdogTimes >= 1) {
            NSLog(@"⚠️Consecutive watchdog 1 time");
        }
        if (info.OOMTimes >= 1) {
            NSLog(@"⚠️Consecutive oom 1 time");
        }
    }];
```


<span id="6a6ed505"></span>
## End\-to\-end monitoring

After the business system integrates with APMPlus server\-side monitoring, configure the client as follows to turn on full trace monitoring. For more information, refer to [end-to-end trace monitoring](https://docs.byteplus.com/en/docs/apmplus/Full_trace_monitoring).

```objectivec
// You need to import the following header file.
#import <RangersAPMConfig+NetworkPro.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
    RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
    apmConfig.channel = @"App Store";
    
    // Configure enableTracing to YES to enable the full - link monitoring function.
    apmConfig.enableTracing = YES;

    [RangersAPM startWithConfig:apmConfig];
    
    return YES;
}
```


<span id="4beda33f"></span>
## Obtain device count and user count

By default, the Application Performance Management Plus SDK internally uses the DeviceID generated by its own service to identify a device and user.

If you do not want to use the DeviceID generated by the SDK's own service, you can refer to the alternative solutions described below. If you select another solution, the SDK will not internally request its own service to generate the DeviceID again.

<span id="10ba2e4a"></span>
### DeviceID generated by RangersAppLog

If you want to or have already integrated RangersAppLog, please follow the steps below to obtain the device count.


1. Declare the RangersAppLog dependency in the Podfile, and ensure that the RangersAppLog version is greater than 6.0.1.

   ```Ruby
   pod 'RangersAppLog', '>=6.0.1', :subspecs => [
     'Core',
     'Host/CN'
   ]
   ```
   

2. Initialize the RangersAppLog SDK.

   ```objectivec
   #import <BDAutoTrack.h>
   
   - (BOOL)application:(UIApplication *)application 
   didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   
      BDAutoTrackConfig *config = [BDAutoTrackConfig configWithAppID:@"{{app_id}}" launchOptions:launchOptions];
      config.channel = @"App Store";
      [BDAutoTrack startTrackWithConfig:config];
   
      // Initialize the APMPlus SDK.
   
      return YES;
   }
   ```
   

3. Configure the deviceIDSource in the SDK initialization config. Application Performance Management Plus will automatically obtain the deviceID from RangersAppLog.

   ```objectivec
   #import <RangersAPM.h>
      
      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
      
      // Initialize RangersAppLog.
      
      RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
      
      apmConfig.channel = @"App Store";
      
      apmConfig.deviceIDSource = RAPMDeviceIDSourceFromRAppLog;
      
      [RangersAPM startWithConfig:apmConfig];
      
      return YES;
      
      }
   ```
   


<span id="075f257a"></span>
### Use your own DeviceID

If you want to use your own deviceID, please strictly follow the steps below to obtain the number of devices.


1. Configure the deviceIDSource in the Application Performance Management Plus SDK initialization config.

2. After calling the initialization method of the Application Performance Management Plus SDK, set the deviceID.

   ```objectivec
   #import <RangersAPM.h>
   
       - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   
           RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
           apmConfig.channel = @"App Store";
           apmConfig.deviceIDSource = RAPMDeviceIDSourceFromUser;
           [RangersAPM startWithConfig:apmConfig];
   
           [RangersAPM setDeviceID:@"MYDEVICEID"];
   
           return YES;
       }
   ```
   


<span id="f48f38e5"></span>
## Register post\-crash callback

Register a post\-crash callback, which can be invoked when an exception occurs to record key information at the time of the exception.

```objectivec
// RangersAPM+CrashCallback.h

/**
After RangersAPM internally handles a crash, it will call back the business side. The custom data will be displayed in the custom data section of the APMInsight platform.
 
⚠️⚠️⚠️ Warning ⚠️⚠️⚠️
⚠️⚠️⚠️ After a crash, the App's running environment is quite fragile, which may easily lead to secondary crashes or deadlocks. Unless it is absolutely necessary, it is not recommended to use this method. ⚠️⚠️⚠️
 
When the business side receives the callback, it indicates that the App has crashed and is running in an abnormal environment. Therefore, there are usage restrictions and the following agreements should be followed:
 
The callback method should be as simple as possible, only used to record key information and end as soon as possible (during the crash, the user - side interface appears to be frozen).
At this time, all threads except the current one are suspended, so do not start other threads.
Do not call OC methods, as it may easily cause deadlocks.
Try not to allocate memory on the heap using malloc.
*/

@interface RangersAPM (CrashCallback)

+ (void)registerCallback:(apm_crash_callback)callback;

+ (void)removeCallback:(apm_crash_callback)callback;
```


<span id="37eb91fa"></span>
## Actively report custom logs

Recovery of custom logs is limited by user behavior. When user feedback is received or when a user experiences an exception, developers may not be able to obtain logs in a timely manner for troubleshooting.


* User crash logs

   * **Configuration method**: By configuring **crash analytic \> whether to upload custom logs**, you can enable the SDK to report custom logs along with crash logs. For details, see [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

   * **View log**: On the **crash details** page, select the **custom log** tab to view.

* In other scenarios, for example when a user provides feedback within the app or when a business error occurs, if you want to report custom logs to assist with troubleshooting, you can use the methods provided by the SDK to report custom logs within a specified time.

   * **Configuration methods**:

      ```objectivec
      /**
      Manually report custom logs generated by the user's active logging.
      @param fetchStartTime The start time of the custom logs to be reported.
      @param fetchEndTime The end time of the custom logs to be reported.
      @param callback The callback for the upload status. isSuccess == YES indicates a successful upload, and fileCount indicates the number of files reported this time.
      */
      + (void)reportALogWithFetchStartTime:(NSTimeInterval)fetchStartTime
                              fetchEndTime:(NSTimeInterval)fetchEndTime
                                  callback:(void(^)(BOOL isSuccess, NSInteger fileCount))callback;
      ```
      

   * **View log**: For this portion of actively reported data, you can go to the **custom log** page, enter the DID to query, and select the event type **Active Report**.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The volume of actively reported custom logs is uncontrollable, and event consumption is high. It is recommended to modify <strong>custom file \> sampling rate for actively reporting custom logs</strong>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#f5bc7ef3">SDK reporting configuration</a>.      </div>
      

<span id="eef6ad07"></span>
## APMPlus logs

Considering cost and performance, the reporting policy for some features in APMPlus uses sampling. As a result, when it is necessary to troubleshoot an issue for a specific user, the absence of complete feature logs can make the investigation more difficult. To address this issue, the SDK supports writing certain feature logs as custom logs, but does not report individual feature logs. This approach facilitates recovery or proactive reporting when troubleshooting is required.

<span id="310a27d7"></span>
### Prerequisites


* Upgrade the SDK to version 3.10.4 or later.

* Custom log configuration has been completed. For details, refer to [log recovery](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#5e60c23f).

* The **APMPlus log sampling rate** has been configured. For details, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#f5bc7ef3).

* Create an **APMPlus log recovery** task. For details, refer to [Create a log recovery task](https://docs.byteplus.com/en/docs/apmplus/Recovery#.5paw5bu65Lu75Yqh).


<span id="67eb2471"></span>
### Active reporting


* Logs before the user's crash

   * **Configuration method**: By configuring the **crash analytic \> APMPlus log crash reporting sampling rate**, the SDK will report APMPlus logs together with crash logs. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

   * **View log**: On the **crash details** page, select the **custom log** tab to view.

* In other scenarios, such as when a user provides feedback within the app or when a business error occurs, you may want to report APMPlus logs to assist with troubleshooting. You can use the method provided by the SDK to report APMPlus logs within a specified time period.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to report both user custom logs and APMPlus logs at the same time, you can pass the logType parameter as follows:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>[RangersAPM reportALogOfType:(RangersAPMALogTypeCustom | RangersAPMALogTypeMonitor) ...]</code>   </div>
   

   * **Configuration methods**:

      ```objectivec
      typedef NS_OPTIONS(NSUInteger, RangersAPMALogType) {
          RangersAPMALogTypeCustom = 1<<0,  // User - initiated logging.
          RangersAPMALogTypeMonitor = 1<<1  // Built - in logging of the SDK.
      };
      
      /**
      Manually report multiple types of custom logs.
      @param logType The types of logs to be reported. For example, to report multiple types simultaneously: RangersAPMALogTypeCustom | RangersAPMALogTypeMonitor.
      @param fetchStartTime The start time of the custom logs to be reported.
      @param fetchEndTime The end time of the custom logs to be reported.
      @param detailCallback The callback for the upload status. If multiple types are reported simultaneously, the callback may be executed multiple times. logType identifies the type reported in this callback. isSuccess == YES indicates a successful upload in this callback, and fileCount indicates the number of files reported in this callback.
      */
      + (void)reportALogOfType:(RangersAPMALogType)logType
                fetchStartTime:(NSTimeInterval)fetchStartTime
                  fetchEndTime:(NSTimeInterval)fetchEndTime
                detailCallback:(void(^)(RangersAPMALogType logType, BOOL isSuccess, NSInteger fileCount))detailCallback;
      ```
      

   * **View log**: You can view this actively reported data on the **custom log** page by entering the DID for the query and selecting the event type **Active reporting**.


<span id="73699796"></span>
## Page experience exception data governance

Prior to version 5.1.2, page experience supports the following stages:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca3e7af6c3024f9fa37df3cea4b916f0~tplv-goo7wpa0wc-image.image) </span>


* loadView: Time spent on loadView

* viewDidLoad: viewDidLoad time cost

* viewWillAppear execution time

* viewDidAppear: viewDidAppear execution time

* methodsTotalTime: end time of viewDidAppear minus start time of loadView


When the creation and presentation of controllers are decentralized, it can cause data exceptions, especially with the methodsTotalTime data, which may become exceptionally large and affect the overall metric.

To address this compatibility issue, we have implemented the following logic in version 5.1.2:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb24ddec577d42349cbf1bcabd4cac69~tplv-goo7wpa0wc-image.image) </span>


* loadView to viewDidLoad: the start time of viewDidLoad minus the end time of loadView

* viewDidLoad_to_viewWillAppear: viewWillAppear's start time minus viewDidLoad's end time

* viewWillAppear_to_viewDidAppear: start time of viewDidAppear minus end time of viewWillAppear


In addition, to prevent controllers from being created and displayed at scattered times, a threshold is set for the aforementioned time. This threshold applies separately to each of the three time values mentioned above. If any time value exceeds the threshold, that specific time value will be discarded. Additionally, adjust the calculation formula for methodsTotalTime to be the sum of the values of the above fields.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default value of the threshold is 20 seconds. If you want to modify it, refer to the <a href="https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#f5bc7ef3">SDK setting</a>.</div>


<span id="CugN3gJd"></span>
## Report domain name configuration

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This configuration applies to RangersAPM \>= 5.1.6</div>


When the data generated by the Product SDK within the application only needs to be reported to a single Elastic Compute Service, integrate according to the process described in [Application integration with iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app). If you need to configure data reporting to a private cloud server, or if you need to integrate multiple public cloud reporting domain names and control the actual reporting server through initialization parameters, you can refer to the following content.

<span id="FKTcTSyq"></span>
### Subspec introduction


|Subspec name |The server address |Applicable scenarios |
|---|---|---|
|CN |Beijing |Applications released in mainland China (excluding Hong Kong, Macau, and Taiwan) |
|Global |Johor |Applications released overseas |


<span id="b5yBVKiW"></span>
### Overview of initialization parameters

This initialization parameter is used to implement certain special reporting configurations. It is recommended to first read the following description to understand the meaning of each parameter, and then configure them according to your own application scenario.

```C++
/**
 The domain type SDK should choose.
 */
typedef enum {
    /**
     Only one of the domian subspecs should be involved.
     */
    RangersAPMDomainTypeSingle,
    /**
     No need for any domain subspec.
     ⚠️ You must set config.domain as your own host which is necessary to avoid exceptions.
     */
    RangersAPMDomainTypePrivate,
    /**
     Muiltiple domain subspecs can be involved, and use CN.
     ⚠️ The config.domain you set will be ignored.
     */
    RangersAPMDomainTypeCN,
    /**
     Muiltiple domain subspecs can be involved, and use Global.
     ⚠️ The config.domain you set will be ignored.
     */
    RangersAPMDomainTypeGlobal
    
} RangersAPMDomainType;
```



* RangersAPMDomainTypeSingle: Default value. You must introduce one and only one subspec that contains the reporting domain name, and data will be reported using the domain name specified in that subspec. For example, to report data to a public Elastic Compute Service in China, you need to integrate the CN subspec.

* RangersAPMDomainTypePrivate: Reported to private cloud Elastic Compute Service. Any reporting domain names introduced by subspecs will not be used; only the Elastic Compute Service address specified in the initialization configuration will be used. If the Elastic Compute Service address in the initialization configuration is empty, data reporting will fail. RangersAPMDomainTypeSingle can also be configured with a private Elastic Compute Service address during initialization. However, if the private Elastic Compute Service address specified in the initialization configuration is empty, the reporting domain name from the imported subspec will be used.

* RangersAPMDomainTypeCN: Reported to the public Elastic Compute Service in China. You can import multiple subspecs that contain reporting domain names, but only the reporting domain names in the CN subspec will be used. If the CN subspec is not imported, data reporting will fail.

* RangersAPMDomainTypeGlobal: Reported to public cloud Elastic Compute Service \- Global. You can introduce multiple subspecs containing reporting domain names, but only the reporting domain names in Global will be used. If Global is not introduced, data reporting will fail.


<span id="PFfRF0CJ"></span>
### Report to Cloud Service

This section describes how to report data to the private Cloud Service. There are two solutions.


* Plan 1: RangersAPMDomainTypeSingle

   1. Integrate a subspec that includes a reporting domain name. If the domain in the initialization configuration is empty, the domain from the subspec will be used as a fallback.

   2. Perform configuration of RangersAPMConfig.domainType and RangersAPMConfig.domain during initialization.

   ```Objective-C
   #import <RangersAPM.h>
   
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   
       RangersAPMConfig *config = [RangersAPMConfig configWithAppID:@"app_id" appToken:@"app_token"]; // You need to replace app_id and app_token here with your own application information
       config.domainType = RangersAPMDomainTypeSingle;  //This line can also be omitted, as the default is RangersAPMDomainTypeSingle
       config.domain = @"domain";  //Replace this with the private Elastic Compute Service address. If the domain specified in the configuration does not include a protocol, https:// is used by default.
       ...  // Here you can add other configuration as needed
       [RangersAPM startWithConfig:config];
   
       return YES;
   }
   ```
   

* Option 2: RangersAPMDomainTypePrivate

   1. It is not necessary to integrate any subspecs that contain reporting domains; even if such subspecs are integrated, they will not be used. If the domain in the initialization configuration is empty, reporting will fail.

   2. Configure RangersAPMConfig.domainType and RangersAPMConfig.domain during initialization.

   ```Objective-C
   #import <RangersAPM.h>
   
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   
       RangersAPMConfig *config = [RangersAPMConfig configWithAppID:@"app_id" appToken:@"app_token"]; // You need to replace the app_id and app_token here with your own application information
       config.domainType = RangersAPMDomainTypePrivate;
       config.domain = @"domain";  // Replace this with the private cloud server address. If the domain specified in the configuration does not include a protocol, https:// is used by default.
       ...  // You can add other configurations as needed
       [RangersAPM startWithConfig:config];
   
       return YES;
   }
   ```
   


<span id="ZcCRckOu"></span>
### Integrate reporting domain names for multiple public clouds

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If you order services in the North China region and Johor region, we recommend that you integrate the CN public cloud reporting domain name into application packages released domestically, and the Global public cloud reporting domain name into application packages released overseas. If you wish to integrate multiple regional public cloud reporting domain names within the same application package, you must independently assess and determine legal compliance risks to avoid losses resulting from the data reporting region not complying with local laws and regulations.</div>


This section describes how to integrate multiple public cloud reporting domains and configure the actual reporting address through initialization parameters. This applies to scenarios where the same application package is provided to both domestic and overseas users, and the data generated by this SDK is reported to different servers based on the download channel.


1. The subspec required for integration

2. Configure the RangersAPMConfig.domainType during initialization.


```Objective-C
#import <RangersAPM.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    RangersAPMConfig *config = [RangersAPMConfig configWithAppID:@"app_id" appToken:@"app_token"]; // You need to replace the app_id and app_token here with your own application information
    config.domainType = RangersAPMDomainTypeCN;  //Configure different domainType as needed
    ...  // You can add other configuration here as needed
    [RangersAPM startWithConfig:config];

    return YES;
}
```
