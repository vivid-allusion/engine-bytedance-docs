---
title: "Filtering"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Filtering"
---

The dashboard's filtering features, through four types of controls—global filter, dynamic dimension/metric, global parameter, and query container—allow users to set filter conditions for one or more charts within the dashboard, meeting data analysis and chart display needs for different business scenarios. This article provides a detailed explanation of the functions, usage scenarios, operation steps, and special configurations of each control.

<span id="23087295"></span>
# Feature overview

Filtering refers to the ability for users to set filter conditions for one or more charts within the dashboard using related features, facilitating data analysis and chart display according to various business situations. The dashboard editing page provides the following four types of filtering controls.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcc09a70fd9a41b596efd8ca0a160a39~tplv-goo7wpa0wc-image.image) </span>


|Control name |Control introduction |For more information, refer to |
|---|---|---|
|Global filter |Filters that can be applied simultaneously to multiple tables allow users to filter multiple charts within the dashboard without needing to configure each one individually. |[Global Filter](https://docs.byteplus.com/docs/DataWind/Global_Filter) |
|Dynamic dimensions/metrics |Allows switching between dimensions and metrics to quickly meet the needs of different users for various dimensions and metrics. |[Dynamic Dimensions and Dynamic Metrics](https://docs.byteplus.com/docs/DataWind/Dynamic_Dimensions_and_Dynamic_Metrics) |
|Global parameters |Global parameters that take effect across multiple tables allow users to filter multiple charts within the dashboard without needing to configure each one individually. |[Parameter Management](https://docs.byteplus.com/docs/DataWind/Parameter_Management) |
|Query container |Some of the controls mentioned above may be bound to only one field, while others are bound to multiple fields. Since only one container can be pinned to the top, displaying them on the dashboard may result in an uncoordinated and unattractive layout. In such cases, the query container can be used to place different components in the same container, making the layout both visually appealing and easy to use. This container can simultaneously accommodate all three types of controls mentioned above. |For detailed information, see the query container section in the **Quick Start** part of this document. |


<span id="660b7c21"></span>
# Quick start

<span id="9996322c"></span>
## Common usage scenarios

<span id="d7a751bd"></span>
### **Global filter**

Use a single filter to control options for multiple charts.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The format of the control fields must be consistent; however, the field values and datasets used can be different.</div>


* <div data-tips="true" data-tips-type="warning">When users purchase and deploy VeCDP simultaneously, the global filter supports <a href="https://www.volcengine.com/docs/6356/81286">VeCDP audience packages</a>.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88b990ad51ed4626ada73107cfa88303~tplv-goo7wpa0wc-image.image) </span>

<span id="1fe08cd4"></span>
### **Dynamic dimension/metric**

Enables quick switching of the current dimension and metric of a chart without modifying the chart itself. The global dynamic dimension/parameter allows simultaneous switching of dynamic dimensions/parameters for all bound charts on the dashboard, quickly meeting different users' needs for various dimensions and metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dff2429bb7984513bcd9ce59a28bc170~tplv-goo7wpa0wc-image.image) </span>

<span id="ff6506aa"></span>
### **Dynamic parameter**

When multiple charts use the same parameter, a global parameter filter can be created to adjust parameter values for multiple charts at the same time, reducing repetitive operations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Global parameters require that the parameters associated with multiple charts are the same.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b51d2d0ef9794254a0c79e871e20ef24~tplv-goo7wpa0wc-image.image) </span>

<span id="235db0aa"></span>
### **Query container**

The query container can simultaneously hold global filters, dynamic dimensions/metrics, and global parameters, enabling all three components to be placed within a single container.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63a1f319d0f541a6ac78929b3ccf6891~tplv-goo7wpa0wc-image.image) </span>

The parameter selection, dynamic dimension, dynamic metric, and global filter in the query container support custom ordering.

<span id="97e35714"></span>
## Usage example

<span id="2222a0fb"></span>
### **Global filter**


1. On the dashboard editing page, click "Global Filter" in the control panel on the left to open the configuration page for the global filter.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/910edc771cd44b6b932364b9707f80a3~tplv-goo7wpa0wc-image.image) </span>

2. Select the associated charts and the required filter fields.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b75903ff1004155b2e77d4249acc14a~tplv-goo7wpa0wc-image.image) </span>

3. Configure the public filter, such as the default filter conditions, filter method, filter style, and more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8ea4d53bb064ab3973758974400a346~tplv-goo7wpa0wc-image.image) </span>

4. Modify the filter name, choose whether to pin the public filter to the top, or click the "+" icon to add more filters. After configuration is complete, save the dashboard.

5. After saving the dashboard, the public filter will be available.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c53b4731163242189dc3243189292979~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Starting from version V2.87.0, users can directly modify the filter criteria for numeric filters.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/091976c07bbd43a3b40252a690b57c87~tplv-goo7wpa0wc-image.image" width="2045px" />   </div>
   

<span id="3f177a58"></span>
### **Public dynamic dimension/metric filter**


1. On the dashboard editing page, click "Dimension/Metric" in the component panel on the left to open the configuration page for global dynamic dimensions/metrics.

2. Select the charts to associate and the corresponding dynamic dimensions/metrics.

3. Select the default dynamic dimension/metric, choose the required style, and click Confirm.

   * The options in dynamic dimensions/metrics are the union of all associated charts' dynamic dimensions/metrics.

4. After configuration is complete, save the dashboard for the global dynamic dimensions/metrics to take effect.


<span id="766b0c77"></span>
### Global parameters


1. On the dashboard editing page, select "Dynamic Parameter" in the control panel on the left to open the configuration page for global parameters.

2. Click "Add Parameter", select the parameter to bind, style, control visibility, and more. After configuration is complete, click the Complete icon.

3. You can continue to click "Add Parameter" to configure multiple global parameters. After configuration is complete, click Confirm.

4. After configuration is complete, save the dashboard. You can then use the global parameter to control the parameters of all bound charts.


<span id="951a6dee"></span>
### Query container

A query container can simultaneously include a global filter, dynamic dimensions/metrics, and global parameters.


1. On the dashboard editing page, click Query Container in the component panel on the left to generate a query container on the dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/947fc78fc0cc43baaafc135e979866cb~tplv-goo7wpa0wc-image.image) </span>

2. Click the upper right corner of the query container to add the required components. From left to right, these are: global filter, global dynamic dimension/metric, and global parameter. You can also identify them by their icons.

3. Configure the global filter, dynamic dimension/metric, and global parameter as needed.


<span id="6b2594c4"></span>
# Introduction to global filter functionality

The global filter is one of the controls for filtering and selection. It supports simultaneous application to multiple charts, allowing users to filter multiple charts within the dashboard without setting each one individually, thereby enabling data analysis and chart display. For more information, refer to [Global Filter](https://docs.byteplus.com/docs/DataWind/Global_Filter).

<span id="d099c016"></span>
# Introduction to dynamic dimension/metric functionality

<span id="88c1302d"></span>
## Same dataset

When using the same dataset, the enumeration values for dynamic dimensions/metrics default to the union of all dynamic dimensions/metrics associated with the related charts.

<span id="7de6ec3a"></span>
## Different datasets

When using different datasets, you can establish associations between fields from different datasets.

<span id="7d3f5561"></span>
# Introduction to global parameter functionality

<span id="1b4681f2"></span>
## Control visibility


* If the control visibility is set to hidden, the public parameter will not be displayed on the dashboard.
