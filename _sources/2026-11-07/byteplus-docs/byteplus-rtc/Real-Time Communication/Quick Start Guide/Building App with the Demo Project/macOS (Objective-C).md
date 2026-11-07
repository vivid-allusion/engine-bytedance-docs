---
title: "macOS (Objective-C)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70127"
---

The Quick Start Demo is an open source sample project file with basic audio & video calling functions provided by BytePlus RTC. After obtaining this project file, you can quickly build an application to experience the performance of BytePlus RTC. You can also read the code to learn about basic audio & video calling best practices.

<span id="usage-instructions"></span>
## Usage Instructions

After building the project, you can use the resulting application for audio and video calls.

You and your colleagues must join the same room to make an audio and video call.

<span id="prerequisites"></span>
## Prerequisites


* A Mac running macOS 10.10 or later (M1 chips are not supported).

* Installed Xcode 9.0+.

* Have a valid [Apple ID](http://appleid.apple.com/).

* [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793).


<span id="operation-steps"></span>
## Operation Steps

<span id="step-1-get-appid-and-temporary-token"></span>
### Step 1. Get AppID and Temporary Token

For more information about getting your AppID and temporary token on the management console, see [Getting AppID](https://docs.byteplus.com/en/docs/12/docs-69865).

> The Room ID and User ID used to generate the temporary token must match the ones you enter on the demo application's Join Room screen.

> The temporary token is used only for testing and running the demo. You can learn more about tokens by reading the [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) documentation.


<span id="step-2-configure-the-demo-project-file"></span>
### Step 2. Configure the Demo Project File


1. Open the **`QuickStart.xcodeproj`** project file in the `QuickStart_macOSDemo` folder with Xcode.

2. Select the `Constants.h` file and fill in the **APPID** and **TOKEN** with the values you obtained from the management console.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70127_1.png) </span>

<span id="step-3-compile-and-run-the-demo-project-file"></span>
### Step 3. Compile and Run the Demo Project File

Select **Product** \> **Run**, or press the shortcut **Command** + **R**. The login interface of the demo application is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70127_2.png) </span>

<span id="experience-rtc-features"></span>
## Experience RTC Features

To better experience RTC features, you can invite a friend or use another device to run the sample project, and make sure that the AppID and Token you enter are the same when configuring this project on both devices. After both devices join the same room, you can make audio and video calls between them.

<span id="follow-up-steps"></span>
## Follow\-up Steps

After experiencing this demo, you can read the following documents to learn more:


* In test or production environments, you need to use a Token for authentication. To ensure communication security, it is recommended to obtain the Token from the server. For details, see [Complete Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, see [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).


<span id="frequently-asked-questions"></span>
## Frequently Asked Questions

<span id="q1-after-the-quick-start-demo-runs-successfully-if-2-test-devices-are-too-close-to-each-other-howling-will-occur"></span>
### Q1: Howling may occur if two test devices running the demo are too close to each other.

Reason: If audio is enabled on test devices that are in close proximity, near\-field audio feedback (howling) can occur. This is expected behavior, not a bug. To prevent this, keep the devices separated.

<span id="q2-after-the-demo-runs-error-messages-are-prompted"></span>
### Q2: Error messages appear after the demo runs.

Reason: This indicates an internal SDK error. For details about specific error codes, refer to [Error Codes](https://docs.byteplus.com/en/docs/12/docs-70091#bytertcerrorcode).
