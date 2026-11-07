---
title: "Real-time image processing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-realtime-image-processing"
---

Real\-time image processing applies transformations when an image URL is requested. Use it to resize, crop, pad, or change the format of stored images, including video snapshots and cover images.

For AI super resolution and processing tasks that save output files, see [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement). To upload and manage images, see [Managing image assets](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management).

## Constructing the image URL

Once you have an image asset, you access and process it by constructing a URL. The URL structure allows you to retrieve the original image or apply various transformations on\-the\-fly.

### Prerequisites

Before using the image processing and URL construction features, you must have the following ready:

* An image asset stored within the BytePlus VOD service.

* The `StoreUri` (storage identifier) for that image asset.

* An **image domain name** configured and enabled for your VOD space. For details, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management).

### URL construction rule

The image URL uses the following structure:

```Shell
{Protocol}://{Image_Domain}/{StoreUri}~{Processing_Method}.{Format}
```

The URL consists of the following elements:

|**Element** |**Description** |
|---|---|
|Protocol |You can use either HTTP or HTTPS. If you choose HTTPS, make sure to enable HTTPS for the image domain and configure the certificate. |
|Image_Domain |The image domain that you added to the BytePlus VOD console. For details, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management). |
|StoreUri |The unique storage identifier for the image file. For image assets, retrieve it from `OriginalImageInfo` or `ProcessedImageInfos` in [GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos). For materials, use [MaterialUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-materialuploadcomplete). For video snapshots, use [GetMediaInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getmediainfos) or [GetWorkflowExecutionResult](https://docs.byteplus.com/docs/byteplus-vod/reference-getworkflowexecutionresult). |
|Processing_Method |(Optional) A command that tells the system how to transform the image. If omitted, the original image is returned. See the [Image processing methods](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing#54777ae6) section below for all options. |
|Format |(Optional) The desired output format for the image. The available image formats are:<br><br><br>* `image`: Retains the original format of the image.<br><br>* `jpeg`: (Default) JPEG.<br><br>* `webp`: WebP.<br><br>* `avif`: Supports both static and animated AVIF images.<br><br><br>> **Warning**<br><br><br><br>* > To obtain images in JPEG format, the width and height of the original image must not exceed 65,535, or an error will occur.<br><br><br>* > For animated images, the processing timeout is set to 30 seconds. Upon timeout, the system returns the original image without reporting an error.<br> |

### URL construction example

Here's an example to demonstrate how to construct a cover image URL based on the aforementioned rules. Suppose we want to select a static image from video snapshots as the cover image. In this example:

* The image domain uses the HTTP protocol.

* The image domain is `vod.demo.com`.

* The obtained snapshot `StoreUri` is `tos-path-v-da1111/123456abcdef123456abcdef12345***`.

* We want to centrally crop the image with an aspect ratio of 720:480, so the cover image processing method is `tplv-vod-cc:720:480`.

* We want the cover image to retain the original format of the snapshot.

Based on these elements, we can construct the cover image URL as follows:

```Plain
http://vod.demo.com/tos-path-v-da1111/123456abcdef123456abcdef12345***~tplv-vod-cc:720:480.image
```

## Image processing methods

### Processing method reference

You can apply various transformations by specifying a `Processing_Method` in the URL.

> **Note**

> Charges depend on the processing tier. Please refer to [Image processing pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#8804d205) for detailed information on pricing and billing.

The available image processing methods are:

|Method |Parameters |Description |
|---|---|---|
|`tplv-vod-obj` |None |**Original image.**  Retrieves the original image without any modifications. |
|`tplv-vod-noop` |None |**Compressed image.**  Retrieves the original image with standard compression applied to reduce file size.<br><br>> **Note**<br><br><br>> This method does not support AVIF format.<br> |
|`tplv-vod-rs` |`:width:height` |**Resize & fit.**  Resizes the image to fit within the specified dimensions while maintaining the original aspect ratio. For example, `tplv-vod-rs:300:200`. If either the width or height is set to 0, the image will be scaled proportionally based on the other dimension. |
|`tplv-vod-cc` |`:width:height` |**Center crop.**  Crops the center of the image to the specified aspect ratio and then resizes it to the target dimensions. For example, `tplv-vod-cc:300:200`. If either the width or height is set to 0, the corresponding dimension of the original image will be used. |
|`tplv-vod-pad` |`:expand:width:height:color` |**Resize & pad.**  Resizes the image to fit within the target dimensions and fills the remaining space with a specified color.<br><br><br>* `expand`: Determines whether the original image should be stretched if its width and height are smaller than the desired dimensions. It supports the following values:<br><br>   * `1`: Stretch the original image to fill the desired width or height. The stretched image is centered in the output and padded with the specified color.<br><br>   * `0`: Do not stretch the original image. Instead, the original image will be directly centered in the output and the surrounding area will be filled with the specified color.<br><br>      > **Note**<br>      <br><br>      > Note that the `expand` parameter is only applicable when the width and height of the original image are smaller than the desired dimensions. If the original image is larger, it will be resized to fit the target dimensions while maintaining its aspect ratio.<br>      <br><br>* `width` and `height`: The desired width and height of the output image in pixels. Both values must be greater than 0.<br><br>* `color`: The color used for padding the image, in 6\-digit hexadecimal format. For example, FFFFFF represents the color white, while 000000 represents the color black. Please note that the '#' prefix is not required. |

### Image processing examples

Assuming the original width and height of the cover image are 640×360, as shown in the image below:

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a04ce4fe85854ea29078f2fe644683ee~tplv-goo7wpa0wc-image.image)

Here are the output images for different image processing methods:

* If you set the `Processing_Method` to `tplv-vod-rs:540:180`, the output image will have a width and height of 320×180, as shown in the image below:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3db8c763ec94f909efdc8162bf5aac2~tplv-goo7wpa0wc-image.image)

* If you set the `Processing_Method` to `tplv-vod-cc:540:180`, the output image will have a width and height of 540×180, as shown in the image below:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4a7d80ad9664cbc983ee4afef1615b6~tplv-goo7wpa0wc-image.image)

* If the `Processing_Method` is set to `tplv-vod-pad:0:800:700:ffff00`, the output image will have a width and height of 800×700, as shown in the image below:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c63f018d8d724582a66ac5dd6d0b8572~tplv-goo7wpa0wc-image.image)

## Use an image as a video cover

See [Video covers](https://docs.byteplus.com/docs/byteplus-vod/docs-video-cover) for associating an image with video metadata and retrieving its cover URL.
