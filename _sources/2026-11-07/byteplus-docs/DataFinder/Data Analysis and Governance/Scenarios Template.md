---
title: "Scenarios Template"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Scenarios_Template"
---

<span id="_1-介绍"></span>
# 1. Introduction

Scenario templates are a series of metrics, analysis methods, and Dashboard boards that ByteDance analysts preset in their growth analysis by industry and use case. Customers can choose templates on demand, understand the analysis ideas behind the templates, and generate Dashboard boards with one click through simple configuration. It can be used in multiple scenarios, such as tracking daily business metrics or analyzing specific business goals, lowering the threshold for analysis and enhancing the value of data analytics.

<span id="_2-使用入口"></span>
# 2. Use the entrance

Click on the **scene template** in the top navigation bar to enter the template list page.

The current template is classified according to **industry**. The template is displayed in the form of cover + card, including the template name and description.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66b66c1c017d4445bab3e98be3db3b2e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-场景介绍"></span>
# 3. Scene introduction

Click the **Introduction** button of any template cover image to view the detailed introduction of the template and the template overview diagram.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47af098db52e4913a3ffaf3c90ffe89d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/134af8a4754b49208dd6affa40f36aed~tplv-goo7wpa0wc-image.image) </span>

The purpose of the scenario introduction is to provide users with the business background, analysis ideas, and landing indicators of the scenario, so as to help users quickly understand the content of the scenario and determine whether it meets business requirements. The scene introduction usually includes:


* Business Scenario: Introduce the context of the scenario corresponding to the template and how the template supports the scenario.

* Analysis ideas: The template is a specific/complete analysis scenario, and the analysis logic is analyzed.

* Analysis target: The analysis target of the template.

* Analysis indicators: the name and caliber of the core indicators in the template.

* Optimization Suggestions: Abnormalities that can occur in core metrics, and the reasons behind them.


At the same time, you can also download the [event tracking plan] to learn about the industry and the events and attributes used by this template.

<span id="_4-模板使用"></span>
# 4. Template usage

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39eb0f1b873d4df6acc3065919dfa6aa~tplv-goo7wpa0wc-image.image) </span>

After understanding the scene template information, you can click the **Use Template** button to enter the template configuration page. In the configuration page, the left side is the template chart area, and the right side is the data configuration area.

Growth analysis automatically matches the events/properties used within the template with those in your application.


* If the event & property names are the same, it will automatically match and select your reported event. If they are inconsistent, the following reasons may occur:

   * Unable to find event or property with the same name.

   * Attribute with the same name, but inconsistent data types.

   * The event/property has been disabled.


In the above cases, you can:


1. Select events/properties that match the business scenario.

   
   |**Operation introduction** |**Schematic diagram** |
   |---|---|
   |You can configure events and properties on demand based on the behavior description or diagram name. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/759bef04161e45f7b1b250f9be1eef8e~tplv-goo7wpa0wc-image.image) </span> |
   |Once the configuration is complete, click the **Chart Preview** button to view the updated data. | |
   |Delete unwanted charts or drag and drop charts for layout. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f922a287671c461aa5b164eae702daa8~tplv-goo7wpa0wc-image.image) </span> |
   

2. Retain template events, metadata will be created when saved as a Dashboard board (you can manage the corresponding events/properties in Data Management).


<span id="_5-生成看板"></span>
# 5. Generate Dashboard

After the event configuration is complete, click the **Save as Dashboard** button, enter the Dashboard name and save location, and generate the Dashboard.

After generating Dashboard, it is consistent with the function of ordinary Dashboard. If you need to modify the chart, you can drill down to the analysis page to modify it.

<span id="_6-常见问题"></span>
# 6. Frequently Asked Questions

**6.1 How to automatically match templates using events and properties?** 

Growth analysis matches the event/property names used based on the template with custom event/property & preset property names that have been successfully reported in your application. If the match is not successful, the possible situation is as follows:

The event/attribute is not reported in your app.

2) Your property type does not match the data type used by the template; if the template uses int, you report the type as float.

3) Your attribute type does not match the attribute category used by the template; if the template uses an event attribute, the attribute with the same name you reported is a user attribute.

4) The event/attribute with the same name is a virtual event/attribute or disabled for special reasons.

**6.2 What if the template doesn't match the in\-app event?** 


* You can download the [event tracking scheme] and report the corresponding events and properties according to the event tracking scheme.

* You can select the template to use events/properties, generate Dashboard and create metadata, and then report the corresponding event/property data. After the report is successful, the Dashboard board will automatically read the data.

* You can select the reported event/property to replace the template event/property and save it as a Dashboard board.


**6.3 How to modify the Dashboard template created?** 

The template creates a Dashboard that is indistinguishable from other Dashboard boards. You can click on a single chart to drill down to the analysis page and configure the data modification.
