---
title: "FAQ—SDKs"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-faq-sdks"
---

This section details the frequently asked questions about our SDK packages.

<span id="How do I download the BytePlus Effects demo app?"></span>
# How do I download the BytePlus Effects demo app?

For more information on downloading the BytePlus Effects demo app, refer [here](https://bytedance.feishu.cn/docs/doccnYQRH1vcUyjOwAq153yK8gc).

<span id="9171bef8"></span>
# Who developed BytePlus Effects and which platforms is it supported on?

BytePlus Effects is independently developed and provided by the ByteDance Intelligent Creation team. Currently, it can support iOS, Android, Windows PC, and MAC OS. The BytePlus Effects team also provides a sub\-set of our features on the web. Our web version is constantly being updated with new features. Interested clients should reach out to the BytePlus Effects team to get more information on these features and their availability.

For more information on SDK integration guides, refer [here](https://docs.byteplus.com/effects/docs/android-v4101-access-guide).

<span id="d72822ce"></span>
# What are the minimum device version requirements for integrating Effects SDK?

Devices have to meet a certain version requirement before clients can integrate the BytePlus Effects SDK.

**Android**

For Android devices, the following are required:


* Android version 4.4 and above.

* CPU requirements: `armeabi-v7`, `arm64-v8a` and above, or `X86`.


**iOS**

For iOS devices, the following are required:


* iOS system version 8.0 and above.

* Phone model: iPhone 6 and above.


**Windows PC or Mac**

For Windows PC or Mac devices, the following are required:


* PC CPU: INTEL or AMD.

* System version WIN7 (X86) and above or MAC OS X.


<span id="How many facial keypoints can Effects SDK detect? How many angles can the head rotate at the most? What is the farthest it can be detected?"></span>
# How many facial keypoints can Effects SDK detect? How many angles can the head rotate at the most? What is the farthest it can be detected?

BytePlus Effects SDK product detects **106** and **280** face keypoints. Clients can choose the amount that best suits their business needs.

It supports an yaw and pitch angle of <±90 ° and pitch <±90 °.

BytePlus Effects can recognize facial keypoints up to five meters away.

<span id="What are the sizes of the SDK installation package on each platform and of each sticker?"></span>
# What are the sizes of the SDK installation package on each platform and of each sticker?

The sizes for each installation package are as follows:


* a.a package: 300 MB

* .aar. package: 18.8 MB

* .so package: 25.9 MB

* arm64: 25.9 MB

* armeabi package: 17.6 MB


The size of each package may increase depending on the number of stickers included. The average size of a sticker is around 0.7 MB. For more information on the increased installation package sizes, refer [here](https://docs.byteplus.com/en/docs/13/**https://docs.byteplus.com/effects/docs/faq#will-the-sdk-installation-package-size-increase**).

<span id="Will the SDK installation package size increase?"></span>
# Will the SDK installation package size increase?

The size depends on the number of stickers within the package.


* **Android**: The SDK incremental size for Android is approximately 18 MB, including both 32 bit and 64 bit. If only one of them is needed, the incremental size will be reduced to 9 MB.

* **iOS**: The SDK incremental size for iOS varies depending on the features selected. For example, the expected SDK incremental size for iOS is approximately 50 MB, assuming the selected features are beauty effects (toning, buffing, sharpening), face shaping effects, and various advanced makeup sets.

* **PC**: The SDK incremental size for PC is approximately 20 to 30 MB.

* **Mac**: The SDK incremental size for Mac is approximately 20 to 30 MB.


The average size of a sticker is around 0.7 MB. However, hosting sticker assets on the cloud and enabling download on demand can greatly affect the SDK size. Therefore, the sticker asset size should not be included in the total SDK size.

<span id="What files are included in the SDK package besides an APK file, product specifications, authorization instructions, and development documents?"></span>
# What files are included in the SDK package besides an APK file, product specifications, authorization instructions, and development documents?

The following files are included in the SDK packages:


* `android_sdk.aar`: Java interface.

* `ios_c_sdk.a`: C interface.

* `android_c_sdk.zip`: C interface.

* `android_sample.zip`: Project to compile APK.

* `resource.zip`: License, related algorithm model file, and effect\-related asset files.


<span id="I am using a live broadcast service from a cloud provider. Am I able to integrate the BytePlus Effects SDK to my service, and what is the average time needed for the integration?"></span>
# I am using a live broadcast service from a cloud provider. Am I able to integrate the BytePlus Effects SDK to my service, and what is the average time needed for the integration?

The BytedEffects SDK can be integrated with various cloud platforms and requires the following basic technical capabilities:


* For Android and iOS devices: Familiarity with OpenGL ES, and understanding of texture and FrameBuffer operations.

* Commonly used camera video stream capturing.

* Integration can be completed in 1 to 2 weeks depending on the requests. The BytePlus Effects team provides sample app and integration codes for mainstream broadcast services that help get clients on board.


<span id="What is our sticker designing process?"></span>
# What is our sticker designing process?

The BytePlus Effects team has a group of designers that can help create customized stickers according to our clients' requirements. If our clients want to design the stickers by themselves, they can purchase our EffectCreator tool license. You can use popular design tools to generate the visuals and upload them to EffectCreator to create your personalized stickers. For a smoother onboarding process, we have guides and tutorials available to help your designers get started with our tools. For more information on EffectCreator, refer [here](https://bytedance.feishu.cn/docs/doccnCwPGdYl48ZytuwhL3Ww3Gb).

<span id="What is your authentication method and why?"></span>
# What is your authentication method and why?

Integration of the BytePlus Effects SDK is completely offline. The BytePlus Effects team is currently using offline authentication, which works well in a no\-internet environment. This is more reliable for partners, as disruptions due to network problems are more easily avoided. In the case of no internet access, all functions are still readily available. In addition, there is no possibility of you being subjected to any functional or process failures because of networking issues.

Offline authorization assures that our partners' information is secure. No additional information is collected on our end.

If there is an update, you simply need to publish a new version of your app to run the authorization update. You will also need to notify your users to update the app.

<span id="How does the BytePlus Effects team charge clients for the SDK packages?"></span>
# How does the BytePlus Effects team charge clients for the SDK packages?

We provide the SDK license, catering to all functional feature needs, for an annual fee. The BytePlus Effects team also charges according to the number of platforms (iOS, Android, Windows, Mac, Linux) and SDK applications.

<span id="Does BytePlus Effects have any pricing models other than the annual license fee?"></span>
# Does BytePlus Effects have any pricing models other than the annual license fee?

The BytePlus Effects team can customize different pricing models for different companies. For more information, contact the BytePlus Effects team at ai2b\-service\-support@bytedance.com.

<span id="Is there any other commercial model besides the annual fee?"></span>
# Is there any other commercial model besides the annual fee?

Under normal circumstances, the commercial model is based on the annual license fee. Other cooperation models can be discussed on a case\-by\-case basis.

<span id="I am a client with a wide range of devices looking to integrate the BytePlus Effects SDK. Are there any discounts?"></span>
# I am a client with a wide range of devices looking to integrate the BytePlus Effects SDK. Are there any discounts?

If there are multiple apps or applications belonging to the same client, the BytePlus team will calculate the price for each app or application\-use and possibly offer a discount. For more information, contact the BytePlus Effects team at ai2b\-service\-support@bytedance.com.

<span id="When the authorization period expires but is not renewed, can the functions that our users have in the downloaded app still be used?"></span>
# When the authorization period expires but is not renewed, can the functions that our users have in the downloaded app still be used?

If the authorization period is not renewed, the certificate will expire. Users will not be able to continue to use the functions provided by our SDK through their app.

<span id="How does the SDK bind the customer's ApplicationID or BundleID?"></span>
# How does the SDK bind the customer's ApplicationID or BundleID?

At present, the included ByteEffect SDK authorization file will be tied to our default ApplicationID/BundleID, com.bytedance.labcv.demo. Customer integration tests need to have their ApplicationID/BundleID changed to "com.bytedance.labcv.demo" to complete the test.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/59b1b2a-b43ebe56-d03c-4ef7-a3c1-403371d040fa.png) </span>

There are times when the client has integrated SDKs officially authorized by other third parties and has been bound with an ApplicationID/BundleID. In situations like this, modifying the ApplicationID/BundleID causes third\-party functions to be unavailable. To allow access to the third\-party functions, clients can reach out to the BytePlus Effects team to apply for binding test services for the customized Application ID/BundleID.

There are some disadvantages such as:


* Only test functions required by the client are subjected to binding.

* There is a short test period allowed (usually two weeks or one month).

* If the client uses the temporary authorization of the custom binding ApplicationID/BundleID to go live on the App Store, there is a high risk that a number of functions will expire. This will implicate your business but will not be covered by the BytePlus Effects team.


<span id="Are there any sample demo app integration guides available for reference?"></span>
# Are there any sample demo app integration guides available for reference?

Yes. If clients want to integrate a simple camera app and need a reference, they can visit our repository. For example, if clients want a reference to integrating the Camera2 API and BytePlus Effects' Java SDK to Android apps, they can refer [here](https://github.com/byteplus-sdk/effectsdk-android-camera). Some effects included in this example are filters, sunglass AR try\-on, and makeup stickers.

<span id="What is the data format your SDK returns after processing camera data?"></span>
# What is the data format your SDK returns after processing camera data?

Returns are in OpenGL Texture format after processing SDK packages consisting of beauty filters, stickers, and many others.

<span id="Other than the Android app for mobile devices, what other Android devices do you support?"></span>
# Other than the Android app for mobile devices, what other Android devices do you support?

BytePlus Effects supports Android TV. Clients should reach out to our team members to customize their SDK packages for specific devices.

<span id="Can I use SDK offline processing on pre-recorded videos and not in real time?"></span>
# Can I use SDK offline processing on pre\-recorded videos and not in real time?

Yes.
