---
title: "Watermarking"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-watermarking"
---

You can add text watermarks, image watermarks, and text\-image watermarks to images in TOS buckets. The following describes the parameters and examples of the watermark feature.

<span id="qOyBSb3h"></span>
## Constraints and limitations


* For limitations on the format and size of watermark images, see the Constraints and limitations section in [Overview](https://www.volcengine.com/docs/6349/153623).

* Once a watermark is applied, both the original image and the watermark become static.

* Adding a watermark using an SSE\-C\-encrypted image is currently not supported.


<span id="08465cc2"></span>
## Basic parameters

Basic parameters are available for both text and image watermarks. The following table lists the basic parameters.


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|t |Opacity of the text or image watermark. |* [0,100]<br><br>* Default value: 100, which indicates opaque. |No |
|g |Location of the watermark in an image. |* nw: upper\-left<br><br>* north: upper\-middle<br><br>* ne: upper\-right<br><br>* west: middle\-left<br><br>* center: middle<br><br>* east: middle\-right<br><br>* sw: lower\-left<br><br>* south: lower\-middle<br><br>* se (default value): lower\-right |No |
|x |Horizontal margin, that is, horizontal distance between the watermark and the image edge. This parameter is valid only when the watermark is on the upper left, middle left, lower left, upper right, middle right, or lower right of the image. |* [0,4096]<br><br>* Default value: 10<br><br>* Unit: px |No |
|y |Vertical margin, that is, vertical distance between the watermark and the image edge. This parameter is valid only when the watermark is on the upper left, upper middle, upper right, lower left, lower middle, or lower right of the image. |* [0,4096]<br><br>* Default value: 10<br><br>* Unit: px |No |
|voffset |Vertical offset from the middle line. This parameter is valid if the watermark is on the middle left, middle, or middle right of the image. |* [\-1000,1000]<br><br>* Default value: 0<br><br>* Unit: px |No |


<span id="6164b7dd"></span>
## Image watermark

The following table lists the image watermark parameters and preprocessed parameters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use watermark.jpg as the watermark image, the Base64\-encoded URL is <code>image/watermark,image_d2F0ZXJtYXJrLmpwZw</code>.</div>



|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|image |Object name of the watermark image, which must be a Base64\-encoded URL. The image needs to be in the same bucket as the target image. |Base64\-encoded string. |Required for watermark image adding |
|P |Percent to resize the watermark image. |This parameter is special for the resizing function and is valid only for watermark image preprocessing. |No |
|Other preprocessing operations |Watermark image preprocessing. |Image resizing, custom cropping, indexed slicing, or rotation can be performed on the image. |No |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A watermark image is preprocessed based on the value of image, which needs to be Base64\-encoded. For example, if you use watermark.jpg as the watermark image and resize it to 30%, the original parameter is <code>image_watermark.jpg?x-tos-process=image/resize,P_30</code> and the Base64\-encoded URL is <code>image_d2F0ZXJtYXJrLmpwZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxQXzMw</code>.</div>


<span id="fbd4bf6f"></span>
## Text watermark

The following table lists the text watermark parameters. You can specify the content, font, font size, and font color for a text watermark in the parameters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use "Hello world" as the text watermark, select fangzhengshusong as the font, and set the clockwise rotation degree to 45, the original parameter is <code>text_Hello world,type_fangzhengshusong,rotate_45</code> and the Base64\-encoded URL is <code>text_SGVsbG8gd29ybGQ,type_ZmFuZ3poZW5nc2h1c29uZw,rotate_45</code>.</div>



|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|text |Content of the text watermark, which needs to be a Base64\-encoded URL. |The string to encode can contain up to 128 characters. |Required for adding a text watermark |
|type |Font of the text watermark, which needs to be a Base64\-encoded URL. |The options are wqy\-zenhei (default), wqy\-microhei, fangzhengshusong, fangzhengkaiti, fangzhengheiti, fangzhengfangsong, and droidsansfallback. For more information on font encoding, see the table below. |No |
|color |Color of the text watermark. |Hex color code. Value range: 000000–FFFFFF. The default value is 000000, indicating black. |No |
|size |Size of the text watermark. |(0,1000]<br><br>Default value: 40<br><br>Unit: px |No |
|shadow |Shadow opacity of the text watermark. |[0,100]<br><br>Default value: 0, indicating no shadow |No |
|rotate |Degree of the clockwise rotation of the text watermark. |[0,360]<br><br>Default value: 0, indicating no rotation |No |
|fill |Specifies whether to fill the original image with the text watermark. |* 1: yes<br><br>* 0 (default value): no |No |


The following table lists options of **type** and the Base64\-encoded URLs.


|**Original Value** |**Base64\-Encoded URL** |**Font** |**Remarks** |
|---|---|---|---|
|wqy\-zenhei |d3F5LXplbmhlaQ |WenQuanYi Zen Hei |The filler ( = ) can be omitted. |
|wqy\-microhei |d3F5LW1pY3JvaGVp |WenQuanYi Micro Hei | |
|fangzhengshusong |ZmFuZ3poZW5nc2h1c29uZw |Fāng Zhèng Shū Sòng |The filler ( = ) can be omitted. |
|fangzhengkaiti |ZmFuZ3poZW5na2FpdGk |Fāng Zhèng Kǎi Tǐ |The filler ( = ) can be omitted. |
|fangzhengheiti |ZmFuZ3poZW5naGVpdGk |Fāng Zhèng Hēi Tǐ |The filler ( = ) can be omitted. |
|fangzhengfangsong |ZmFuZ3poZW5nZmFuZ3Nvbmc |Fāng Zhèng Fǎng Sòng |The filler ( = ) can be omitted. |
|droidsansfallback |ZHJvaWRzYW5zZmFsbGJhY2s |Droid Sans Fallback |The filler ( = ) can be omitted. |


<span id="923a9a61"></span>
## Text\-Image watermark

You can specify both an image and text for watermarking and arrange them by using the following text\-image watermarking parameters.


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|order |Order of the watermark text and image. |* 0 (default value): image in front of text<br><br>* 1: text in front of image |No |
|align |Alignment mode of text and image watermarks. |* 0: align text and image watermarks along their top edges.<br><br>* 1: align text and image watermarks along their central axes.<br><br>* 2 (default value): align text and image watermarks along their bottom edges. |No |
|interval |Margin between the text and image watermarks. |* [0,1000]<br><br>* Default value: 0<br><br>* Unit: px |No |


<span id="b2749e5a"></span>
## Examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to encode parameters of text and image watermarks with <a href="https://simplycalc.com/base64url-encode.php?spm=a2c4g.11186623.0.0.59c724cbw8IPL4">Base64URL Encode</a>.</div>


<span id="796e4bc6"></span>
### **Text watermark examples**


* Add the text watermark "Hello". Set the font size to 72, color to red, and font to fangzhengshusong.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/watermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/watermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d34c76fd3e14e75996af518cd0996dd~tplv-goo7wpa0wc-image.image) </span>

