---
title: "Enable Message Notification"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75110"
---

You can use our message notification service to get RTC usage status right from your RTC application's business server.

<span id="how-it-works"></span>
## How it works

When you enable message notification service, you can specify which events you want to be notified about. You can enable message notification service to receive callbacks from BytePlus RTC service when certain events occur. The following figure shows how this service works.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_0b53b13a545022a099fd5ac74430fd03) </span>

<span id="enable-the-notification-service"></span>
## Enable the notification service


1. Log in to the BytePlus RTC [console](https://console.byteplus.com/rtc/workplaceRTC).

2. Click **Configuration** to add a new callback configuration.

3. Fill in the following information:

* **Event:**  Select the desired callback events. For details of supported events, see Reference for Eventtype.

* **Callback URL:**  Provide the URL that will receive the callback when an event occurs. For how to receive callbacks, see Receive Callbacks of Message Notification.

* **Secret Key:**  Add a secret key to generate a digital signature.


Once the service is enabled, the specified URL will receive a callback when the subscribed event occurs. For details, see [Callback Format Reference](https://docs.byteplus.com/en/docs/12/docs-75124) .
