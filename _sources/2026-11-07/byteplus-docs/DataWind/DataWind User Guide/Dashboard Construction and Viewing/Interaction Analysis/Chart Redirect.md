---
title: "Chart Redirect"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Chart_Redirect"
---

The dashboard chart redirect feature allows viewers to quickly access related dashboards or external web pages by clicking data fields. This article provides a detailed explanation of how to configure chart redirect rules and parameter passing methods in edit mode.

<span id="a5656f83"></span>
# Feature overview

Dashboard editors can configure redirects for chart fields in the dashboard editing interface. After the redirect is configured, dashboard viewers can click chart fields to redirect to other dashboards or web pages. The redirect feature also supports redirecting to other dashboards with filter conditions, or to web pages with parameter values.

<span id="3a4466e5"></span>
# Feature introduction

Chart redirects can be configured in two ways:


* **Dashboard\-configured chart redirect**: On the dashboard editing page, set a redirect for a chart field to a web page or dashboard. This configuration only applies to chart fields within the current dashboard; the same chart in other dashboards is not affected.

* **Visual query\-configured chart redirect (template link)** : On the chart visual query page, set a template link for a field to redirect to a web page. After saving, the configuration takes effect in all dashboards containing this chart.


<span id="ebcf0bdf"></span>
## Dashboard\-configured chart redirect

<span id="54598974"></span>
### Access redirect settings


1. Edit the dashboard, select the chart for which you want to enable redirect, and click the ⋮ in the upper right corner of the chart to select redirect settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d34c5e6b80064c26972ed5c6db83eb1e~tplv-goo7wpa0wc-image.image) </span>

2. Select the metric field for which you want to configure the redirect, and set the redirect method for each field.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96e245ea7cd540888231d0acf20ab4ed~tplv-goo7wpa0wc-image.image) </span>

   For charts that meet the following conditions, different redirect methods can be configured for fields:

   1. The chart supports multi\-metric plotting;

   2. Multiple metrics are not in the same mark;

   3. If there are drill\-down fields under the current primary field, drill\-down fields also support redirect configuration;

   4. Example: column charts (three types), bar charts (three types), line chart, area charts (two types), dual\-axis chart, bidirectional bar chart, combination chart, pie charts (three types), funnel chart, indicator trend chart, progress chart.

   5. **For example, with table\-type charts**: Table\-type charts can be configured with bound fields. Clicking a bound field enables the corresponding redirect. Different redirect rules can be configured for different fields, and the fields used in redirect rules do not conflict with the bound fields.

      After configuration, clicking different fields allows you to redirect to different destinations.


<span id="f65985d1"></span>
### Configure redirect methods separately.

For a specific field, select a redirect method. You can choose to redirect to another dashboard or to a web page link. redirect settings support copying. After clicking Copy, a new configuration entry is added with the bound field left empty. The redirect configuration on the right is consistent with the configuration of the copied source.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1760e3c45be246cfa80d45b351d9618d~tplv-goo7wpa0wc-image.image) </span>


* If you choose to redirect to a dashboard, select the target dashboard below. This supports setting a redirect with filter conditions, meaning the dimension items in the current chart are used as input values for the public filter of the target dashboard. After clicking redirect, the public filter configured with the corresponding field in the target dashboard will automatically filter the chart field's value.

* If you choose to redirect to a web page, you can configure the redirect URL, and you can also use the field value`Field name`as a parameter in the URL redirect rule. As shown in the figure, clicking the column for "Shandong" will redirect to https://www.baidu.com/s?wd=Shandong, which means searching for "Shandong" in Baidu.


<span id="651efb2c"></span>
### "Redirect to" settings

<span id="3f8fbf9e"></span>
#### Redirect to dashboard

Target dashboard: The dashboard page to which the field redirects when clicked. Only dashboards under the current project can be selected. After selecting a dashboard, you can enable "redirect with filter conditions".

Redirect with filter conditions: Configure the matching relationship to use the dimension items in the chart as input values for the public filter of the target dashboard. After clicking redirect, the public filter configured with the corresponding field in the target dashboard will automatically filter the chart field's value. As shown in the configuration below, when you click the data for Shandong on the chart, the target dashboard's filter for "Province" will automatically be set to Shandong. Field multi\-language adaptation is supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7129c28728674f77985475c367fbbbad~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f98ddd8d035c4c2fb151923234feccf0~tplv-goo7wpa0wc-image.image) </span>

<span id="0c8b9749"></span>
#### Redirect to web page

Target web page: Set the URL of the target web page. You can insert parameters into the URL using the {field} format. When you click to redirect, the value of the "field" will automatically be substituted into the URL.

<span id="800ffdd2"></span>
### Open location settings

Multiple web page opening methods are supported for redirection:


* New window: The redirected page will open in a newly created window.

* Current window: The redirected page will open in the current page.

* Popup (centered): The redirected page will open as a centered popup on the current page.

* Popup (right side): The redirected page will open as a right\-side popup on the current page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/530d488068454ddd89f77bffe805cae0~tplv-goo7wpa0wc-image.image) </span>

<span id="500a2d5c"></span>
## Configure chart redirection with template links


1. On the visual query editing page, select the field to configure for redirection, then select **Parse text \- Template link.**  from the dropdown menu.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c42a3158a1748ef90d0bb55111e3e97~tplv-goo7wpa0wc-image.image) </span>

2. Enter the redirection URL in the popup window. You can insert parameters into the URL using the {field} format. When you click to redirect, the value of the "field" will automatically be substituted into the URL.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8aed16c60a354b2c987cd0c94ec36d94~tplv-goo7wpa0wc-image.image) </span>
