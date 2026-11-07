---
title: "Custom Cropping"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-custom-cropping"
---

This section describes how to specify a point as the origin and crop a rectangle of a specified size. The following describes the parameters and examples.

<span id="8afd63e3"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|g |Origin of coordinates for cropping. |* nw (default value): upper\-left<br><br>* north: upper\-middle<br><br>* ne: upper\-right<br><br>* west: middle\-left<br><br>* center: middle<br><br>* east: middle\-right<br><br>* sw: lower\-left<br><br>* south: lower\-middle<br><br>* se: lower\-right |No |
|w |Width to crop. |[0,Image width]<br><br>Default value: maximum value |No |
|h |Height to crop. |[0,Image height]<br><br>Default value: maximum value |No |
|x |X\-axis offset to the origin. |On the x\-axis, positive values indicate offset to the right, and negative values indicate offset to the left. |No |
|y |Y\-axis offset to the origin. |On the y\-axis, positive values indicate offset downward, and negative values indicate offset upward. |No |


The following table describes the coordinates of origins, where srcW and srcH are the width and height of the original image.


|**Origin** |**Location** |
|---|---|
|nw |0, 0 |
|north |srcW/2 – w/2, 0 |
|ne |srcW – w, 0 |
|west |0, srcH/2 – h/2 |
|center |srcW/2 – w/2, srcH/2 – h/2 |
|east |srcW – w, srcH/2 – h/2 |
|sw |0, srcH – h |
|south |srcW/2 – w/2, srcH – h |
|se |srcW – w, srcH – h |


<span id="7365f35e"></span>
## Note


* If the calculated origin is out of the scope of the original image, the BadRequest error is returned and error information is "Advance cut's position is out of image".

* If the width and height specified from the origin exceed those of the original image, the original image is cropped to the boundaries.

* A multi\-frame image will become a single\-frame one after cropping.


<span id="198251ec"></span>
## Examples


* Use the default origin, set both the width and height to 400, and do not set the x\-axis or y\-axis offset.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/crop,w_400,h_400](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/crop,w_400,h_400)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e283942431148a0a25ba39729590d2d~tplv-goo7wpa0wc-image.image) </span>

* Use the default origin and set both the width and height to 400 and both the x\-axis and y\-axis offset to 50.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/crop,w_400,h_400,x_50,y_50](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/crop,w_400,h_400,x_50,y_50)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a0046a6a18b43e180270206feb39d2d~tplv-goo7wpa0wc-image.image) </span>
