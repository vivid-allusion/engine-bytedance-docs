---
title: "Parameter Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Parameter_Management"
---

<span id="_1-概述"></span>
# 1. Overview

A parameter is a variable that can be flexibly adjusted. This variable can be used in calculated fields to implement dynamic logic solutions for a single calculated field or even an entire chart. When a parameter takes different values, the field expression will correspond to different calculation logic.

<span id="_2-使用场景"></span>
# 2. Feature overview

<span id="_3-1-参数管理"></span>
## 2.1 Parameter management

<span id="_3-1-1-公共参数"></span>
### 2.1.1 Public parameters

Users with project view permission or above, and with edit permission for at least one dataset, can create public parameters.

Public parameters must be configured with effective datasets, and only the specified datasets can use these parameters. If there is no edit permission for any dataset, public parameters cannot be added.

When editing the dataset scope for an existing public parameter, regular users can only switch from "all datasets in the project" to "some datasets" and cannot switch back to "all datasets in the project".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad5072f7a5eb479da5a525fb6644b434~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa3cf48991864a948b6d63b5c8a18882~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-1-2-个人参数"></span>
### 2.1.2 Personal parameters

Administrators or regular users with project view permission or above can create and manage personal parameters. Personal parameters are at the project level. Personal parameters are available globally within the project. Once created, personal parameters can be applied to all datasets.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61194e06e9e248aaaa910ab4578ced14~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-3-参数格式类型"></span>
### 2.1.3 Parameter format types

**a. Text parameters**

Text parameters are divided into manual input, list selection, and dataset value retrieval.

> Manual input: Users can enter any value for the parameter in the input box for calculation, with no restrictions on input.

> List selection: Options for built\-in parameter values. Users can only select from the values in the built\-in list.

> Dataset value retrieval: Values are retrieved from datasets, supporting value retrieval from non\-ClickHouse direct connection datasets. Supported non\-ClickHouse direct connection data sources include Hologres, StaRocks, and MySQL.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/442ab657c03d4be490bb1569853fc773~tplv-goo7wpa0wc-image.image) </span>


* For dataset value retrieval, it supports setting field hierarchy, style (single selection/multiple selection), and default value. By clicking Advanced Settings, you can set to hide null values or hide empty strings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350c2ef2cc854639aa40b5b661ce815f~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fed945ddc8754e39b62689e3376fc97c~tplv-goo7wpa0wc-image.image) </span>

**b. Integer and floating\-point parameters**

Integer and floating\-point parameters are divided into manual input, list selection, and specified range. Manual input: Users can enter any value for the parameter in the input box for calculation, with no restrictions on input. List selection: These are selectable options for built\-in parameter values. Users can only select from the values in the built\-in list. Specified range: You can restrict the range of values users can enter (maximum and minimum values). By setting the step size, you can also restrict users to only use certain values within the range. As shown in the figure below, only the following values can be obtained: 1, 3, 5, 7, 9. Other values are not accessible.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/793b4271639e4d9f864ffdd6bb3a6621~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**c. Date and time parameters**

Date and time parameters only support manual input. The default value of a parameter can be set to a fixed date or a dynamic date.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40a632e6e64d4b0ea23125eaac8b2037~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-2-应用参数"></span>
## 2.2 Application parameters

<span id="_3-2-1-数据集-创建字段"></span>
### 2.2.1 Dataset \- Create field

In the field management section of the dataset editing interface, the "Add field" function allows you to use all **public parameters** applied to the current dataset to create new fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a01135035cfe49408ab6ae4fd9bf5a18~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05cf9c86644c406db8b0ad11b224469f~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43eed522ecd64ceebd32c93b627811bb~tplv-goo7wpa0wc-image.image) </span>
