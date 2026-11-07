---
title: "Creating an Image Style"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-creating-an-image-style"
---

An image style is a template that contains multiple image processing parameters such as format conversion and progressive display. You can use it to uniformly process multiple images to simplify operations. This topic describes how to create an image style using the graphical user interface (GUI) or API code.

<span id="aab85541"></span>
## Precautions


* A bucket supports up to 100 image styles.

* The image style function is in the invitation\-based testing state. If you need to use it, please contact your account manager.


<span id="036d0831"></span>
## **Creating a style using the GUI**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Data processing** \> **Image processing**.

4. On the **Image processing** page, click **style** tab,then click **Create style**.

5. On the **Create style** page, click **Basic Edit**, set the following parameters, and click **Create**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When setting style parameters, you can preview the processed image and its API code on the right of the <strong>Create style</strong> page.   </div>
   

   
   |**Parameter** |**Description** |
   |---|---|
   |Rule name |Specifies the style name,which should conform to the following rules:<br><br><br>* It can start with uppercase and lowercase letters, digits, or underscores ( _ ) only.<br><br>* It can contain digits, uppercase and lowercase letters, underscores ( _ ), en dashes ( – ), and periods ( . ) only.<br><br>* It must contain 1–256 characters. |
   |Rule effective prefix |Set the prefix of the object for which the style is applied. If left blank, the style will be applied to all objects in the bucket. The format for entering the prefix is as follows:<br><br><br>* Supports Chinese, English, numbers, and common characters.<br><br>* Do not support starting with a forward slash (/) or backslash (), and do not support using consecutive forward slashes (/).<br><br>* Do not support the use of ".." as a directory name.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The same style can have up to 10 different effective prefixes configured, and there should be no inclusion relationship between the prefixes. For example, when setting multiple effective prefixes for the same style, if prefix 1 is set as "event", then prefix 2 cannot be set as "event/test". You can create multiple styles with the same name, and then configure different effective prefixes for each style, so that the same style can handle images with different prefixes, resulting in different effects.</div><br> |
   |Format conversion |Specifies the target format of the image, which can be **Original Format**, **jpg**, **jpeg**, **png**, **bmp**, **gif**, **webp, or tiff**. The default value is **Original Format**. |
   |Progressive display |Specifies whether to enable progressive display, where the image looks blurry and then sharpens as more data is loaded. **Progressive Display** is disabled by default.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only for JPG images.</div><br> |
   |Adaptive direction |Specifies whether to rotate according to the EXIF orientation information of the original image. **Adaptive Direction** is enabled by default.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only if the orientation parameter is specified for the original image.</div><br> |
   |Image quality |Specifies whether to compress the original image and adjust its quality. The default value is **Relative Quality**, with a compression percent of **90**. Below are the different values:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Image quality is only valid for JPG and WEBP images. For WEBP images, relative quality is the same as absolute quality.</div><br><br><br><br>* **Relative Quality**: compresses the original image by q%.<br><br>* **Absolute Quality**: compresses the image to Q%. It does not depend on the original image.<br><br>* **No compression**: the original image is not compressed. |
   |Resizing method |Specifies whether to resize the image, which can be **No Resize** (default),**Scale Down, Scale Up**, or **Specified Width and Height Resizing Mode**.<br><br>If you select **Specified Width and Height Resizing Mode**, **Fixed Width + Adaptive Height**, **Fixed Height + Adaptive Width**, and more options are available.<br><br><br>* **Fixed Width + Adaptive Height**: proportionally resizes the image based on a fixed width.<br><br>* **Fixed Height + Adaptive Width**: proportionally resizes the image based on a fixed height.<br><br>* **Fixed Width & Height + Resize by Longer Side**: proportionally resizes the original image as large as possible in a rectangle with a fixed width and height.<br><br>* **Fixed Width & Height + Resize by Shorter Side**: proportionally resizes the original image as small as possible outside a rectangle with a fixed width and height.<br><br>* **Fixed Width & Height + Resizing Fill**: resizes the original image as large as possible in a rectangle with a fixed width and height, centers it in the rectangle, and fills the blank area with a specified color.<br><br>* **Fixed Width & Height + Center Crop**: proportionally resizes the original image as small as possible outside a rectangle with a fixed width and height, and then crops the resized image from the center based on the specified width and height.<br><br>* **Fixed Width & Height**: resizes the image based on a fixed width and height. |
   |Image brightness |Specifies the image brightness. The value range is \-100 to 100, and the default value is 0. Valid values:<br><br><br>* A negative value decreases brightness.<br><br>* 0 indicates no brightness adjustment.<br><br>* A positive value increases brightness. |
   |Image contrast |Specifies the image contrast. The value range is \-100 to 100, and the default value is 0. Valid values:<br><br><br>* A negative value decreases the amount of contrast.<br><br>* 0 indicates no contrast adjustment.<br><br>* A positive value increases the amount of contrast. |
   |Image sharpening |Adjusts the image clarity. The value range is 50–399. **Image Sharpening** is disabled by default.<br><br>The larger the value, the clearer the image. But a value too large may distort the image. 100 is recommended for optimal effect. |
   |Image blur |Specifies whether to blur the image. **Image Blur** is disabled by default. If it is enabled, you need to set the following parameters:<br><br><br>* **Blur Radius**: The value range is 1–50. The larger the value is, the blurrier the image becomes.<br><br>* **Blur Standard Deviation**: The value range is 1–50. The larger the value is, the blurrier the image becomes. |
   |Image rotation |Specifies the degrees to rotate the image clockwise. The value range is 0–360, and the default value is 0.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the degree is not 90, 180, 270, or 360, the processed image will be larger in size.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The image width or height can be up to 4,096 pixels.</div><br> |
   |Watermark method |Specifies whether to add an image watermark or text watermark to the image. Image and text watermarks cannot be set at the same time. The default value is **No Watermark**. Below are some of the parameters:<br><br><br>* **Image Watermark:**  If you select this option, you need to set the path, preprocessing, opacity, and other parameters for the watermark image. Note:<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to preview the watermark effect, you need to set the permission of the watermark image to Public Read.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The watermark image must be in the same bucket as the original image; otherwise, it will fail to be applied.   </div><br>   <br><br>   * **Watermark Image Path**: specifies the path of the image in the bucket. For example, if the watermark image is named "abc.jpg" and stored under folder "test" in the bucket, the path will be `test/abc.jpg`.<br><br>   * **Proportion**: specifies the proportion of the watermark image to the original image. This parameter is available if you enable **Watermark Image Preprocessing**.<br><br>   * **Vertical Margin**: specifies the distance between the watermark and the bottom edge of the image. This parameter is valid only when the watermark is on the upper left, upper middle, upper right, lower left, lower middle, or lower right of the image.<br><br>   * **Horizontal Margin**: specifies the distance between the watermark and the right edge of the image. This parameter is valid only when the watermark is on the upper left, middle left, lower left, upper right, middle right, or lower right of the image.<br><br>* **Text Watermark:**  If you select this option, you need to set the text content, font, font size, degrees of clockwise rotation, and other parameters. Below are some of the parameters:<br><br>   * **Text Content**: It can contain up to 16 characters.<br><br>   * **Text Font**: Valid values are Default (that is, WenQuanYi Zen Hei), WenQuanYi Zen Hei, WenQuanYi Micro Hei, Fāng Zhèng Shū Sòng, Fāng Zhèng Kǎi Tǐ, Fāng Zhèng Hēi Tǐ, Fāng Zhèng Fǎng Sòng, and Droid Sans Fallback.<br><br>   * **Vertical Margin**: specifies the distance between the text and the bottom edge of the image. This parameter is valid only when the watermark is on the upper left, upper middle, upper right, lower left, lower middle, or lower right of the image.<br><br>   * **Horizontal Margin**: specifies the distance between the text and the right edge of the image. This parameter is valid only when the watermark is on the upper left, middle left, lower left, upper right, middle right, or lower right of the image. |
   


