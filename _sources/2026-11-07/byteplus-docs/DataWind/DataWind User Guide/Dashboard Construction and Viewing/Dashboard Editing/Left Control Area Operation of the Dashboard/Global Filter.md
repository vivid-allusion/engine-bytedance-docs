---
title: "Global Filter"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Global_Filter"
---

<span id="_1-概述"></span>
# 1. Overview

The global filter is one of the filtering controls. It can be applied to multiple tables simultaneously, allowing users to filter multiple charts within a dashboard without configuring each one individually, thereby facilitating data analysis and chart presentation. The global filter is divided into the standard global filter, combination filter, and cutoff date filter.

<span id="_2-全局筛选器介绍"></span>
# 2. Standard global filter

Click the global filter icon in the left action bar to add a global filter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f517eb55ab0e411688a03b67428ceb69~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-子筛选器"></span>
## 2.1 Sub\-filter

<span id="_2-1-1-配置过程"></span>
### 2.1.1 Configuration process

**Application scenario**: When a field with a hierarchical structure is used as a filter, the filter options need to display relevant values. This prevents users from selecting interfering items. For example: province, city; primary category, secondary category.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3040e2b248b14c4d92d9e175727731e7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c991f5342a7644dd8c78bf7b3e0a331f~tplv-goo7wpa0wc-image.image) </span>

 **[Method 1] Link two existing filters**

Drag filter 1 and hover over filter 2; filter 1 will become a sub\-filter of filter 2.

 **[Method 2] Add a sub\-filter directly; up to 20 levels of sub\-filters are supported.** 

<span id="_2-1-2-子筛选器分类"></span>
### 2.1.2 Sub\-filter types

This feature supports adding independent sub\-filters or parallel sub\-filters. Sub\-filters in a parallel relationship are parallel sub\-filters.


* Parallel sub\-filters can be added by dragging filters using Method 1.

* Multiple sub\-filters added using Method 2 will be independent sub\-filters.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f468c07aff647e3b3cd3810fe2d6dc4~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-树状筛选器"></span>
## 2.2 Tree filter

The dashboard's public filter supports configuring a tree filter to achieve the hierarchical effect shown in the illustration.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa8382867719a573812fa4a396053668.png) </span>

<span id="_2-2-1-配置过程"></span>
### 2.2.1 Configuration process


* When configuring a public filter, after selecting the corresponding chart and binding field (the field type must be numeric or text), select "Tree filter" in the "Filter settings" section.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cf326de7a954406b353764ed9b26ede~tplv-goo7wpa0wc-image.image) </span>


* Select the source dataset for the tree hierarchy. The filter will determine the hierarchy names and available options for each level based on the data in the selected dataset. After selecting the dataset, configure the hierarchy fields.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9346911aaac34ce18c5abab94a5339a1~tplv-goo7wpa0wc-image.image) </span>


* Like other filter types, the tree filter supports single or multiple selection and allows you to set default filter values.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bdb9710038f4cb2ac08164142cfce20~tplv-goo7wpa0wc-image.image) </span>


* After configuring the tree filter, set up the associations in the "Filter fields" section by linking the fields from the dataset used in the chart to the levels you just configured.


If there are multiple datasets, you need to set up the corresponding relationships for each one individually.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/155da1e84a1c4f36b0865c423a31fd4b~tplv-goo7wpa0wc-image.image) </span>


* Once the tree filter is configured, this filter does not support further association configuration. Click Confirm to save and apply the filter.


<span id="_2-2-2-是否自动勾选下级"></span>
### 2.2.2 Whether to automatically select lower levels

The tree filter allows you to choose not to automatically select lower levels during configuration; this option is disabled by default.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba08f5883a9b46038cf9efccc1840abe~tplv-goo7wpa0wc-image.image) </span>


* When this option is disabled, selecting a higher\-level item in the tree filter will automatically select all lower\-level options.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a7886bbc6d44a7bac8706545bb7a708~tplv-goo7wpa0wc-image.image) </span>


* After enabling this option, you can select higher\-level items individually or specify the selection range.


<span id="_3-功能介绍"></span>
# 3. Combination filter

Users can select multiple conditions to combine and filter data. For example, you can filter data based on multiple dimensions such as region, product category, and customer at the same time to obtain a dataset within a specific scope.

Operation steps:

(1) Click the global filter in the left operation bar, then click the three dots "More" in the pop\-up window, and select Add combination filter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd00153414a34b4dbccebadb397b8e8e~tplv-goo7wpa0wc-image.image) </span>

