---
title: "Crashes occur when using the Demo or integrating the SDK, and this issue only occurs on devices running iOS 15 or earlier."
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Crashes_occur_when_using_the_Demo_or_integrating_the_SDK"
---

According to the description in Apple documentation, this is caused by changes introduced in Xcode 15. You can try to resolve \-Wl,\-ld_classic by adding the link directive. For details, refer to [Xcode 15 Release Notes](https://developer.apple.com/documentation/xcode-release-notes/xcode-15-release-notes).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b5b38ae3182466a8d4548bd7bcc20c1~tplv-goo7wpa0wc-image.image) </span>
