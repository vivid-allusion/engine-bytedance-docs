---
title: "iOS APPExtension SDK integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_iOS_APPExtension_SDK"
---

The RUM iOS APPExtension SDK is non\-intrusive. This topic introduces the detailed integration steps for the iOS APPExtension SDK.

> **warning**

* > The iOS APPExtension SDK is restricted to use in the Chinese mainland (excluding Hong Kong, Macau, and Taiwan regions).

* > The iOS APPExtension SDK only supports the crash analysis feature.

* > Calling the SDK initialization API does not collect user information. Calling the SDK startup API will begin collecting user information. Ensure that user authorization has been obtained before collecting user information according to [SDK privacy policy](https://docs.byteplus.com/en/docs/apmplus/The_SDK_privacy_policy).

## Prerequisites

iOS APPExtension performance monitoring depends on Host APP performance monitoring. For details, see [iOS SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

> **warning**

> The initialization code requires configuration of the groupID attribute of the RangersAPMConfig object, with the value being the same APP GroupID as the extension program.

```Objective-C
#import <RangersAPM.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
    apmConfig.channel = @"App Store";
    apmConfig.groupID = @"{{groupID}}";
    [RangersAPM startWithConfig:apmConfig];
  
    return YES;
}
```

## Step 1: Obtain the SDK package

1. Add the following code under the "target" of the extension in the Podfile.

   ```Ruby
   source 'https://github.com/volcengine/volcengine-specs.git'
   pod 'RangersAPMForExtension', '1.0.5'
   ```

2. Execute the following command to install the SDK.

   ```PowerShell
   pod install
   ```

## Step 2: Initialization

Add the following initialization code at an appropriate time during the extension's lifecycle (after the user agrees to the privacy policy).

```Objective-C
// First add app Groups in Capability, then modify the groupID
RangersAPMForAPPExtensionConfig *extensionConfig = [RangersAPMForAPPExtensionConfig configWithAppID:@"{{app_id}}" groupID:@"{{groupID}}"]; 
```

## Step 3: Start the SDK and enable data collection

Add the following startup code at an appropriate time during the extension's lifecycle (after the user agrees to the privacy policy). extensionConfig is the configuration generated during initialization.

```Objective-C
[RangersAPMForAPPExtension startWithConfig:extensionConfig];
```

> **warning**

> The SDK start code is only effective on the first call.

## Step 4: Verify data reporting

You can check whether each module has been successfully integrated by comparing it with the descriptions of the following modules, as needed.

### Enable debug logs

After enabling the Debug log output feature, the SDK will output logs to the Xcode console for key events, such as successful initialization and reporting, helping you verify the SDK integration and reporting.

Example code for enabling Debug log output:

```Objective-C
#import <RangersAPMForAPPExtension.h>

[RangersAPMForAPPExtension allowDebugLogUsingLogger:^(NSString * _Nonnull log) {
      NSLog(@"APMPlus Debug Log : %@", log);
}];
```

* Supports customizing the log output format by modifying the block.

   The following example code shows the default internal output format of the SDK. If nil is passed in, the SDK will use the default format to output logs.

   ```Objective-C
   [RangersAPMForAPPExtension allowDebugLogUsingLogger:nil];
   ```

* Please initialize the following example code before the RangersAPM start method. Otherwise, logs may not be output for some synchronous events.

   ```Objective-C
   #if DEBUG
   [RangersAPMForAPPExtension allowDebugLogUsingLogger:^(NSString * _Nonnull log) {
       NSLog(@"APMPlus : %@", log);
   }];
   #endif
   
   [RangersAPMForAPPExtension startWithGroupID:@"{{groupID}}" forAppID:@"{{app_id}}"];  // Enable the debug logs before this code
   ```

### Crash analysis

#### Test cases

Through test cases, you can verify whether the SDK functions are correctly enabled. You can add test cases in your code yourself.

The following code will trigger a crash of the NSException type. For more types, see [Example project](https://github.com/volcengine/APMInsight_iOS).

```Objective-C
NSArray *array = [NSArray array];
[array objectAtIndex:10];
```

1. Change the Build Configuration to Release in Xcode, then install the Host APP to the simulator or a real device via Run.

2. Open the extension program in the simulator or on a real device, then wait for the crash code to execute. The extension program will crash (flash exit).

   > **warning**

   > Do not start the extension program directly via Xcode Run. Crashes triggered this way cannot be captured.

3. Starting the Host APP will immediately report the crashes that occurred in the Host APP and the extension program during the previous launch.

   You can start the APP via Xcode Run and see the reported logs in the console.

#### Debug logs

After [enabling the debug logs](https://docs.byteplus.com/en/docs/apmplus/Integrate_iOS_APPExtension_SDK#18ada565), verify whether the module is successfully integrated based on the output logs.

|**Log content** |**Description** |
|---|---|
|Crash\-Monitor start successfully! |Crash monitoring module started |
