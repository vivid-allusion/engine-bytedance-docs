---
title: "Publishing Custom Plugin Packages and Plugin Package Resources"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Publishing_Custom_Plugin_Packages_and_Plugin_Package_Resources"
---

<span id="ff30dd16"></span>
# 1. Overview

Custom visualization is one of the open capabilities provided by this product. It enables users to create personalized data displays according to their needs. This document introduces plugin publishing and plugin package resource deployment in custom visualization. Use this document to obtain resources for deploying plugin packages or to develop the required plugins yourself, and complete the plugin package publishing process. (Currently, the custom visualization feature is still in the internal testing phase. If you have specific needs for this feature, please contact the Volcano Engine business team to obtain more details about purchasing and collaboration.)

**Caution: Before reading and completing the configuration items in this document, you must first complete the relevant configurations in** [Custom Visualization Overview](https://docs.byteplus.com/docs/DataWind/Custom_Visualization_Overview) **,**  [Structure and Development of Custom Chart Plugins](https://docs.byteplus.com/docs/DataWind/Structure_and_Development_of_Custom_Chart_Plugins) **, and** [Custom Chart Data Structure and Plugin Property Configuration](https://docs.byteplus.com/docs/DataWind/Custom_Chart_Data_Structure_and_Plugin_Property_Configuration) **in sequence.** 

<span id="aebb35b0"></span>
# 2. Plugin package publishing

To use plugins in this product, you must first upload the plugin package to the plugin marketplace. After uploading and passing the review, the plugin can be used within this product.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26e75e68f9e5403fabc88839d393a0f2~tplv-goo7wpa0wc-image.image) </span>

> The content on this page is for demonstration purposes. Please determine the actual resource package based on your development situation. For official plugin package resources, refer to Section 3.


<span id="2da107fa"></span>
## 2.1 Preparation

Prepare all plugin packages, plugin icons, sample images, and description information for the plugins to be uploaded.

<span id="bdcd3908"></span>
### 2.2.1 Developing plugins yourself

For plugins you develop yourself, after completing local debugging, you need to execute the following command in the project root directory:

```JavaScript
npm run build
```


After execution, a compressed package named `satellite.tgz` will appear in the root directory. This is the plugin package to be uploaded.

In addition, you also need to prepare the corresponding plugin icon (`SVG`/`PNG` are both acceptable), sample images (images describing the display effect of the plugin), and description information (basic information about the plugin).

<span id="c4be8c05"></span>
### 2.1.2 Official plugins

This product also provides official plugin charts such as `Boxplot`, `Mekko`, and `Treemap`. You can directly upload these official plugin packages to the plugin marketplace for use. For related resources, please refer to Section 3 "Plugin Package Resources" in this document.

<span id="e2c97325"></span>
## 2.2 Plugin upload

**Caution**: To upload a plugin that already exists in the plugin marketplace, it is recommended to install the plugin by updating to a newer version. Otherwise, multiple plugins of the same type will appear in the plugin marketplace.

Access the developer console page of this product at `/bi/developers/console/` as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc1bb4d51f5945dcaa422ba0cb1280f1~tplv-goo7wpa0wc-image.image) </span>

> The content on this page is for demonstration purposes. Please determine the actual resource package based on your development situation. For official plugin package resources, refer to Section 3.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ee56414a6ea4fe7a1afce6ad92de670~tplv-goo7wpa0wc-image.image) </span>

Click 【Upload Plugin】 to enter the upload page.

<span id="32a14301"></span>
### 2.2.1 Complete the information

Please configure the name, summary, and description, and upload the corresponding icon and illustration. (For official plugins, you can refer to the information provided in Section 3 "Plugin Package Resources" of this document.)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2c81c91d2e84afb92fc2c970e1abd1d~tplv-goo7wpa0wc-image.image) </span>

After completing the information, click 【Next】 to proceed to 【Visibility Settings】.

<span id="3438187a"></span>
### 2.2.2 Visibility settings

First, you need to set the visibility range of the plugin in the plugin marketplace:

 **(1) Public**

Everyone can access the plugin in the plugin marketplace.

 **(2) Selected projects**


* After selecting "Selected projects", you need to enter the projects with access.

* The projects with access can access the plugin in the plugin marketplace.


 **(3) Private**

When set to private, the plugin cannot be found in the plugin marketplace.

Next, after making your selection, click 【Next】 to proceed to 【Upload Plugin】.

<span id="7794ae08"></span>
### 2.2.3 Start upload

Upload the plugin package generated in Step 1 by clicking 【Upload】. After the upload is complete, click 【Publish】. The plugin will be in a pending review state. Once approved by an administrator, the plugin will be published.

You can see the uploaded plugin in the plugin marketplace.

<span id="3dccb603"></span>
## 2.3 Plugin review

Currently, only the primary account or system administrator can approve plugins. Log in to the developer backend with administrator privileges. In the upper right corner, you can see the Administrator Center. Click to enter the administrator console.

In the administrator console, under Plugin Review, you can view all plugins currently in pending review status and completed status.

In the pending review list, click Approve in the Actions column to complete the plugin review. Plugins that pass the review will be automatically published in the plugin marketplace.

<span id="67a1f673"></span>
## 2.4 Update version

To update a plugin version later, go to the developer backend page `/bi/developers/console/`, and click the View button in the list to enter the plugin details page.

After entering the details page, first click Version Management on the left to go to the version operations page, then click the Create Version button in the upper right corner:

In the Create Version popup, enter the new version number and update notes, upload the new plugin package, and after clicking Confirm, the new plugin version will enter the review status. Once approved, the new version will be published.

<span id="aaf3dc18"></span>
# 3. Plugin package resources

<span id="f84ddb52"></span>
## 3.1 Treemap

