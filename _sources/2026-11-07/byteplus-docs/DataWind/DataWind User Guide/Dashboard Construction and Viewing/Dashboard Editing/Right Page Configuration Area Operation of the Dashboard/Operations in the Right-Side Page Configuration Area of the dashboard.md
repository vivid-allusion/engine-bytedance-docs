---
title: "Operations in the Right-Side Page Configuration Area of the dashboard"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Operations_in_the_Right-Side_Page_Configuration_Area_of_the_dashboard"
---

Dashboard editing, also referred to as dashboard design, dashboard creation, or dashboard layout, is the process of combining and arranging components (widgets) such as charts, text, images, and filters to build a data story dashboard based on business logic. This article introduces the editing operations in the right\-side page configuration area of the dashboard.

<span id="7bc7caae"></span>
# Feature overview

The new dashboard editing interface is divided into the top navigation area, left widget area, central canvas area, right\-side page configuration area, and bottom multi\-page editing area.

This article will introduce the right\-side page configuration area. As shown in the figure below, the yellow\-marked area on the right is the page configuration area. The specific methods for page configuration and chart configuration operations in the page configuration area are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e11f7bb6775447b7947aca8c51076bf1~tplv-goo7wpa0wc-image.image) </span>

<span id="51db2b0b"></span>
# General overview

The rightmost area is the settings area for the entire page. By default, or by clicking the "Page Configuration" button in the navigation bar, you can enter page configuration; clicking a chart component on the canvas will enter chart configuration.


|Page configuration |Chart configuration |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cae0c5441a948839831a5c615c0a8e1~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56fd1294239f495ea73749609ab92d07~tplv-goo7wpa0wc-image.image) </span> |


<span id="47b4cb2c"></span>
# Page configuration

<span id="84da07b6"></span>
## Dashboard theme

Dashboard theme configuration supports multiple official themes and custom themes. For details, see the documentation [Dashboard Theme](https://docs.byteplus.com/docs/DataWind/Dashboard_Theme).

<span id="bf5332f6"></span>
## Layout mode

Both tile layout and free layout are supported. For details, see the above document [Operations in the Central Canvas Area of the Dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Central_Canvas_Area_of_the_Dashboard).

<span id="380f48c7"></span>
## Canvas background

Adjustments to background color, transparency, and more are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ef56d58459b4e9e83dbaa1590bf6345~tplv-goo7wpa0wc-image.image) </span>

<span id="b1e079ef"></span>
## Canvas size

When **free layout** is selected in editing mode, you can adjust the background canvas size as needed. The platform also provides several preset options.

If adaptive is selected, the canvas width or height will automatically adjust according to the layout of charts and widgets on the page to cover all charts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bcc10c7b62d49bebad22ff966eba953~tplv-goo7wpa0wc-image.image) </span>

<span id="1f4ea47b"></span>
## View mode settings

<span id="844bc590"></span>
### Navigation anchors are expanded by default

This option controls whether anchor points on the dashboard viewing page are expanded by default. If 'Expand by default' is selected, the names of all anchor points will be expanded by default in view mode. For anchor point configuration methods, see [Anchor point settings](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Central_Canvas_Area_of_the_Dashboard#_2-2-5-%E9%94%9A%E7%82%B9%E8%AE%BE%E7%BD%AE).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6316bc34e657431286c692e2efaeed10~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After V2.83.0, users can move navigation anchors in "Edit" or "Preview" mode.</div>


<span id="eefc2f0b"></span>
### Display toolbars and tooltip icons in view mode

After enabling this option, the content displayed in the toolbars of all chart components on the dashboard will be uniformly and forcibly set according to the dashboard page configuration.

After enabling this option, the content displayed in the tooltip icons of all chart components on the dashboard will be uniformly and forcibly set according to the dashboard page configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18769613d23a43f4a66ce74a4ab90183~tplv-goo7wpa0wc-image.image) </span>

Users can set whether the toolbar is collapsed by default, and configure the content displayed by toolbar icons.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04b120d571ad419e9fd5d86d3e045001~tplv-goo7wpa0wc-image.image) </span>

<span id="1845ec81"></span>
### Adaptive width in view mode

When this option is selected, the dashboard page will adjust according to the device size in viewing mode.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2df30f852b5f46fa878af11ffeac9f76~tplv-goo7wpa0wc-image.image) </span>


* Scale width and height: After calculating the width based on the viewport size, the overall width and height are scaled proportionally.

* Scale width: After calculating the width based on the viewport size, only the width is scaled proportionally while the height remains unchanged.


<span id="7e623700"></span>
### Scheduled refresh