* Add the text watermark in the middle, rotate it 45 degrees clockwise, and set other parameters the same as above.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/watermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw,g_center,rotate_45](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/watermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw,g_center,rotate_45)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bcae9e33a8e49c181745e7dc20dfcf6~tplv-goo7wpa0wc-image.image) </span>

* Add the text watermark to fill the image and set other parameters the same as above.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/watermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw,g_center,rotate_45,fill_1](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/watermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw,g_center,rotate_45,fill_1)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06aede8d900d42cf9764fe33a32552ac~tplv-goo7wpa0wc-image.image) </span>


<span id="3138065c"></span>
### **Image watermark example**

Original image: [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/watermark1.png](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/watermark1.png)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1260ec4f2fc7422e96277cb04c8fa229~tplv-goo7wpa0wc-image.image) </span>


* Proportionally resize the original image to 60%, add it as the image watermark, resize it to 300%, and encode misc/watermark1.png?x\-tos\-process=image/resize,p_300 to bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6909a202772141589d99505e056406d5~tplv-goo7wpa0wc-image.image) </span>

* Add the image watermark in the middle, rotate it 45 degrees clockwise, and set parameters the same as above.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==,g_center,rotate_45](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==,g_center,rotate_45)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/044847e9fa2f40a3a54f355c0b60c2a9~tplv-goo7wpa0wc-image.image) </span>


<span id="a007b93d"></span>
### **Text\-image watermark**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can add a watermark containing both an image and text and arrange them using the following parameters.</div>



* Add a text\-image watermark and use the default values.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==,text_SGVsbG8](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==,text_SGVsbG8)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53842ead0c0746398a749b89bb1bd896~tplv-goo7wpa0wc-image.image) </span>

* Add a text\-image watermark, align the text on the left and image on the right along their central axes, and leave a 100 margin between them.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==,text_SGVsbG8,align_1,order_1,interval_100](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzMwMA==,text_SGVsbG8,align_1,order_1,interval_100)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e48d4f8b91c451eac58b22a396bd80b~tplv-goo7wpa0wc-image.image) </span>


<span id="344dc4bb"></span>
### **Adding multiple image and text watermarks**

Add watermark1.png and watermark2.png image watermarks and "Hello World" and "Hi" text watermarks.


* Proportionally resize them to 60%.

* Hello World: Set the font size to 60, font to fangzhengshusong, and color to 000000 (black). Put it in the upper\-right corner.

* Hi: Set the font size to 50, font to fangzhengkaiti, and color to FF0000 (red). Put it in the middle.

* watermark1.png: Proportionally resize it to 150%, put it in the lower\-left corner, set opacity to 60, and encode misc/watermark1.png?x\-tos\-process=image/resize,p_5 to bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzU=.

* watermark2.png: Proportionally resize it to 20%, put it in the lower\-right corner, and encode misc/watermark2.png?x\-tos\-process=image/resize,p_5 to bWlzYy93YXRlcm1hcmsyLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzU=.


[https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzE1MA==,g_sw/watermark,image_bWlzYy9taXNjX3dhdGVybWFyazIucG5nP3gtdG9zLXByb2Nlc3M9aW1hZ2UvcmVzaXplLHBfMjA=,g_se/watermark,text_SGVsbG8gV29ybGQ,g_ne,size_60,type_ZmFuZ3poZW5nc2h1c29uZw/watermark,text_SGk=,g_center,size_50,type_ZmFuZ3poZW5na2FpdGk,color_FF0000](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,p_60/watermark,image_bWlzYy93YXRlcm1hcmsxLnBuZz94LXRvcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSxwXzE1MA==,g_sw/watermark,image_bWlzYy9taXNjX3dhdGVybWFyazIucG5nP3gtdG9zLXByb2Nlc3M9aW1hZ2UvcmVzaXplLHBfMjA=,g_se/watermark,text_SGVsbG8gV29ybGQ,g_ne,size_60,type_ZmFuZ3poZW5nc2h1c29uZw/watermark,text_SGk=,g_center,size_50,type_ZmFuZ3poZW5na2FpdGk,color_FF0000)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c012c52a054e3b8621d952fc44916d~tplv-goo7wpa0wc-image.image) </span>
