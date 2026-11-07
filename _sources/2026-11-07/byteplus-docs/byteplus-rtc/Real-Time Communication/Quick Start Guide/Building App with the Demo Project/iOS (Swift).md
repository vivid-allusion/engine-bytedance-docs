---
title: "iOS (Swift)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-517557"
---

To quickly experience the basic real\-time communication (RTC) functions of BytePlus RTC on iOS, you can use this open\-source Swift demo project. This guide provides step\-by\-step instructions to help you build and run a sample application, giving you a hands\-on experience and a code reference for best practices.

RTC provides SDK for iOS. The APIs in the SDK are Objective\-C APIs. You can easily integrate the SDK in your Swift project for real\-time media communication.

Follow the instructions to build an application with the demo project.

<span id="prerequisites"></span>
## Prerequisites


* Installed Xcode 13.0+.

* A physical device running iOS 12.0 or later.

* A valid Apple ID.

* Got [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793).


<span id="operation-steps"></span>
## Operation Steps

<span id="step-1-configure-the-demo-project-file"></span>
### Step 1. Configure the Demo Project File


1. Change working directory to the root directory of `QuickStartSwift_Demo`, and generate `QuickStartSwift.xcworkspace` with the command `pod install`. Open the project with Xcode.

2. Fill in the fields of `AppID` and `TOKEN` in the `QuickStartSwift_Demo/Constants.swift` file with the value you get from the console.

> See [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) and [Using Token for Authentication](https://docs.byteplus.com/en/docs/12/docs-70121#generate-temporary-token) for more information on getting RTC AppID and temporary token.


<span id="step-2-configure-the-developer-certificate"></span>
### Step 2. Configure the Developer Certificate


1. Log in with your Apple ID.

   1. In Xcode, select **Xcode** \> **Preferences**.

   2. Add **Accounts** with your Apple ID.

2. Configure the developer certificate for the project.

   1. Select **Signing & Capabilities**.

   2. Select **Automatically manage signing** or manually configure and download the certificate at [https://developer.apple.com/ ](https://developer.apple.com/).

   3. Select **Personal Team**.

   4. Replace the default `com.ss.rtc.demo.quickstart.dev` in the Bundle Identifier with your Bundle ID. The format should start with `com.`.


<span id="step-3-compile-and-run-the-demo-project-file"></span>
### Step 3. Compile and Run the Demo Project File


1. Connect to your iOS device and run the project.

2. Trust the developer in **Settings** \> **General** \> **VPN & Device Management** on your iOS device.

3. Enter your RoomID and UserID in the Quick Start demo, and select **Enter Room**.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70128_2.jpeg) </span>


<span id="experience-rtc-features"></span>
## Experience RTC Features

To better experience RTC features, you can invite a friend or use another device to run the sample project, and make sure that the AppID and AppKey filled in are the same when configuring this project on both devices. After two devices join the same room, you can experience audio and video calls within the same room.

<span id="follow-up-steps"></span>
## Follow\-up Steps

After experiencing this demo, you can read the following documents to learn more:


* In test or production environments, you need to use a Token for authentication. To ensure communication security, it is recommended to obtain the Token from the server. For details, please refer to [Complete Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, please refer to [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).


<span id="usage-instructions"></span>
## Usage Instructions

After building an application with the project, you can use the application for RTC calls.

You and your colleagues must use the same AppID and join the same room to make a successful RTC call.

<span id="frequently-asked-questions"></span>
## Frequently Asked Questions

<span id="q1-howling"></span>
### Q1: Howling

Q: After the Quick Start Demo runs successfully, if test devices are too close to each other, howling will occur.

A: If the test devices are in the same room and the voice is turned on, near\-field howling occurs when the serial gain is greater than 1. This is not a bug of the demo itself. Keep the test devices apart to prevent audio feedback.

<span id="error-messages"></span>
### Error Messages

Q: Error messages prompted during demo running.

A: Internal error of the SDK. For details of error codes, please refer to [Error Code](https://docs.byteplus.com/en/docs/12/docs-70085#bytertcerrorcode).
