---
title: "BytePlus Web RTC SDK Compatibility Upgrade to Address Chrome Browser Changes"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1564074"
---

<span id="background-and-impact"></span>
## Background and Impact

Due to Chrome's initiative to [[strictly limit the modification of SDP during the RTC connection establishment process](https://groups.google.com/g/discuss-webrtc/c/PIJZN5MTZF4/m/JHVmmn8yDgAJ)], some features of the BytePlus [Web RTC SDK](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104477) ([@byteplus/rtc](https://www.npmjs.com/package/@byteplus/rtc)) may be affected. BytePlus has already released a compatible version, and we recommend that you upgrade your SDK version as soon as possible.

<span id="solution"></span>
## Solution

We strongly recommend that you **upgrade your BytePlus Web RTC SDK as soon as possible before the release of Chrome 139**. If time permits, we highly advise upgrading to our latest version, 4.66.29, for an optimized experience.

Alternatively, you may refer to the version list below for a seamless upgrade. The SDK API is fully backward compatible. Simply update the SDK version number, perform basic functional verification, and go live—no additional code modifications are required.

**Steps**:


1. Confirm the version (X.Y.Z) of the Web RTC SDK you are currently using.

2. Refer to the table below to find the compatible upgrade version for your current X.Y version.

   * **If using a package manager (e.g.,**  **npm)** : In the `package.json` file, update the version number of `@byteplus/rtc` to the latest patch version. It is recommended to use the tilde prefix (~) followed by the version number (e.g., `"@byteplus/rtc": "~4.66.15"`) to ensure automatic updates to the latest patch version in the future.

   * **If manually integrating the SDK**: Use the UMD URL in the table below or visit [the version list](https://www.npmjs.com/package/@byteplus/rtc?activeTab=versions), download the SDK package of the latest patch version, and replace the old SDK files in your project.

   
   |@byteplus/rtc versions:<br><br>[https://www.npmjs.com/package/@byteplus/rtc?activeTab=versions](https://www.npmjs.com/package/@byteplus/rtc?activeTab=versions) |||
   |---|---|---|
   |**Your current X.Y version** |**Compatible Upgrade Version** |**UMD URL** |
   |4.66,4.65 |~4.66.29 |https://sf\-unpkg.bytepluscdn.com/obj/byteplusfe\-sg/sdk/@byteplus/rtc/4.66.29/1760341626742/index.min.js |
   |4.63,4.62,4.61,4.60 |~4.63.17 |https://sf\-unpkg.bytepluscdn.com/obj/byteplusfe\-sg/sdk/@byteplus/rtc/4.63.17/index.min.js |
   |4.58,4.56 |~4.58.22 |https://sf\-unpkg.bytepluscdn.com/obj/byteplusfe\-sg/sdk/@byteplus/rtc/4.58.22/index.min.js |
   |4.55,4.54,4.53 |~4.55.17 |https://sf\-unpkg.bytepluscdn.com/obj/byteplusfe\-sg/sdk/@byteplus/rtc/4.55.17/1762241280358/index.min.js |
   |4.51,4.49 |~4.51.13 |https://sf\-unpkg.bytepluscdn.com/obj/byteplusfe\-sg/sdk/@byteplus/rtc/4.51.13/1762241365149/index.min.js |
   


<span id="contact-us"></span>
## Contact us

If you have any questions about the upgrade process, you can contact us by [submitting a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000762&FlowKey=hooomjXXojvNpHrZdAQT&aiSearchQuestion=&aiID=).
