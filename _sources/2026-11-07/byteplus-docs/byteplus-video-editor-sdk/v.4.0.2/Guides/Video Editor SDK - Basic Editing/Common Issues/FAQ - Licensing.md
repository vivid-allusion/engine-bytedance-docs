---
title: "FAQ - Licensing"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-faq-licensing-v.4.0.2"
---

<span id="85e00871"></span>
## 1. Can I use the license file bound with my app ID for the integration test?

To test all functions provided in the demo, you are advised to use the default license file and assets under the **resource** directory. After the integration test, you can apply for the formal assets and license file bound with your app ID and replace the default assets and license file with the formal ones. The replacement will have no impact on the previous test result. If you still want to use the license file bound with your app ID for the integration test, please contact our business personnel and let us know your concern.

<span id="875c4020"></span>
## 2. How can I use the default license file in the demo for the integration test?

In our demo's license file, the app ID for Android is **com.ss.android.vesdk.vedemo** and the bundle ID for iOS is **com.IESVideoEditor.demo.inhouse**. Change the app ID and bundle ID respectively for Android and iOS before the integration test as follows:


* For Android: Change the value of **ApplicationId** to **com.ss.android.vesdk.vedemo** in the **build.gradle** file.

* For iOS: Change the value of **Bundle Identifier** in **General/Identity** to **com.IESVideoEditor.demo.inhouse**. To implement the integration test for an iOS app, you'll need an enterprise developer account. After changing the bundle ID, select and deselect **Automatically manage signing** for several times and wait until the account is updated. If you do not have an enterprise developer account, contact our business personnel for help.


<span id="64bdfc52"></span>
## 3. Should the version of the license file and assets be consistent with the SDK version?

You are advised to keep the versions consistent. Otherwise, risks or issues may occur.

<span id="1a8404df"></span>
## 4. When the license expires, do I have to release a new app version with the updated license file and prompt users to perform the update?

You'll need a new license file after the existing one expires, while you do not have to release a new app version. It is recommended that you deliver the new license file to the app in a similar way for delivering resources (pictures, videos, or others) to the app. This is an app\-level logic.

<span id="ea598c04"></span>
## 5. What are the possible causes of authorization failure?

Verify that:


1. The system time of the mobile is correct.

2. The app ID you set for the Android app or the bundle ID you set for the iOS app is the authorized one.

3. The license file matches the assets.

4. The license file matches the SDK version.


<span id="3965d2da"></span>
## 6. Can l use the same license file and assets for my apps with different app IDs?

No. For details, please contact our business personnel.

<span id="4bc07e18"></span>
## Note

You are advised to deliver the license file from the server to the client so that you do not have to release a version to update the license file.
