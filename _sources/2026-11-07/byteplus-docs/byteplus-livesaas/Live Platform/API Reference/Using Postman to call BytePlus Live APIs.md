---
title: "Using Postman to call BytePlus Live APIs"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis"
---

To test and debug BytePlus Live APIs, you can use the popular API client Postman. This guide provides step\-by\-step instructions on how to fork the official collection, configure authentication headers, and send your first request.

<span id="prerequisites"></span>
## Prerequisites


* A Postman account.

* A BytePlus account. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

* AccessKey ID (AK) and Secret Access Key (SK). To obtain them, go to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) \> **User Profile** \> **IAM** \> **Key management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36d6e087508a4a61914ea025d4158706~tplv-goo7wpa0wc-image.image) </span>


<span id="context"></span>
## Context

Postman provides a user\-friendly interface for sending API requests and allows you to easily inspect and analyze the responses. It supports a variety of request methods, including GET, POST, PUT, and DELETE, and enables you to add headers, parameters, and other data to your requests. With its robust features and intuitive interface, Postman has become an essential tool for API development and testing.

<span id="procedure"></span>
## Procedure


1. Use either the online or offline version of Postman.

   * Postman online version: Sign in to the [Postman online platform](https://www.postman.com/livesaas/workspace/byteplus-live/overview). Click **BytePlus Live Open API** on the left and click **Fork** to fork the BytePlus Live collection to your own workspace. You must fork the collection because requests cannot currently be sent from public workspaces. For more information about how to create a fork, see [Creating a fork](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis#creating-a-fork).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ae8dcfea7534baf9fbb01edfc310152~tplv-goo7wpa0wc-image.image) </span>

   * Postman offline version: Click **Import** and select the following file.

      [openapi-call-example.postman_collection.json](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eed499b8cade40f6ad95d12aa5b36727~tplv-goo7wpa0wc-image.image)

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d93480913664f6c9e15b3d1aa00ef44~tplv-goo7wpa0wc-image.image) </span>

2. Click the **View more actions** icon and select **Duplicate**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8c95d7e5c2c4d24a49e9054805f730a~tplv-goo7wpa0wc-image.image) </span>

3. Change the API name, request method, request URI, query parameters, and body parameters as needed. For more information, see the corresponding documentation for the API that you want to call.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f521e8d41bab40858db6b4da32fd6674~tplv-goo7wpa0wc-image.image) </span>

4. Replace the `AccessKey` and `SecretKey` values on the **Headers** tab with those you obtained in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis#152c47a4) section.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b6869ae77ac4b169f829fe5806c1692~tplv-goo7wpa0wc-image.image) </span>

5. Click **Send** to send the request.

6. View the response at the bottom of the page.


<span id="troubleshooting"></span>
## Troubleshooting

If the response returns an error, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes) for more information.

To avoid common errors, make sure that you meet the following requirements:


* The AK and SK match the keys obtained in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis#152c47a4) section.

* All required parameters are added.

* The added parameters and their corresponding values are correct.

* The request method and request URI are correct.


If the issue still persists, contact your sales representative for help. If you do not have a sales representative, click [here](https://www.byteplus.com/en/contact) to fill out the contact form, and a member of the BytePlus sales team will follow up with you.
