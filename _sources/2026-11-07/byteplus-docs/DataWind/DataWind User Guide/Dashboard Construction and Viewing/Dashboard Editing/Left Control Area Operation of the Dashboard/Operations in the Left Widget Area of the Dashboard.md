---
title: "Operations in the Left Widget Area of the Dashboard"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Operations_in_the_Left_Widget_Area_of_the_Dashboard"
---

Dashboard editing, also referred to as dashboard design, dashboard creation, or dashboard layout, is the process of combining and arranging components (widgets) such as charts, text, images, and filters to build a data story board based on business logic. This article introduces the editing operations for the left widget area of the dashboard.

<span id="5b0b1985"></span>
# Function overview

The new dashboard editing interface is divided into the top navigation area, left widget area, central canvas area, right page configuration area, and bottom multi\-page editing area.

This article will introduce the left widget area. As shown in the figure below, the red\-marked area on the left is the widget area. The specific operations will be introduced below in the order of the widgets from top to bottom:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39f0d9a8650e475faa630a5b289289c4~tplv-goo7wpa0wc-image.image) </span>

<span id="e8c54786"></span>
# Add chart


* Click the Add Chart button to create an empty chart widget on the page. The user can click "Select existing chart" and choose the needed chart from the chart list on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59b49c02f2434ee3ba5f90d847c75bbe~tplv-goo7wpa0wc-image.image) </span>

   * Supports searching charts by chart name.

   * The chart list is sorted by creation time, with the most recently saved charts displayed at the top.

* Alternatively, click the blank area of the widget, and in the chart configuration area that pops up on the right, select a dataset, drag dimensions and metrics into the configuration area, choose the chart type and analysis method, and create a new chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eebeef3057b4f1790470eb6a84ca913~tplv-goo7wpa0wc-image.image) </span>


<span id="e909f11e"></span>
# Global filters, dimensions/metrics, query containers, dynamic parameters

Because global filters, dimensions/metrics, query containers, and dynamic parameters have similarities in their functions, they are introduced together in this section.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2353ccd4654b4a17a0b143dd76ef2bfa~tplv-goo7wpa0wc-image.image) </span>


* Supports adding global filters, dynamic dimensions, dynamic metrics, and dynamic parameters to control multiple charts on the dashboard simultaneously.

* The query container can simultaneously include all three types of global query filters mentioned above.

* You can use the values of the top\-level public filters on the current page as parameters and apply them to the link when adding a web page link.

* The operations for filtering and screening are quite extensive, so they are described in a separate document. For details, see [Filtering](https://docs.byteplus.com/docs/DataWind/Filtering).


<span id="bc559a24"></span>
# Tabs

By adding tabs to the dashboard, you can add a multi\-page component with switchable tabs to the page. Each tab can contain multiple charts, text, web pages, images, and even other tabs.


* You can also select multiple widgets within a tab and move them in batches.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c999b7ddcf54cd394cb1241479b484e~tplv-goo7wpa0wc-image.image) </span>

* You can double\-click to edit the tab name, add tabs, and perform other operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de7888841f4e4584849bfd85d3f28dff~tplv-goo7wpa0wc-image.image) </span>

* Drag widgets from the widget list on the left to the tab, or drag existing widgets from the current dashboard into the tab, to display the corresponding content in the tab.

* The style settings of the tab, such as tab font size, position, and the layout of components within the tab, can all be adjusted.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3295218f4f794e5cadce132e9e3880c5~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Tab component layout options include tile layout and free layout. The default option follows the dashboard layout. If the dashboard uses tile layout, newly added Tab components will also use tile layout.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Tile layout: The tab page will automatically adjust the layout, suitable for scenarios where dashboards need to be built quickly.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Free layout: The tab page allows flexible adjustment of element positions and layers, suitable for scenarios with more content and higher requirements for canvas layout and display.   </div>
   


<span id="4715d19c"></span>
# Add text

Dashboards usually require text to introduce the nature of the dashboard, data definitions, and other information. Sometimes, text is also needed to supplement the display and explanation of charts. Add a text widget to insert text descriptions.

