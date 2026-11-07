---
title: "Indexed Slicing"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-indexed-slicing"
---

In indexed slicing, the upper\-left point is the starting point, width represents the x\-axis, and height represents the y\-axis. This section describes how to slice the original image to a specified size and get the slice. The following table lists the parameters and examples.

<span id="cba0c9c8"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|x |Length of each slice after horizontal slicing. |[1,Image width]You can specify either x or y. |Yes |
|y |Length of each slice after vertical slicing. |[1,Image height]You can specify either x or y. |Yes |
|i |Number of the slice to get. |If there are n slices, the value range is [0,n\-1] and the default value is 0. |No |


<span id="65c27f33"></span>
## Note


* If there are n slices, the value range of i is [0,n\-1]. The value 0 indicates the first slice. If the value exceeds the maximum number, the original image is returned.

* If both x and y are specified and valid, the value of y prevails.


<span id="7d22116d"></span>
## Examples


* Set x to 200 and i to 0.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/indexcrop,x_100,i_0](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/indexcrop,x_100,i_0)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf7b0976a2cf415a9098cac54bafe830~tplv-goo7wpa0wc-image.image) </span>

* Set y to 200 and i to 0.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/indexcrop,y_200,i_0](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/indexcrop,y_200,i_0)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651987e40daa411baf4eb5f7bfa5243b~tplv-goo7wpa0wc-image.image) </span>

* Set both x and y to 200 and i to 0.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/indexcrop,x_200,y_200,i_0](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/indexcrop,x_200,y_200,i_0)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7063d6a931824fc6b43d0010ddeea049~tplv-goo7wpa0wc-image.image) </span>
