---
title: "Turn off crash protection"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Turn_off_crash_protection"
---

Crash protection is not required during debugging or in certain special scenarios. You can turn off crash protection using the following method. The detailed steps for turning off crash protection are described below, using iOS as an example.


* Method 1: Delete the crash protection module from the SDK.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37c263f5cb5949328744bfde7bc6fa2a~tplv-goo7wpa0wc-image.image) </span>

   Delete the crash protection submodule during debugging, and ensure that you add the submodule back when releasing.

* Method 2: During local debugging, configure a specific channel value. Then, on the **SDK reporting configuration** page, under the **crash protection** module, add a parameter for the **crash protection submodule switch**. For the filter condition, select **download channel**, and configure the value for the crash protection submodule switch.**0**。

&nbsp;

   * For information on how to modify parameters, refer to [Create SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#b29d0396).

   * For the crash protection submodule configuration, refer to [Crash protection submodule switch](https://docs.byteplus.com/en/docs/apmplus/iOS_crash_protection#69b8297e).