You can edit the style of the text content, including color, font size, weight, spacing, adding hyperlinks, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4bb3b6add234679aec03271fc8a8737~tplv-goo7wpa0wc-image.image) </span>

In V2.58.0 and later versions, users can select text in the text component editing area and set it as first\-, second\-, or third\-level heading styles to achieve a clear emphasis in the dashboard.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10079ee669be4027999ae73c46731701~tplv-goo7wpa0wc-image.image) </span>

<span id="d346d86a"></span>
# Add web page

Select the web page option, and a web page widget will appear on the page. After selecting it, you can enter the web page link on the right. After entering the link, the web page widget will display the content of the linked page. You can configure the web page in the configuration panel on the right, including changing the URL (choosing whether to include a token), setting the display of the view mode icon, general settings, padding settings, and appearance settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed1e7a9f6dae4d4bac0811b8bac7777f~tplv-goo7wpa0wc-image.image) </span>

<span id="0f88094d"></span>
# Add media

In the material components section of the dashboard's left sidebar, you can select image, header image, title image, and divider components to help users more easily build a dashboard with a clear hierarchy.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5306acfdb6b640cf81a44135898d9913~tplv-goo7wpa0wc-image.image) </span>

<span id="04d68894"></span>
## Add an image

Click the material and select the image widget. You can configure the image in the image configuration panel on the right, including selecting the image source (you can upload a local image), view state icon settings, general settings, padding settings, and appearance configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fa90cefe56049d799f7829607c1653f~tplv-goo7wpa0wc-image.image) </span>

<span id="c9bf60db"></span>
## Add a header image

Click the material and select the header image widget. A default header image will appear on the dashboard. You can configure the header image in the header image configuration panel on the right, including selecting the image source (you can use an official image or upload a local image), general settings, padding settings, appearance configuration, and height settings.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Starting from V2.87.0, the minimum height restriction for the dashboard header image has been removed, allowing users to freely adjust the header image height.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fcb38e3c2b040afb731b533d0a017f3~tplv-goo7wpa0wc-image.image) </span>

<span id="09f0a26c"></span>
## Add a title image

Click the material and select the title image widget. A default title image will appear on the dashboard. You can configure the title image in the title image configuration panel on the right, including selecting the image source (you can use an official image or upload a local image), general settings, padding settings, and appearance configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/535d130cc3ad4d43b516a1239b626940~tplv-goo7wpa0wc-image.image) </span>

<span id="b1ead6fc"></span>
## Add a divider

Click the material and select the divider widget. A default divider will appear on the dashboard. You can configure the divider in the divider configuration panel on the right, including selecting the line style, general settings, and appearance configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e127d3146c1a48ddb58a95781030b250~tplv-goo7wpa0wc-image.image) </span>

<span id="a29f7972"></span>
# Relationship diagram

Click the "Relationship Diagram" widget and drag it to add the component. You can use the relationship diagram to connect indicator cards with mathematical operators, creating a more intuitive chart. The effect is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/445910f6024d4217a279f7fb3e829a8e~tplv-goo7wpa0wc-image.image) </span>

**Steps:** 


1. On the relationship diagram configuration page on the right, select the required indicator cards.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f9f674c81cb44e0812721308ff03011~tplv-goo7wpa0wc-image.image) </span>

2. Based on the initially added indicator cards, add peer indicators, subordinate indicators, or constants as needed.

3. Adjust the relationships between indicator cards as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7d351ef2b434be28abe6a06cfad50b3~tplv-goo7wpa0wc-image.image) </span>

4. Repeat the above steps to create the relationship diagram you need.


<span id="a3d8c123"></span>
# Merged table

The dashboard supports the merged table feature, which allows multiple independent tables to be combined into a single table, making it easier for users to efficiently adjust the dashboard's chart layout.

Applicable scenarios are as follows:


* Data comes from multiple datasets and cannot be queried in a single table;

* The same dataset, but the display units or filter conditions for different metric rows are different;

* Indicators from different statistical periods are merged horizontally.


<span id="3f7b212f"></span>
## Create a merged table

