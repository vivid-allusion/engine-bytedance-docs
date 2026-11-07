---
title: "Scan the Code to Enter the Device ID"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Scan-the-Code-to-Enter-the-Device-ID"
---

In some scenarios where the user ID needs to be entered manually, such as filling in a whitelist, the manually entered UUID and SSID numbers are long (eg: ssid = "a0166a58\-137a\-410c\-1111\-04acc905\*\*\*\*"), which is prone to errors and inconvenient. Therefore, for mobile applications (iOS, Android), DataTester supports entering the corresponding ID by scanning the QR code. This article introduces the key points of scanning code to enter ID.

<span id="dff1fda2"></span>
# Precondition


* Currently only mobile end App (iOS, Android) scan code to enter ID is supported. WeChat Mini Program, Web/H5/WAP are not supported.

* Application integration data access SDK version requirements: 5.2.0 and above versions of iOS SDK, Android SDK.

* For the device mobile phone to be entered with ID, install the APP downloaded from the app store, and the APP has integrated the SDK that meets the version requirements.


<span id="f609972d"></span>
# Operation entrance

<span id="044dfaba"></span>
## User Testing Whitelist \- Create a Whitelist

In the Global Settings \> Audience Settings \> User Test Whitelist page, click "+ Test Whitelist", as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abc481b7a7eb4bef80541f6fe0562c27~tplv-goo7wpa0wc-image.image) </span>

<span id="8e7418a2"></span>
## 2. Create an experiment \- select a target audience \- add a whitelist

When **creating an experiment** \- **configuring an experimental version** \- **adding a test user**, click the icon "Scan QR code entry" to scan the code entry, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9b8a541c7d34414bc35a1c2a090f42b~tplv-goo7wpa0wc-image.image) </span>

<span id="2787a84c"></span>
# Operation process


1. Through the above operation entrance, open the scan code to obtain the SSID pop\-up page.

2. Use the mobile app (such as WeChat, Alipay, etc.) to scan the QR code, enter the scan code success page, and click "Open in browser" in the upper right corner of the page.

3. Enter the browser H5 page and click "Open App and Get UUID/SSID".

4. Check whether the UUID/SSID of the device is synchronized in the "UUID/SSID text box" on the Create Whitelist page or scan the code to get the UUID/SSID page.


Regarding the "UUID/SSID" above, when the customer accesses the application, they will determine which type of ID the user uses, so they need to display the corresponding UUID or SSID according to the ID of the current application.

<span id="1a2daaaa"></span>
# Failed to obtain ID, independent investigation guidance

If you cannot obtain the "UUID/SSID", you can check it according to the following process:

<span id="05993122"></span>
## 1. Please check that the correct version of the App is installed on the mobile phone.

<span id="78fdfd22"></span>
## 2. Confirm that the correct application information is used when initializing the SDK.

<span id="61b00361"></span>
### Android

```Plain
final InitConfig config = new InitConfig("2174","【您的App渠道号】"); //your App channel code

config.setAutoStart(true);
config.setUriConfig(UriConfig.DEFAULT);
config.setPicker(new Picker(this, config));
config.setAbEnable(true);  // start ABTest
AppLog.init(this, config);
```


<span id="db4f89c9"></span>
### iOS

Please initialize the configuration when the app is launched (if the configuration is initialized after the page is displayed, some event collection will be missing).

```Plain
#import <RangersAppLog/BDAutoTrack.h>
#import <RangersAppLog/BDAutoTrackConfig.h>
#import <RangersAppLog/BDAutoTrackURLHostItemCN.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
      
    /* Initialization begins */
    BDAutoTrackConfig*config =[BDAutoTrackConfig configWithAppID:@"appid"]; //You are applying for an APPID. If you are unsure, please contact the dedicated customer manager
    config.serviceVendor = BDAutoTrackServiceVendorCN; //data reporting

    config.appName = @"your appName";  It is the same as app_name when you applying for APPID
    config.channel = @"App Store"; // For iOS, the default is App Store
    
    config.abEnable = YES; //enable AB testing, the default is YES
    config.showDebugLog = NO; // Whether to output logs on the console for debugging purposes only, and also set up the logger. Please set the release version to NO.
    //config.logger = ^(NSString * _Nullable log) {NSLog(@"%@",log);}; //if showDebugLog is set to YES, please open the first note of this line.
    config.logNeedEncrypt = YES; // Whether encrypt log, the default is yes. Please set to YES for release version.
    config.autoTrackEnabled = YES; //Whether enable full event tracking collection for Circle Feature.
    
    [BDAutoTrack startTrackWithConfig:config];
    /* Initialization ends */  
}
```


