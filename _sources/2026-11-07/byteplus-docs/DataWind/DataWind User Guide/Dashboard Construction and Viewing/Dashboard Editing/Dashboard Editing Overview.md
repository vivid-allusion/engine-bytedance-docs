---
title: "Dashboard Editing Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dashboard_Editing_Overview"
---

This article introduces the workflow and operation areas of the dashboard editing page.

<span id="cf91c02d"></span>
# Feature overview

Dashboard editing, also referred to as dashboard design, dashboard creation, or dashboard layout, is the process of combining and arranging components (widgets) such as charts, text, images, and filters to build a data storyboard based on business logic.

This article provides an overview of the dashboard editing process. For detailed feature descriptions, refer to the specific documentation for each operation area.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f299f402ec034e0b8815f72f487ebde8~tplv-goo7wpa0wc-image.image) </span>


|Control area |Introduction |
|---|---|
|[Operations in the Dashboard Top Navigation Area](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Dashboard_Top_Navigation_Area) |From left to right: Rename dashboard, previous step, next step, layer order, group, page zoom, replace dataset, page settings, mobile layout, preview and save, Smart Build.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">"Smart Builder" is a secondary feature under the value\-added module Analysis Assistant and is disabled by default. To use this feature, contact Volcano Engine technical support. After purchasing and enabling this feature, it will be available for use.</div><br> |
|[Operations in the Left Widget Area of the Dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Left_Widget_Area_of_the_Dashboard) |From top to bottom: Add chart, global filter, tab, text, web page, asset, pinned container, merged table, metric, query container, dynamic parameter, dimension/metric, relationship graph, tooltip, analysis tree, add plugin, layer list, help. |
|[Operations in the Central Canvas Area of the Dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Central_Canvas_Area_of_the_Dashboard) |Supports adjusting chart layout here (snap\-to\-grid layout/free layout) as well as other chart operations in the canvas area (chart editing, linking, navigation, in\-chart controls, copy and delete, anchor point settings, and additional operations). |
|[Operations in the Right-Side Page Configuration Area of the dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Right-Side_Page_Configuration_Area_of_the_dashboard) |* Page configuration: Click the blank area of the central canvas to open the "Page configuration" sidebar, which supports dashboard theme, layout, canvas background, and view mode configuration.<br><br>* Chart configuration: Click a single chart to display the "Chart Configuration" sidebar, which supports chart data, style, and analysis configuration.<br><br>* Widget configuration: Click a single xx widget to display the "xx Configuration" sidebar, which supports related configuration for the widget. |
|[Operations in the Multi-Page Editing Area at the Bottom of the Dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Multi-Page_Editing_Area_at_the_Bottom_of_the_Dashboard) |Supports adding new pages at the bottom of the dashboard and performing operations such as adding, deleting, copying, renaming, hiding, and more. |


<span id="63e9967a"></span>
# Quick start

<span id="43991d53"></span>
## Create a new dashboard


1. Go to the "Dashboard" module, click the "+" in the upper right corner of the dashboard list, and select "Create Dashboard".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/386b63aff6944434892631615dcfb4f8~tplv-goo7wpa0wc-image.image) </span>

2. Enter the dashboard name and select the save location. Click "OK" to create.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f270c673128420087eeb0c660cdc1b8~tplv-goo7wpa0wc-image.image) </span>

3. Click the "Edit" button in the upper right corner to enter the editing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09a727a6653647ea8518e3632d3417c1~tplv-goo7wpa0wc-image.image) </span>

4. Click "Add Chart" in the left widget area. You can select from historical charts or create a new chart.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63fdcb947bbc4a9da2ef434d80a7a34c~tplv-goo7wpa0wc-image.image) </span>


* To select from historical charts: Click "Select Existing Chart", then choose the required historical chart in the "Select Chart" panel on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b821e1f77004f79b9b1638a5962ea21~tplv-goo7wpa0wc-image.image) </span>

* To create a new chart: Click a blank area in the chart area, select a dataset in the "Chart Configuration" area on the right, drag dimensions and metrics from the dataset to the data area, and select the chart type.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f1c6b371c5446f9bea298abe3822a06~tplv-goo7wpa0wc-image.image) </span>

5. Click a blank area on the central canvas. In the page configuration on the right, you can select the dashboard theme, layout, canvas background, canvas size, and configure view mode and other operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99403efd4aae444ba635eb50059ac9e8~tplv-goo7wpa0wc-image.image) </span>

6. Drag a widget from the left widget area onto the canvas to specify its position, or click the widget to add it automatically. If you accidentally drag a widget, or accidentally delete or add content, you can quickly undo using the command+z/ctrl+z shortcut.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87a11c2d4d5d4d2884e90b179639c0b0~tplv-goo7wpa0wc-image.image) </span>


<span id="844268da"></span>
## Edit dashboard


1. Select the dashboard you want to edit, click "Edit", and enter the chart editing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44fa3021f5bc4b1cb397c0f2546c534a~tplv-goo7wpa0wc-image.image) </span>

2. You can click an individual chart and modify the chart's data, style, or analysis method in the "Chart Configuration" area on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8886e0ee311428ca24198dbdf008be6~tplv-goo7wpa0wc-image.image) </span>

3. You can click the blank area of the central canvas to modify the overall theme, layout, and other settings of the dashboard in the "Page configuration" panel on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83550efa06754e548f4ec3caa8d32d0d~tplv-goo7wpa0wc-image.image) </span>

4. You can drag new widgets from the widget area on the left to the central canvas, and configure tab settings in the tab configuration area on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/573f0c39a12f436e96ab5cc3a6176a23~tplv-goo7wpa0wc-image.image) </span>


<span id="e9b5e576"></span>
# Simultaneous editing instructions

To prevent modifications from being overwritten by others during simultaneous editing, the dashboard does not support multiple users editing the dashboard at the same time.


* Dashboard viewing page: When a user is editing the dashboard, other users cannot access the dashboard editing page. To edit the dashboard, contact the current editor to exit editing mode.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bfac729f4e343f194ea2ed310f22e26~tplv-goo7wpa0wc-image.image) </span>

* Saving charts: When a user is editing the dashboard, other users cannot save charts to this dashboard (charts on the dashboard itself can be edited by clicking the chart name or editing the chart from the viewing page, but cannot be saved to the current dashboard).
