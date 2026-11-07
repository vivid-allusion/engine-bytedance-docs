---
title: "Sourcemap upload error"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Sourcemap_upload_error"
---

This article introduces the various error messages that may occur when uploading Soucemap in Webpro, as well as the corresponding solutions.

<span id="3c35ce84"></span>
## 1 Note Cannot find module 'tslib'

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6785bda478ea4517a7b4a21dbe162682~tplv-goo7wpa0wc-image.image) </span>

Reason: Missing required dependencies for the reporting plugin

Solution: Just run `npm install tslib --save-dev` to install the tslib dependency.

<span id="b2f1f575"></span>
## 2 Note: AxiosError: Request failed with status code 401

Reason: There is an error in the aid, API_KEY, or API_Token you entered. Please confirm that you have entered them correctly.

Solution: Correctly enter aid, API_KEY, and API_Token

&nbsp;
