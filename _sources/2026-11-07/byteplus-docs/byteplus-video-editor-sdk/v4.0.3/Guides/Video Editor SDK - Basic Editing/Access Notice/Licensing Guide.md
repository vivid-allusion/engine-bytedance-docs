---
title: "Licensing Guide"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-licensing-guide"
---

<span id="4e0fd565"></span>
## Overview

Authentication is required for the use of the VE SDK. Offline authorization is used on Android and iOS devices.

<span id="0a0becef"></span>
## Offline authorization for Android and iOS

The authorization file verifies both the ApplicationID/BundleID and the validity period. The SDK becomes invalid either when the ApplicationID/BundleID does not match or when the valid period expires. Currently, the authorization file (such as **ve_test_20210222_20210822_com.IESVideoEditor.demo.inhouse_v1.0.1.licbag**) in the demo will bind the preset ApplicationID/BundleID (com.IESVideoEditor.demo.inhouse). You can start testing simply after changing the ApplicationID/BundleID to **com.IESVideoEditor.demo.inhouse**.

This method enables you to test all features in the demo. After the integration test, you can apply for the formal assets and license file bound with your app ID and replace the default assets and license file with the formal ones. The replacement has no impact on the previous test result.

<span id="0afa898b"></span>
## Test authorization for binding user\-defined ApplicationID/BundleID

If you have integrated another SDK officially authorized by a third party and have clearly bound the ApplicationID/BundleID, modifying its ApplicationID/BundleID will cause the features of the third\-party SDK unavailable. If you want to use the authorization file bound to your app ID for testing, communicate with the corresponding business representative first. Then, explain the specific reasons, and submit an application for testing with the user\-defined ApplicationID/BundleID. In this case, pay attention to the following points:


1. Bind only the required testing feature.

2. Only a few weeks of binding testing can be provided.

3. Do not launch the app on the appstore when a user\-defined ApplicationID/BundleID is used for temporary testing authorization. You are responsible for the online losses arising from feature expiration.

4. The authorization file corresponds to the assets. The assets take effect only when the corresponding authorization file is used. Do not mix up the authorization bound to your app ID with demo assets.


<span id="04d503b8"></span>
## Note


* It is advised to deliver the license file from the server to the client, so that there will be no need to release a version to update the license file.
