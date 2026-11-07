---
title: "About License"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-about-license"
---

<span id="Overview"></span>
## Overview

License is required to use our SDK, where offline licensing is used for Android and iOS, and online licensing is used for Windows, macOS, and Linux.

<span id="Offline Licensing (for Android and iOS)"></span>
# Offline Licensing (for Android and iOS)

The license file verifies both the ApplicationID/BundleID and the expiration date of the application. If the ApplicationID/BundleID is mismatched or the application is not within the licensed period, the SDK will fail. The license file in the current demo (for example, labcv_test_20200501_20200615_com.bytedance.labcv.demo_labcv_test_v3.9.0.licbag) is bound to our preset application ID/bundle ID (special effects version: com.bytedance.labcv.demo; algorithm version: com.bytedance.labcv.demo.algo). You only need to change the application ID/bundle ID to "com.bytedance.labcv.demo" or "com.bytedance.labcv.demo.algo" to start integration testing.

The advantage of this approach is that you can test and experience all features in the demo. After the integration test is completed, you can then apply for the official license and materials bound to your package name and use them to replace the current ones, which will not affect the integration test results.

<span id="Testing with a Custom Application ID/Bundle ID"></span>
### Testing with a Custom Application ID/Bundle ID

If you have imported an officially licensed third\-party SDK and bound a specific application ID/bundle ID, changing the ApplicationID/BundleID will render the functions of the third\-party SDK unusable. In this case, if you want to use the license file bound to your package name for testing, first communicate with relevant business personnel and explain your specific reasons.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Before applying to use a self\-defined ApplicationID/BundleID for testing, be aware of the following:</div>



* <div data-tips="true" data-tips-type="danger"><strong>Only the required test functions</strong> can be bound.</div>


* <div data-tips="true" data-tips-type="danger">The bound test period is <strong>only x weeks or less</strong>.</div>


* <div data-tips="true" data-tips-type="danger"><strong>Do not</strong> use the temporary trial license bound to your self\-defined ApplicationID/BundleID <strong>for release</strong> in App Store; otherwise, function expiration and online losses may occur, for which you will be responsible, no support will be given for any problem without special circumstances.</div>


* <div data-tips="true" data-tips-type="danger">The license file and materials (beautification, stickers, filters, and other resource files) are matched, and the license <strong>only takes effect</strong> <strong>for its matched materials</strong>. Do not use the license bound to your package name with the demo materials.</div>



<span id="Online Licensing (for Windows, macOS, and Linux)"></span>
# Online Licensing (for Windows, macOS, and Linux)

Online licensing is used for Windows, macOS, and Linux, which requires the key and secret pair for testing. Contact relevant business personnel for the key and secret. For more information about online licensing, see [Online License Guide](https://docs.byteplus.com/effects/docs/ online\-license\-guide).
