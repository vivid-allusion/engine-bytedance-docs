---
title: "Feature key Usage Monitoring"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Feature-key-Usage-Monitoring"
---

<span id="一-概述"></span>
# 1. Overview

The usage monitoring of feature keys mainly refers to the monitoring of the usage of each variant of the feature during the entire life cycle of the feature.

At the same time, you can visually view important changes in the Feature life cycle: such as opening A/B experiments and releasing new versions, which can help product and R&D personnel more intuitively understand the user usage of each variant of the Feature and important changes in the whole life cycle, so as to more accurately judge the function usage trend, locate abnormal problems, etc.

**Prerequisites:**  To view the monitoring details of Feature key usage, you need to upgrade to the corresponding SDK version. As follows:


* iOS SDK：5.6.3\-rc.3

* Android SDK：5.5.0\-rc.5

* Web/H5/WAP SDK：4.1.15

* WeChat Mini Program SDK: 1.3.14

* Server side SDK: Please upgrade the server side SDK to 2.0.0 version (you can contact Business to get the latest SDK version package).


<span id="二-名词解释"></span>
# 2. Term explanation


* **Variants:**  The different values of a feature are called variants.


(For example, if the login methods include QQ login and WeChat login, Feature is the login method, which has two variants: QQ login and WeChat login)


* **Feature Version:**  A new version is generated for each iteration of the Feature about "Variant Value, Release Audience" changes.

* **Feature Usage:**  The number of times the Feature's variant (key and value) is actually used in the business (i.e. the amount of PV).

* **Last Used Time:**  The date the variant was last used (time granularity is in days).

* **Recent Uses:**  The number of times the variant was used on the date it was last used.

* **Variant Trend Chart:**  Show usage trends for each variant.

* **Variant Proportion Chart:**  Show the usage ratio of each variant.

* **Variant Usage Details:**  Shows the most recently used date and number of uses for each variant.


<span id="三-应用场景"></span>
# 3. Application scenario


* **New feature release:**  During the Feature release process, get the online usage of each variant of the Feature in time, judge whether it meets expectations, detect usage, and roll back in time if there is a problem.

* **Clean up invalid code:**  Long\-term function iteration generates a lot of redundant code in the code, such as long\-term unused/expired features. We can quickly determine which feature variants have been unused for a long time based on feature usage, which is easy to clear invalid code.

* **Assist in locating abnormal problems:**  After the function is released, if there is an abnormal problem, it can be combined with the monitoring data of the problematic time period & key changes to help business students quickly locate the problem.


<span id="四-如何使用"></span>
# 4. How to use

<span id="_1-功能入口"></span>
## 1. Function entry

On the Feature list page, you can click "Monitor" to enter the usage monitoring page of the Feature key, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/611c7daf59754a089dd69c66e0aab3b8~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-变体使用趋势-使用量占比"></span>
## 2. Variant usage trends & usage share

After entering the usage monitoring page, you can view the usage trend graph and usage percentage of each variant of the Feature.


* Support viewing: last use time, last modification time.

* Time Filter: Support to view the trend of the corresponding time by the most recent number of days or a custom time range.

   * The time range supports querying time intervals of up to 60 days.

   * After selecting a query time, the trend graph and usage percentage below will show the data during the query time.

* The number of variants in use, the 7 most used variants are displayed by default, and to view more variants, click the corresponding legend.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34ae3566eb494ae7bd9bc4a7c9a50300~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3c69023e6f34bb29219e6cc71866720~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-如何查看feature的重点变更"></span>
## 3. How to view Feature core changes

Feature core changes, such as conducting A/B experiments, releasing new versions, and modifying features, and the corresponding data points will be highlighted in the trend chart.


* Hover the amount of variant usage on a given day to see the variant usage and major changes for that day.

* If you have started an A/B experiment and released a new version of the Feature, you can click the corresponding experiment and Feature version link to view the specific situation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68a403f1f63841bd9ba7eb56190ea27e~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-所有变体使用详情"></span>
## 4. All variant usage details

At the bottom right of the usage monitoring page, the usage details of all variants of the Feature are displayed, including: variant, variant value, last usage time, and last usage. As follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6b70eb09e4848cc998df058fbee63ce~tplv-goo7wpa0wc-image.image) </span>
