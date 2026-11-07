---
title: "Flutter"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-132234"
---

The Quick Start Demo is an open\-source sample project file with basic RTC functions provided by BytePlus RTC. With this project file, you can quickly build an app for the hands\-on experience of BytePlus RTC. You can also refer to the codes for best practices of basic RTC calls.

<span id="prerequisites"></span>
## Prerequisites


* Flutter 2.0.0+

* Dart 2.12.0+

* If the target system is Android:

   * Android Studio 3.5+

   * Android API Level 19+ for real devices or emulators

* If the target system is iOS:

   * Xcode 12.5+

   * iOS 11.0+ on real devices or emulators

* [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793)


<span id="run-the-demo"></span>
## Run the demo

<span id="step-1-get-appid-and-temporary-token"></span>
### Step 1. Get AppID and Temporary Token

Before getting started, you should get an AppID and a temporary token on the BytePlus RTC Console. See [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) and [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for details.

The temporary token is for testing purposes only, such as running the demo.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/132234_1.png) </span>

> Note:

> 1. When joining a room after your app is successfully built, enter the RoomID and UserID you use when obtaining the token.

> 2. Different users must use the same AppID and join the same room to successfully make an RTC call.


<span id="step-2-configure-the-demo-project-file"></span>
### Step 2. Configure the Demo Project File

Add your AppID and Token to the corresponding fields in the `./lib/constants.dart` configuration file.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/132234_2.png) </span>

<span id="step-3-install-dependencies"></span>
### Step 3. Install Dependencies

In the demo project's root directory, run the following command to install dependencies:

```bash
flutter pub get
```


<span id="step-4-run-the-demo"></span>
### Step 4. Run the Demo

Connect a target device and run the following command:

```bash
flutter run
```


If your target device is an iPhone, you need to use Xcode to open the `Runner.xcodeproj` file in the `./ios` directory and add a code signing certificate. See [Configure the Developer Certificate](https://docs.byteplus.com/en/docs/12/docs-70128#step-3-compiling-the-project) for details.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/132234_3.png) </span>

After the build is successful, the app's interface appears. Enter the RoomID and UserID used to generate the temporary token. Now you can start a video call.

> Note: Different users must use the same AppID and join the same room to successfully make an RTC call.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/132234_4.png) </span>

<span id="experience-rtc-features"></span>
## Experience RTC Features

To test the RTC features, you can run the sample project on a second device or share it with a friend. Ensure that both devices are configured with the same AppID and Token. Once both devices have joined the same room, you can make audio and video calls between them.

<span id="follow-up-steps"></span>
## Follow\-up Steps

After trying this demo, refer to the following documents to learn more:


* In test or production environments, you need to use a Token for authentication. To ensure communication security, it is recommended to obtain the Token from the server. For details, see [Complete Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, see [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).
