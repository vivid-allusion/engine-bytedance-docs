---
title: "Parameter Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Parameter_Management"
---

<span id="_1-概述"></span>
# Overview

A parameter is a variable that can be flexibly adjusted. This variable can be used in calculated fields to implement dynamic logic for a single calculated field or even an entire chart. When the parameter takes different values, the field expression will correspond to different calculation logic.

<span id="af9cc210"></span>
# Use cases

<span id="ea8d9475"></span>
## Set dynamic target values and dynamically calculate target completion progress

<span id="3febe232"></span>
### Implementation results

In sales scenarios, target values for a specific time period can be set as needed by month, week, day, and so on. Because the target value changes dynamically according to business needs, the calculated value for target completion progress also changes dynamically. As shown in the figure below, you can manually enter the target value and dynamically calculate the target completion progress.

<span id="b2317b27"></span>
### Implementation plan (public parameter)


* Click Data Preparation in the top navigation bar \-\-\> Dataset, click Overview on the left (the default page is Overview, so this step is optional), and the "Parameter Management" button will appear on the right.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7265415e5ee4e96a4a054690f193daa~tplv-goo7wpa0wc-image.image) </span>


* Click the **Parameter Management** button to open the parameter management dialog box, then click the **Create Parameter** button on the right to start creating a parameter.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbec542ff4de4dd79c329a362d8f63f8~tplv-goo7wpa0wc-image.image) </span>


* Refer to the figure below and fill in the fields in order.

   * Name \-\- Custom

   * Type \-\- Select Integer here

   * Data option \-\- Select Manual Input here

   * Initial value \-\- Any custom value

   * Style \-\- Default input box

   * Applied dataset \-\- Select the dataset you intend to use

* Then click OK to save the parameter.

* Select Visual Query from the top navigation, and choose the dataset where the parameter was set.

* Click the dataset, then click "Add Field" to start setting up the new target completion progress field.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25960f294eca432cb396448506127deb~tplv-goo7wpa0wc-image.image) </span>


* The numerator of the field expression is obtained from the dataset field, and the dynamically calculated denominator is obtained from the parameter. Double\-click these fields to add them to the field expression box, then click the OK button in the lower right corner to save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d871750a83fa400d864ecf161109b503~tplv-goo7wpa0wc-image.image) </span>


* Next, drag the corresponding date, GMV field, and the calculated target completion field into the box as shown below. Add the required filter conditions to obtain the result shown in the following figure. After saving, you can modify the target value to achieve dynamic calculation effects.


<span id="c75b1e8e"></span>
## Dynamic comparison of two groups of data

<span id="ae80d767"></span>
### Implementation result

Currently, there is a set of data where each group number corresponds to a data set. The requirement is to select two groups—one as the experimental group and the other as the control group—to compare the differences between the two groups. You can also switch the experimental and control groups at any time.


|Group |Results |
|---|---|
|1201 |11772228 |
|1202 |11829734 |
|1203 |11887240 |
|1204 |11944746 |
|1205 |12002252 |
|1206 |12059758 |


The effect achieved through the parameter functionality is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c0ebffcff40f962cd312f37db4aa388.gif) </span>

<span id="e556730c"></span>
### Implementation plan (personal parameters)


* Click "Data Preparation" in the top navigation bar, then "Dataset". Click "Overview" on the left (by default, you are already on the Overview page, so this step is optional). The "Parameter Management" button will appear on the right.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcbed4f191eb4cc9adcc9035a6e25161~tplv-goo7wpa0wc-image.image) </span>


* Click "Parameter Management" to open the "Parameter Management" dialog box. Select "Personal Parameters", then click the "Create Parameter" button on the right to start creating parameters.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b5a5265ec8443ef80d014d4ee187d0a~tplv-goo7wpa0wc-image.image) </span>


* Add two parameters named "Experimental Group" and "Control Group". For the data options, you can choose either list selection or manual input as needed. If you choose list selection, all groups will be displayed for easy selection. If there are too many groups, you can manually input the group names.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78caa1ab480d4c7e9c6fdfc16a7f4ce4~tplv-goo7wpa0wc-image.image) </span>


* Then click OK to save the parameter.

* From the top navigation, select Visual Query and choose the dataset with the parameters set.

* Click the dataset, then click "Add Field" to start configuring the new metric fields.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e940478589944cd0a1ba6d185be9f1a4~tplv-goo7wpa0wc-image.image" width="564px" /></div>



* Add new metric fields named "Experimental Group Data" and "Control Group Data". Using the "Data Result" field as an example, the expression for "Experimental Group Data" is: `sum(if([group]={individual}.{experimental group},[data result],0))`, and the expression for "Control Group Data" is: `sum(if([group]={individual}.{control group},[data result],0))`

* The "Group" and "Data Result" fields in the field expression are obtained from dataset fields, while the `{Personal}.{Experimental Group}` and `{Personal}.{Control Group}` fields are obtained from parameters. Double\-click these fields to add them to the field expression box, then click the Confirm button in the lower right corner to save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6d3670840634e92a7cc5dd878344c6a~tplv-goo7wpa0wc-image.image) </span>


* Next, place these two fields into the chart to enable dynamic adjustment of the experimental group and control group data, thereby updating the field display results.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef3bb8f8caac46d384011e0e99989938~tplv-goo7wpa0wc-image.image) </span>


