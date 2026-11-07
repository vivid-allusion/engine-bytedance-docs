---
title: "Original Image Protection"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-original-image-protection"
---

Original image protection is used to prevent anonymous users from stealing original images. If it is enabled, anonymous users can access images only through the URL with image style parameters or presigned URL. This topic describes how to use original image protection.

<span id="3ced8824"></span>
## **Description**

If original image protection is enabled, anonymous users can access images through:


* URLs with image style parameters, in the format of `https://<bucket name>.<Endpoint>/<image name>?x-tos-process=style/<style name>`. For more information, see [Using an Image Style](https://docs.byteplus.com/en/tos/docs/using-an-image-style?version=1.0.0).

* Presigned URLs in the format of `https://<bucket name>.<Endpoint>/<image name>?<signature>`.


<span id="39f35eaa"></span>
## Precautions

The original image protection function is in the invitation\-based testing state. If you need to use it, please contact your account manager.

<span id="5c70bc36"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Data Processing** \> **Image processing**.

4. On the **Image processing** page, click **Original image protection** tab,then click **Edit**.

5. In the **Original image protection** tab, set the following parameters:



|**Parameter** |**Description** |
|---|---|
|Current status |Specifies whether to enable **Original image protection**. |
|Original image protection suffix |Specifies the suffix of images to protect, that is, all images with this suffix in the bucket will be protected. Specifically:<br><br><br>* Valid values: \*, **png**, **jpg**, **jpeg**, **gif**, **bmp**, **tiff**, **heic**, **webp**.<br><br>* If you select \*, original image protection will apply to all objects in the bucket, including image and non\-image objects.<br><br>* Multiple suffixes can be selected. |
|Custom delimiter |You can use custom delimiters instead of the image style parameter (?x\-tos\-process=style/) to simplify image URLs. Valid values: en dash ( – ), underscore ( _ ), forward slash ( / ), exclamation point ( ! ).<br><br>For example, if the URL with the image style parameter is`https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=style/test`and you use an en dash ( – ) as the custom delimiter, the image URL can also be `https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg-test`. |



6. Click **Select.**
