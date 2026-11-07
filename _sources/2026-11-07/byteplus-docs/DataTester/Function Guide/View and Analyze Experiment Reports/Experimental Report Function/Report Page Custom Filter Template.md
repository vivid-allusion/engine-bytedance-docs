---
title: "Report Page Custom Filter Template"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Report-Page-Custom-Filter-Template"
---

<span id="303041a6"></span>
# Feature Overview

**Custom filter templates:**  Filtered component configurations can be saved to the template, which can be reused and shared. Avoid multiple configurations of the same filter latitude, and can coordinate and unify the results of experiments. Each experiment can only be configured with up to 10 custom templates.

**Application filtering template:**  The template rules configured by other experiments in the app are only convenient for users to call the template rules stored by others when configuring, and still take the current query route. Each app can only be configured with up to 50 custom templates.

<span id="3fc38e98"></span>
# Application scenario


* **Single experiment \- single dimension filter example:**  In a red envelope activity, push push a/b experiment was done, and the key channels were oppo and vivo. Every time you review and observe the indicators, you will click on the channels of oppo and vivo to filter.

* At this time, you can configure a filter template for a key channel, click the saved icon, and name the template. After each time you view the overall report, you can generate the report data under the filter latitude of oppo and vivo, which is convenient for reuse.

* **Single experiment \- multi\-dimensional combination example**: A coupon was distributed to do a visual a/b experiment, on the basis of this experiment, it is necessary to carry out a high\-version special project tracking analysis of a certain type of first\-tier users. Data analyst defines the analysis of special project experiments for first\-tier cities, above version 14, new users. Products and operations need to view and follow up the experimental data of this caliber.

* At this time, the analyst can configure a filter template for the special project, so that the filter conditions can be configured without repeated clicking, and the special project can be reused with the product and operation students in the module of a unified caliber.

* **Example of app\-filter template reuse:**  For example, in an e\-commerce product, a certain model or low version of the user needs to be filtered, and multiple experiments need to be filtered, but some experiments do not need to be filtered.

* At this time, low\-version and low\-model filter templates can be configured, configured in an experiment, and can be reused in the app_id.


<span id="c8e6a193"></span>
# Create a filter template

<span id="d7a107a8"></span>
## Operation entrance

**Entry:**  Experiment list page \- click on a certain experiment report page \- data metrics \- custom filter template.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34e574984a09437389a4d9c5d08e75ae~tplv-goo7wpa0wc-image.image) </span>


* **Experiment template:**  The administrator, creator, collaborator, and saved templates of the experiment belong to the custom template of the experiment. [The template can be customized and configured for the user, you can click Save to Experiment Custom Template after calling the app template]

* **Application template:**  You can call the filter template of other experimental configurations under the app, click to present the template rules, save to the custom template of the experiment, the app template does not contain the new custom template.


<span id="e2703692"></span>
## Save the new filter template


1. To configure the desired combination of filter dimensions, click **Save as Template**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7944adf07254d4dbcb613d58e066bd8~tplv-goo7wpa0wc-image.image) </span>

2. Configure the relevant parameters in the pop\-up custom template pop\-up window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f7f831aa9f947b7ab604b761c502dae~tplv-goo7wpa0wc-image.image) </span>

   * Template name: The template name can be defined and configured according to the business situation. For example, high\-paying users, key monitoring channels, etc.

   * Template description: note the relevant template content, play the role of prompts. (The word limit is limited to 50 characters.)

3. After configuring the above information, click **OK** to generate a custom filter template.


<span id="10a21b64"></span>
# Use filter templates

In the Experiment or Application tab, click the corresponding filter template to use the corresponding filter template directly.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ccc5cdbf35f413e8808c2f553b365d9~tplv-goo7wpa0wc-image.image) </span>


* Reuse experiment template: The customized template configured for this experiment can be clicked directly to reuse and fill to the filter dimension.

* Reuse application templates: Customized templates configured in other experiments can be reused in app templates to facilitate collaborative application of templates for multiple experiments.


<span id="d341645f"></span>
# View the list of filter templates


* View the list of created filter templates

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ff2561df7a24de1b9c9bdfb6ddaf83b~tplv-goo7wpa0wc-image.image) </span>

* Delete filter template

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acf441c53c0147d5a79ea057995b1e44~tplv-goo7wpa0wc-image.image) </span>
