---
title: "iOS add-on monitoring for integrated SDK"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_component_monitoring_SDK"
---

The iOS SDK for RUM is generally non\-intrusive. This topic describes the detailed integration steps for the SDK.

> **warning**

* > Currently, the iOS SDK is restricted to use in the Chinese mainland (excluding Hong Kong, Macao, and Taiwan).

* > This topic applies to the following scenario: You want to monitor crashes, hangs, or custom events that occur within a specific SDK or add\-on. If you want to monitor crashes, hangs, and similar issues occurring in the app, see [Integrating the iOS SDK into your apps](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* > Add\-on monitoring capabilities are not fully equivalent to app monitoring capabilities. Currently, only crash monitoring, custom errors, and event tracking points are supported.

* > Calling the SDK initialization API does not collect user information. Calling the SDK startup API will begin collecting user information. Ensure that user authorization has been obtained before collecting user information according to [SDK privacy policy](https://docs.byteplus.com/en/docs/apmplus/The_SDK_privacy_policy).

## Demo description

[APMPlus_iOS](https://github.com/volcengine/APMInsight_iOS)

The Demo provides sub\-libraries for each functional module. The relationship between sub\-libraries and modules is shown in the table below.

|**Sub\-libraries** |**Description** |**Corresponding platform module** |**The first version that supports it** |
|---|---|---|---|
|Crash |Crash monitoring: Captures CPP Exception, Mach Exception, NSException Exception, and Signal Exception. |Crash analysis |2.8.1 |
|WatchDog |Hang monitoring: Monitors situations where the main thread is stuck for a long time and is force\-killed by the system watchdog. |Crash analysis |2.8.1 |
|UserException |Custom errors, which require manual logging by the business developers. |Error analysis \- Custom errors |2.8.1 |
|EventMonitor |Event analysis. Records custom events and requires manually added tracking points. |Event analysis |2.8.1 |
|SessionTracker |PV/UV statistics. Data is automatically reported after integration. |Exception rate of each module, proportion of users with exceptions, and more. |2.8.1 |
|BootingProtectLite |Consecutive crash protection |\- |2.10.0 |
|APMLog |APM log library. It allows manual logging to record SDK runtime logs |Single\-point tracing \- Retrieval<br><br>Crash analysis \- Crash details \- Custom logs |3.5.3 |
|CloudCommand |Retrieval |Single\-point tracing \- Retrieval |3.5.3 |

## Step 1: Obtain the SDK package

There are two ways to integrate add\-on monitoring capabilities: Integrating through the host app itself and integrating through add\-on dependencies.

* Integrate through the host app itself

   1. Add the following code to the host app's Podfile.

      ```Ruby
      source 'https://github.com/volcengine/volcengine-specs.git'
      
        pod 'RangersAPM', '5.2.7', :subspecs => [
            'Crash',
            'WatchDog',
            'UserException',
            'EventMonitor',
            'SessionTracker',
            'CN'  #Must be imported
        ]
      ```

   2. Execute `pod install` or `pod update` to install the SDK.

* Integrate through add\-on dependencies

   1. Add the following code to the add\-on's podspec.

      ```Ruby
      Pod::Spec.new do |s|
        s.name             = 'xxx'
        s.version          = '0.0.1'
        s.summary          = 'xxx'
        s.source_files = 'Classes/**/*'
        ...
        s.dependency 'RangersAPM/Crash', '5.2.7'
        s.dependency 'RangersAPM/WatchDog', '5.2.7'
        s.dependency 'RangersAPM/UserException', '5.2.7'
        s.dependency 'RangersAPM/EventMonitor', '5.2.7'
        s.dependency 'RangersAPM/SessionTracker', '5.2.7'
        s.dependency 'RangersAPM/CN', '5.2.7'
      end
      ```

   2. Import sub\-libraries as needed. For details, see [Demo description](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_component_monitoring_SDK#9c4ecfc7).

## Step 2: Initialization

Add the following code in the add\-on's initialization code (or at an appropriate time after the user agrees to the privacy policy).

Replace `{{sdk_id}}` and `{{app_token}}` with the AppID and AppToken of the application you created. For details, see [How to query AppID and AppToken?](https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken)

```Objective-C
#import <RangersAPMForSDK.h>

- (void)init {
    RangersAPMForSDKConfig *sdkConfig = [RangersAPMForSDKConfig configWithSDKID:@"{{sdk_id}}" appToken:@"{{app_token}}"];
    sdkConfig.channel = @"Cocoapods";   //SDK release channel (optional)
    sdkConfig.hostAppID = @"host_app_id"; //Host app identifier (optional)
    sdkConfig.sdkVersion = @"1.0.0";   //SDK version (required)
}
```

## Step 3: Start the SDK and enable data collection

Add the following code to the add\-on's initialization code (or at an appropriate time after the user agrees to the privacy policy). sdkConfig is the configuration generated during initialization.

```Objective-C
#import <RangersAPMForSDK.h>

- (void)start {
    RangersAPMForSDK *sdkMonitor = [[RangersAPMForSDK alloc] initWithConfig:sdkConfig];
}
```

> **tip**

> We recommend calling the startup code as early as possible. Data about events such as crashes that occur before the above code is executed cannot be captured.

## Step 4: Upload the symbol table

> **warning**

> Crash logs for add\-on monitoring can only be parsed after the symbol table is uploaded. If your SDK is a static library, the symbol table is generated when the host app is packaged after integration.

### Manual upload

1. Ensure your symbol table conforms to the following format.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d965b673661433289a2cfe897ac5cfa~tplv-goo7wpa0wc-image.image)

2. Compress the symbol table into a zip file.

   On macOS, you need to execute the following command to remove the default\-generated `DS_Store and__MACOSX` files from the zip file.

   ```PowerShell
   zip -r test.app.dSYM.zip test.app.dSYM -x "*.DS_Store" -x "__MACOSX"
   ```

   Replace `test.app.dSYM.zip` and `test.app.dSYM` with your symbol table name.

3. Upload the symbol table.

   * Upload the symbol table in the **Symbol table management** module.

   * Upload using the curl command.

      ```PowerShell
      curl https://console.byteplus.com/observe/apmplus-client_api/eue/guest/app/mapping/upload -F "file=@dSYMZipName" -F "type=Dwarf" -F "os=iOS" -F "aid=APMPlusID" -H "Content-Type: multipart/form-data" -w %{http_code}
      ```

      * Note that the command parameter values need to be wrapped in '' ", otherwise spaces in the parameters may cause command parsing errors.

      * Replace `dSYMZipName` in the above command with your symbol table file path, and `APMPlusID` with your AppID.

         After execution is complete, a return like the following indicates a successful upload.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86349efd62354753afdffd8425a85f78~tplv-goo7wpa0wc-image.image)

### Automatic upload

You can achieve automatic symbol table upload during app packaging by configuring Build Phases and adding a Run Script under the corresponding Target in Xcode.

> **tip**

> By default, symbol tables are not uploaded in Debug mode or simulator builds. If you need to upload symbol tables in these two cases, see [Manual upload](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_component_monitoring_SDK#2aa0c127).

1. Select **Build Settings \> Debug Information Format** to check whether the project configuration generates symbol tables.

2. Select **Build Phases \> New Run Script Phase** to add a Run Script.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51fa4b2efc3c441c94c399a69e3f8da7~tplv-goo7wpa0wc-image.image)

3. Place the added Run Script at the end to prevent the script from executing before the symbol table is generated.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74e042f7947c4c41bfb1f074e5d46392~tplv-goo7wpa0wc-image.image)

4. Modify the script content.

   * If the SDK version you have integrated is 1.5.0 (inclusive) or later, you only need to add the following code to the script and replace `APMPlusID` in the command with your app ID. With this method, the symbol table will not be uploaded in Debug mode or during simulator builds.

      ```PowerShell
      /bin/sh ${PODS_ROOT}/RangersAPM/RangersAPM/APMPlus_DSYMUploader.sh "APMPlusID"
      ```

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f00af3a2aee14cf49ae5a6fd13f6f15b~tplv-goo7wpa0wc-image.image)

   * If you have integrated a lower SDK version and do not want to upgrade, or if Debug mode and simulator builds are required, the symbol table can be uploaded.

      1. Download the script file.

         [APMPlus_DSYMUploaderV2.0.sh](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96694b29f2214efc9bb7506bab3f93d0~tplv-goo7wpa0wc-image.image)

      2. Copy the content of the downloaded script file into the Run Script, and replace `APMPlus_APP_ID` with your app ID.

      3. Modify the `UPLOAD_DEBUG_SYMBOLS` and `UPLOAD_SIMULATOR_SYMBOLS` fields in the script as needed.

