---
title: "Image Resizing"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-image-resizing"
---

The original image can be resized. The following table lists the parameters and examples.

<span id="0111de37"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|m |Image resizing mode. |* lfit (default value): Proportionally resizes the original image as large as possible in a rectangle of `w` x `h`.<br><br>* mfit: Proportionally resizes the original image as small as possible outside a rectangle of `w` x `h`.<br><br>* fill: Proportionally resizes the original image as small as possible outside a rectangle of `w` x `h` (`mfit`) and cuts off the part outside the specified rectangle.<br><br>* pad: Resizes the original image as large as possible in a rectangle of `w` and `h` (`lfit`) and fills the blank area in the specified rectangle with a specified color (`color`).<br><br>* fixed: Fixes the width and height for resizing. |No |
|w |Width of the resized image. |[1,16384] |Yes |
|h |Height of the resized image. |[1,16384] |Yes |
|l |Length of the longer side of the resized image. |[1,16384] |Yes |
|s |Length of the shorter side of the resized image. |[1,16384] |Yes |
|limit |Specifies whether to resize the original image when it is smaller than the target image. |* 1 (default value): no (TOS returns the original image).<br><br>* 0: yes. |No |
|color |Fill color (in pad mode). |Hex color code. Value range: 000000–FFFFFF. The default value is FFFFFF, indicating white. |No |
|p |Image resizing in percent. |[1,1000]<br><br>A value smaller than 100 indicates to make an image smaller, and a value greater than 100 indicates to make it larger (`limit` is required for the latter case). |Yes |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Required: You need to specify one of the required resize parameters; otherwise, the MissingArgument error will occur.</div>


* <div data-tips="true" data-tips-type="tip">Longer side: The rate of the original size to the target size for the longer side is higher than that for the shorter side.</div>


* <div data-tips="true" data-tips-type="tip">Shorter side: The rate of the original size to the target size for the shorter side is lower than that for the longer side.</div>



<span id="be8c8311"></span>
## **Rectangle calculation and parameter priorities**


1. Specify both `w` and `h` to get a rectangle.

2. If you specify either `w` or `h`:

   * `lfit`, `mfit`, or `fixed`: TOS calculates the other parameter based on the original image size to get a rectangle.

   * `fill` or `pad`: TOS gets a square based on the specified parameter.

3. If you specify neither `w` nor `h`:

   1. If l and s are contained, TOS sets the longer side of the rectangle to `l` and the shorter side to `s`.

   2. If you specify either `l` or `s`:

      1. `lfit`, `mfit`, or `fixed`: TOS calculates the other parameter based on the original image size to get a rectangle.

      2. `fill` or `pad`: TOS gets a square based on the specified parameter.

   3. If you specify neither `l` nor `s`: TOS proportionally resizes the image by using `p`.


<span id="de0d63d4"></span>
## **Parameter calculation**

In this document, the original image size is 400 x 200 pixels.


1. If you set `w` to 100 and `h` to 100, you will get a 100 x 100 rectangle based on the parameter priority of `w` and `h`.

   * lfit: Proportionally resizes the original image as large as possible in the specified rectangle, that is, resizes it to 100 x 50.

   * mfit: Proportionally resizes the original image as small as possible outside the specified rectangle, that is, resizes it to 200 x 100.

   * fixed: Fixes the width and height at 100 to resize the original image to 100 x 100.

   * fill: Resizes the original image as in mfit mode and cut off the parts outside the specified rectangle (100 x 100).

   * pad: Resizes the original image as in lfit mode and fills the blank area in the specified rectangle (100 x 100) with a specified color.

2. If you set `w` to 200 and the aspect ratio of the original image is 2:1, `h` is 100. Then, TOS resizes the image based on the 200 x 100 rectangle.

3. If you set `l` to 200 and `s` to 100, TOS gets a rectangle with the longer side being 200 and shorter side being 100. As the width of the original image is the longer side and height is the shorter side, TOS resizes the image based on a 200 × 100 rectangle.

4. If you set `l` to 200, as the width of the original image is the longer side and the aspect ratio is 2:1, TOS resizes the image based on a 200 × 100 rectangle.


<span id="0d4de4d2"></span>
## Examples

Original image: [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this document, this image is used as the static image for all tests.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf215ff0fca444afa3ef432bc1f3d133~tplv-goo7wpa0wc-image.image) </span>


* Set the width to 100 for proportional resizing.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_100](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_100)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c75eea7278c47cd86c26730d397aa30~tplv-goo7wpa0wc-image.image) </span>

* Set the height to 100 for proportional resizing.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,h_100](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,h_100)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/833564dd27fa4fcf89de2e80a0c42ce5~tplv-goo7wpa0wc-image.image) </span>

* Set the longer side to 100 for proportional resizing.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,l_100](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,l_100)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f2d097f1b4b4211bf25f269fcb19263~tplv-goo7wpa0wc-image.image) </span>

* Set the shorter side to 100 for proportional resizing.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,s_100](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,s_100)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da39ff57201f4c7ba11b71afc73305c1~tplv-goo7wpa0wc-image.image) </span>

* Set the height to 200 and width to 200 in lfit mode.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_lfit](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_lfit)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b10b334082ff454b87f749efa929c86f~tplv-goo7wpa0wc-image.image) </span>

* Set the height to 200 and width to 200 in mfit mode.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_mfit](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_mfit)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce2542e2fc2d446bbcf264291649c850~tplv-goo7wpa0wc-image.image) </span>

* Set the height to 200 and width to 200 in fixed mode.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fixed](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fixed)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5b196e1b3be4e51a0e6e3c0b9c43abf~tplv-goo7wpa0wc-image.image) </span>

* Set the height to 200 and width to 200 in fill mode.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fill](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fill)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/019fe22d482f4ad381f3d266513a6fc3~tplv-goo7wpa0wc-image.image) </span>

* Set the height to 200, width to 200, and fill color to FF0000 (red) in pad mode.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_pad,color_FF0000](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_pad,color_FF0000)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/774acb0be486416b8176f1728f9af265~tplv-goo7wpa0wc-image.image) </span>

* Proportionally resize the image to 30%.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_30](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_30)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f752aa8b90ab427ca4cd9fa1c8278e24~tplv-goo7wpa0wc-image.image) </span>
