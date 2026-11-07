---
title: "Custom Color Schemes"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Custom_Color_Schemes"
---

<span id="_1-概述"></span>
# 1. Overview

A custom color scheme allows you to use color standards defined by your company, team, or business requirements, in addition to the default visualization chart color schemes provided by the system. To standardize the color styles of multiple charts, you can add a custom color scheme and quickly apply it to visualization charts.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-不绑定数据项配色方案"></span>
## 2.1 Color schemes not bound to data items

**Step 1**: Using a bar chart as an example, click Custom color

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47847cb36606483dadfe9e24b925f9ec~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: In the pop\-up window, add a new color scheme

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2faceecfe5914aa2bdecaf1d66709397~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Add colors in sequence; the legend colors in the chart will be taken from the color palette in order

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e70ceea16e44445cb57b8b29a60d56af~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Edit the scheme name and save the color scheme

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfd08628a6c24556bae937d013866acd~tplv-goo7wpa0wc-image.image) </span>

**Step 5**: In "Edit color", select the color scheme

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/958d78729ab548daa03d16574918b1f2~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-绑定数据项配色方案"></span>
## 2.2 Color schemes bound to data items

**Step 1**: Select the required dimensions and metrics, and create the desired chart

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d0cd0ef6c694030a53363fe5ece97f9~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Expand the Edit color option below the chart panel and select Custom color

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a367a3412a4f469c9e82cc01b2863ab4~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Select Add color scheme and check Bind data items

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f0aa0a03cf34806a262a5559ce11e3c~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Bind the corresponding data items to colors. After manually entering a data item, press Enter to add it, or upload in bulk using the template. Click Save after configuration is complete

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d78a4815e41447029e7446b1a39d3907~tplv-goo7wpa0wc-image.image) </span>

**Step 5**: In Edit color, select the previously bound color scheme to apply it. If you change the chart conditions, the data items will remain bound to the configured colors and can be applied directly

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/561bd5927ef14464aff765e74634ec1e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-配色方案管理"></span>
## 3.1 Color scheme management

Created color schemes support editing and deletion. Click "Custom color". In the pop\-up window, hover over the corresponding color scheme, then click Edit or Delete to perform the respective operation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51b8a0237ff94c9f868399413ca6d223~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-修改配色方案"></span>
## 3.2 Modify color schemes

<span id="_3-2-1-未绑定数据项时的效果"></span>
### 3.2.1 Effects when not bound to data items

**When you add, delete, or modify colors, all charts using that color scheme will automatically reapply the updated scheme. For example:** 


* Change colors

   * Change green to red; all charts using this color scheme will have the legend color that was originally green changed to red.

* Delete color

   * Originally, there were three colors: red, green, and blue. After green is deleted, all charts using this color scheme will reapply the scheme, and the two remaining colors, red and blue, will be cycled through in order.

* Add color

   * Originally, there were three colors: red, green, and blue. After adding yellow, all charts using this color scheme will reapply the scheme, and red, green, blue, and yellow will be cycled through in order.


<span id="_3-2-2-绑定数据项时的效果"></span>
### 3.2.2 Effect when binding data items

**If add, delete, or modify operations are performed, all charts using this color scheme will reapply the color scheme. For example:** 

<span id="（1）更改颜色"></span>
#### (1) Change color


* The current chart's color scheme consists of three colors: red, green, and blue.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b80d0adec1ed4f5ba46d4babd844bf7a~tplv-goo7wpa0wc-image.image) </span>


* Now, change the **green corresponding to the "product_id" data item to yellow**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0b78c48d8c14361aa97596d2d049bbc~tplv-goo7wpa0wc-image.image) </span>


* After saving, in all charts using this color scheme, **the legend color corresponding to "product_id" is changed to yellow.** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd2ac7a1b1f14b0e81aefa3ca05a57c2~tplv-goo7wpa0wc-image.image) </span>

<span id="（2）更改数据项"></span>
#### (2) Change data item


* The current chart's color scheme consists of three colors: red, yellow, and blue.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a36f5cb7908d4f81a0dd9530c7f2ed1e~tplv-goo7wpa0wc-image.image) </span>


* Now, change the data item bound to yellow to "sale_price", and change the data item bound to blue to "product_id".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe6981325007457192ef4e7a14fa80b9~tplv-goo7wpa0wc-image.image) </span>


* After saving, in all charts using this color scheme, "Profit" is displayed in yellow, and "Cost Calculation" is displayed in blue.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/183ca309470e4a3a9b1ec23af3703e5d~tplv-goo7wpa0wc-image.image) </span>

<span id="（3）增加对应关系"></span>
#### (3) Add mapping relationship


* In all charts using this color scheme, data items that meet the criteria are **recolored according to the new mapping relationship**


<span id="（4）删除对应关系"></span>
#### (4) Delete mapping relationship


* In all charts using this color scheme, the corresponding data items are colored according to the setting for data items without a bound color.


<span id="_3-3-批量上传配色"></span>
## 3.3 Batch upload color schemes

The platform supports batch uploading of color schemes to quickly create color schemes.

When editing or adding a color scheme, click Download Template to download the batch color scheme template.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0af88ce29f984827be5c4a4ea99a8472~tplv-goo7wpa0wc-image.image) </span>

Fill in the color codes in the table in order and save. Hex values (such as #00000000) and rgba format (such as rgba(0,0,0,0.9)) are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc2d8da958624a0ebe4605c9edfd118d~tplv-goo7wpa0wc-image.image) </span>

In the color scheme editing interface, click Batch Upload and select the color scheme file to upload.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c32cae95c9346089cb7910f8bb24f79~tplv-goo7wpa0wc-image.image) </span>

The platform will automatically parse the color codes entered in the file to generate a color scheme. Once confirmed, just save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ba005c96b55491da0f71f3390199293~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-公共配色方案"></span>
## 3.4 Public color schemes

When creating or editing a color scheme, you can check "Set as public color scheme".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/013c8b9bb94442319e140f6e6fec6375~tplv-goo7wpa0wc-image.image) </span>

After checking and saving, this color scheme will become a public color scheme. Other users in the project can view and use this color scheme.

Switch to the "Public" tab in Edit Colors to see the saved public color schemes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cac345f679eb4b2e81d717336929915e~tplv-goo7wpa0wc-image.image) </span>
