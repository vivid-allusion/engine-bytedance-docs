---
title: "Mosaic"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Mosaic"
---

The mosaic feature allows you to apply a mosaic effect to an image. This topic introduces the parameters and provides examples of the mosaic feature.

<span id="ypriE44m"></span>
## Description


|**Parameter** |**Description** |**Value** |**Required** |
|---|---|---|---|
|g |The origin for selecting the area. |Possible values:<br><br><br>* nw (Default): Top left<br><br>* north: Top center<br><br>* ne: Top right<br><br>* west: Center left<br><br>* center: Center<br><br>* east: Center right<br><br>* sw: Bottom left<br><br>* south: Bottom center<br><br>* se: Bottom right |No |
|w |The width of the selected area. |Range: [0, Image width]. Default: The maximum value. |No |
|h |The height of the selected area. |Range: [0, Image height]. Default: The maximum value. |No |
|x |The horizontal offset of the starting point (X\-axis) relative to the specified origin (g). |A positive value shifts the starting point to the right, while a negative value shifts the starting point to the left. |No |
|y |The vertical offset of the starting point (Y\-axis) relative to the specified origin (g). |A positive value shifts the starting point down, while a negative value shifts the starting point up. |No |
|t |The type of the mosaic effect. |Possible values:<br><br><br>* square: Square<br><br>* blur: Gaussian blur<br><br><br>The default value is square. |No |
|r |The radius of the blur. |Range: [0, 50]. Default: 0.<br><br>This parameter only takes effect for Gaussian blur. The larger the value, the blurrier the image becomes. |No |
|s |The standard deviation for a normal distribution. |Range: [1, 50]. Default: 20.<br><br>This parameter only takes effect for Gaussian blur. The larger the value, the blurrier the image becomes. |No |


<span id="xD0r67qv"></span>
## Example

Create a mosaic that is 500 pixels wide and 500 pixels tall. Set the x\-offset to 100 and the y\-offset to 100. Finally, select the square mosaic option.

[https://tos-tools.tos-cn-beijing.volces.com/misc/sample.png?x-tos-process=image/mosaic,w_500,h_500,x_100,y_100,t_square](https://tos-tools.tos-cn-beijing.volces.com/misc/sample.png?x-tos-process=image/mosaic,w_500,h_500,x_100,y_100,t_square)
