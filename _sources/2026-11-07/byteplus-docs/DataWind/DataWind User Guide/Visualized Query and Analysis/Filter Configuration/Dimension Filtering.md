---
title: "Dimension Filtering"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dimension_Filtering"
---

Filtering is a fundamental part of data analysis. This article introduces multiple ways to perform **dimension filtering** on data in product charts.

<span id="143b73d9"></span>
# Feature overview


|Filter modes |Mode overview |
|---|---|
|**Exact filtering** |Select or search for target values from the predefined option list. |
|**Conditional filtering** |Dynamically filter data using logical operators. |
|**Manual input** |Paste directly or upload a CSV file for filtering. |
|**Subquery** |Reference results from other charts as filter criteria. |


<span id="_2-快速入门"></span>
# Quick start


1. After dragging a dimension field into the "Filter" area, a settings panel will pop up.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d6866bfbc7847a3af9be1683df7c3da~tplv-goo7wpa0wc-image.image) </span>

2. Switch to the desired mode and set the filter criteria.

   * No chart filter required

      After clicking OK, the filter criteria will take effect for the current chart.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdb5161d2fee4773b28fd0c9b21059f5~tplv-goo7wpa0wc-image.image) </span>

   * Chart filter required

      After checking the "Show as chart filter" checkbox at the lower left of the panel and clicking OK, the filter criteria will take effect and a filter control will be displayed on the page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c7cf733a3d04fc59086da3f7bb90b8b~tplv-goo7wpa0wc-image.image) </span>

      Display effect:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5320025fd9bc41eeb0fa7464fa62190e~tplv-goo7wpa0wc-image.image) </span>


<span id="2fbaa9de"></span>
# Exact filtering


1. Click "Exact filtering" to enter the exact filtering parameter configuration page.

2. By directly checking or searching for filter content, you can view selected items (all items), set options, sort options, select all, exclude, and perform other operations.

3. Click "OK" to complete data filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab1afeebd6864ca1bf14328d6588d078~tplv-goo7wpa0wc-image.image) </span>

The relevant parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|Option area |The option list is displayed in the settings panel. You can select options by checking them, or search for keywords and select them in bulk.<br><br><br>* If the search does not return the corresponding option, press "Enter" to manually add the input content to the options.<br><br>* Click "View selected options" to see the options you have already selected.<br><br>* When there are many filter options, to ensure filter performance, only a sample of options is displayed. Click "More data items" to display all options. |
|Option settings |To configure the option list, use the option settings feature. If the settings are unsatisfactory, select "Clear settings".<br><br><br>* Manual input<br><br>* Subquery<br><br>* From other datasets |
|Option sorting |To define the order of options, use the option sorting feature. The following is a description of the option sorting functionality:<br><br><br>* Ascending: Options will be sorted in alphabetical ascending order<br><br>* Descending: Options will be sorted in alphabetical descending order<br><br>* Manual sorting: Manually specify the order of options |
|Select all |Select all options on the current page; can be used with the search function |
|Exclude |Inverse selection: Equivalent to "not in" |
|Display as chart filter |After selecting "Display as chart filter", you can set the filter name. A dropdown list is displayed on the right, allowing you to choose the style of the filter control.<br><br><br>* Multiple selection (dropdown): All options are displayed as a dropdown list, supporting the selection of multiple filter options<br><br>* Single selection (dropdown): All options are displayed as a dropdown list, supporting the selection of a single filter option<br><br>* Multiple selection (tiled): All options are displayed in a tiled layout, supporting the selection of multiple filter options<br><br>* Single selection (tiled): All options are displayed in a tiled layout, supporting the selection of a single filter option |


The following is a detailed explanation of the option settings feature:


|Option setting type |Description |
|---|---|
|Manual input |You can add options by manual input or by uploading a CSV file, to replace the automatically read option list.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1217217d62014d2cb375f726d64e4e6d~tplv-goo7wpa0wc-image.image) </span> |
|Subquery |Options depend on a dimension field in another chart.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f43e2603138b4423b1547c29b64d49ff~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For performance reasons, it is recommended to keep the number of members below 50,000, that is, the number of members (rows or columns) returned by the subquery should not exceed 50,000.</div><br> |
|From other datasets |From other datasets: Obtain values from other datasets (such as from a dimension table dataset) |


<span id="_3-3-条件筛选"></span>
# Conditional filtering


1. Click "Conditional filtering" to enter the conditional filtering parameter configuration page.

2. By manually entering or selecting filter content from a list, you can select operators, enter conditions, and perform other operations.

3. Click "OK" to complete data filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/136e1b4369644ab2aa972681b1c6b46c~tplv-goo7wpa0wc-image.image) </span>

