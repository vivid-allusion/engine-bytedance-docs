---
title: "Viewing instance health overview"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/view-instance-health-overview"
---

This topic describes how to check the health status of a Cloud Search instance by viewing the health overview.

<span id="1a558b05"></span>
### Prerequisites


* Health diagnostics has been performed and diagnosis reports have been generated previously.

* Health diagnostics is performed automatically at a specified time (01:00 a.m. by default) or instantly by manual trigger. For more information, please see [Performing a diagnostic on an instance](https://docs.byteplus.com/docs/cloudsearch/32009).


<span id="69d61bff"></span>
### Procedure


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left\-side navigation bar of **Instance details** page, select **Intelligent operation**  **\> Health overview**.

5. On **Health overview** page, view the health status of the instance.

   * Latest instance diagnosis results: it displays the results of the latest diagnosis report including the number of high\-risk, low\-risk and safe items, as well as diagnosis time and diagnosis type (i.e. automatic or manual).

   * Trends of diagnosis results in the last 7 days: it displays the instance health status of the last 7 days in a line chart .

   * Health check item: it displays the number of items with high risk, low risk, no risk, and unchecked items in different tabs, as well as the diagnosis description and diagnosis result for each item.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/215964602f2541f48aa099b70b865302~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Intelligent O&M uses red, yellow, and green to indicate the health status of an instance.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Red</strong>: a severe issue or threat that may affect the usage of the instance exists which requires immediate processing. If you do not address this issue, data loss or instance crash may occur.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Yellow</strong>: a moderate issue or threat that may affect the usage of the instance exists and requires prompt processing.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Green</strong>: the instance is healthy.   </div>
