---
title: "Report verification data"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Report_verification_data"
---

Based on your business needs, you can refer to the following module description to check whether each corresponding module has been successfully integrated.

<span id="78ce0b1b"></span>
## Prerequisites

<span id="a9950564"></span>
### Complete SDK reporting configuration


* Configure device allowlist

   **SDK setting** page uses a low default sampling rate. During the SDK integration testing phase, please configure the DID allowlist to ensure that all performance data from the current device is sampled and reported, so you can view these data on the platform. For details, refer to [Obtain device count and user count](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features#4beda33f) and [Allowlist configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#22523dce).

* Configuration of module sampling rates

   Crash reports are always sent and are not subject to sampling rate control. Except for crash data, other monitoring data requires sampling reporting to be configured on the **SDK setting** page. By default, data is reported only when sampling is hit.

   For example, before verifying lag data, please enable the main switch on the **SDK setting** page and set the lag sampling rate configuration to 100%. Once verification is complete, then modify to an appropriate sampling rate. For details, refer to [module sampling configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#b29d0396).


<span id="13271ab1"></span>
### **Turn on debug log**

When you turn on the Debug log output feature, the SDK will output logs to the Xcode console at key moments, such as when initialization and reporting are successful, helping you verify SDK integration and reporting.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please confirm that you have enabled the sampling switch and configured the reporting policy for the target module; otherwise, the module data will not be sampled. Even if the module is connected successfully, no log indicating successful module connection will be generated. For related documentation, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#cb80bde4">Step 1: Open the sampling switch</a> and <a href="https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#b564fce8">Step 2: Configure the sampling reporting policy</a>.</div>


Example code:

```objectivec
#import <RangersAPM+DebugLog.h>

#if DEBUG
                // By modifying the block, you can customize your own log output format. The following code example is the default output format inside the SDK. If you pass in nil, the SDK will use the default format to output logs.
    [RangersAPM allowDebugLogUsingLogger:^(NSString * _Nonnull log) {
        NSLog(@"APMPlus : %@", log);
    }];
#endif

                // Please enable debug logs before this code. Otherwise, logs may not be output for some synchronous events.
    [RangersAPM startWithConfig:config];
```


Log entry description:


|**Log content** |**DescriptionS** |
|---|---|
|AppLog registered successfully! UserInfo: |AppLog has been registered, and the registration information is displayed simultaneously.<br><br>If you do not use RangersAppLog for device registration, no action is required. |
|Setup APMPlus \- version : |SDK initialization begins, preparing to start each feature module while outputting the current version. |


<span id="edd40741"></span>
## crash analytic

The complete crash analytic feature requires the introduction of submodules, including Crash, WatchDog, and OOM, with support for introducing each submodule independently.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you only need the OOM feature, make sure to include Crash and WatchDog as well; otherwise, the OOM data may be inaccurate.</div>


<span id="a57fdc5a"></span>
### **Test cases**

Test cases are used to verify whether the SDK can capture logs for the corresponding events. This is done by adding sample code to the project and triggering it at the appropriate time. You can refer to the sample code and description provided for each module, or to the Demo project.


1. Add the following code to the app code to trigger an NSException type crash.

   ```objectivec
       dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(5 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
           NSArray *array = [NSArray array];
           [array objectAtIndex:10];
       });
   ```
   

2. In Xcode, set the Build Configuration to Release, then use Run to install the App on the simulator or a physical device.

3. Open the app on an emulator or a physical device, then wait for the crash code to execute; the app crashes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not start the app directly using Xcode Run, as crashes triggered in this way cannot be captured.   </div>
   

4. In Xcode, when you restart the app via Run, the SDK will immediately report any crash that occurred during the previous start, and then you will see a log in the console indicating that the report was successful.


<span id="7beba9d8"></span>
### **Log description**

After completing [turning on Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**Log contents** |**DescriptionS** |
|---|---|
|Crash\-Monitor start successfully! |Crash Monitoring module started successfully |
|WatchDog\-Monitor start successfully! |Hang monitoring module started successfully |
|OOMCrash\-Monitor start successfully! |OOM Monitoring Module started successfully |
|Crash log is uploading... |Start uploading crash log |
|Crash log is uploaded successfully! |Crash log reported successfully. |
|Watchdog log is uploading... |Start uploading hang logs |
|OOM log is uploading... |Start uploading the OOM logs |


<span id="eba382d1"></span>
## error analytic

The error analysis module is divided into custom errors and network errors.


* Custom error module: requires importing the sub\-library UserException.

   Custom errors are a self\-instrumentation feature that requires manually calling the API to record errors occurring in the app and report them to the Application Performance Management Plus platform for centralized viewing.

* The network error module: You need to import the Network sublibrary.


<span id="ae1e0b8f"></span>
### **Test cases**

Test cases are used to verify whether the SDK can capture the log for the corresponding event by adding sample code to the project and triggering the sample code at the appropriate time. You can refer to the sample code and description provided by each module, or refer to the Demo project.

The following example code records one custom error log. The SDK triggers a report each time it records five logs. Network error logs can be automatically recorded by sending a single network request that will result in an error.

```objectivec
#import <RangersAPM+UserException.h>

[RangersAPM trackAllThreadsLogExceptionType:@"testUserException" 
                               skippedDepth:0  
                             customParams:@{@"testCustomKey":@"testCustomValue"}
                                  filters:@{@"testFilterKey":@"testFilterValue"}
                                 callback:^(NSError * _Nullable error){
                                    NSLog(@"%@",error); 
                                 }
];
```


If you cannot find the above header files and interfaces during SDK installation, please check the SDK version and upgrade it to 1.1.0 or later, or refer to the following code to record a custom error.

```objectivec
    #import <RangersAPMUserExceptionManager.h>
            
    [RangersAPMUserExceptionManager trackAllThreadsLogExceptionType:@"testUserException" 
                       skippedDepth:0 
                       customParams:@{@"testCustomKey":@"testCustomValue"} 
                            filters:@{@"testFilterKey":@"testFilterValue"}
                           callback:^(NSError * _Nullable error) {
                                 NSLog(@"%@",error);}
    ];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When an error occurs while using this feature, you can obtain the error code via error.code. The error code mapping table is located in the RangersAPMUserExceptionErrorType.h file of the current SDK, along with relevant descriptions. Similarly, you can also obtain a detailed error description through the reason field in the error.userInfo dictionary.</div>


<span id="a1ca7f72"></span>
### Reporting policy

Network error logs are not reported immediately after being recorded; they will be automatically reported at the following times:


* Trigger a report once 15 seconds after the app starts.

* A report is triggered every 60 seconds.

* When the App status switches to background, a report is sent once.


<span id="2f44b3a3"></span>
### **Log descriptions**

After completing [turning on Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**Log content** |**DescriptionS** |
|---|---|
|UserException\-Monitor start successfully! |The custom error monitoring module started successfully. |
|Network\-Monitor start successfully! |The Network Monitoring module started successfully |


<span id="f829dddd"></span>
## lag analytic

The lag analytic module requires the inclusion of the LAG sublibrary.

<span id="22e4e930"></span>
### **Test cases**

By adding sample code to the project and triggering the sample code at the appropriate time, test cases are used to verify whether the SDK can capture the log of the corresponding event. You can refer to the sample code and description provided by each module, or refer to the Demo project.

Simulate a lag event by blocking the main thread. The blocking time must be greater than the **lag threshold** configured in your **SDK setting** in order for the SDK to detect and report it. If the lag threshold is not modified, the default threshold is 2.5s.

```objectivec
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(5 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
    sleep(5);
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you need to perform some custom handling when a lag scenario occurs, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features#79df71df">notification</a>.</div>



<span id="1e9ba56f"></span>
### **Log description**

After [turning on the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify using the output log whether the module has been successfully integrated.


|**The log content** |**DescriptionS** |
|---|---|
|Lag\-Monitor start successfully! |The lag monitoring module started successfully |
|Lag log is uploading... |Start upload lag logs |


<span id="58cb19df"></span>
## event analytic

The event analytic module is a self\-embedding feature that requires you to manually call the interface to record events. To use this feature, you need to import the EventMonitor module.

<span id="0e3d99dc"></span>
### **Test cases**

Test cases are created by adding sample code to the project and triggering the sample code at the appropriate time, in order to verify whether the SDK can capture logs for the corresponding events. You can refer to the sample code and description provided by each module, or to the Demo project.

The following sample code can record an event. Relevant parameters can be found in the header file documentation.

```objectivec
#import "RangersAPM+EventMonitor.h"
  
  [RangersAPM trackEvent:@"event_name1"
          metrics:@{@"metric1":@(0)}
         dimension:@{@"dimension1":@"test"}// The Metrics parameter only supports an NSDictionary object where the key is of type NSString and the value is of type NSNumber. The Metrics parameter does not support nested structures.
        extraValue:@{@"extra1":@"extravalue"}];//The dimension parameter only supports an NSDictionary object where both the key and the value are of type NSString. The dimension parameter does not support nested structures.
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An event is recorded and reported only if it has been created in the console, the event status is turned on or under verification, and the client matches the event sampling rule.</div>


<span id="364eca54"></span>
### Reporting policy

After an event is recorded, it is not reported immediately. The client reporting rules are as follows:


* A report is triggered after the app starts.

* A report is triggered every 60 seconds.

* When the app status switches to background, trigger a report once.


<span id="74f8b87a"></span>
### **Log description**

After completing [enabling the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify module integration based on the output log.


|**Log content** |**DescriptionS** |
|---|---|
|Record an event\-log successfully, name: |Successfully record an event log and output the event name. |


<span id="a9101b01"></span>
## user experience

The user experience module consists of startup analytic, page response analysis, and fluency analysis.


* Startup analytic module: The Monitors sub\-library must be imported.

* Fluency analysis module: The Monitors sub\-library must be imported.

* The page response analysis module requires importing the UITrackers sub\-library.


<span id="5beecef5"></span>
### **Test cases**

Test cases are implemented by adding sample code to the project and triggering it at the appropriate time, in order to verify whether the SDK can capture the log for the corresponding event. You can refer to the sample code and description provided by each module, or to the Demo project.

The user experience module log is recorded when the App's status or scenario changes. The trigger methods are as follows:


* startup analytic

   * A Cold Start log is recorded when the app starts. This log cannot be triggered manually, and only one Cold Start log is recorded for each app start.

   * When the app switches from background to foreground, it records a warm start log. You can trigger this by switching between foreground and background.

* Page response log

   When the app switches scenes, a page response log is recorded. The log includes the time taken for the following stages: loadView, viewDidLoad, viewWillAppear, and viewDidAppear. You can trigger this by switching the viewController.


<span id="e4947e43"></span>
### Reporting policy

The user experience log is not reported immediately after being recorded; it will be reported automatically at the following times:


* A report is triggered once 15 seconds after the app starts.

* A report is triggered every 60 seconds.

* Each time the app status switches to the background, a report is triggered.


<span id="749486db"></span>
### **Log descriptions**

After completing [enabling the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**The log content** |**DescriptionS** |
|---|---|
|Start\-Monitor start successfully! |Monitoring module started successfully |
|FPS\-Monitor start successfully! |Fluency Monitoring Module started successfully |
|FrameDrop\-Monitor start successfully! |The frame drop analysis module has started successfully |
|PageLoad\-Monitor start successfully! |Page response analysis module started successfully |


<span id="2bb2081f"></span>
## Page monitoring

The page monitoring module captures load, request, and error events that occur in the app's WebView. To turn on this feature, you need to import the Hybrid sub\-library.

<span id="c567090e"></span>
### **Test cases**

Test cases verify whether the SDK can capture the logs for the corresponding event by adding sample code to the project and triggering the sample code at the appropriate time. You can refer to the sample code and description provided by each module, or to the Demo project.

You can use [Web Demo](https://datarangers.com.cn/apminsight/demo/demo/rangers-site-hybrid-sdk-script) to create a new WebView in your app for testing, or you can refer to the Demo to write test cases in the original WebView page of your app.

<span id="35ee9e39"></span>
### Reporting policy

After a page monitoring log is recorded, it is not reported immediately. It will be automatically reported at the following times:


* A report is triggered once 15 seconds after the app starts.

* A report is triggered every 60 seconds.

* A report is triggered once when the app status switches to background.


<span id="26e783ce"></span>
### **Log description**

After completing [turning on the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**Log content** |**DescriptionS** |
|---|---|
|Hybrid\-Monitor start successfully! |Hybrid monitoring module started successfully |


<span id="faa07592"></span>
## memory optimization

When the app's memory usage exceeds 1GB, the memory optimization module collects all memory nodes and reference relationships in the current state, generates a memory snapshot file, and uploads it. Accordingly, on the platform, you can view the app’s memory allocation when memory usage is high, and use runtime information to troubleshoot issues such as memory leaks, large memory allocations, and other related issues. To turn on the memory optimization feature, you need to import the MemoryGraph sub\-library.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Memory collection incurs some performance overhead. Because collecting memory requires ensuring heap safety, threads are suspended when memory collection is triggered. During this period, user operations are blocked, resulting in lag. However, memory collection is triggered only when memory usage exceeds the exception threshold, and does not affect users under normal usage.</div>


* <div data-tips="true" data-tips-type="tip">The memory analysis feature can only be triggered on 64\-bit physical devices, supports only iPhone 6s and newer device models, and requires Operating System iOS 10 or above.</div>


   <div data-tips="true" data-tips-type="tip">Using the iPhone 8 Plus device model as an example, when the app's memory usage exceeds 1 GB:   </div>
   

   * <div data-tips="true" data-tips-type="tip">Collection time: 1.5 to 2 seconds</div>


   * <div data-tips="true" data-tips-type="tip">Additional memory consumption of 10 MB to 20 MB during collection.</div>


   * <div data-tips="true" data-tips-type="tip">The size of the generated files after compression is between 5MB and 20MB.</div>



<span id="0a566e40"></span>
### **Test cases**

Test cases verify whether the SDK can capture the log for the corresponding event by adding sample code to the project and triggering the sample code at the appropriate time. You can refer to the sample code and description provided for each module, or to the Demo project.

Add the following code to call the OOMTrigger function and trigger a memory leak.

```objectivec
#import <mach/mach.h>
    //The set memory collection start threshold. When the App's memory exceeds this value, the memory optimization module will be started to collect the App's memory status.
    static float dangerousMemoryThreshold = 1024.0;
            
    // Calculate the current memory usage of the App. When the memory usage exceeds the memory collection start threshold, return true; otherwise, return false.
    bool overMemoryThreshold(void)
    {
        kern_return_t kr;
                
        task_vm_info_data_t task_vm;
        mach_msg_type_number_t task_vm_count = TASK_VM_INFO_COUNT;
        kr = task_info(mach_task_self(), TASK_VM_INFO, (task_info_t) &task_vm, &task_vm_count);
                   
        if (kr == KERN_SUCCESS) {
            printf("Current App Memory is :%f\n\n", task_vm.phys_footprint / (1024.0 * 1024.0));
            if (task_vm.phys_footprint / (1024.0 * 1024.0) > dangerousMemoryThreshold) {
                return true;
            } else {
                return false;
            }
        }
            
        return false;
    }
            
    //Trigger a memory leak. When the current memory usage of the App is less than the memory collection start threshold, a memory leak will be continuously triggered.
    - (void)OOMTrigger{
        dispatch_async(dispatch_get_global_queue(0, 0), ^{
            while (1) {
                if (!overMemoryThreshold()) {
                    CGSize size = CGSizeMake(1024 * 8, 1024 * 8 * 9.0f/16.0);
                    const size_t bitsPerComponent = 8;
                    const size_t bytesPerRow = size.width * 4;
                    CGContextRef ctx = CGBitmapContextCreate(calloc(sizeof(unsigned char), bytesPerRow * size.height), size.width, size.height, bitsPerComponent, bytesPerRow, CGColorSpaceCreateDeviceRGB(), kCGImageAlphaPremultipliedLast);
                    CGContextSetRGBFillColor(ctx, 1.0, 1.0, 1.0, 1.0);
                    CGContextFillRect(ctx, CGRectMake(0, 0, size.width, size.height));
                    sleep(1);
                } else {
                    break;
                }
            }
        });
    }
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The value of the <code>dangerousMemoryThreshold</code> variable must be changed to the <strong>memory collection start threshold</strong> that you configured in the <strong>SDK setting</strong>. If you have not configured or modified this value, no modification is required.</div>


<span id="0a7c575a"></span>
### Reporting policy

After the App's memory status is collected, it will be reported the next time the App is started.

Before uploading the memory file, a request is sent to the Server to check whether uploading is allowed. If the Server does not allow upload, a request will be made again the next time the App starts. Memory files whose upload requests were not approved are cached in the app sandbox and will be uploaded together when the server allows uploads. For more information, refer to [How to determine whether the Server allows uploading memory files?](https://docs.byteplus.com/en/docs/apmplus/Determine_whether_the_server_allows_the_upload_of_memory_files).

<span id="560ac1be"></span>
### **Log descriptions**

After turning on [the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**The log content** |**DescriptionS** |
|---|---|
|OOMCrash\-Monitor start successfully! |OOM crash monitoring module started successfully |
|MemoryGraph start successfully! |MemoryGraph module started successfully |
|MemoryGraph start failed. Reason: ... |MemoryGraph module failed to start. Reason: ... |
|Memory\-Monitor start successfully! |Memory metric monitoring module started successfully |
|MemoryGraph generate start. |When app memory reaches the threshold, start memory collection. |
|MemoryGraph generate failed, reason : |Memory collection failed, and the cause of the error is displayed. |
|MemoryGraph generate successfully! |Memory collection successful |
|Upload MemoryGraph \-\- server check failed. |Server currently does not allow upload of MemoryGraph file |
|MemoryGraph file is uploading... |Uploading MemoryGraph file |
|Upload MemoryGraph file successfully! |MemoryGraph file uploaded successfully. |
|Upload MemoryGraph file failed. |Failed to upload MemoryGraph |


<span id="c53977f9"></span>
## network analytic

The network analytic module requires importing the Network sub\-library.

<span id="3896f157"></span>
### **Test cases**

Test cases verify whether the SDK can capture the log for the corresponding event by adding sample code to the project and triggering it at the appropriate time. You can refer to the sample code and description provided by each module, or refer to the Demo project.

You can send some network requests to trigger SDK network data logging.

<span id="b5aed241"></span>
### Reporting policy

Network analytic logs are not reported immediately after they are recorded. They will be automatically reported at the following times:


* A report is triggered once 15 seconds after the App starts.

* A report is triggered every 60 seconds.

* A report is triggered once when the app status switches to background.


If you do not want to monitor network requests, or only want to monitor those for certain URLs, you can configure these settings in the **network request configuration**.

<span id="59d53adf"></span>
### **Log descriptions**

After [turning on Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**Log content** |**DescriptionS** |
|---|---|
|Network\-Monitor start successfully! |Network Monitoring module started successfully |


<span id="5e60c23f"></span>
## Log recovery

The log recovery module needs to import the APMLog sub\-library. By using the interfaces provided by the SDK to log events, you can record logs generated during app runtime. This module is a high\-efficiency log instrumentation framework based on mmap, with a log compression ratio of up to 25 times. Combined with cloud control, it enables real\-time targeted recovery of online user logs, helping you efficiently and accurately locate and resolve issues.

Not all logs are reported. The methods to obtain these logs are as follows:


* After a crash occurs, logs generated during the period preceding the crash are automatically reported.

   Reported logs can be viewed in the custom log section of the crash details page.

* Issue a cloud control command to obtain logs generated by specified devices or users within a specified time period. For more information, refer to [recovery](https://docs.byteplus.com/en/docs/apmplus/Recovery).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The string length for a custom log is limited to 4\*1024 characters.</div>


<span id="0fa7c9c7"></span>
### **Test cases**

Test cases are used to verify whether the SDK can capture the log of the corresponding event by adding sample code to the project and triggering it at the appropriate time. You can refer to the sample code and description provided by each module, or refer to the Demo project.

For C/C++, Objective\-C, and Swift, APMPlus provides three categories of log interfaces. Each category includes four interfaces: Debug, Info, Warn, and Error, which correspond to four levels of log severity. When viewing logs on the platform, you can filter them by severity level.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Improper handling of log parameters may result in a crash.</div>


<div data-tips="true" data-tips-type="danger"><code>RANGERSAPM_ALOG_INFO(tag, format, ...)</code> interface expects the second parameter to be a <code>format</code>, followed by variable arguments, similar to</div>


<div data-tips="true" data-tips-type="danger"><code>[NSString stringWithFormat:format, ...]</code>, when the <code>format</code> string does not contain format specifiers, the variable parameters can be omitted.</div>


<div data-tips="true" data-tips-type="danger">In certain usage scenarios, a variable from the code may be directly passed as the <code>format</code> parameter. If this variable unexpectedly contains format specifiers—especially when the variable is a URL—a mismatch between the format specifiers and the variadic arguments can result in a crash.</div>


<div data-tips="true" data-tips-type="danger">To use the interface more safely, if you want to pass the variable <code>urlString</code> as the <code>format</code> parameter, it is recommended to refer to the following sample code:</div>


<div data-tips="true" data-tips-type="danger"><code>RANGERSAPM_ALOG_INFO("TAG", @"%@", urlString);</code></div>


```objectivec
// Regardless of which type of interface is used, you first need to call the following interface to enable the Alog function.
// Note: It only needs to be called once when the App starts.
#import "RangersAPM+ALog.h"

// For custom log-related configurations, you need to set the alogParams attribute of the RangersAPMConfig parameter passed in when starting the SDK. See the header file comments for configuration details.
RangersAPMALogParams *alogParams = [[RangersAPMALogParams alloc] init];
alogParams.maxDiskUsage = 50 * 1024 * 1024;
alogParams.validityPeriod = 7 * 24 * 60 * 60;
RangersAPMConfig *apmConfig = ...
apmConfig.alogParams = alogParams;
[RangersAPM startWithConfig:apmConfig];

[RangersAPM setALogEnabled];  //Enable ALog.
[RangersAPM enableConsoleLog];  // Output logs to the console at the same time.

BOOL isALogEnabled = [RangersAPM isALogEnabled];  //ALog enabled status.

//In Objective - C, you can use the following interface to log.
#import "RangersAPM+ALog.h"

//The first parameter identifies information such as the current log's business and scenario.
//The second parameter is the specific log information. You can use the format type. If you use the format, you need to continue to pass in the corresponding parameters.
 RANGERSAPM_ALOG_DEBUG(@"Business", @"version : %@", [self version]);  //Debug - type logs.
 RANGERSAPM_ALOG_INFO(@"Business", @"version : %@", [self version]);   // Info - type logs.
 RANGERSAPM_ALOG_WARN(@"Business", @"version : %@", [self version]);   //Warn - type logs.
 RANGERSAPM_ALOG_ERROR(@"Business", @"version : %@", [self version]);   //Error - type logs.
  
// In C/C++, you can use the following interface to log.
#import "RangersAPM_ALog.h"
 
// The first parameter identifies information such as the current log's business and scenario.
// The second parameter is the specific log information. You can use the format type. If you use the format, you need to continue to pass in the corresponding parameters.
 RANGERSAPM_ALOG_DEBUG_C("Business", "version : %s", version());
 RANGERSAPM_ALOG_INFO_C("Business", "version : %s", version());
 RANGERSAPM_ALOG_WARN_C("Business", "version : %s", version());
 RANGERSAPM_ALOG_ERROR_C("Business", "version : %s", version());
 
// In Swift, you can use the following interface to log.
#import "RangersAPM+ALog.h"

// The first parameter is the specific log information.
// The tag identifies information such as the current log's business and scenario.
// The fileName is the name of the current file. You can refer to the example and pass in #file.
// The funcName is the name of the current method. You can refer to the example and pass in #function.
// The line is the line number of the current file. You can refer to the example and pass in #line.
RangersAPM.debugALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
RangersAPM.infoALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
RangersAPM.warnALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
RangersAPM.errorALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
```


<span id="01b4424b"></span>
### **Log descriptions**

Once [the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1) is turned on, verify whether the module has been successfully integrated using the output log.


|**Log content** |**DescriptionS** |
|---|---|
|ALog is uploaded successfully! |(recovery) Custom log reported successfully |
|Upload ALog failed, reason : |(Recovery) Custom log reporting failed; output the reason |
|ALog is uploaded manually! |Custom log reported manually successfully |
|Manually upload ALog failed |Manually report custom log failure |
|CloudCommand start successfully! |The recovery feature started successfully. |
|CloudCommand is being executed ... |Recovery command is in progress |
|ALog start successfully! |Custom log feature started successfully |


<span id="e5813cea"></span>
## CPU monitor

The CPU monitor module contains two submodules: CPU metrics and CPU anomalies.


* CPU metric module: Requires importing the Monitors sub\-library.

   Monitor CPU usage while the app is running; additionally, the SDK version must be higher than 2.7.3.

* CPU anomaly module: requires importing the CPUException sub\-library.

   Monitor for scenarios in which CPU utilization is excessively high during app operation, and record the stack trace at that time.


<span id="edd265a2"></span>
### **Test cases**

Test cases verify whether the SDK can capture the log for the corresponding event by adding sample code to the project and triggering it at the appropriate time. You can refer to the sample code and description provided by each module, or refer to the Demo project.

CPU metric will be automatically reported during app runtime. The following sample code simulates a scenario of excessively high CPU utilization and triggers the reporting of a CPU anomaly.

```objectivec
for (int i = 0; i < 10; i++) {
        NSString *queueName = [NSString stringWithFormat:@"com.apmplus.testcpu%d",i];
        dispatch_queue_t queue = dispatch_queue_create([queueName UTF8String], DISPATCH_QUEUE_SERIAL);
                dispatch_async(queue, ^{
                        int count = 0;
                        while (1) {
                                count++;
                        }
                });
}
```


<span id="a78c8965"></span>
### **Log descriptions**

After completing [enabling the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**Log content** |**DescriptionS** |
|---|---|
|CPUException log is uploading... |CPU anomaly log is being reported |
|CPUException\-Monitor start successfully! |The CPU anomaly monitoring feature started successfully |
|Record CPUException log successfully! |Successfully record CPU anomaly logs |
|CPUMetric\-Monitor start successfully! |The monitoring feature for the CPU metric started successfully. |


<span id="8019329c"></span>
## MetricKit

The MetricKit module monitors the system logs generated by MetricKit.framework and reports them to the platform. To integrate, import the MetricKit sub\-library and ensure that the APMPlus SDK version is higher than 2.12.1.

<span id="58cc2d9c"></span>
### **Test cases**

To verify whether the SDK can capture the log of the corresponding event, test cases are created by adding sample code to the project and triggering it at the appropriate time. You can refer to the sample code and description provided by each module, or refer to the Demo project.

The operating system generates a MetricKit log every day and provides it to the business side. If you want to test whether the integration is successful, please perform the following actions while debugging on a real device:

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6d58f71a60a321bc10325d78e7e14a0f.png) </span>

<span id="ec1b2fd0"></span>
### **Log description**

After [turning on the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated according to the output log.


|**Log content** |**DescriptionS** |
|---|---|
|MetricKit start successfully! |MetricKit module started successfully |
|MetricKit log is uploading... |MetricKit log is being reported |


<span id="781b1f1a"></span>
## Disk

The Disk module monitors the usage of the sandbox. At the same time, the generated metrics and exception information will be reported to the platform. To integrate, please import the Disk sub\-library, and ensure that the APMPlus SDK version is higher than 3.0.0.

<span id="37bcb43d"></span>
### **Test cases**

Test cases are implemented by adding sample code to the project and triggering the sample code at the appropriate time, in order to verify whether the SDK can capture the log of the corresponding event. You can refer to the sample code and description provided by each module, or the Demo project.

To prevent retrieving sandbox files from affecting user experience. When the disk monitor starts, the Disk module will retrieve sandbox files in the program background and report them.

<span id="ac272ab6"></span>
### **Log descriptions**

After completing [turning on the Debug log](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#13271ab1), verify whether the module has been successfully integrated based on the output log.


|**Log content** |**DescriptionS** |
|---|---|
|Disk start successfully! |Disk module started successfully |


<span id="601121a2"></span>
## Custom recovery

Custom recovery can, according to the configuration, retrieve specified information from the sandbox or memory and send it to the APMPlus platform for troubleshooting or data analysis. To integrate, please import the CloudCommand sub\-library, and ensure that the APMPlus SDK version is higher than 3.5.3.

<span id="335e0d7e"></span>
### Test cases


1. Create a class to respond to recovery commands.

   ```objectivec
   #import <Foundation/Foundation.h>
   #import "RangersAPM+CloudCommand.h"
   
   NS_ASSUME_NONNULL_BEGIN
   // Inherit from the custom data retrieval base class.
   @interface APMPlusCustomCloudHandler : RangersAPMCustomCommandBase
   @end
   NS_ASSUME_NONNULL_END
   ```
   

   ```objectivec
   #import "APMPlusCustomCloudHandler.h"
   
   @implementation APMPlusCustomCloudHandler
   // Respond to the command value in the data retrieval parameters.
   + (NSString *)cloudCommandIdentifier {
       return @"pull_file";
   }
   /// Create an instance variable for executing instructions.
   + (instancetype)createInstance {
       static APMPlusCustomCloudHandler *handler = nil;
       static dispatch_once_t onceToken;
       dispatch_once(&onceToken, ^{
           handler = [[APMPlusCustomCloudHandler alloc] init];
       });
       return handler;
   }
   
   /// Execute a custom command.
   - (void)executeCustomCommandWithParams:(NSDictionary *)params completion:(RangersAPMCustomCommandCompletion)completion {
       
       RangersAPMCustomCommandResult *result = [[RangersAPMCustomCommandResult alloc] init];
       // The dictionary information to be reported.
       result.specificParams = @{@"aKey": @"aValue", @"bKey": @"bValue"};
       // The binary information of the file to be reported.
       ...
       result.data = [NSData dataWithContentsOfFile:toBeUplodFilePath];
       // The name of the file to be reported.
       result.fileName = @"custom_file_name";
       if (completion) {
           completion(result);
       }
   }
   /// The result was successfully uploaded to the server.
   - (void)uploadCustomCommandResultSucceededWithParams:(NSDictionary *)params {
       NSLog(@"------ %s", __func__);
   }
   /// Failed to upload the result to the server.
   - (void)uploadCustomCommandResultFailedWithParams:(NSDictionary *)params error:(NSError *)error {
       NSLog(@"------ %s", __func__);
   }
   @end
   ```
   

2. Register classes that respond to recovery commands.

   After RangersAPM starts, call the following code to inject the custom recovery response class.

   ```objectivec
   // Register a custom data retrieval class.
   [RangersAPM addCustomCommandHandlerCls:[APMPlusCustomCloudHandler class]];
   ```
   

3. Create a custom recovery task. For details, please refer to [Create a log recovery task](https://docs.byteplus.com/en/docs/apmplus/Recovery#.5paw5bu65Lu75Yqh).

   In the recovery parameter, add the following content.

   ```JSON
   {
       "business_Akey":"business_Avalue",
       "business_Bkey":"business_Bvalue",
       "command":"pull_file"
   }
   ```
   

   * command: In an iOS project, the value of this field is used to dispatch commands to different handlers for execution.

   * Please configure other fields on your own according to your business requirements.


<span id="ec5e1f41"></span>
### Log descriptions

After turning on the Debug log, verify whether the module has been successfully integrated based on the output log.


|**Log content** |**DescriptionS** |
|---|---|
|CloudCommand start successfully! |The recovery feature started successfully. |
|CloudCommand is being executed ... |Recovery command is in progress |