After configuration, the dashboard will refresh at the specified interval to update query data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf9ea4fbed5d48cb940cb8f0a12378ea~tplv-goo7wpa0wc-image.image) </span>

<span id="1c1aee42"></span>
### Advanced comment feature configuration

When there is a large amount of data in table components that requires pagination, enabling this feature allows quick navigation to the cell corresponding to a comment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0763aebd24e48a0bfc43e4288288733~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When table data is set with data masking or row and column permissions, it is not recommended to enable this feature.</div>


<span id="d6679b9d"></span>
# Chart configuration

The chart configuration section includes three main modules: data, style, and analysis. Among them, data and analysis are for chart creation functionality; see [Visual Query Overview](https://docs.byteplus.com/docs/DataWind/Visual_Query_Overview) for details. The style section is for adjusting and configuring chart styles. For details, refer to the following content.

<span id="dedff61f"></span>
### Chart name

You can choose whether to display the chart name or customize its content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21f3233000da45d3a5b58e27240fd5ab~tplv-goo7wpa0wc-image.image) </span>

You can configure the text content, font size, color, and other properties of the chart name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8629accd3ae04aacb1b0451710c804af~tplv-goo7wpa0wc-image.image) </span>

<span id="701ab095"></span>
### Description configuration

You can select to display basic information and field descriptions.


* After selecting 'Basic information', clicking the chart tooltip icon will display the source information of the chart dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c247ed797b64cf3ba12429515ad0f82~tplv-goo7wpa0wc-image.image) </span>


* After selecting "Field description", hovering the mouse over the table header will display the description of that field.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/152fb1eeb01e40a6beac07e9af6b927d~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Method for setting field descriptions: In visual query, click the field dropdown, select "Field information", and check "Show field description". For details, see <a href="https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration">Overview of Field Configuration</a>.</div>


<span id="8ed1848d"></span>
### Edit chart description

You can add a chart description for charts that require special explanations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f9885a9301042cbb00791dd8ab30a42~tplv-goo7wpa0wc-image.image) </span>

<span id="5c05954d"></span>
### Display of icons in view mode

This includes whether to display toolbar icons and tooltip icons, mainly controlling whether icons are shown on the chart in view or edit mode.


* In scenarios where multiple charts are combined, if you do not want to display elements such as the toolbar, you can choose to hide them.

* To prevent viewers from seeing features such as data download, you can hide them.


<span id="fb3a143e"></span>
### General settings

<span id="4e546504"></span>
#### Set as floating

In dashboard tile layout mode, the floating feature is supported. After enabling floating, charts can be freely placed anywhere on the canvas. When disabled, charts will be automatically rearranged as tiles nearby.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd48b3c5f58441ccb96faefbf981d981~tplv-goo7wpa0wc-image.image) </span>

<span id="b00480d9"></span>
#### Navigation anchor

The dashboard supports the anchor feature, allowing you to set an anchor for each chart. After configuration, anchors will be displayed on the right side of the dashboard view page, making it easier to quickly locate charts when there are many charts on the dashboard.

Dragging navigation anchors to adjust their positions is supported in both "edit mode" and "view mode".

<span id="1776fd25"></span>
#### Data loading animation

The dashboard supports the data loading animation feature. When enabled, dashboard charts will display a data loading animation until data loading is complete.

<span id="bca92fd0"></span>
#### Data update animation

For line charts, the dashboard supports adding data update animations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17c3a96e5b9c47d88ecbd7056f8181d1~tplv-goo7wpa0wc-image.image) </span>

<span id="58fb2d7c"></span>
### Chart appearance


* Inner padding: Adjusts the distance between the chart content and the outer edge of the chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ad5b70d124e408a85646e9491605a46~tplv-goo7wpa0wc-image.image) </span>

* Appearance: Adjusts the chart's visual effects, including background color, border color, border radius, and border width.

* Position and size: The position of the chart itself on the canvas, which can be set by manually adjusting the values.


<span id="75150f1f"></span>
### Select chart

For newly created charts, clicking "Select existing chart" will open the "Select chart" sidebar.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfc5a40f088049fbbc5adae6683d8482~tplv-goo7wpa0wc-image.image) </span>

You can:


* View and select recent charts.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only charts with management permissions are displayed in Recent charts: Only the chart owner and those with management permissions for the dashboard containing the chart have management permissions for the chart.   </div>
   

* Support searching for recent charts by chart name;

* The chart list is sorted by the creation time of the charts, with the most recently saved charts displayed at the top;

* After selecting a chart and then clicking "Recent charts", the current chart will be replaced by the new chart.
