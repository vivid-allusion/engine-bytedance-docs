---
title: "macOS (Swift)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1108915"
---

The Quick Start Demo is an open source sample project file with basic RTC functions provided by BytePlus RTC. With this project file, you can quickly build an application for the hand\-on experience of BytePlus RTC. You can also refer to the code for best practices of basic RTC calls.

RTC provides an SDK for macOS. The APIs in the SDK are Objective\-C APIs.

Follow the instructions to build an application with the demo project.

<span id="prerequisites"></span>
## Prerequisites


* Installed Xcode 13.0+.

* Tested on a physical device with macOS 10.10+ system. (Some of the functions may fail on emulators.)

* Got a valid [AppleID](http://appleid.apple.com/).

* Got [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793).

* Installed CocoaPods.


<span id="operation-steps"></span>
## Operation Steps

<span id="step-1-configure-the-demo-project-file"></span>
### Step 1. Configure the Demo Project File


1. Change the working directory to the root directory of `QuickStartSwift_Demo`, and generate `QuickStartSwift.xcworkspace` with the command `pod install`. Open the project with Xcode.

2. Fill in the fields of `AppID` and `TOKEN` in file `QuickStartSwift.Constants` with the value you get from the console.

> See [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) and [Using Token for Authentication](https://docs.byteplus.com/en/docs/12/docs-70121#generate-temporary-token) for more information on getting RTC AppID and temporary token.


<span id="step-2-configure-the-developer-certificate"></span>
### Step 2. Configure the Developer Certificate


1. Log in with your Apple ID.

   1. Select **Xcode** \> **Preferences**.

   2. Add **Accounts** with your Apple ID.

2. Configure the developer certificate for the project.

   1. Select **Signing & Capabilities**.

   2. Select **Automatically manage signing** or manually configure and download the certificate at [https://developer.apple.com/ ](https://developer.apple.com/).

   3. Select **Personal Team**.

   4. Replace the default `com.ss.rtc.demo.quickstart.dev` in the Bundle Identifier with your Bundle ID. The format should start with `com.`.


<span id="step-3-compile-and-run-the-demo-project-file"></span>
### Step 3. Compile and Run the Demo Project File


1. Run the project.

2. Start the demo, type in your RoomID and UserID, and select **Enter Room**.

3. Grant the permissions to enable the camera and the microphone.


<span id="usage-instructions"></span>
## Usage Instructions

After building an application with the project, you can use the application for RTC calls.

You and your colleagues must use the same AppID and join the same room to make a successful RTC call.

<span id="experience-rtc-features"></span>
## Experience RTC Features

To test all RTC features, invite a friend to run the sample project on another device. Make sure you both use the same AppID and TOKEN. After two devices join the same room, you can make audio and video calls to each other.

<span id="follow-up-steps"></span>
## Follow\-up Steps

After trying this demo, read the following documents to learn more:


* In test or production environments, you need to use a Token for authentication. To ensure communication security, we recommend obtaining the token from your server. For details, please refer to [Complete Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, please refer to [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).


<span id="frequently-asked-questions"></span>
## Frequently Asked Questions

<span id="q1"></span>
### Q1

Q: After the Quick Start Demo runs successfully, if test devices are too close to each other, howling will occur.

A: If the test devices are in the same room and audio is enabled, near\-field howling occurs when the serial gain is greater than 1. This is not a bug in the demo. Keep the test devices at a distance from each other.

<span id="q2"></span>
### Q2

Q: Error messages appear while running the demo.

A: Internal error of the SDK. For details about error codes, please refer to [Error Code](https://docs.byteplus.com/en/docs/12/docs-70091#bytertcerrorcode).
