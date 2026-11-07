---
title: "Reference: Flutter SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Flutter_SDK_Integration_FAQ"
---

<span id="9275f7ef"></span>
# SDK integration

<span id="f87a88f7"></span>
## An error message such as Namespace not specified appears?

A: Upgrade to SDK 1.5.0 version and above.

<span id="087bb696"></span>
## No launch event reported on Android?

Answer: Since the Android side starts faster than flutter, the Android startup lifecycle method has been executed after flutter starts, so the startup event and the first page event cannot be obtained. You can place the initialization operation of Flutter on the native side, and flutter can directly call the Rangers ApplogPlugin.

<span id="fea98d41"></span>
## Running times' @volcengine/applog@1.3.0\-rc 'package not found

Because the Hongmeng version is still in rapid iteration and has not been released to Huawei's official warehouse for the time being, you need to contact BytePlus technical support staff to obtain the offline package.

After getting the offline package, add the offline package of @volcengine/applog in the root directory/ohos/har/, and then add overrides in the root directory/ohos/oh\-package.json5.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/708e8db72679434d802affc38ce72c6f~tplv-goo7wpa0wc-image.image) </span>

<span id="c73fa302"></span>
# More FAQ

See the FAQ for more information on data access [SDK Integration & Data Reporting](https://docs.byteplus.com/docs/DataFinder/SDK_Integration_Data_Reporting).