(2) After selecting the chart associated with this combination filter, select the dimensions and metrics to filter in the filter fields. In the filter field list, you can set the display name for each field filter. Duplicate filter field names are not allowed within a single filter. Click the plus sign on the left to add filter fields; click the minus sign to remove fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fec0a3fb5d84f6dbe170844ee1ccbf8~tplv-goo7wpa0wc-image.image) </span>

(3) In the filter settings on the right, you can set the AND/OR relationships and hierarchical relationships between fields. Click Add filter item to add fields at the same level; click Add filter group to add a subset filter field group. Click the "AND" or "OR" labels to switch between AND and OR relationships.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32ebb33f269342b699c4bc6d1cd82f99~tplv-goo7wpa0wc-image.image) </span>

<span id="8f6875ac"></span>
# 4. Deadline filter (OKR global filter)

When a dashboard contains multiple OKR charts, inconsistent OKR deadlines may cause confusion regarding the data. Users can add a public due date filter in the dashboard to unify the due dates of all OKR charts in the current dashboard (the original due dates in the OKR charts will be overridden by this public filter). When tracking OKRs for multiple projects, users no longer need to open each OKR chart one by one to check the due dates. Instead, they can quickly view the overall timeline by using the public due date filter in the dashboard, significantly saving time and effort.

Steps:

(1) Click the global filter in the left sidebar, then click the three dots "More" in the pop\-up window, and select Add Due Date Filter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/caf6fc4ea703406a8c5b1e979b473a78~tplv-goo7wpa0wc-image.image) </span>

(2) Select the charts associated with the filter (only check OKR charts).

(3) Select the due date, supporting options such as the most recent 1 day, T\-1/T\-N, or a custom due date.

<span id="867c8080"></span>
# 5. Feature introduction

<span id="_3-1-调整筛选器的顺序"></span>
## 5.1 Adjust the order of filters

The filter tree on the left can be reordered by dragging and dropping. After adjusting, click "OK". The order of filters in the filter area of the dashboard will be updated.

<span id="_3-2-树状筛选器-and-or-配置场景示例"></span>
## 5.2 Example scenarios for configuring tree filters with and/or rules

<span id="_3-2-1-不同层级按照-and-规则生效"></span>
### 5.2.1 Different levels take effect according to the rules

The dataset corresponding to the associated chart contains multiple hierarchical relationship fields , and it is desired that different hierarchical fields are mapped one\-to\-one with the tree hierarchy.

<span id="_3-2-2-不同层级按照-or-规则生效"></span>
### 5.2.2 Different levels take effect according to the or rule


* The dataset corresponding to the associated chart contains only one hierarchical relationship field, and the values of this field are all the lowest\-level hierarchy values.

* The associated dataset contains only one hierarchical relationship field, and the values of this field include data from multiple hierarchical levels.


<span id="_3-3-图表筛选器的激活"></span>
## 5.3 Activation of chart filters

When the fields used by the public filter overlap with those of the chart filter, the public filter takes precedence.

Users can click the "Activate" button in the upper right corner of the chart to activate the chart filter. At this point, the chart filter will apply to the current chart, disabling all public filters applied to this chart.

<span id="_3-4-图表筛选器的隐藏"></span>
## 5.4 Hiding chart filters

The hide function is located in the chart's upper right options—Display In\-Chart Controls. After clicking Hide, the filter will be hidden immediately.

<span id="_3-5-显示查询按钮"></span>
## 5.5 Display query button

The public filter and chart filter in the dashboard provide a "Display query button" feature. The purpose of the query button is: after setting the filter conditions, you need to click the query button to trigger a query. Can reduce ineffective query overhead.

<span id="_3-5-1-公共筛选器"></span>
### 5.5.1 Public filter

Configuration entry:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a64eb6240134f49b0a0387eb727bec9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-2-图表筛选器"></span>
### 5.5.2 Chart filter

Configuration entry，

Located in the chart's upper right options, –the In\-chart controls display

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84c910385b91481cbb0138a015a012e6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-筛选器设置"></span>
## 5.6 Filter settings

Supports configuration of filter layout and style (query button, background color, height, and more).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/768cbf5ebb2e4e418c90bfd781a68789~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-图表提示"></span>
## 5.7 Chart tips

After a public filter is applied, the controlled charts will display a filter icon, indicating that the chart is affected by the public filter.

Hovering the mouse over this icon will show which public filters are affecting the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc5ade87af3e46ceae14194be72b8499~tplv-goo7wpa0wc-image.image) </span>