The relevant parameter descriptions are as follows:


|Parameter |Configuration description |
|---|---|
|Operator |* For string\-type fields, the following operators are supported: (not) contains, starts with (ends with), (not) like, (not) null, (not) empty string, and more<br><br>* For numeric\-type fields, the following operators are supported: =, ≠, \>, ≥, <, ≤, (not) null, and more |
|Manual input and list selection |Conditional filter items support both manual input and list selection.<br><br><br>* Manual input: You can directly enter text such as abc to perform fuzzy matching for data items containing abc, which is equivalent to like:%abc%<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64f3bbf67cfb43e1a2b4447727c7e518~tplv-goo7wpa0wc-image.image) </span><br><br>* List selection: You can manually select filter items from the enumeration values of the current field; supports operators as well as "Option setting" and "Option sorting" in precise filtering.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/770181923ea74c16b3931c110fa5fda7~tplv-goo7wpa0wc-image.image) </span> |
|Display as chart filter |After selecting "Display as chart filter", you can set the filter name. A drop\-down list appears on the right, allowing you to choose the style of the filter control.<br><br><br>* Multiple selection (drop\-down list): All options are displayed in a drop\-down list and support multiple filter options.<br><br>* Single selection (drop\-down list): All options are displayed in a drop\-down list and support a single filter option.<br><br>* Multiple selection (tiled): All options are displayed in a tiled layout and support multiple filter options.<br><br>* Single selection (tiled): All options are displayed in a tiled layout and support a single filter option. |


The following is an introduction to the operators:


* For string types, the list of operators is as follows:

   
   |Operator |Actual operation |Example |
   |---|---|---|
   |Contains |like |User input: Beijing, Shanghai.<br><br>The corresponding SQL is:<br><br>```plaintext```<br>```where `city` like ("%Beijing%","%Shanghai%")```<br> |
   |Does not contain |nok like |User input: Beijing, Shanghai.<br><br>The corresponding SQL is:<br><br>```plaintext```<br>```where `city`  not like ("%Beijing%","%Shanghai%")```<br> |
   |Starts with |like |User input: Bei, Shang.<br><br>The corresponding SQL is:<br><br>```plaintext```<br>```where `city` like ("Bei%","Shang%")```<br> |
   |Ends with |like |User input: Bei, Shang.<br><br>The corresponding SQL is:<br><br>```plaintext```<br>```where `city` like ("%Bei","%Shang")```<br> |
   |like |like |\ |
   |not like |not like |\ |
   |Is null |is null |\ |
   |Is not null |is not null |\ |
   |Is empty string |is empty |\ |
   |Is not empty string |is not empty |\ |
   

* For numeric types, the list of operators is as follows:

   
   |Operator |
   |---|
   | |
   |< |
   |≧ |
   |≦ |
   |Range |
   |Not in range |
   |Is null |
   |Is not null |
   

   If "Range" or "Not in range" is selected, you also need to specify whether the range boundaries are open or closed intervals.


<span id="_3-3-2-手动输入与列表选择"></span>
# Manual input

The user can copy content from Excel and paste it into the text box, where the content will be split into capsules according to the delimiter below the text box; or upload a CSV file. Multiple uploads will overwrite previous uploads, with the latter overwriting the former.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71b0b40168544fb3b4ee0fb53d6700a9~tplv-goo7wpa0wc-image.image" width="610px" /></div>


If invalid characters appear in the content, the capsule will be highlighted in red.

<span id="9c6b3821"></span>
# Subquery

Dimension filtering supports the subquery feature, allowing users to use the query results of other charts as filter options for the current chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a96bdca022614170be1e0f5f009f6ef4~tplv-goo7wpa0wc-image.image) </span>

The relevant parameter configuration description is as follows:


|Parameter |Configuration instructions |
|---|---|
|Select chart |Select the subquery chart.<br><br><br>* By chart name: This is the default selection method, which performs a fuzzy search based on the entered chart name.<br><br>* By chart ID: Users can manually switch to this method to search by chart ID or chart query link.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the entered chart ID or query link is incorrect or does not exist, the input box will turn red and display the message "Chart ID does not exist. Please re\-enter."</div><br><br><br>   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21ff320579344a83b8b872cc710aecff~tplv-goo7wpa0wc-image.image" width="367px" />   </div><br>   <br><br>* <div data-tips="true" data-tips-type="tip">The user's selection mode is recorded: After "By chart ID" has been selected, the next time this dialog is opened, "By chart ID" will be selected by default to prevent reverting to the initial "By chart name" state.</div><br><br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Charts that meet the following conditions are not supported as subquery charts:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Self\-reference is not allowed</div><br><br><br>* <div data-tips="true" data-tips-type="warning">All included subquery charts must also have the corresponding dataset read or higher permissions</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Dynamic dimensions or metrics are not allowed</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Associated datasets cannot be used</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Parameter\-bound fields are not allowed</div><br> |
|Select dimension |Select the subquery dimension field. |
|Advanced settings |You can set the maximum number of members allowed in the subquery.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For performance reasons, it is recommended to keep the number of members below 50,000, that is, the number of members (rows or columns) in the subquery result should not exceed 50,000.</div><br> |


