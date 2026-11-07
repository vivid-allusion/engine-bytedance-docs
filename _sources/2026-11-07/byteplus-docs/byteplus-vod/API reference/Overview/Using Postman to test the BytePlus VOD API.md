---
title: "Using Postman to test the BytePlus VOD API"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-using-postman-to-test-the-byteplus-vod-api"
---

To quickly test and debug the BytePlus VOD API, you can use the popular API platform Postman. Postman is a popular tool for testing and debugging APIs. It provides a user\-friendly interface for sending API requests and allows you to easily inspect and analyze the responses. It supports a variety of request methods, including GET, POST, PUT, and DELETE, and enables you to add headers, parameters, and other data to your requests.

This guide provides step\-by\-step instructions on how to use the official BytePlus VOD API collection to configure your authentication credentials and send your first request.

<span id="04632a21"></span>
## Prerequisites


* A Postman account.

* A BytePlus account. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

* Contact your sales representative to activate BytePlus VOD for your BytePlus account.

* Get the Access Key ID (AK) and Secret Access Key (SK) of your account, which are used for API request authentication. To obtain them, log in to the [BytePlus console](https://console.byteplus.com/), click your account name in the upper right corner of the page, and then select **IAM** \> **Key Management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36d6e087508a4a61914ea025d4158706~tplv-goo7wpa0wc-image.image) </span>


<span id="f4545c25"></span>
## Procedure


1. Sign in to the [Postman online platform](https://www.postman.com/byteplus-vod-doc/workspace/byteplus-vod/overview).

2. Click **BytePlus VOD API** on the left and click **Fork** to fork the BytePlus VOD API collection to your own workspace to send a request, as requests cannot be sent in public workspaces right now. For more information about how to create a fork, see [Creating a fork](https://learning.postman.com/docs/collaborating-in-postman/using-version-control/forking-elements#creating-a-fork).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The BytePlus VOD API collection includes a pre\-request script for API authentication.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8db1cb30c4b94238be74bbbcaaa7c5ad~tplv-goo7wpa0wc-image.image) </span>

3. Click the **View more actions** icon and select **Duplicate** to duplicate the existing API.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2a930078a1043cab92cdc42173e470f~tplv-goo7wpa0wc-image.image) </span>

4. Change the API name, request method, request URI, query parameters, and body parameters as needed. For more information, see the corresponding documentation for the API that you want to call.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e092cc7aa92e4d6292108942e2c460cb~tplv-goo7wpa0wc-image.image) </span>

5. Replace the AccessKey and SecretKey values on the **Headers** tab with your AK and SK obtained in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-vod/reference-using-postman-to-test-the-byteplus-vod-api#Prerequisites).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c5f22c5e5f14915afaedb12e21ff44f~tplv-goo7wpa0wc-image.image) </span>

6. Click **Send** to send the request.

7. View the response at the bottom of the page.


<span id="13b2f178"></span>
## Troubleshooting

If the response returns an error, see [Shared errors](https://docs.byteplus.com/en/byteplus-vod/reference/common-error-codes) for more information.

To avoid common errors, make sure that you meet the following requirements:


* The AK and SK are the ones obtained in the [Prerequisites](https://docs.byteplus.com/docs/byteplus-vod/reference-using-postman-to-test-the-byteplus-vod-api#Prerequisites).

* All required parameters are added.

* The added parameters and their corresponding values are correct.

* The request method and request URI are correct.


If the issue still persists, contact your sales representative for help. If you do not have a sales representative, click [here](https://www.byteplus.com/en/contact) to fill in the form so that the BytePlus sales team can contact you later.
