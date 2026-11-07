---
title: "Running VeLiveQuickStartDemo for iOS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios"
---

BytePlus MediaLive VeLiveQuickStartDemo is designed to help you get started with developing a mobile app using the BytePlus MediaLive SDKs for Android and iOS. With simple UI design, it allows you to quickly understand the core code logic for implementing the key features offered by the SDK.

VeLiveQuickStartDemo contains three types of features:


* Basic features, including push\-pull streaming.

* Advanced features, including:

   * Adaptive bitrate

   * Pushing external audio and video sources

   * H.265 hardware encoding

   * Picture\-in\-Picture (PiP)

* Interactive live features, including co\-hosting with audience members and host PK battle.


This article provides a comprehensive guide on how to run VeLiveQuickStartDemo for iOS.

<span id="208fe723"></span>
## System requirements


* Xcode 14.0 or higher

* CocoaPods 1.11.3 or higher

* A physical iOS device running iOS 11.0 or higher

* A development provisioning profile


<span id="4cff3e13"></span>
## Prerequisites

Complete the following tasks before you start:


* Sign up for a BytePlus account. For detailed instructions, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Activate the BytePlus MediaLive service and add domain names for pull streaming and push streaming through the console. Refer to [Getting started with BytePlus MediaLive](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started) for detailed instructions.

* If you want to experience interactive live features, you also need to enable the BytePlus RTC service. You can find detailed instructions in [enable RTC service](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865).


<span id="99cadc58"></span>
## Preparations

You need to prepare an SDK license, an App ID, and token information before you run the demo.

<span id="96bcd67f"></span>
### Configuring the accelerated domain


1. Log in to the [BytePlus MediaLive console.](https://console.byteplus.com/live)

2. In the left navigation pane, click **Domains**.

3. Add the domain for push\-pull streaming.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dec0195bac047c384081882dfec2e64~tplv-goo7wpa0wc-image.image) </span>

<span id="9dacd3e8"></span>
### **Downloading a MediaLive license**

Follow the instructions in [SDK management](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) to create an SDK application and then download the corresponding SDK license. Note down the App ID and bundle ID as you will need them in future steps.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bea7ca3024e46998c225be78e7dff60~tplv-goo7wpa0wc-image.image) </span>

<span id="9377cabf"></span>
### **Acquiring an RTC App ID and token**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you do not want to experience interactive live features, you can skip this section.</div>



1. Log in to the [BytePlus RTC console.](https://console.byteplus.com/rtc/workplaceRTC)

2. In the left navigation pane, click **Application Management**.

3. Click **Create an App** and enter your app name in the dialog box that opens. Leave the **Affiliated project** field at the default value.

4. Click **OK** to save the settings.

5. Locate your application in the application list and take note of your App ID and App Key.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b565075eda70420d85d70cc7cc950223~tplv-goo7wpa0wc-image.image) </span>


<span id="abc77f0b"></span>
## Running the demo

This section introduces the detailed steps for setting up and running the demo.

<span id="619e2c8e"></span>
### Downloading the source code


1. Go to GitHub and clone the [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git) repository.

2. The directory tree of the demo is as follows:


```Bash
iOS/VeLiveQuickStartDemo
└── VeLiveQuickStartDemo
    ├── App // Entry point of the demo app
    ├── Features // Features
    │   ├── Basic // Basic features
    │   │   ├── PullStream // pull streaming
    │   │   └── PushCamera // Video capture and push streaming
    │   ├── Advanced // Advanced features
    │   │   ├── PullRTM // Pulling an RTM stream
    │   │   ├── PushAutoBitrate // Adaptive bitrate
    │   │   ├── PushBeauty // Beauty AR and special effects
    │   │   ├── PushCustom // Pushing external audio and video sources
    │   │   ├── PushH265Codec // H.265 hardware encoding
    │   │   ├── PictureInPicture // Picture-in-Picture
    │   │   └── ScreenCapture // Push streaming of mobile screen recording
    │   └── Interact // Interactive live features
    │       ├── Link // Co-hosting with audience members
    │       ├── Manager // Common host and audience activities
    │       └── PK // Host PK battle
    ├── Helper // Utilities, such as SDK initialization and external video capture
```


<span id="6febb740"></span>
### Integrating the SDK license


1. Rename the MediaLive SDK license you have downloaded as `ttsdk.lic`.

2. Replace the original `ttsdk.lic` file in the `iOS/VeLiveQuickStartDemo/VeLiveQuickStartDemo/Resource/` directory with your own SDK license.


