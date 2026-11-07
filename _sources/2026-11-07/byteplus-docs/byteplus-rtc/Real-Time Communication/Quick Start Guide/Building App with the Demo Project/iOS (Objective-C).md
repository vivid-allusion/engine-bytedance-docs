---
title: "iOS (Objective-C)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70128"
---

BytePlus RTC provides an open source sample project file with basic RTC functions. With this project file, you can quickly build an application for the hand\-on experience of BytePlus RTC.

<span id="prerequisites"></span>
## Prerequisites


* System requirements:

   * Xcode 14.0 or higher

   * CocoaPods 1.10.0 or higher

   * A physical mobile device that runs iOS 13.0 or higher.

* Create an access key for the account, and obtain the Access Key ID (AK) and Secret Access Key (SK). [How to create an access key?](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey)

* Activate the BytePlus RTC service, create a RTC app and obtain the AppId and AppKey. See details in [Before Using RTC Service](https://docs.byteplus.com/docs/byteplus-rtc/docs-69865).


<span id="procedures"></span>
## Procedures

<span id="step-1-cloning-the-project"></span>
### Step 1: Cloning the project


1. Go to GitHub and clone the [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) repository.

2. Open Terminal, and change the current directory to `Client/iOS`, which is the root directory of the project.

3. Move the license files that you have acquired in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-rtc/docs-70128#Prerequisites) section to the `Component/AppConfig/License` directory. You may need to rename the license files if you have several licenses with the same file name.

4. Run `pod install` to install dependencies.


<span id="step-2-modify-the-configuration-file"></span>
### Step 2: Modify the configuration file


1. Under the root directory of the project, open the `VideoOne.xcworkspace` file in Xcode.

   Set the app server.

2. In Xcode, navigate to `Pods/Development Pods/AppConfig` and open the `BuildConfig.h` file. Configure the following fields with the values you obtained in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-rtc/docs-70128#prerequisites) section. The information is used for authentication when the client communicates with the BytePlus RTC service.



|Field name |Description |Example |
|---|---|---|
|ServerUrl |Specify the address of your app server. |You can use the app server provided by BytePlus: `https://videocloud.byteplusapi.com/videoone_opensource` |
|RTCAPPID |The **AppId** of your BytePlus RTC app. |123456\*\*\*\*\*\*\*\*3deb567a86 |
|RTCAPPKey |The **AppKey** of your BytePlus RTC app. |1bfaa8e\*\*\*\*\*\*\*\*fjb6j6hhde68c07d |
|AccessKeyID |The **Access Key ID (AK)**  of your BytePlus account. |AKAPZ7\*\*\*\*\*\*\*\*FLB0D38CM8DK49SO39D83KD820DFK4k9 |
|SecretAccessKey |The **Secret Access Key (SK)**  of your BytePlus account. |8dk39vK\*\*\*\*\*\*\*\*k7D93KDHS8DJSLud830DJEO37EI3UDK37WODKu3oQ |


<span id="step-3-compiling-the-project"></span>
### Step 3: Compiling the project


1. Connect the mobile device to your computer, and set it as the target device in Xcode.

2. Click **Product** \> **Run** to initiate the compilation process.


<span id="step-4-trying-the-app"></span>
### Step 4: Try the app

If compilation succeeds, the VideoOne app is installed on your device and opens to the login screen. Log into the app with your email and then start exploring the different scenarios and functions in the app.

> If you are using a free Apple developer account, you may need to adjust the settings on your mobile device to allow apps from untrusted developers. In most cases, you can go to **Settings** \> **General** \> **Device Management** to configure this setting.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d3018959d2c79e96cbf53b48048b56af.png) </span>