## Step 5: Verify data reporting

You can check whether each module has been successfully integrated by comparing it with the descriptions of the following modules, as needed.

### Debug log description

**Prerequisites**

Configure the following code before the SDK's startup method. Otherwise, some sync events may fail to output logs.

```Objective-C
 #if DEBUG
 [RangersAPM allowDebugLogUsingLogger:^(NSString * _Nonnull log) {
     NSLog(@"APMPlus : %@", log);
 }];
 #endif

 RangersAPMForSDK *sdkMonitor = [[RangersAPMForSDK alloc] initWithConfig:sdkConfig];
```

**Enable debug logs**

After enabling the Debug output feature, the SDK will print logs in the Xcode console when key events occur (such as successful initialization or successful reporting), helping you verify the SDK integration and data reporting.

Sample code:

```Objective-C
#import <RangersAPM+DebugLog.h>

[RangersAPM allowDebugLogUsingLogger:^(NSString * _Nonnull log) {
    NSLog(@"APMPlus : %@", log);
}];
```

Supports customizing the log output format by modifying the block.

If nil is passed in, the SDK will output logs using the internal default format:

```Objective-C
[RangersAPM allowDebugLogUsingLogger:nil];
```

### Test case description

Through test cases, you can verify whether the SDK functions are correctly enabled. You can add test cases in your code yourself.

