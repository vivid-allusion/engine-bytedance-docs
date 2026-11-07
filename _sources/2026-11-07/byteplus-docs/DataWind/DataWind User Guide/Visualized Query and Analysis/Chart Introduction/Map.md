---
title: "Map"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Map"
---

<span id="_1-概述"></span>
# 1. Overview

A map is a chart that is categorized by continent, country, province, and city, and is used to display geographic information and related data. On a map, the magnitude of an indicator can be distinguished by color intensity. The product currently supports world maps and China maps. The world map supports continent\-level and country\-level views, while the China map supports province\-level and city\-level views.

In the visualization query editing interface, you can see the following map icon in the chart:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cb48d18be0e4d5896525624e2cdfae8~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In map charts, the number of decimal places for latitude and longitude data must not exceed five; otherwise, the map chart may not render properly.</div>


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

The map visualization format is suitable for analysis projects that require spatial data or datasets containing geographic location information, which can greatly enhance the reader's spatial awareness. For example, the average temperature in January across different administrative divisions.

**Map example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7a862e58d2946b6ac4e3c2ae8c361f9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set the geographic role**

[1. Overview of dimension field configuration](https://docs.byteplus.com/docs/DataWind/Dimension_Field_Configuration#_1-%E7%BB%B4%E5%BA%A6%E5%AD%97%E6%AE%B5%E9%85%8D%E7%BD%AE%E6%A6%82%E8%BF%B0)


* In editing, you need to set the geographic role for the region field in the dimension. For example, for the country field below, click the ⋮ next to the field, select the geographic role as Country/Region, and similarly set the geographic role for the province field in the following figure to match Province/Autonomous Region.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4359478dc5354d7393466ae6ff3349a3~tplv-goo7wpa0wc-image.image) </span>


* Generally, geographic roles have hierarchical relationships. You can set a hierarchy for country and province. For example, click the right side of Country, select Create Hierarchy "Country\-Hierarchy", and then add Province to the newly created "Country\-Hierarchy".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0b5aeab99e84dbf924657f956919186~tplv-goo7wpa0wc-image.image" width="508px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d1288008bf94dd4bb12a07bbaa701cc~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- Map**

Select Filled Map here, or choose from more map types. The following sections will introduce operations for multiple map types.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9988e5720c3b454a932d33d58323859e~tplv-goo7wpa0wc-image.image" width="661px" /></div>


**Step 3: Drag dimension and metric fields**


* Drag or click the sale_province field in the hierarchy you just set to the dimension area.

* Drag or click the member count field to the metric area.

* As shown below, the following effect will appear.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/252df7df15614bd2b388c3caf2e9049c~tplv-goo7wpa0wc-image.image) </span>


* Click the China map in the chart to drill down into detailed data for each province and city in China.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7f2c3f45ed04f0782436e2957514bd1~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/855f465af0fb458196ab041915523d96~tplv-goo7wpa0wc-image.image) </span>

**Step 4: Modify the chart color scheme as needed** For example, use the registration channel to distinguish the registration channels of members in each province.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c5323ab2574d43936d67610fb80dcd~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-编辑地理角色"></span>
## 3.1 Edit geographic roles

<span id="_3-1-1-填充地图-标记地图"></span>
### 3.1.1 Filled map/marker map


* When using maps, the dimension field must be a geographic role field. If it is not a geographic role field, the visualization chart area will display "The dimension field used by this chart must be set as a geographic role."


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba6345e110304e86b0f15d4de1528131~tplv-goo7wpa0wc-image.image) </span>


* In the field list area, you can set the geographic role for a field and match the field's values with the geographic role. You can choose to match "Country/Region" or "Province/Autonomous Region" (applicable to filled maps/marker maps). This method also allows for custom matching of geographic roles, overcoming the limitations of automatic parsing. The currently available geographic roles include: continent, country/region, province/autonomous region, city, county/district, street, dimension, longitude, latitude and longitude, and location matching.

* Operation: Click the ⋮ next to the corresponding field, select geographic role, and after selecting the geographic role type, configure the matching relationship between the field values and the geographic role in the pop\-up window.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9c7fa5de60c4c8d8e5643c5255d25a7~tplv-goo7wpa0wc-image.image" width="548px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ad7daf6fe7546cd9070208d716d8e92~tplv-goo7wpa0wc-image.image) </span>


* To modify the matching relationship, click the ⋮ next to the corresponding field and reselect as needed.

* You can also select geographic role \- location matching to enable automatic location matching. For any modifications to the automatic matching, click to edit.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb1ca55aaeec4576a493041f44959b0e~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e00c2d57ce164775bf3cb236e722b935~tplv-goo7wpa0wc-image.image) </span>

**Note:**  *Only one geographic role can be set for a field; it cannot be set as both "Country/Region" and "Province/Autonomous Region" at the same time.* 

<span id="_3-2-填充地图-标记地图"></span>
## 3.2 Filled map/marker map

<span id="_3-2-1-颜色-编辑颜色"></span>
### 3.2.1 Color/edit color


