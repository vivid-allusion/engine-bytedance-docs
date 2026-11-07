---
title: "Android"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70129"
---

To quickly experience BytePlus RTC on Android, you can use the provided open\-source sample project. This guide walks you through cloning the project, configuring it with your credentials, and compiling it to build a functional application for a hands\-on trial.

<span id="prerequisites"></span>
## Prerequisites


* System requirements:

   * Android Studio Arctic Fox or higher. We recommend using the latest version of Android Studio for optimal performance.

   * A physical mobile device that runs Android 5.0 or higher.

   * Ensure the CPU architecture that you use is armv7 or arm64.

* Create an access key for the account, and obtain the Access Key ID (AK) and Secret Access Key (SK). [How to create an access key?](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey)

* Activate the BytePlus RTC service, create an RTC app and obtain the AppId and AppKey. See details in [Before Using RTC Service](https://docs.byteplus.com/docs/byteplus-rtc/docs-69865).


<span id="procedures"></span>
## Procedures

<span id="step-1-cloning-the-project"></span>
### Step 1: Cloning the project


1. Go to GitHub and clone the [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) repository.

2. Under the `Client` directory, open the `Android` folder in Android Studio. This is the root directory of the demo project.


<span id="step-2-modify-the-configuration-file"></span>
### Step 2: Modify the configuration file


1. Open the configuration file (`settings.gradle`) shown in the figure below and comment out the code that is not related to RTC:

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0cfbcadc104b7858b2ed5cb9caf6986c.png) </span>

2. Open the file Client/Android/gradle.properties, and configure the following fields with the values from the Prerequisites section. These credentials are used to authenticate your client with the BytePlus RTC service.



|Field name |Description |Example |
|---|---|---|
|APP_ID |The **AppId** of your BytePlus RTC app. |123456\*\*\*\*\*\*\*\*3deb567a86 |
|APP_KEY |The **AppKey** of your BytePlus RTC app. |1bfaa8e\*\*\*\*\*\*\*\*fjb6j6hhde68c07d |
|ACCESS_KEY_ID |The **Access Key ID (AK)**  of your BytePlus account. |AKAPZ7\*\*\*\*\*\*\*\*FLB0D38CM8DK49SO39D83KD820DFK4k9 |
|SECRET_ACCESS_KEY |The **Secret Access Key (SK)**  of your BytePlus account. |8dk39vK\*\*\*\*\*\*\*\*k7D93KDHS8DJSLud830DJEO37EI3UDK37WODKu3oQ |


<span id="step-3-compiling-the-project"></span>
### Step 3: Compiling the project


1. Connect the mobile device to your computer, and set it as the target device in Android Studio.

2. Click the **Sync Project with Gradle Files** button.

3. Click the **Run** button to start the compilation.


<span id="step-4-trying-the-app"></span>
### Step 4: Run the app

After a successful compilation, the VideoOne app is installed on your device and the login screen appears automatically. Log into the app with your email, then you can start exploring the app's features and scenarios.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f5199eb71aaabfab7e09b3eb2ef8e9ba.png) </span>

<span id="faq"></span>
## FAQ


* **Q**: I encountered the following error: `Caused by: org.gradle.process.internal.ExecException: Process 'command 'git'' finished with non-zero exit value 128.`

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_565a839068f2d9cea16d5468983a703f.png) </span>

* **A**: Comment out the Git\-related code in the file `Client/Android/app/build.gradle`.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4c44300b4631f6e232a3112cb7433fbf.png) </span>