<span id="c50a8104"></span>
## **Creating a style using API code**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Data processing** \> **Image processing**.

4. On the **Image processing** page, click **style** tab,then click **Create style**.

5. On the **Create Style** page, click **Advanced Edit**, set the following parameters, and click **Create**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Rule Name |Specifies the style name,which should conform to the following rules:<br><br><br>* It can start with uppercase and lowercase letters, digits, or underscores ( _ ) only.<br><br>* It can contain digits, uppercase and lowercase letters, underscores ( _ ), en dashes ( – ), and periods ( . ) only.<br><br>* It must contain 1–256 characters. |
   |Rule effective prefix |Set the prefix of the object for which the style is applied. If left blank, the style will be applied to all objects in the bucket. The format for entering the prefix is as follows:<br><br><br>* Supports Chinese, English, numbers, and common characters.<br><br>* Do not support starting with a forward slash (/) or backslash (), and do not support using consecutive forward slashes (/).<br><br>* Do not support the use of ".." as a directory name.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The same style can have up to 10 different effective prefixes configured, and there should be no inclusion relationship between the prefixes. For example, when setting multiple effective prefixes for the same style, if prefix 1 is set as "event", then prefix 2 cannot be set as "event/test". You can create multiple styles with the same name, and then configure different effective prefixes for each style, so that the same style can handle images with different prefixes, resulting in different effects.</div><br> |
   |Code |Type API code in the format of `image/action1,parame_value1/action2,parame_value2/...`. For example, to set the width to 200, type `image/resize,w_200`.<br><br>For more information, see [Image Processing Parameters](https://docs.byteplus.com/en/tos/docs/overview_2?version=1.0.0). |
   


<span id="08d5c50b"></span>
## **Further operations**

After an image style is created, you can use it to process imagesas instructed in [Using an Image Style](https://docs.byteplus.com/en/tos/docs/using-an-image-style?version=1.0.0).

<span id="bcc4322d"></span>
## **Related operations**


* Exporting a style

   On the **Image Processing** page, select a style and click **Export style** to save it locally.

* Importing a style

   On the **Image Processing** page, click **Import style** and select a local style.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The imported style must be in txt format, be no larger than 256 KB, and conform to the style specifications.   </div>