Treemap implemented based on G2

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/658a152b624d4d2fbe71f635fa627b69~tplv-goo7wpa0wc-image.image" name="satellite.tgz">satellite.tgz</Attachment>


&nbsp;

 **(1) Plugin icon**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/487d6baa4ea04b78a30171ee1f2c9db9~tplv-goo7wpa0wc-image.image) </span>

 **(2) Example image**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c16b37e47be45c39d90c59922879bad~tplv-goo7wpa0wc-image.image) </span>

 **(3) Description**

The treemap visually displays the proportion of data using area size, supporting one or more dimensions with one metric, or zero dimensions with multiple metrics.


* One or more dimensions with one metric, for example: Dimension [Province], Metric [Profit], generates a treemap showing the profit size for different provinces.

* Zero dimensions with multiple metrics, for example: Dimension [None], Metrics [Profit] [Sales amount], generates a treemap showing the proportion relationship between profit and sales amount.


<span id="1ff502bf"></span>
## 3.2 Mekko chart

The Mekko chart (market matrix segmentation chart) is a type of two\-dimensional stacked chart.

**Plugin package**

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8dbff5cee624d389740d237889a962a~tplv-goo7wpa0wc-image.image" name="satellite (1).tgz">satellite (1).tgz</Attachment>


&nbsp;

**New version of the mekko plugin package (temporary version supporting field\-specified colors)** 

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/535b117bb7954cb5b29eccc8c08711a7~tplv-goo7wpa0wc-image.image" name="extension.tgz">extension.tgz</Attachment>


&nbsp;

**New version of the mekko plugin package (version with maximum stack count limit removed)** 

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe75ff094d846eda868eb6446b13309~tplv-goo7wpa0wc-image.image" name="extension (1).tgz">extension (1).tgz</Attachment>


&nbsp;

 **(1) Plugin icon**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5211b95a8d9240049f62402d33f455aa~tplv-goo7wpa0wc-image.image) </span>

 **(2) Example image**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9e579f677aa48569099ac54c93c6ee1~tplv-goo7wpa0wc-image.image) </span>

 **(3) Description**

The dimension axis of the Mekko chart displays groups, while the measure axis shows the normalized percentage value for each category item. The size of each group represents its value.

In a Mekko chart, you need two dimensions and one measure:


* Each bar corresponds to the first dimension and is divided into smaller category labels based on the second dimension, with different categories displayed in different colors.

* The value of the measure determines the height of each category within the bar as well as the size of the bar.

* You can also drag in a color dimension. When a color dimension is present, the labels will display colors according to the categories of that color dimension.

   * For example: Dimensions [Creation Type] [Creation Status], Measure [Read Count], Color [Platform]. The chart will display several bars divided by creation type, with each bar containing several labels divided by creation status. The height of each label represents the read count value, and the label color corresponds to the color for the current platform dimension.


<span id="209333bf"></span>
## 3.3 Calendar heatmap

The calendar heatmap is a chart composed of small, orderly, and compact color blocks, displayed in a calendar format, and is used to show the data distribution over a period of time.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a25952bdfd1460396a582672d0a7dc3~tplv-goo7wpa0wc-image.image" name="package.tgz">package.tgz</Attachment>


&nbsp;

 **(1) Plugin icon**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13f04fbada7848ad8ec217474e51de81~tplv-goo7wpa0wc-image.image) </span>

 **(2) Example image**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d4badd7d996491eb09e63a54f8f8edb~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


 **(3) Description**

Each small color block represents the time dimension, and the color of the block represents the measure.

One dimension and one measure, and the dimension type must be a date type, for example: Dimension [Date], Measure [Read Count].

<span id="2e0e7724"></span>
## 3.4 Leaderboard chart

The leaderboard chart is a bar chart that describes ranking order or key progress indicators.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfc85b94eff94ec1b045e46f92252143~tplv-goo7wpa0wc-image.image" name="satellite (3).tgz">satellite (3).tgz</Attachment>


&nbsp;

 **(1) Plugin icon**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b38a86d7bb6447aa35fdc72e4ad5f34~tplv-goo7wpa0wc-image.image) </span>

 **(2) Example image**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1dc3f6427fd437aa3ee193c46bc893a~tplv-goo7wpa0wc-image.image" width="1465px" /></div>


 **(3) Description**

The leaderboard generally reflects the distribution and ranking order of the measure within the dimension, and concisely displays the descending order of the top N. For example, the leaderboard displays the top 10 provinces in descending order according to payment amount.

<span id="debc498f"></span>
## 3.5 Boxplot chart

Boxplot chart implemented based on G2

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11549b86fe042729e4561b3608b291e~tplv-goo7wpa0wc-image.image" name="satellite (4).tgz">satellite (4).tgz</Attachment>


&nbsp;

 **(1) Plugin icon**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77ca14fc588044c2a1f505084ffbd290~tplv-goo7wpa0wc-image.image) </span>

 **(2) Example image**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ef2d3efd77b41b582e4849700b3acad~tplv-goo7wpa0wc-image.image" width="2690px" /></div>


 **(3) Description**

The boxplot, also known as box\-and\-whisker plot, box plot, or box line plot, is a statistical chart used to show data dispersion. It supports plotting with one or more dimensions and one measure.


* One dimension and one measure, for example: Dimension [City], Measure [Profit]

   * Generate a box plot showing the profit distribution across different cities. The visualization displays the data points for the maximum, minimum, median, and upper and lower quartiles, enabling users to understand the statistical distribution of profit values for each city.

* Two dimensions and one indicator, for example: dimensions [Province] [City], indicator [Profit]

   * Generate multiple box plots with provinces as the coordinate axis. Generate a box plot for each province to represent the statistical distribution of profits among different cities within that province.


&nbsp;
