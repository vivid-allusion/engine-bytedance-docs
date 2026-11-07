---
title: "HTML5 monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/HTML5_monitoring"
---

By using the JS Bridge method to inject the JavaScript monitor SDK into the App monitoring SDK, once the App monitoring SDK is integrated, you can directly monitor front\-end metrics on H5 pages within the app, such as JavaScript error, Ajax request, page load time, and more.

<span id=".5Yqf6IO96K-05piO"></span>
## Feature description

The main capabilities of page monitoring include: page list, JavaScript error, request error, request monitor, and page loading. The use of specific features is consistent with monitoring on the web side. For more information, see the description in Web Monitoring.

<span id="c7fb0f06"></span>
## page list

The page list provides a leaderboard of key metrics for each H5 page.

<span id="5ba0e9e8"></span>
## JavaScript error

JavaScript errors can be counted, and the problems they cause can be located.

<span id="43342aa7"></span>
## Request error

For Ajax request statistics, errors can be identified and analyzed to determine their scope and causes.

<span id="f06cdb4e"></span>
## request monitor

The request monitor aggregates all Ajax requests and provides overall metric statistics, enabling analysis of request success rate, request time, and more.

<span id="79ddfe4d"></span>
## Page load

Page loading provides various RUM metrics during the page loading process, as well as technical metrics in navigation, to help frontend developers understand the actual user experience during page loading and the specific factors that affect load time.


* Real user performance metrics

   * Page rendering metrics: First Paint, First Contentful Paint, and First Meaningful Paint.

   * User interaction metrics: first interaction time, maximum interaction latency, and Time to Interactive.

   * Overall satisfaction metrics: first load bounce rate, slow launch ratio.

* Page technical performance metrics

   * Show time consumption, sample size trend chart, and time consumption distribution for each stage.

* Lazy loading list

   * Display the results after aggregating slow\-loading pages by Host and Path

* Multidimensional analysis

   * Display multiple metrics: version number, network type, device model, and regional distribution


<span id="c4f8444b"></span>
## References

A SourceMap is a file that stores information mapping the positions between source code and compiled code. It allows you to restore compressed, obfuscated, or merged output code back to its original source code, helping you accurately locate the line and column where an issue occurs in a production environment. For details, refer to [SourceMap management](https://docs.byteplus.com/en/docs/apmplus/File_management#6232e17e).