Users can choose to create a new table or use an existing one to create a merged table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39333505b72f4d17b1deb2ba824c63fa~tplv-goo7wpa0wc-image.image) </span>

<span id="2c131bec"></span>
## Configure the merged table title

When the merged table is selected, the table title and chart description can be configured on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3786f08ac9b4a2580e29623a8d8c5de~tplv-goo7wpa0wc-image.image) </span>

<span id="466aaaf6"></span>
## Configure the merged table

<span id="144d86ef"></span>
### Merge method

The merged table supports four merge methods: vertical, horizontal, custom, and hierarchical.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/061960e6e6094793b07147e0e1b31d41~tplv-goo7wpa0wc-image.image) </span>

<span id="c281939e"></span>
### Merged table sorting

The merged table supports adjusting the order of tables. After adjusting the order, the order of tables in the merged table will be updated accordingly.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ee42879ef0b443bbbb0318956c34c02~tplv-goo7wpa0wc-image.image) </span>

<span id="6ac67da7"></span>
## Add and modify tables

In the splicing configuration panel on the right, you can choose to add more tables to the current merged table or modify the current table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dfc75546a3b4acca712b1c40f281804~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The differences between concatenated tables and regular tables are as follows:</div>



* <div data-tips="true" data-tips-type="tip">Row and column transposition: If a table is configured with row and column transposition, concatenation will be performed based on the original, non\-transposed state.</div>


* <div data-tips="true" data-tips-type="tip">Chart sorting: During concatenation, each chart will be concatenated according to its own sorting result.</div>


* <div data-tips="true" data-tips-type="tip">Chart filters: The chart filters of different charts will be displayed together above the concatenated table.</div>



<span id="7027b110"></span>
# Tooltip

Tooltips are often needed in dashboards to provide additional information. Tooltips not only solve the problem of limited chart space and incomplete information display, but also help users quickly obtain data details and context, improving the efficiency and accuracy of dashboard data interpretation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/154753a1390a47a0a8b8e27cd004e61e~tplv-goo7wpa0wc-image.image) </span>

The tooltip icon can be selected from system icons or custom uploaded images. Style editing is supported for both the tooltip icon and the tooltip itself, including color, size, border thickness, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c66bba9c11f84b6ca8101977d23a683b~tplv-goo7wpa0wc-image.image) </span>


|General settings |Checked state |Unchecked state |
|---|---|---|
|Set as floating |The widget can be freely placed anywhere on the canvas. |The widget is arranged compactly in a tile format. |
|Navigation anchor |Enter the anchor name under the navigation anchor. When the user selects this anchor, it will automatically jump to the location of the analysis tree. |\-\- |


<span id="59dae4c1"></span>
# Add plugin

Click "Add Plugin" to open the plugin marketplace, where users can insert custom plugins to create personalized data displays.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported in private deployments.</div>


<span id="ca3a081d"></span>
# Layer list

Click Layer List to display all widgets currently on the dashboard.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/887e205975c04c4ebcdcbffeaf147005~tplv-goo7wpa0wc-image.image) </span>

With the layer list, you can


* Quickly adjust layer order: When multiple widgets overlap, you can quickly adjust their stacking order in the layer list.

* Check dashboard content: The layer list allows you to view all widgets on the dashboard. By reviewing the layer list, you can identify data that should not be displayed but was accidentally added to the dashboard, and also locate content that is covered by other layers.

* Hide layers: You can hide certain widgets to facilitate editing.


<span id="dbad7fe8"></span>
# Help


* Keyboard shortcuts

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5e14edb1b9f4c20a42a0b4be3611c6a~tplv-goo7wpa0wc-image.image) </span>


<span id="3d49ad1b"></span>
# Common scenarios


* Cross\-project display of dashboards or charts

   You can embed links to dashboards or charts from other projects; for details, see [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding).

* Cross\-platform content display

   You can embed links from other platforms into the current dashboard using the web widget.

* Embedding explanatory links such as Lark Docs

   Embed explanatory Lark Docs into the dashboard to help readers better understand the meaning of the charts.