If you do not know how to add test cases, you can download the [Example project](https://github.com/volcengine/APMInsight_iOS), or refer to the sample code provided for each module below.

#### General

**Debug logs**

|**Log content** |**Description** |
|---|---|
|Setup APMPlus \- version : |SDK initialization started, preparing to start each feature module, and outputting the current version at the same time. |

### Crash analysis

The complete crash analysis feature requires the following sub\-libraries: Crash and WatchDog. You can also import each sub\-library individually.

#### Get the address range of the add\-on

To monitor crashes occurring within the add\-on, you first need to obtain the add\-on's address range. We provide three solutions.

**Solution 1: Add a marker function**

This solution is simple to integrate and requires no additional configuration from the host app. However, it is intrusive to the add\-on to a certain extent, and the accuracy of the address range cannot be guaranteed after binary reordering.

1. Add the following two source files to the add\-on and define two functions: Use the address of one function as the add\-on's start address and the address of the other function as the add\-on's end address.

   > **warning**

   > Do not use the example file names and function names directly. You need to add a prefix to avoid conflicts.

   ```Objective-C
   //SDKBegin.c
   #include "SDKBegin.h"
   extern void * SDKBeginAddress(void) {
       return &SDKBeginAddress;
   }
   
   //SDKEnd.c
   #include "SDKEnd.h"
   extern void * SDKEndAddress(void) {
       return &SDKEndAddress;
   }
   ```

2. Adjust the compilation order in Xcode Build Phases \- Compile Sources.

   As shown below, `SDKBegin.c` is compiled first, and `SDKEnd.c` is compiled last.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99acb9f62d504b5294ea0eb8da2eb3b6~tplv-goo7wpa0wc-image.image)

   * Alternatively, you can add the prefix AAA to the file that marks the start of the SDK symbols and the prefix ZZZ to the file that marks the end of the SDK symbols.

   * For an SDK with multiple subspecs, you can add two subspecs: One named AAA\*\*\* and the other named ZZZ\*\*\*, and make all other subspecs depend on these two. This can ensure the SDK address range is obtained correctly, regardless of which subspecs the user integrates.