swift：

```Plain
import RangersAppLog

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        
        let config = BDAutoTrackConfig(appID: "your appID") // If you are unsure, please contact the dedicated customer manager
        config.appName = "your app name" // It is the same as app_name when you applying for APPID
        config.serviceVendor = BDAutoTrackServiceVendorCN; //data reporting
        config.channel = "App Store" // For iOS, the default is App Store
        config.showDebugLog = false // Whether to output logs on the console for debugging purposes only, and also set up the logger. Please set the release version to false.
       //config.logger = { (log) inprint(log ?? "log is nil")} // If you set showDebugLog = true, please open the first note of this line.
        config.logNeedEncrypt = true // Whether encrypt log, the default is yes. Please set to true for release version.
        config.autoTrackEnabled = true //Whether enable full event tracking collection for Circle Feature.
        
        BDAutoTrack.start(with: config)
                
        return true
    }
```


<span id="f186c1d8"></span>
## 3. Make sure the URL Scheme is set correctly

<span id="7ddb5623"></span>
### Android

In the build.gradle at the module level, add the url scheme:

```Plain
// add in the defaultConfig of Android
manifestPlaceholders.put("APPLOG_SCHEME", "".toLowerCase())
```


<span id="41608c00"></span>
### iOS

Find the URL Scheme in the application information:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3fc47667b264d36bad9a4f9df2f3863~tplv-goo7wpa0wc-image.image) </span>

Add the URL Scheme to your project:

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/05c8d79157234ccdb322d456e96daf29~tplv-em5hxbkur4-noop.image?width=1816&height=746) </span>

If iOS 13, override the UISceneDelegate callback method:

```objc
#import <RangersAppLog/BDAutoTrackSchemeHandler.h>

- (void)scene:(UIScene *)scene openURLContexts:(NSSet<UIOpenURLContext *> *)URLContexts {
    for (UIOpenURLContext *context in URLContexts) {
        NSURL *URL = context.URL;
        if ([[BDAutoTrackSchemeHandler sharedHandler] handleURL:URL appID:@"appid" scene:scene]) {
            continue;
        }

        /// ……
    }
}
```


Swift：

```swift
import RangersAppLog

func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {  
    if(BDAutoTrackSchemeHandler.shared().handle(url, appID: "appid", scene: nil)) {
       return true
    }      
    return false
}
```


If iOS version is lower than 13, override UIApplicationDelegate callback method

```objc
#import <RangersAppLog/BDAutoTrackSchemeHandler.h>

- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey, id> *)options {
    if ([[BDAutoTrackSchemeHandler sharedHandler] handleURL:url appID:@"appid" scene:nil]) {
        return YES;
    }
    /// ……
    return NO;
}
```


<span id="bec80df7"></span>
## 4. Confirm SDK version ≥ 5.2.0

<span id="90ace0b4"></span>
### Android

In the project\-level build.gradle, add the reference:

```Plain
// add in dependencies of buildscript
classpath 'com.bytedance.applog:RangersAppLog-All-plugin:5.2.0'
```


In the build.gradle at the module level, add the reference:

```Plain
// add at the beginning of the file
apply plugin: 'com.bytedance.std.tracker'
```


and

```Plain
// add in dependencies
implementation 'com.bytedance.applog:RangersAppLog-All-cn:5.2.0'

// To comply with GDPR, please change to
// implementation 'com.bytedance.applog:RangersAppLog-All-global:5.2.0'
```


<span id="4bf71036"></span>
### iOS

In the Podfile, confirm that the integration version is ≥ 5.2.0 and that the selected sublibrary contains'Picker ',' UITracker'.
