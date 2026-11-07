---
title: "Use offline plugin to verify data reporting"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_offline_plugin_to_verify_data_reporting"
---

To more intuitively verify the integration status of each feature module, you can use the offline plugin. After the SDK is integrated into the application, the offline plugin can display in the application interface whether each feature module is turned on and whether data is being reported.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This plugin is primarily intended for offline verification; therefore, its performance is not guaranteed. It is recommended that you only turn it on during development verification or internal testing, for validating new module integration and feature regression.</div>


<span id="2e04d598"></span>
## Step 1: Install a plugin


1. In the Podfile, add the following example code. The plugin has requirements for the version of the RangersAPM SDK. For version restrictions, refer to [SDK update log](https://docs.byteplus.com/en/docs/apmplus/SDK_update_log).

   ```Ruby
   source 'https://github.com/volcengine/volcengine-specs.git'
   
   pod 'RangersAPMDoctor', '2.0.0'
   ```
   

2. Run the following command to install the add\-on.

   ```PowerShell
   pod install
   ```
   


<span id="e3d75b96"></span>
## Step 2: Enable plugin

Please call the following method(s) before initializing the performance monitor component; otherwise, it cannot be guaranteed that all features of the performance monitor component can be smoothly verified.

```objectivec
#import <RangersAPM+Doctor.h>

[RangersAPM setDoctorEnabled:YES];
```


<span id="a485cdf3"></span>
## Step 3: Initialize the plugin page

<span id="e3a37a4c"></span>
### Method 1: Initialize the plugin page using a floating window

By initializing the plugin page using this method, you can see a floating window on any page of the application. Click the floating window to enter the data reporting verification interface.

```objectivec
#import <RangersAPM+Doctor.h>

// When using AppDelegate, you can pass nil for windowScene. You can call the initialization method anywhere in the code
[RangersAPM setupWindowWithAppID:@"xxxxxx" windowScene:nil];

// When using SceneDelegate, you need to configure the correct windowScene
- (void)scene:(UIScene *)scene willConnectToSession:(UISceneSession *)session options:(UISceneConnectionOptions *)connectionOptions {
    [RangersAPM setupWindowWithAppID:@"xxxxxx" windowScene:scene];
}
```


<span id="45b31adf"></span>
### Method 2: Initialize the plugin page through an embedded page

By initializing the plugin page using this method, you can embed the plugin page into any page of your application.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The page must be opened using the navigationController pushViewController method; otherwise, secondary pages cannot be displayed properly.</div>


```objectivec
#import <RangersAPM+Doctor.h>

UIViewController *doctorView = [RangersAPM generateViewControllerWithAppID:appID];
[self.navigationController pushViewController:doctorView animated:YES];
```


<span id="d182d0f4"></span>
## Step 4: Use plugins

After initializing the plugin, you can view the debugging page in the plugin. Currently, all verification items are divided into three items. Click each item to enter its respective secondary page:


* Global status detection: Used to detect configurations that may affect data reporting at the global level, for example, deviceID, event volume, and more.

* Performance module detection: Used to monitor data reporting from each feature module, for example, crash, OOM, disk, and so on.

* Event tracking detection: Used to detect the reporting status of custom events created in event analytics.


<span id="919046ff"></span>
### Global status detection

After clicking, you will enter the secondary page, where configurations that may affect global data reporting are displayed. The left side shows parameters, while the right side displays detection results. The detection result button changes color depending on whether it passes: green when passed, and red when not passed.

<span id="98ef8d8d"></span>
### Performance module detection

After clicking, you will enter the second\-level page, which displays the switch status and data reporting status for each performance monitoring module. The module names are shown on the left, while the detection results are shown on the right, including the switch status and reporting status. The detection result button changes color based on whether the check passes: green indicates a pass, and red indicates a failure.

<span id="7ada9214"></span>
### Event instrumentation detection

After clicking, you enter the secondary page, which displays the reporting status for each tracking point. The page presents the information in a list format, with columns from left to right showing the time of the tracking record, the name of the tracking point, and the detection result. The test result button displays different colors depending on whether the test is passed. It shows green when the test is passed and red when it is not.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you do not call the SDK's interface to record tracking points, this page will not display any data. To add tracking points, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#58cb19df">the event analytic</a>.</div>


<span id="dfc76455"></span>
## Step 5: Report a problem

If the information provided by the plugin still does not resolve your access issue, please provide the following materials to technical support to seek assistance:


* Screenshot of the plugin notification messages.

* The network packet capture exported by Charles using Export Session is with the domain apmplus.volces.com.

* The SDK version currently integrated and the list of integrated subspecs.

* The SDK initialization code.


<span id="5e215909"></span>
## FAQ

<span id="f62ab9ee"></span>
### Are there any requirements for the initialization order of plugins and the performance monitor component

Make sure to call the following methods first, before calling other methods of monitoring components and plugins.

```objectivec
#import <RangersAPM+Doctor.h>

[RangersAPM setDoctorEnabled:YES];
```


<span id="9ab9711d"></span>
### Impact on performance after plugin integration?

The performance of the plugin itself is not guaranteed, and after integration, it has a slight impact on the performance monitor component. Therefore, it is recommended that you integrate it only during offline testing or internal testing phases.

<span id="ccf779d5"></span>
### The plugin data update frequency

The plugin refreshes the displayed data on the page every 5 seconds. After a log is recorded, you can wait a moment before viewing it.

<span id="776ed57b"></span>
### Why does the plugin still prompt that the switch is not turned on, even though the switch has already been turned on?

You can check whether a version blocklist has been configured on the SDK setting page.

<span id="ff05c2f0"></span>
### Why does the plugin indicate that data has been reported, but the platform still does not display it?

Data processing on the platform requires a certain amount of time, and reported data is typically processed within 1 to 5 minutes. If you do not see data for an extended period of time, you can provide relevant materials to technical support. For details, refer to [Step 5: Report an issue](https://docs.byteplus.com/en/docs/apmplus/Use_offline_plugin_to_verify_data_reporting#dfc76455).
