---
title: "Draw"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Draw"
---

The draw feature allows you to draw points and lines on an image. This topic introduces the parameters and provides examples of the draw feature.

<span id="G67t43ai"></span>
## Description


|**Parameter** |**Description** |**Value** |**Required** |
|---|---|---|---|
|p |Point position |To draw three points at the coordinates (50,50), (100,100), and (200,200), enter `50x50-100x100-200x200`. |Yes |
|r |Point radius |The default value is 6. |No |
|l |Specifies whether to draw lines between the points. |Possible values:<br><br><br>* true: Yes.<br><br>* false: No. |No |
|lw |Line width |Width of the lines used to connect points. The default value is 3. |No |
|color |Color |A hexadecimal color code ranging from 000000 to FFFFFF. The default is 000000 (black). |No |


<span id="6GYSjclA"></span>
## Example

Draw five points at the following coordinates: (50, 50), (50, 100), (100, 100), (100, 200), and (200, 200). Set the point radius to 10, connect the points with lines, and set the line width to 3 and the line color to blue.

[https://tos-tools.tos-cn-beijing.volces.com/misc/sample.png?x-tos-process=image/draw,p_50x50-50x100-100x100-100x200-200x200,r_10,l_true,lw_3,color_0000FF](https://tos-tools.tos-cn-beijing.volces.com/misc/sample.png?x-tos-process=image/draw,p_50x50-50x100-100x100-100x200-200x200,r_10,l_true,lw_3,color_0000FF)

&nbsp;
