---
title: "Windows"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70125"
---

The Quick Start Demo is an open source sample project file with basic RTC functions provided by BytePlus RTC. With this project file, you can quickly build an application for the hand\-on experience of BytePlus RTC. You can also refer to the code for best practices of basic RTC calls.

<span id="usage-instructions"></span>
## Usage Instructions

After building an application with the project, you can use the application for RTC calls.

You and your colleagues must use the same AppID and join the same room to make a successful RTC call.

<span id="prerequisites"></span>
## Prerequisites


* Visual Studio 2017+

* Qt 5.9+

* The version of Visual Studio must correspond to Qt running environment (for example, Visual Studio 2017 corresponds to msvc 2017)

* cmake 3.1+

* Windows 7+ (Windows 10 is recommended)

* Use C++ as the development language (support C++ version 11)

* Get [Demo Project](https://docs.byteplus.com/en/docs/12/docs-1163793)


<span id="operation-steps"></span>
## Operation steps

<span id="step-1-configure-environment-variables"></span>
### Step 1. Configure Environment Variables

Configure QT environment variables `Qt32Path` and `Qt64Path`. The values of `Qt32Path` and `Qt64Path` are the corresponding cmake folder path in your QT installation directory.

<span id="step-2-get-appid-and-temporary-token"></span>
### Step 2. Get AppID and Temporary Token

For more information about getting your AppID and temporary token on the console, see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865).


> * The room ID and the user ID must be the same when used to generate temporary token at the console and when filled in the UI on the built application.

> * The temporary token is used only for debug. See [Using Token for Authentication](https://docs.byteplus.com/en/docs/12/docs-70121).


<span id="step-3-configure-the-demo-project-file"></span>
### Step 3. Configure the Demo Project File


1. Change directory to `QuickStart_WindowsDemo`, and run `cmake -G "Visual Studio 16" -B build_win` to generate the demo project under `build_win`.

> The value `16` in the `cmake -G "Visual Studio 16" - Bbuild_win` command is the version number of the Visual Studio you installed. For example, the version number of Visual Studio 2019 is `16`, and that of Visual Studio 2017 is `15`. See [Visual Studio build numbers and release dates](https://docs.microsoft.com/en-us/visualstudio/install/visual-studio-build-numbers-and-release-dates?view=vs-2019).


2. Change directory to `QuickStart_WindowsDemo\build_win` and open the project `QuickStart.sln` with Visual Studio.

3. Fill in the `AppID` and `TOKEN` fields in `sources\Constants.h` with the value you get from the console.


<span id="step-4-compile-and-run-the-demo-project-file"></span>
### Step 4. Compile and Run the Demo Project File

Start debugging the demo project.

The login interface of the demo application is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70125.jpeg) </span>

<span id="experience-rtc-features"></span>
## Experience RTC Features

To better experience RTC features, you can invite a friend or use another device to run the sample project, and make sure that the AppID and Token filled in are the same when configuring this project on both devices. After two devices join the same room, you can experience audio and video calls within the same room.

<span id="follow-up-steps"></span>
## Follow\-up Steps

After experience this demo, you can read the following documents for further understanding:


* In test or production environments, you need to use a Token for authentication. To ensure communication security, it is recommended to obtain the Token from the server. For details, please refer to [Complete Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, please refer to [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).


<span id="frequently-asked-questions"></span>
## Frequently Asked Questions

<span id="q1-after-the-quick-start-demo-runs-successfully-if-test-devices-are-too-close-to-each-other-howling-will-occur"></span>
### Q1: After the Quick Start Demo runs successfully, if test devices are too close to each other, howling will occur.

A: If the test devices are in the same room and the voice is turned on, near\-field howling occurs when the serial gain is greater than 1. This is not a bug of the demo itself. Please keep the distance between each other of the test devices.

<span id="q2-error-messages-prompted-during-demo-running"></span>
### Q2: Error messages prompted during demo running.

A: Internal error of the SDK. For details of error codes, please refer to [Error Code](https://docs.byteplus.com/en/docs/12/docs-70097#errorcode).

<span id="q3-after-clicking-start-debugging-an-error-message-about-failing-to-find-all-build-is-reported"></span>
### Q3: After clicking Start Debugging, an error message about failing to find "all_build" is reported.

A: Visual Studio starts the first project "all_build" by default. You need to set the "Quickstart" project as the project to start.