* The above figure shows how to use parameters to change the data for the experimental group and control group. These two sets of data can then be used to generate other required data. For example, to calculate the percentage difference between the experimental group and control group data, you can create a new "Percentage Difference" field with the following field expression: `([Personal].[Experimental Group Data]-[Personal].[Control Group Data])/[Personal].[Control Group Data]`

* Then, drag the "Percentage Difference" field to the metrics area, and adjust the data format to percentage.

* You can then add the data you want to view to the dimension indicators.

* With richer data dimensions, you can also select more analytical dimensions, switch chart formats, and present more comprehensive analysis results.


<span id="10933a37"></span>
# Feature overview

<span id="e4e1ca58"></span>
## Parameter management

<span id="34ead777"></span>
### Public parameters

Users with project view permission or higher, and at least editing permission for one dataset, can then create public parameters.

Public parameters must be configured with effective datasets, and only specified datasets can use these parameters. If you do not have editing permission for any dataset, you cannot add public parameters.

When editing the dataset scope for an existing public parameter, regular users can only switch from "All datasets in the project" to "Some datasets" and cannot switch back to "All datasets in the project".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6acf86a43a72455aa81dca321cbb684b~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3301d417ec94af8b7bac08744465f51~tplv-goo7wpa0wc-image.image" width="577px" /></div>


<span id="11ce2c0d"></span>
### Personal parameters

Administrators or regular users with project view permission or above can create and manage personal parameters. Personal parameters are at the project level. Personal parameters are available globally within the project. Once created, personal parameters can be applied to all datasets.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bffe721e79348a8a5d1a74bb7b963c3~tplv-goo7wpa0wc-image.image) </span>

<span id="ad3aa13c"></span>
### Parameter format types

**a. Text parameters**

Text parameters are divided into manual input, list selection, and dataset value retrieval.

> Manual input: Users can enter any value for the parameter in the input box for calculation. There are no restrictions on input.

> List selection: Options for built\-in parameter values. Users can only select from the values in the built\-in list.

> Dataset value retrieval: Values are retrieved from datasets, supporting retrieval from datasets not directly connected to ClickHouse. Supported data sources not directly connected to ClickHouse include Hologres, StaRocks, and MySQL.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbfa359561754577978d8b85aed96b86~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* For dataset value retrieval, you can configure field hierarchy, style (single selection/multiple selection), and default value. Click Advanced Settings to configure hiding null values or empty strings.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7af88098709c4e7eaabc141487cdc093~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e2a912cb12e46d8b12584c7ad819061~tplv-goo7wpa0wc-image.image" width="707px" /></div>


**b. Integer and floating\-point parameters**

Integer and floating\-point parameters are divided into manual input, list selection, and specified range. Manual input: Users can enter any value for the parameter in the input box for calculation. There are no restrictions on input. List selection: Options for built\-in parameter values. Users can only select from the values in the built\-in list. Specified range: You can restrict the range of values users can enter (maximum and minimum values). By setting the step size, you can also restrict users to only use certain values within the range. As shown in the figure below, only the values 1, 3, 5, 7, and 9 are available. Other values are not accessible.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e811a97fd2d4d58935a31a5f656bc93~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**c. Date and time parameters**

Date and time parameters only support manual input. The default value of a parameter can be set to a fixed date or a dynamic date.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7de62cce4bdc4e2092995f0b7314180e~tplv-goo7wpa0wc-image.image) </span>

<span id="b05146ff"></span>
## Apply parameters

<span id="2323495e"></span>
### Dataset \- create field

In the field management section of the dataset editing interface, you can use all **public parameters** applied to the current dataset to create new fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b163189565b743abb6f5ca228177d262~tplv-goo7wpa0wc-image.image) </span>

<span id="00aa19dd"></span>
### Visual query \- create field

In the visual query interface, "Add Field" allows you to create new fields using all **public parameters** and **personal parameters** applied to the current dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb1d1b40f0aa4aa7b1cf2adccddfe123~tplv-goo7wpa0wc-image.image) </span>

<span id="0ba12a1c"></span>
## You can pass the filter values of date or metric filters as parameter values

On the visual query page, if any field in the current chart uses parameters, you can pass the filter values from date or metric filters as the values for parameters used in expressions. For example, to calculate the average sales amount over a period, the calculation is typically sum(sales amount)/{count(days)}. However, if there is a day with no sales record, that day will not be counted, but it should be included in the calculation. This feature can be used to address this scenario. Steps:


* On the dataset overview page, go to parameter management in the upper right corner and create two new parameters, such as start date and end date, and set the parameter type to date.

* Return to the visualization page and create a new field with the expression dateDiff({start date}, {end date}), which calculates the difference between the start date parameter and the end date parameter.

* Select the required date filter, for example, p_date. Click the configuration in the upper right corner and bind the start date and end date to the corresponding parameters.

* After saving, when you modify the date filter range, the start and end values of the date filter will be passed to the bound parameters.


<span id="c0489325"></span>
## Display parameters

<span id="4af36ea3"></span>
### **In\-chart parameters**

If the field expressions used for plotting and analysis contain parameters, or if the field expressions directly or indirectly reference parameters. Then the parameter will be displayed in the visual query. You can set the parameter to be shown or hidden in "In\-chart parameters".

<span id="f0ace6d1"></span>
### **Dashboard global parameters**

In the global parameter configuration of the dashboard, you can configure the style and visibility of public and personal parameters.
