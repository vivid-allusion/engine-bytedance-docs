---
title: "Dimension Filtering"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dimension_Filtering"
---

This article introduces multiple methods for dimension filtering in datasets.

<span id="418a083d"></span>
# Quick start


1. Click "Filter configuration" to enter the dataset filter configuration interface, then click "Add" to set the filter criteria for the dimension fields used by the agent.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6decfe4dd3c54c1591a511106b13a73d~tplv-goo7wpa0wc-image.image) </span>


2. For dimension fields, three methods are provided: "Exact filtering", "Conditional filtering", and "Manual input". Set the relevant filter parameters according to actual data requirements, then click "Confirm" to execute the filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92d4088f408844a782848d9b4da6d21a~tplv-goo7wpa0wc-image.image) </span>

<span id="d3993d7a"></span>
# Applicable scenarios


|Dimension filtering methods |Applicable scenarios |
|---|---|
|Exact filtering |Suitable for precisely locating small batches of data with clear objectives |
|Conditional filtering |Suitable for filtering data with complex logic or range\-based criteria |
|Manual input |Suitable for flexible customization or filtering non\-standard data |


<span id="d9c1ecc4"></span>
# Feature overview

<span id="1d636dd5"></span>
## Exact filtering


1. Click "Exact filtering" to enter the exact filtering parameter configuration page.

2. By directly selecting or searching for filter content, you can perform operations such as viewing selected items (all items), option settings, option sorting, select all, and exclude.

3. Click "Confirm" to complete data filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd1bd583864a4b118830e89dd4f3e420~tplv-goo7wpa0wc-image.image) </span>

Relevant parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|View selected items (all items) |Click to switch between viewing selected items and all items. |
|Option settings |Click to set manual input or clear settings.<br><br><br>* Set manual input: You can manually enter multiple precise filter criteria here, separated by commas, spaces, or line breaks; or input filter criteria by uploading or dragging a CSV file.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12410d1b997c48b18c63bf33166cab6c~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clear settings: Clear the currently set manual input filter criteria. |
|Option sorting |You can set the display order of all items to ascending, descending, or custom sorting. You can also choose to clear settings to remove the current sorting. |
|Select all |When selecting all, all options in the current option area are selected. If the filter is empty, all data is selected. |
|Exclude |Performs inverse selection, equivalent to "not in". |


<span id="709dabc6"></span>
## Conditional filtering


1. Click "Conditional filtering" to enter the conditional filtering parameter configuration page.

2. By manually entering or selecting from a list, you can perform operations such as choosing operators and entering conditions.

3. Click "Confirm" to complete data filtering.

* Conditional filtering \- manual input


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3d2802bacff4bd9a0fe41999c711a7a~tplv-goo7wpa0wc-image.image) </span>

Relevant parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|Operators |* For string\-type fields, supports contains and does not contain, starts with and ends with, like and not like, empty and not empty, empty string and not empty string, and other operators.<br><br>* For numeric\-type fields, supports =, ≠, \>, ≥, <, ≤, empty and not empty, and other operators |
|Manual input |You can directly enter the text abc to perform fuzzy matching for data items containing abc, which is equivalent to like: %abc% |
|Separator |Manually entered criteria support separation by commas, spaces, or line breaks |



* Conditional filtering \- list selection


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de632d647a954aaab594da494bf2b932~tplv-goo7wpa0wc-image.image) </span>

Relevant parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|Operators |* For string\-type fields, supports contains and does not contain, starts with and ends with, like and not like, empty and not empty, empty string and not empty string, and other operators.<br><br>* For numeric\-type fields, supports =, ≠, \>, ≥, <, ≤, empty and not empty, and other operators |
|List selection |You can manually select filter items from the enumeration values of the current field. Supports the operators described above, as well as "View selected items (all items)", "Option settings", "Option sorting", and "Select all" in precise filtering. |


<span id="550251cf"></span>
## Manual input


1. Click "Manual input" to enter the manual input filter parameter configuration page.

2. Enter filter criteria by manually inputting multiple values (separated by commas, spaces, or line breaks), or by uploading/dragging a CSV file.

3. Click "Confirm" to complete data filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52cbb7f36f004c88870124d163851065~tplv-goo7wpa0wc-image.image) </span>
