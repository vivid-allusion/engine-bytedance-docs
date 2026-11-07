---
title: "Unity"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1139327"
---

The Quick Start Demo is an open\-source sample project file with basic RTC functions provided by BytePlus RTC. With this project file, you can quickly build an app for the hands\-on experience of BytePlus RTC. You can also refer to the codes for best practices of basic RTC calls.

<span id="prerequisites"></span>
## Prerequisites


* Follow instructions in [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) to obtain the AppID

* Follow instructions in [Generate temporary token](https://docs.byteplus.com/en/docs/12/docs-1163793) to obtain the temporary Token.

* Unity Editor 2017+

* Android Studio 3.5+

* [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended to use a real device for testing, as some features may not work properly on emulators.</div>


<span id="operational-steps"></span>
## Procedure

<span id="step-1-configure-the-demo-project-file"></span>
### Step 1: Configure the Demo Project File


1. Unzip the downloaded RTC Quick Start Demo project file (Unity) and open the project file with Unity Hub.

2. Search and open **Constants.cs**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac6ff9518b0fa501792acfc74f2056b3.png) </span>


3. After opening the `Constants.cs` file, enter your AppID and temporary token in the corresponding `APP_ID` and `TOKEN` fields.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dcddbc1034516975defa66e29453b02b.png) </span>

<span id="step-2-compile-and-run"></span>
### Step 2: Compile and Run

Click **File** \-\> **Build Settings** or use the shortcut Ctrl+Shift+B (Unity Windows version)/Shift+Command+B (Unity macOS version) to open the following interface.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_131fa2058de8b1bdaee84f252c29df6a.png) </span>

<span id="windows-platform"></span>
#### Windows Platform

In the Unity Build interface, select `PC, Mac & Linux Standalone` as the Platform and click `Build` to compile the Windows platform package.

<span id="android-platform"></span>
#### Android Platform

Before compiling the Android package, you must configure the Android SDK, JDK, and NDK in the Unity IDE. To open the configuration interface, go to **Unity** \> **Settings** \> **External Tools** on macOS, or **Edit** \> **Preferences** \> **External Tools** on Windows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_356600b02b7e24d1ea35897b529cd2ee.png) </span>

Then, in the Unity Build interface, select `Android` as the Platform, uncheck `Export Project`, and click **Build** to output the Android apk.

<span id="ios-platform"></span>
#### iOS Platform

In the Unity Build interface, select `iOS` as the Platform, click **Build**, then generate the Xcode project and run it.

**The running application appears as follows:** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ffd56db35548dcb278333b85e46c2816.png) </span>

<span id="experience-rtc-features"></span>
## Experience RTC Features

To test the RTC features, you can invite a friend or use another device to run the sample project, and make sure that the AppID and Token you entered are the same on both devices. After two devices join the same room, you can make audio and video calls to each other.

<span id="follow-up-steps"></span>
## Follow\-up Steps

After experiencing this demo, you can read the following documents to learn more:


* In test or production environments, you need to use a Token for authentication. To ensure communication security, it is recommended to obtain the Token from the server. For details, please refer to [Complete Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, please refer to [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).