**Scenario example:** 


* For example, suppose there are two datasets, A and B, both containing the "Order ID" field. The requirement is that the final filtered "Order ID" must meet the relevant filtering criteria of both dataset A and dataset B. In this case, the subquery feature can be used. First, use dataset A's fields to filter out a batch of "User IDs". Then, use the "Order IDs" of these "User IDs" in dataset B for further filtering to obtain the final result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f1720387614430295a8e9b30c0c91b9~tplv-goo7wpa0wc-image.image) </span>


**Operation steps:** 


1. Create a subquery chart. In the current project, create and save a chart (you can view existing charts under the current project in "Project Center" \- "Chart Management").

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3089be38cd434b2187f1aee9d64aa02f~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7bfeaf6316a4eedb7b0e240e4535da3~tplv-goo7wpa0wc-image.image) </span>

2. Create a new visual query, add the field to the filter, select "Subquery" mode, and choose the subquery chart and corresponding field.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f1720387614430295a8e9b30c0c91b9~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99c2d07255834a3eaabcd695a35cb3a5~tplv-goo7wpa0wc-image.image) </span>


<span id="9f6f1169"></span>
# Set the filter

<span id="_3-6-显示为图表筛选器"></span>
## Filter style

After selecting "Display as chart filter", a drop\-down list appears on the right, where you can choose the style of the filter control. 3.7 Filter layout settings


* Multiple selection (drop\-down list): All options are displayed as a drop\-down list, supporting the configuration of multiple filter options

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d958e9014a294a3f8527d8ca283d30b8~tplv-goo7wpa0wc-image.image) </span>

* Single selection (drop\-down list): All options are displayed as a drop\-down list, supporting the configuration of a single filter option

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e529ac54974846c19404ba65a7fd1de3~tplv-goo7wpa0wc-image.image) </span>

* Multiple selection (tiled): All options are displayed in a tiled layout, supporting the configuration of multiple filter options

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a97c2ae8ff9644adb7c3495aaf4afde4~tplv-goo7wpa0wc-image.image) </span>

* Single selection (tiled): All options are displayed in a tiled layout, supporting the configuration of a single filter option

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ee50ac4a16a4ac391a37793d8383b1e~tplv-goo7wpa0wc-image.image) </span>


<span id="1a14fa2f"></span>
## Filter layout

Setting entry: Located in the chart settings area on the left

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a26f24219b234238a6ac5418c940042d~tplv-goo7wpa0wc-image.image) </span>

Users can adjust the filter layout according to their actual needs. Two features are provided:


* Title settings

   * Horizontal arrangement

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7490cda49584bd091c28801219d5d63~tplv-goo7wpa0wc-image.image) </span>

   * Vertical arrangement

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a7fbb72e4a04667a013938b9da05e00~tplv-goo7wpa0wc-image.image) </span>

* Layout settings

   * Compact

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d83d968547c44a7b8b93209181565970~tplv-goo7wpa0wc-image.image) </span>

   * Standard

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b5625a28b4b45bfbe64d627ce41f1b7~tplv-goo7wpa0wc-image.image) </span>

   * Relaxed

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00dc4c17a33f4a568061591a1015a0e4~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-8-设置子筛选器"></span>
## Set sub\-filter

When sub\-filter settings are not configured, different filter criteria do not affect each other. For example, in the diagram below, "Province" is set to "Shanghai", but all options remain selectable in the "City" filter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96626e4a454740e8ad3f2aab3d39e44b~tplv-goo7wpa0wc-image.image) </span>

To make the enumerated values in "City" dependent on the "Province" filter, configure "City" as a sub\-filter of the "Province" filter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23c5c5f1825042ec828bfc6f3e99d7da~tplv-goo7wpa0wc-image.image) </span>

After configuring the sub\-filter, only the enumerated values filtered by "Province" will appear in "City".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8acd455950244bf83e3c7fc8ac569db~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-9-筛选器-or-条件"></span>
## Filter OR condition

Click the small arrow on the filter to add an OR condition. Drag the dimension into the corresponding position.

After adding, the filter criteria are connected by an OR relationship.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b1e31036ea14730a1feb978391a9317~tplv-goo7wpa0wc-image.image) </span>