<span id="055049ad"></span>
### Updating the Cocoapods repository


1. Open Terminal and change the current directory to `iOS/VeLiveQuickStartDemo`.

2. Run `pod install --repo-update` to update the local Cocoapods repository clone and install the project dependencies.


<span id="817a8f22"></span>
### Configuring push\-pull streaming


1. Under the root directory of the project, open the `VeLiveQuickStartDemo.xcworkspace` file in Xcode.

2. Within the project tree view, navigate to `VeLiveQuickStartDemo/Helper` and open the `VeLiveSDKHelper.h` file.

3. Enter the App ID, License file name,domain name space, push\-pull streaming domain name, and app name for live streaming.

   ```Java
   // The App ID 
   #define TTSDK_APP_ID @"536110"
   
   // License File Name. If you replace the License File, you need to modify the file name here. If you want to do a quick SDK verification, you can directly replace the content of the original License File (ttsdk.lic).
   #define TTSDK_LICENSE_NAME @"ttsdk.lic"
   
   // Configure the AccessKey ID and AccessKey secret, which are used for API request authentication.
   #define ACCESS_KEY_ID @""
   #define SECRET_ACCESS_KEY @""
   
   // The Domain name space
   #define LIVE_VHOST @"push.example.com"
   
   /* 
   * Example of push-pull streaming address composition: https://{Domain}/{AppName}/{StreamName}.flv
   * Configure the AppName used in the push-pull streaming address, which supports uppercase and lowercase letters, numbers, underscores, and hyphens, with a maximum length of 30 characters. Here is an example: live
   */
   #define LIVE_APP_NAME @"live"
   
   // Configure the push streaming domain name
   #define LIVE_PUSH_DOMAIN @"push.example.com"
   
   // Configure the pull streaming domain name
   #define LIVE_PULL_DOMAIN @"pull.example.com"
   ```
   


<span id="ca1f9885"></span>
### Configuring co\-hosting and host PK battle


1. In Xcode, open the `VeLiveQuickStartDemo/Helper/VeLiveSDKHelper.h` file.

2. Enter the RTC App ID and App Key.


```Java
// The RTC App ID
#define RTC_APPID @""

// The RTC App Key
#define RTC_APPKEY @""
```


<span id="fa7c2a86"></span>
### Configuring the project


1. In the project editor in Xcode, choose the target.

2. Click **Signing & Capabilities**.

3. Set **Bundle Identifier** to the one you have prepared in the [Downloading a MediaLive license](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios#9dacd3e8) section.

4. Select a development provisioning profile.


<span id="36503b02"></span>
### Configuring the Bundle ID


1. Open the `VeLiveQuickStartDemo/VeLiveQuickStartDemo.xcworkspace` .

2. Modify the configuration file Podfile to enable or disable the screen recording push stream. If this variable is modified, pod install needs to be re\-executed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/797eb2573d214d16b54cd219d1c99b98~tplv-goo7wpa0wc-image.image) </span>

3. Modify the Bundle Identifier and GroupID configuration of the main project App and the screen recording push streaming extension.

   1. Modify the Bundle Identifier of the main project App to the Bundle ID filled in when creating the live video application.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0db405f62f804ed09064860e242007dd~tplv-goo7wpa0wc-image.image) </span>

   2. Modify the Bundle Identifier of the screen recording push streaming Extension. This Bundle Identifier must be prefixed with the Bundle Identifier of the App. If screen recording push streaming is disabled, you may skip this step.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b20ab98536c44e79fba177d165090ef~tplv-goo7wpa0wc-image.image) </span>

   3. Modify the GroupID configuration. If the screen recording push streaming function is not enabled, this step can be ignored.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6bee18d237a4a36b128947b50b1ff63~tplv-goo7wpa0wc-image.image) </span>

4. Select the developer signing file (Provisioning Profile) of the main project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27fb2efe3b704291bdb9f9cfde43c237~tplv-goo7wpa0wc-image.image) </span>

5. Select the developer signing file (Provisioning Profile) of the screen recording push streaming Extension. If the screen recording push streaming function is not enabled, please ignore this step.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b590d748ec32437a9d8b55203e108af4~tplv-goo7wpa0wc-image.image) </span>


<span id="6e1c77df"></span>
### Compiling the demo


1. Connect the physical iOS device you have prepared in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios#4cff3e13) section to your computer, and set it as the target device in Xcode.

2. Click the **Run** button to initiate the compilation process.


If the compilation process completes without any errors, the demo app will be installed on the connected mobile device.
