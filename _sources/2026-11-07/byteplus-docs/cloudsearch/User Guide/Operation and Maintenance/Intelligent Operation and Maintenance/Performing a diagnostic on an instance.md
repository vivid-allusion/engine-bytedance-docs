---
title: "Performing a diagnostic on an instance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/perform-diagnostics"
---

After Intelligent O&M feature is enabled, instance diagnostics is performed automatically on a daily basis (01:00 a.m. by default), and diagnostic reports are generated afterwards. In addition to automatic diagnostics, manual diagnostics can also be performed up to five times a day.

This topic describes how to perform manual diagnostics.

<span id="6f7ca569"></span>
### Prerequisites

Intelligent O&M feature is enabled. For more information, please see [Enabling Intelligent O&M feature](https://docs.byteplus.com/docs/undefined/66fa07043c09f003283d69f0).

<span id="0654af25"></span>
### Procedure


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left\-side navigation bar of **Instance details** page, select **Intelligent operation**  **\>**  **Diagnosis report**.

5. On the top of **Diagnosis report** page, configure **Diagnosis Index** and **Diagnosis Items**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c629d589d39347d9b19b309e5716fa1b~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Diagnosis Index |Enter the desired index to apply diagnostics<br><br><br>* Different indices should be separated by a comma (`,`).<br><br>* A wildcard can be used to match multiple indices. |
   |Diagnosis Items |Specify diagnosis dimensions from the dropdown list. |
   

6. After configuration is complete, click **Diagnose now**.


After the diagnosis is complete, the latest diagnosis report is displayed in the central area of **Diagnosis report** page.

You can check report for the latest status of the instance by diagnostic item descriptions, diagnostic results and suggestions.
