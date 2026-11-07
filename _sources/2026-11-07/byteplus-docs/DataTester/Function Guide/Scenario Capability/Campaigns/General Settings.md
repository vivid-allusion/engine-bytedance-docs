---
title: "General Settings"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/General-Settings"
---

<span id="_1-全局频控"></span>
## 1. Global frequency control

**Only administrators and group administrators can save settings**

Each user can accept up to xx pushes per day, and up to xx pushes per hour; the default rule is: each user can accept up to 20 pushes per day, and up to 1 push per hour. After modifying the frequency control, it will take effect within 0 to 10 minutes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb86da1dfba24958a339681c5169b681~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-测试白名单"></span>
## 2. Test the whitelist

A whitelist of test user IDs (user unique IDs), separated by half\-width commas between multiple users. **After setting "Test" and approving in "Push Task Management \- Send Range", the push will only take effect on this part of the test users**.

<span id="_3-webhook安全"></span>
## 3. WebHook Security

To ensure that webhook calls are secure and trusted, you can use the following app_secret to validate webhook requests. For detailed usage, please refer to "Push Channel Management\-Webhook".
