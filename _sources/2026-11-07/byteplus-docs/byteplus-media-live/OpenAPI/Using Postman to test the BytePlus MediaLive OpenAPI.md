---
title: "Using Postman to test the BytePlus MediaLive OpenAPI"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-using-postman-to-test-the-byteplus-medialive-openapi"
---

Postman is a popular tool for testing and debugging APIs. It provides a user\-friendly interface for sending API requests and allows you to easily inspect and analyze the responses. It supports a variety of request methods, including GET, POST, PUT, and DELETE, and enables you to add headers, parameters, and other data to your requests.

This article describes how to use Postman to test the BytePlus MediaLive OpenAPI.

<span id="ee247ee9"></span>
## Prerequisites


* A Postman account.

* A BytePlus account. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

* [Activating the BytePlus MediaLive service](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started#da5a6a63).

* After your service is enabled, log in to the [BytePlus console](https://console.byteplus.com/), click your account name in the upper right corner of the page, and then select **IAM** \> **Key management** to get the Access Key ID (AK) and Secret Access Key (SK) of your account, which are used for API request authentication.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f6dc1b6f2bc466785242136a7995c07~tplv-goo7wpa0wc-image.image) </span>

<span id="f11782de"></span>
## Procedure


1. Sign in to the [Postman online platform](https://www.postman.com/byteplus-medialive-docs/workspace/byteplus-medialive).

2. Click **BytePlus MediaLive OpenAPI** on the left and click **Fork** to fork the entire collection to your own workspace.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c6064319e6e44f982725c3f053fcbff~tplv-goo7wpa0wc-image.image) </span>


3. In your own workspace, select the DescribeDomain API and then click the **Headers** tab.

4. Replace the AK and SK values in the **Headers** tab with your AK and SK obtained in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-media-live/docs-using-postman-to-test-the-byteplus-medialive-openapi#Prerequisites).

5. Click the **Body** tab and replace the domain with your own domain name in `DomainList`.

6. Click **Send** to send the request.


You can view the response at the bottom of the page.