* If there is no dimension in the color (as in the following case), the color attribute applies to the metric.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5a67767327c45baabdbcb779173d3d2~tplv-goo7wpa0wc-image.image) </span>


* There are six default color schemes. By default, the larger the value, the darker the color. Click color inversion to reverse the relationship between the color gradient and the value magnitude.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a46f44fa33341c8909ec043f8c10fed~tplv-goo7wpa0wc-image.image" width="333px" /></div>



* You can also [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4188e66cf924387803762c5011983ae~tplv-goo7wpa0wc-image.image) </span>


* If there is a dimension in the color (as in the following case), the color attribute applies to the dimension.

   * The system provides a default color scheme that can be used directly. After applying it, you can also click on an individual dimension field to modify its color scheme.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5de6312fb2a41c4b5ebc047aeebd15c~tplv-goo7wpa0wc-image.image" width="295px" /></div>



* You can also select [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).


<span id="_3-2-2-图例"></span>
### 3.2.2 Legend


* You can choose whether to enable the legend. Once enabled, you can drag the legend's range to display data for different ranges on the chart.

* You can configure the legend's display position, alignment, maximum number of rows, label font, and font color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce1e30cf8c524018ad2feaf5a7136c94~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-3-标签"></span>
### 3.2.3 Labels


* You can choose whether to enable labels. When enabled, the dimension or metric values will be displayed at the corresponding locations on the map.

* You can select the default style or a custom style. Custom styles allow you to choose the display method, label font, and displayed content.


Caution: In the display method, only one of "Sparse display" or "Allow overlap" can be selected. If one is selected, the other will be grayed out, with a prompt stating "Allow overlap and sparse display cannot be selected at the same time." When the default label display is crowded, it is recommended to select "Sparse display."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1ed1cb0a23e491bba38ab88b53b9095~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-4-提示信息"></span>
### 3.2.4 Tooltips


* You can choose whether to enable tooltips. When enabled, hovering the mouse over a location on the chart will display the data corresponding to that location. By default, the current dimension and metric values are shown.

* You can add fields to single\-point data. The added fields are displayed only as tooltip information and are not involved in chart calculations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1daca5dd22234d45978c750a3e9fd077~tplv-goo7wpa0wc-image.image) </span>


* In advanced settings, you can customize the tooltip content, configure font styles, and insert charts.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c454bee18ab64b7fb32d175a0d12d928~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52bd561988234817a87737946019a191~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-lbs-标记地图"></span>
## 3.3 Map drill\-down

When the geographic data contains hierarchical relationships of geographic locations (such as continent\-country\-province\-city), the drill\-down feature is supported.

> This feature needs to be used in conjunction with [Drill Up and Drill Down](https://docs.byteplus.com/docs/DataWind/Drill_Up_and_Drill_Down).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60241406d5d2422cb415bbfd2dfb95ca~tplv-goo7wpa0wc-image.image) </span>

(1) Taking province/city drill\-down as an example, after setting the geographic roles for the province and city fields, move the mouse to the province field, click ┇, select Create Hierarchy, and complete the hierarchy creation.

> This step requires dataset editing permissions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea58a708ee374ecd869f7e532cacf80a~tplv-goo7wpa0wc-image.image) </span>

(2) You will see that a hierarchical structure appears in the field list. Hover the mouse over the city field, click ┇, select Add to hierarchy, and add the city field to the hierarchy created in the previous step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19e98009dcf84ceebc1325d93847a58b~tplv-goo7wpa0wc-image.image) </span>

(3) After completing the configuration, the hierarchy will be displayed as follows, allowing you to perform drill\-down operations. Use the province field as the map dimension to draw a map of China, as shown in the figure.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aadea721c99469aa0976bc665aab23d~tplv-goo7wpa0wc-image.image) </span>

(4) Click the province on the map that you want to view to drill down.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c3bd1b953854d9e81618bcfe2ba59de~tplv-goo7wpa0wc-image.image) </span>

The same principle applies to drilling down from continent level to country level on the world map. You also need to create and configure the hierarchy, after which drill\-down is available.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36cf63d9a1254c3d976e6a318fa83dae~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-更多说明"></span>
## 3.4 More information

 **(1) Note**

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

 **(2) Geographic information in the English environment**

To meet overseas usage requirements, when the product is switched to the English language, the match location for geographic roles (including country/region, province/autonomous region, and city) will automatically switch to English.

 **(3) In\-chart control style settings**

In\-chart controls include in\-chart filters, dynamic dimensions/metrics, and in\-chart parameters. Once displayed in the chart, you can adjust the layout of titles and filter content, as well as the layout settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34fab67d49be423ba1ec8f56477dd225~tplv-goo7wpa0wc-image.image) </span>


* Restore default settings: Click Restore Default Settings, and all the above chart configurations will be restored to default.

    **(4) Special reminder**

* Street\-level analysis is not supported for Hong Kong, Macao, and Taiwan.

* Currently, due to data compliance requirements and related factors, the world map (covering continent and country levels) is not supported in the SaaS version. We are actively planning related product features and expect to support the world map in future product versions to provide a more comprehensive user experience.
