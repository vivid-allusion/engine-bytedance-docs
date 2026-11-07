---
title: "Running VeLiveQuickStartDemo for Android"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android"
---

BytePlus MediaLive VeLiveQuickStartDemo is designed to help you get started with developing a mobile app using the BytePlus MediaLive SDKs for Android and iOS. With simple UI design, it allows you to quickly understand the core code logic for implementing the key features offered by the SDKs.

VeLiveQuickStartDemo contains three types of features:


* Basic features, including push\-pull streaming.

* Advanced features, including:

   * Adaptive bitrate

   * Pushing external audio and video sources

   * H.265 hardware encoding

   * Picture\-in\-Picture (PiP)

* Interactive live features, including co\-hosting with audience members and host PK battle.


This article provides a comprehensive guide on how to run VeLiveQuickStartDemo for Android.

<span id="e42b27e5"></span>
## System requirements


* Android 5.0 (SDK API Level 21) or higher

* Android Studio 4.0 or higher

* A physical Android device running Android 5.0 or higher

* Ensure the CPU architecture that you use is armeabi\-v7a or arm64\-v8a


<span id="d1ed29bd"></span>
## Prerequisites

Complete the following tasks before you start:


* Sign up for a BytePlus account. For detailed instructions, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Activate the BytePlus MediaLive service and add domain names for push\-pull streaming through the console. Refer to [Getting started with BytePlus MediaLive](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started) for detailed instructions.

* If you want to experience interactive live features, you also need to enable the BytePlus RTC service. You can find detailed instructions in [enable RTC service](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865).


<span id="8c0e37b0"></span>
## Preparations

You need to prepare an SDK license, an App ID, and token information before you run the demo.

<span id="0706aa76"></span>
### **Downloading a MediaLive license**

Follow the instructions in [SDK management](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) to create an SDK application and then download the corresponding SDK license. Note down the App ID and package name as you will need them in future steps.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab6a8e0a0518458bbc61967cbc9e88cb~tplv-goo7wpa0wc-image.image) </span>

<span id="9ae537a8"></span>
### **Acquiring an RTC App ID and App Key**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you do not want to experience interactive live features, you can skip this section.</div>



1. Log in to the [BytePlus RTC console.](https://console.byteplus.com/rtc/workplaceRTC)

2. In the left navigation pane, click **Application Management**.

3. Click **Create an App** and enter your app name in the dialog box that opens. Leave the **Affiliated project** field at the default value.

4. Click **OK** to save the settings.

5. Locate your application in the application list and take note of your App ID and App Key.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b565075eda70420d85d70cc7cc950223~tplv-goo7wpa0wc-image.image) </span>


<span id="b01ced66"></span>
## Running the demo

This section introduces the detailed steps for setting up and running the demo.

<span id="30f72781"></span>
### Downloading the source code


1. Go to GitHub and clone the [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git) repository.

2. The directory tree of the demo is as follows:


```Plain
Android/VeLiveQuickStartDemo/app/src/main/java/com/ttsdk/quickstart
├── app // Entry point of the demo app
├── features // Features
│   ├── basic // Basic features
│   │   ├── PullStreamActivity.java // pull streaming
│   │   └── PushCameraActivity.java // Video capture and push streaming
│   ├── advanced // Advanced features
│   │   ├── PictureInPictureActivity.java // Picture-in-Picture
│   │   ├── PushAutoBitrateActivity.java // Adaptive bitrate
│   │   ├── PushBeautyActivity.java // Beauty AR and special effects
│   │   ├── PushCustomActivity.java // Pushing external audio and video sources
│   │   ├── PushH265CodecActivity.java // H.265 hardware encoding
│   │   └── PullRTMActivity.java // Pulling an RTM stream
│   └── interact // Interactive live features
│       ├── link // Co-hosting with audience members
│       ├── manager // Common host and audience activities
│       └── pk // Host PK battle
└── helper // Utilities, such as SDK initialization and external video capture
```


<span id="743d56e6"></span>
### Integrating the SDK license


1. Rename the MediaLive SDK license you have downloaded as `ttsdk.lic`.

2. Replace the original `ttsdk.lic` file in the `Android/VeLiveQuickStartDemo/app/src/main/assets/`directory with your own SDK license.


<span id="e7a73684"></span>
### Gradle sync


1. Open `Android/VeLiveQuickStartDemo` in Android Studio.

2. Click **Sync Project with Gradle Files** to sync the project with the Gradle files.


<span id="77e37fbf"></span>
### Configuring push\-pull streaming


1. In Android Studio, navigate to `app/src/main/java/com.ttsdk.quickstart/helper` and open the `VeLiveSDKHelper.java` file.

2. Enter the App ID, License file name,domain name space, push\-pull streaming domain name, and app name for live streaming.

   ```Java
   // The App ID
   public static String TTSDK_APP_ID = "536110";
   
   // License File Name. If you replace the License File, you need to modify the file name here. If you want to do a quick SDK verification, you can directly replace the content of the original License File (ttsdk.lic).
   public static String TTSDK_LICENSE_NAME = "ttsdk.lic";
   
   // Configure the AccessKey ID and AccessKey secret, which are used for API request authentication.
   public static String ACCESS_KEY_ID = "";
   public static String SECRET_ACCESS_KEY = "";
   
   // The Domain name space
   public static String LIVE_VHOST = "push.example.com";
       
   /* 
   * Example of push-pull streaming address composition: https://{Domain}/{AppName}/{StreamName}.flv
   * Configure the AppName used in the push-pull streaming address, which supports uppercase and lowercase letters, numbers, underscores, and hyphens, with a maximum length of 30 characters. Here is an example: live
   */
   public static String LIVE_APP_NAME = "live";
   
   // Configure the push streaming domain name
   public static String LIVE_PUSH_DOMAIN = "push.example.com";
   
   // Configure the pull streaming domain name
   public static String LIVE_PULL_DOMAIN = "pull.example.com";
   ```
   


<span id="5609c16c"></span>
### Configuring co\-hosting and host PK battle


1. In Android Studio, open the `app/src/main/java/com.ttsdk.quickstart/helper/VeLiveSDKHelper.java` file.

2. Enter the RTC App ID and App Key.

   ```Java
   // The RTC App ID
   public static String RTC_APPID ="";   
   // The RTC App Key
   public static String RTC_APPKEY ="";    
   ```
   


<span id="3c9d8600"></span>
### Configuring the package name


1. In Android Studio, open the `app/build.gradle` file.

2. Set `applicationId` to the package name you used when creating your SDK application in the [Downloading a MediaLive license](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android#0706aa76) section.


<span id="67945fc7"></span>
### Compiling the demo


1. Connect the physical Android device you have prepared in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android#d1ed29bd) section to your computer, and set it as the target device in Android Studio.

2. Click the **Run** button to initiate the compilation process.


If the compilation process completes without any errors, the demo app will be installed on the connected mobile device.
