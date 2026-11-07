---
title: "SDK changelog"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SDK_changelog_minipro"
---

This document records the update log for the Mini Pro Monitoring SDK.

<span id="itK4Q69T"></span>
## 0.4.0（2025\-05\-22）


* Added full trace monitoring feature; HTTP requests can carry server\-side monitoring trace\-related request headers.


<span id="4c330ac4"></span>
## 0.2.4（2023\-05\-25）


* Fixed an issue where triggering navigateBack followed immediately by a native tab switch caused abnormal route and page switching performance, including page time on site.


<span id="80c4fd5b"></span>
## 0.2.3（2023\-05\-18）


* Fix the exception when calling navigateBack without passing a parameter


<span id="b70a4dbd"></span>
## 0.2.0（2023\-03\-01）


* Append the start_time field when collecting setData to ensure correct waterfall chart display in data explore.


<span id="0.1.0（2022-11-02）"></span>
## 0.1.0（2022\-11\-02）


* Add the token field as a required parameter during initialization

* Add Lark mini program adapter

* Adapt system info collection for desktop versions of WeChat Mini Program and Lark Mini Program

* When downloadFile succeeds in Alipay Mini Program, it does not return a status code; the default is set to 200.

* Append the collection of newly added queries to the current page URL


<span id="0.0.2（2022-09-08）"></span>
## 0.0.2（2022\-09\-08）


* Fix the issue where FrameworksAdapterIntegration cannot listen to HTTP in Alipay Mini Program build output under the Taro framework

* Fix the issue with the Breadcrumb plugin when http is not collected


<span id="0.0.1 (2022-09-01)"></span>
## 0.0.1 (2022\-09\-01)


* Support PV monitoring

   * View page time on site

   * Supports manual reporting of PV and manual settlement of page time on site

* Support Js Error monitoring

   * Automatic monitoring and reporting of Js Error and Navigate Error

   * Manual JavaScript error reporting

* Support HTTP monitoring

   * View request, downloadFile, and uploadFile

   * View callback time

* Support performance monitoring

   * Startup performance: View the performance timing chart from when your users click the mini program to when the first screen finishes loading

   * Pageload performance: View the performance timing chart for your users from when they switch pages to when the second page has finished loading

   * Individual performance metrics: view package download time, script injection time, FR, FP, FCP, and LCP

* Support SetData monitoring

   * View monitoring time consumed and data size

* Supports reporting custom logs and custom events

* All types support importance sampling.

* Supports multiple instances and listens to all lifecycle events; destroying an instance has no side effects.

* Adapt to third\-party frameworks:

   * Taro

   * Uni App

* Adapt four platforms:

   * WeChat Mini Program

   * TikTok Mini Program

   * Alipay Mini Program

   * Baidu Mini Program