3. Configure the addressConfig parameter of config when initializing the RangersAPM SDK. addressConfig supports passing in multiple address ranges to monitor multiple address segments.

   ```Objective-C
   #import <RangersAPMForSDK.h>
   
   extern void * SDKBeginAddress;
   extern void * SDKEndAddress;
   
   -(void)init {
       NSArray * addressRanges = @[[RangersAddressRange addressRangeWithStartAddress:(int64_t)&SDKBeginAddress endAddress:(int64_t)&SDKEndAddress]];
       RangersAPMAddressConfig * addressConfig = [RangersAPMAddressConfig configWithAddressRanges:addressRanges];
       RangersAPMForSDKConfig *sdkConfig = [RangersAPMForSDKConfig configWithSDKID:@"{{app_id}}" appToken:@"{{app_token}}"];
       sdkConfig.addressConfig = addressConfig;
       sdkConfig.channel = @"Cocoapods";
       sdkConfig.hostAppID = @"host_app_id"; //Host app identifier
       sdkConfig.sdkVersion = @"1.0.0";
   }
   ```

**Solution 2: Add a build script**

This solution requires no additional configuration during RangersAPM SDK initialization and is more accurate than Solution 1. However, you need to add a script to the host app in Xcode.

> **warning**

> The script to be added should be added to the host's Project, not the add\-on's Project.

1. Download the script.

   [APMPlus_AddressRange.sh](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a3fbfcc00d748398aa37eb3755c049d~tplv-goo7wpa0wc-image.image)

2. Modify the script content.

   ```PowerShell
   SDKAid="123456"
   SDKName="RangersAPM"
   writeAddressRangeFile $SDKName $SDKAid
   ```

   Parameter description:

   |Parameters |Description |
   |---|---|
   |SDKAid |* Cannot be empty.<br><br>* The AppID applied for on the APMPlus platform. |
   |SDKName |* Cannot be empty.<br><br>* Enter the Pod name if the SDK is integrated via Cocoapods.<br><br>* Enter the name of the outermost folder of the SDK package if the SDK is obtained via download.  |

   When monitoring multiple SDKs simultaneously, note the following:

   * If these SDKs need to be aggregated into a single dashboard (i.e., data is reported under the same appId in APMPlus), you need to modify SDKName and separate the SDK names with |, i.e., SDKName="SDK1|SDK2|SDK3".

      ```PowerShell
      SDKAid="123456"
      SDKName="RangersAPM|RangersAppLog"
      writeAddressRangeFile $SDKName $SDKAid
      ```

   * If these SDKs are relatively independent (i.e., data is reported to their respective AppIDs), there will be multiple AppIDs. Perform the above call for each SDK.

      ```PowerShell
      SDKAid1="123456"
      SDKName1="RangersAPM"
      writeAddressRangeFile $SDKName1 $SDKAid1
      
      SDKAid2="4567890"
      SDKName2="RangersAppLog"
      writeAddressRangeFile $SDKName2 $SDKAid2
      ```

3. In Xcode \- Build Settings, set Write Link Map File to YES to allow the generation of Link Map files.

   Since script execution takes some time, to avoid impacting the development experience, we recommend setting Write Link Map File to YES only in the Release environment.

4. Paste the modified script into the Run Script to complete the script integration.

   The added Run Script needs to be placed before Copy Pods Resources and after Compile Sources. You can move the position of the Run Script by dragging.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72ca56b4867c4a4d9178d5197fe97a1b~tplv-goo7wpa0wc-image.image)

**Solution 3: Configure library names (only applicable to dynamic libraries)**

When initializing the APMPlus, configure the libNames property of RangersAPMForSDKConfig and pass in your SDK package name.

```Objective-C
#import <RangersAPMForSDK.h>

-(void)init {
    RangersAPMForSDKConfig *sdkConfig = [RangersAPMForSDKConfig configWithSDKID:@"{{app_id}}" appToken:@"{{app_token}}"];
    sdkConfig.libNames = @[@"SDK1", @"SDK2"];
    sdkConfig.channel = @"Cocoapods";
    sdkConfig.hostAppID = @"host_app_id"; //Host app identifier
    sdkConfig.sdkVersion = @"1.0.0";
}
```

