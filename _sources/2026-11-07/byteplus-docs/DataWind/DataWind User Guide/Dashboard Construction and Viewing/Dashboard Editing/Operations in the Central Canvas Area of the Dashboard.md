---
title: "Operations in the Central Canvas Area of the Dashboard"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Operations_in_the_Central_Canvas_Area_of_the_Dashboard"
---

Dashboard editing, also referred to as dashboard design, dashboard creation, or dashboard layout, is the process of combining and arranging components (widgets) such as charts, text, images, and filters to construct a data story dashboard based on business logic. This article introduces the editing operations of the central canvas area of the dashboard.

<span id="_1-概述"></span>
# Function overview

The new dashboard editing interface is divided into the top navigation area, the left widget area, the central canvas area, the right page configuration area, and the bottom multi\-page editing area.

This article introduces the central canvas area. As shown in the figure below, the blue highlighted area in the middle is the central canvas area. This area is the display area of the dashboard editing page, where users can design chart combinations, adjust page layouts, and perform specific operations on individual charts. This article introduces how to adjust the layout settings of the central canvas area and specific methods for operating charts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b81ae9deb91a45b3aa34de26e7c8e810~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-图表布局调整"></span>
# Chart layout adjustment

The entire page layout supports switching between tile layout and free layout. When switching the dashboard from free layout to tile layout, the current dashboard layout style may change.

<span id="_2-1-1-磁贴布局"></span>
## Tile layout

In tile layout, all chart widgets are automatically snapped into place and do not overlap by default. On the same layer, an intelligent auto\-layout is applied, and adjustments can be made by moving and resizing different charts within the same layer.


* To enable a single chart to float, for example, to overlap chart A on chart B while maintaining a free layout, set chart A as floating. This allows chart A to be dragged to overlap with chart B.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b12def161554ef79afd3a140d1b69e6~tplv-goo7wpa0wc-image.image) </span>

* By selecting multiple widgets, you can group them and move them together for layout configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68b53fbbacf74b738cc190ce1bbfffa2~tplv-goo7wpa0wc-image.image) </span>

* In editing mode, the canvas supports adjusting its zoom ratio according to the current viewport size.

   In tile layout mode, the canvas and chart components can automatically adjust their scaling ratio based on the current viewport size, ensuring that there is no horizontal scroll bar when entering the editing page. If the scaling ratio is adjusted manually, automatic scaling will not occur.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the zoom ratio reaches the minimum change value (1080), automatic scaling will stop, and a horizontal scroll bar will appear.   </div>
   

<span id="_2-1-2-自由布局"></span>
## Free layout

In free layout mode, chart controls do not automatically snap to each other, can overlap, and their stacking order can be adjusted. The operation is similar to that in PowerPoint.


* When a control is selected and moved, alignment lines, equidistant lines, and other reference lines will appear on the page to help you drag the control to the optimal position. A center line will also appear when a control approaches the center of the page.

* When multiple controls are selected, they can be grouped and moved together for easier layout configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/187ba501a0e041168225a179a1ce8b7a~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-画布区图表操作"></span>
# Chart operations in the canvas area

<span id="_2-2-1-编辑图表"></span>
## Edit chart

Click to go to the chart editing page (the visualization query interface for this chart) to configure settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0ea4cfd27bb4a23a92c03ca8535ba21~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-2-联动、跳转设置"></span>
## Linkage and navigation settings

You can configure [Chart Linkage](https://docs.byteplus.com/docs/DataWind/Chart_Linkage) between charts, and you can also configure [Chart Redirect](https://docs.byteplus.com/docs/DataWind/Chart_Redirect) between charts and other dashboards or web pages.

<span id="_2-2-3-图内控件显示"></span>
## Display of in\-chart controls

**Prerequisites for enabling this feature:** 


* The chart has filter conditions, and the filter conditions are set to "Display as chart filter option".

* The chart has dynamic dimensions or dynamic metrics.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Global filters set on the dashboard page do not take effect   </div>
   

   **Example of using dynamic dimensions and metrics:** 

   * If the query button is set to be displayed, a query button will appear on the chart, and you can filter the query conditions only after clicking it.

   * For dynamic dimension/metric display, when dynamic dimensions or metrics exist in the chart, you can choose whether to display them on the chart.


<span id="_2-2-4-复制与删除图表"></span>
## Copying and deleting charts


* Click Copy Chart to create a duplicate of the chart within the dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89423e3d45bc4bdb8995b6b2583a93d9~tplv-goo7wpa0wc-image.image) </span>

* Click Delete Chart to remove the chart from the dashboard, but you can still find the chart in the chart list and add it back to the dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7f5c346dbf44a82aa78972ec2716d82~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-5-锚点设置"></span>
## Anchor point settings

Quick navigation anchors can be set within the page to improve the efficiency of readers in viewing the page.


* Click the chart where you need to set an anchor, and in the chart settings area on the right, open General Settings \- Navigation Anchor.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eca5d9a9cc641c6a0074f9cfd02e034~tplv-goo7wpa0wc-image.image) </span>

* Enter an anchor name under Navigation Anchor. When the user selects this anchor, the page will automatically jump to the position of the current chart. For detailed instructions on navigation anchors, see the documentation [Operations in the Right-Side Page Configuration Area of the dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Right-Side_Page_Configuration_Area_of_the_dashboard).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23da6714fc7248b9b84621f6c0e76574~tplv-goo7wpa0wc-image.image) </span>
