---
title: "Before Using RTC Service"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865"
---

Before integrating the BytePlus RTC SDK into your application, you must activate the service and obtain an AppID.

To enable RTC service, refer to the following steps.

<span id="step-1-login-to-the-management-console"></span>
## Step 1. Log in to the management console


1. Login to the [console](https://console.byteplus.com/),

* If this is your first time logging in, you must first sign up for an account.

* If you already have a BytePlus account, log in.


<span id="step-2-apply-to-enable-rtc-service"></span>
## Step 2. Enable the RTC service


1. Make sure you have [added your billing information](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account#fb6c7c91).

2. In the console, select **BytePlus RTC** and click **Get started for free**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3321de242ae92c11d15ee666400fcc40.png) </span>

3. Confirm your order information and click **Next Step** to submit your payment information.


<span id="step-3-create-a-byteplus-rtc-app-and-get-the-appid"></span>
## Step 3. Create a BytePlus RTC App and get the AppID


1. In order to facilitate team collaboration and provide minimum access, you may consider using an IAM account. For instructions on how to create and authorize an IAM account, refer to [IAM overview](https://docs.byteplus.com/en/byteplus-platform/docs/overview-3).

2. After entering the BytePlus RTC Console, the system has automatically created a default application `defaultAppName` for you. You can manage the app in **Application Management**.

> Note:

> 1. App name is not AppId.

> 2. **AppID** is the unique identifier for each app. When calling BytePlus RTC SDK APIs (for example, to create an object), you must provide your AppID.

> 3. **AppKey** is the key for each app. Keep it in a safe place. The AppKey is used to generate authentication tokens. If your key is leaked, your traffic might be stolen or misused.

3. To create another app, click **Create App** in **Application Management**. For more information, see [Application Management](https://docs.byteplus.com/en/docs/12/docs-70064).