#### **Test cases**

The code below will trigger an NSException\-type crash. For more case types, you can download the Example project.

```Objective-C
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(5 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
    NSArray *array = [NSArray array];
    [array objectAtIndex:10];
});
```

1. Embed the above code into your app's code.

2. In Xcode, change the Build Configuration to Release, then use Run to install the app on the simulator or a real device.

3. Launch the app on the simulator or real device, then wait for the crash code to execute and the app to crash.

   > **warning**

   > Do not launch the app directly through Xcode Run, as the crash triggered in this way cannot be captured.

4. Restart the app, and the SDK will immediately report the crash that occurred during the previous launch. You can start the app via Xcode Run, and you can see the successful reporting logs in the console.

#### **Debug logs**

|**Log content** |**Description** |
|---|---|
|Crash\-Monitor start successfully! |Crash monitoring module started |
|WatchDog\-Monitor start successfully! |Hang monitoring module started |
|Crash log is uploaded successfully! |Crash logs uploaded |
|Watchdog log is uploading... |Start uploading hang logs |

### Custom error

The custom error module requires the UserException sub\-library. Custom errors depend on custom tracking points. You need to call the APIs manually to record errors occurring in the app and report them to the APMPlus platform for centralized viewing.

#### **Test cases**

The following code will record a custom error log entry, and the SDK will trigger a report every time it records 5 log entries. Network error logs can be recorded automatically by sending a network request that triggers an error. You can refer to the Example project.

```Objective-C
#import <RangersAPMForSDK+UserException.h>
// Get the previously initialized instance. You need to initialize an instance first by referring to the Initialization chapter.
RangersAPMForSDK *sdkMonitor = [RangersAPMForSDK monitorWithSDKID:@"{{sdk_id}}"];

[sdkMonitor trackAllThreadsLogExceptionType:@"testUserException" skippedDepth:0 customParams:@{@"testCustomKey":@"testCustomValue"} filters:@{@"testFilterKey":@"testFilterValue"} callback:^(NSError * _Nullable error){
    NSLog(@"%@",error);
}];
```

#### **Debug logs**

|**Log content** |**Description** |
|---|---|
|UserException\-Monitor start successfully! |Custom error monitoring module started |

### Event analysis

The event analysis module is a custom logging feature that requires you to manually call the API to record events. To use this feature, you need to import the EventMonitor module.

#### **Test cases**

You can record an event using the following code. For related parameters, see the header file documentation.

```Objective-C
#import "RangersAPMForSDK+EventMonitor.h"

// Get the previously initialized instance. You need to initialize an instance first by referring to the Initialization chapter.
RangersAPMForSDK *sdkMonitor = [RangersAPMForSDK monitorWithSDKID:@"{{app_id}}"];

[sdkMonitor trackEvent:@"event_name1"
            metrics:@{@"metric1":@(0)}
            dimension:@{@"dimension1":@"test"}
            extraValue:@{@"extra1":@"extravalue"}];
```

1. An event will only be recorded and reported if it has been created on APMPlus, its status is enabled or under verification, and the client matches the event sampling rules.

2. The Metrics parameter only supports NSDictionary objects where the Key is of type NSString and the Value is of type NSNumber. The Ddimension parameter only supports NSDictionary objects where both the Key and Value are of type NSString. Additionally, neither parameter supports nested structures.

3. Events are not reported immediately after being recorded. The client reporting rules are as follows: A report after the app starts, a report every 120 seconds, and a report when the app state switches to the background.

#### **Debug logs**

|**Log content** |**Description** |
|---|---|
|Record an event\-log successfully, name: |Successfully recorded an event log. The event name is provided in the output. |

### Log retrieval

The log recovery module requires the APMLog sub\-library to be imported. By using the API provided by the SDK for logging, you can record logs generated during an app's runtime. This module is an efficient logging framework based on mmap. The log compression rate is up to 25 times. Combined with cloud control, it can retrieve specified online user logs in real time, helping you efficiently and accurately locate and solve issues.

