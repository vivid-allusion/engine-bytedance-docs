---
title: "FAQ during Building iOS Apps"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1253477"
---

<span id="how-to-add-usage-reason-descriptions-for-api-in-ios-apps"></span>
## How to add usage reason descriptions for API in iOS Apps

As required by Apple, if your iOS App needs to be published on the App Store, you must accurately describe why the App itself and the integrated third\-party SDK use system interfaces within a specified range. Starting from **May 1, 2024**, if such descriptions are not provided, your app will fail the review process on App Store Connect. For more details, refer to Apple's [Describing use of required reason API](https://developer.apple.com).

<span id="if-you-are-using-rtc-sdk-versions-after-3-58-excluding-3-58"></span>
### If you are using RTC SDK versions after 3.58 (excluding 3.58):

Since versions after 3.58 include a built\-in privacy info file, no additional steps are required. Simply follow the standard integration steps to complete the RTC SDK setup.

<span id="if-you-have-integrated-rtc-sdk-3-58-or-earlier-versions-into-your-app-you-need-to-add-the-following-privacy-info-file-to-your-app"></span>
### If you have integrated RTC SDK 3.58 or earlier versions into your app, you need to add the following privacy info file to your app:

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acad7ecceed80baa7caa3485356e8a62.zip" name="PrivacyInfo.xcprivacy.zip">PrivacyInfo.xcprivacy.zip</Attachment>



* **For Apps without a privacy info file:** 

   Add the RTC SDK's privacy info file to the root directory of your project, as shown below:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c1aaa65b4b9f3adbe7b14d1a25ab31c.png) </span>

* **For Apps with an existing privacy info file:** 

   Add the contents of the **RTC SDK's privacy info file** to your app's existing privacy info file.