Not all logs are reported. The methods to obtain these logs are as follows:

* After a crash occurs, the logs generated in the period before the crash are automatically reported.

   The reported logs can be viewed in the custom logs on the crash details page.

* Send a cloud control command to obtain the logs generated by a specified device or user within a specified time range. For more information, see [Retrieval](https://docs.byteplus.com/en/docs/apmplus/Recovery).

#### **Test cases**

A test case is to add sample code to the project and trigger it at an appropriate time to verify whether the SDK can capture the log of the corresponding event. You can see the sample code and description provided by each module, or see [Example project](https://github.com/volcengine/APMInsight_iOS).

For c/c++, Objective\-C, and Swift, APMPlus provides three types of logging APIs. Each type has four APIs: Debug, Info, Warn, and Error, corresponding to the four levels of log severity, which can be filtered when viewing logs on the platform.

```Objective-C
// Regardless of which type of API is used, you need to first call the following API to enable the Alog feature.
// Note: Call only once when the app starts.
#import "RangersAPMForSDK+ALog.h"

RangersAPMForSDK *sdkMonitor = [[RangersAPMForSDK alloc] initWithConfig:sdkConfig];

[sdkMonitor setALogEnabled];  //Enable ALog
[sdkMonitor enableConsoleLog];  // Also print logs in the console



// In Objective-C, you can use the following API for logging
#import "RangersAPMForSDK+ALog.h"

// The first parameter is the SDKID used during initialization
// The second parameter identifies the current log's business, scenario, and other information
// The third parameter is the detailed log information. You can use the format type. If the format type is used, you need to pass in the corresponding parameters
 RANGERSAPM_FORSDK_ALOG_DEBUG(sdkConfig.sdkID, @"Business", @"version : %@", [self version]);  // Debug-type log
 RANGERSAPM_FORSDK_ALOG_INFO(sdkConfig.sdkID, @"Business", @"version : %@", [self version]);   // Info-type log
 RANGERSAPM_FORSDK_ALOG_WARN(sdkConfig.sdkID, @"Business", @"version : %@", [self version]);   // Warn-type log
 RANGERSAPM_FORSDK_ALOG_ERROR(sdkConfig.sdkID, @"Business", @"version : %@", [self version]);   // Error-type log
  
  
  
// In C/C++, you can use the following API for logging
#import "RangersAPM_ForSDK_ALog.h"
 
// The first parameter is the SDKID used during initialization
// The second parameter identifies the current log's business, scenario, and other information
// The third parameter is the detailed log information. You can use the format type. If the format type is used, you need to pass in the corresponding parameters
 RANGERSAPM_FORSDK_ALOG_DEBUG_C([sdkConfig.sdkID UTF8String], "Business", "version : %s", version());
 RANGERSAPM_FORSDK_ALOG_INFO_C([sdkConfig.sdkID UTF8String], "Business", "version : %s", version());
 RANGERSAPM_FORSDK_ALOG_WARN_C([sdkConfig.sdkID UTF8String], "Business", "version : %s", version());
 RANGERSAPM_FORSDK_ALOG_ERROR_C([sdkConfig.sdkID UTF8String], "Business", "version : %s", version());
 
 
 
// In Swift, you can use the following API for logging
#import "RangersAPMForSDK+ALog.h"

// The first parameter is the detailed log information
// The tag identifies the current log's business, scenario, and other information
// fileName is the name of the current file. You can see the example and pass in #file
// funcName is the name of the current method. You can refer to the example and pass in #function
// line is the line number in the current file; you can refer to the example and pass in #line
sdkMonitor.debugALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
sdkMonitor.infoALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
sdkMonitor.warnALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
sdkMonitor.errorALog("alogtest", tag: "Business", fileName: #file, funcName: #function, line: #line)
```

#### **Log description**

After [enabling the debug log](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app#d1e16317), verify whether the module is integrated successfully based on the output log.

|**Log content** |**Description** |
|---|---|
|ALog is uploaded successfully! |(Retrieval) Custom log uploaded |
|Upload ALog failed, reason : |(Retrieval) Failed to upload custom logs. The cause is provided in the output. |
|ALog is uploaded manually! |Manually reported custom logs |
|Manually upload ALog failed |Failed to upload custom logs manually. |
|CloudCommand start successfully! |Retrieval feature started |
|CloudCommand is being executed ... |Executing retrieval command... |
|ALog start successfully! |Custom log feature started |

## (Optional) Step 6: Integrate other features

In addition to common features such as crash, error, and hang analysis, the SDK also supports several enhanced features. You can import sub\-libraries according to business requirements before using these features.

### Custom data

Using the following API, you can add custom environment or business information, such as user email, location information, and business scenarios. This information will be reported together with the SDK logs to help you troubleshoot issues. You can view this information on the **Log details** page.

```Objective-C
#import <RangersAPMForSDK.h>

// Get the previously initialized instance. You need to initialize an instance first by referring to the Initialization chapter.
RangersAPMForSDK *sdkMonitor = [RangersAPMForSDK monitorWithSDKID:@"{{app_id}}"];

//Custom key-value
[sdkMonitor setCustomContextValue:@"sdk1context1value" forKey:@"sdk1context1key"];
```

### Custom dimensions

In addition to reporting custom data, you can also add custom dimensions as needed, which serve as custom filter options for filtering logs in specific situations.

```Objective-C
#import <RangersAPMForSDK.h>

// Get the previously initialized instance. You need to initialize an instance first by referring to the Initialization chapter.
RangersAPMForSDK *sdkMonitor = [RangersAPMForSDK monitorWithSDKID:@"{{app_id}}"];

//Custom filter options
[sdkMonitor setCustomFilterValue:@"sdk1filter1value" forKey:@"sdk1filter1key"];
```

### Consecutive crash protection

Consecutive crash protection requires integrating the SDK's BootingProtectLite module. For details, see [Demo description](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_component_monitoring_SDK#9c4ecfc7). With this feature, you can perform some local handling when the app experiences consecutive crashes, such as clearing caches and deleting files.

```Objective-C
#import <RangersAPMForSDK+BootingProtect.h>

    // Get the previously initialized instance. You need to initialize an instance first by referring to the Initialization chapter.
    RangersAPMForSDK *sdkMonitor = [RangersAPMForSDK monitorWithSDKID:@"{{app_id}}"];
    [sdkMonitor startProtectWithBootingThreshold:10 bootingCrashHandler:^(RangersAPMBootingInfo * _Nonnull info) {
        /**
        Apply protection strategies for scenarios with consecutive exceptions. The demo here only outputs some logs. You can perform local cache clearing or other strategies in your own app. Different strategies can be formulated for different exception counts.
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
    }];
```

### Get device count and user count

* Use APMPlus SDK's own service

   The APMPlus SDK uses the deviceID generated by its own service by default to identify a device and user.

* Use your own DeviceID

   > **tip**

   > If you want to use your own deviceID, the SDK will no longer request its own service to generate a deviceID.

   1. Configure the deviceIDSource of the config when initializing the APMPlus SDK.

   2. Set the deviceID after the APMPlus SDK initialization method.

      ```Objective-C
      #import <RangersAPMForSDK.h>
      
      - (void)init {
          
          RangersAPMForSDKConfig *sdkConfig = [RangersAPMForSDKConfig configWithSDKID:@"{{app_id}}" appToken:@"{{app_token}}"];
          sdkConfig.channel = @"Cocoapods";
          sdkConfig.hostAppID = @"host_app_id"; //Host app identifier
          sdkConfig.sdkVersion = @"1.0.0";
          sdkConfig.deviceIDSource = RAPMDeviceIDSourceFromUser;
         
          RangersAPMForSDK *sdkMonitor = [[RangersAPMForSDK alloc] initWithConfig:sdkConfig];
          
          [sdkMonitor setDeviceID:@"MYDEVICEID"];
      }
      ```
