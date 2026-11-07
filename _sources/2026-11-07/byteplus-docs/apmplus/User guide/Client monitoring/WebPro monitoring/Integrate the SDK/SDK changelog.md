---
title: "SDK changelog"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SDK_changelog"
---

This document records the update history of the Monitoring SDK version for WebPro.

<span id="c3272a94"></span>
## 2.8.0


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2024\-07\-04 |Remove the default reporting of the performance metrics FID and MPFID |


<span id="be8d976f"></span>
## 2.2.0


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-06\-08 |Optimize sampling logic. When the user triggers total sampling, the monitoring instance is automatically destroyed. When the user triggers an individual monitoring sampling, the corresponding monitoring plugin is immediately destroyed. |


<span id="888e019c"></span>
## 2.1.1


|Change type |Release Month |Change |
|---|---|---|
|Add |2023\-05\-25 |A new storageExpires field has been added. You can configure the expiration time for storage through `client.init({storageExpires: boolean \| number})`. |


<span id="01556af5"></span>
## 2.1.0


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-05\-18 |Values stored in localstorage are encrypted as base64.<br><br><br>* Upgrade from the old version to the new version: fully compatible.<br><br>* Downgrading from the new version to the old version will cause UV and PV to be regenerated, which may result in temporarily elevated UV and PV values. |


<span id="7dc45d05"></span>
## 2.0.5


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-05\-09 |* When an event (pageview, http, js_error, and so on) interrupts the blank screen regression testing task, perform blank screen detection again at the end of the regression test.<br><br>* When html2canvas returns "data:,", set the image to a blank picture with dimensions 192 x 108 pixels.<br><br>* Use the context when an event occurs in the http, action, and performance plugins.<br><br>* If the FMP metric has not been settled when the second\-hop routing switch occurs, set isSupport to false, indicating that this metric is distorted due to the routing switch and is not included in the statistical scope.<br><br>* The userId returned by the server side is no longer used, and users do not need to be aware of this. |


<span id="8790c850"></span>
## 2.0.3


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-04\-12 |* If the TTI metric has not been settled when a second\-hop route switch occurs, it is marked as isSupport false, indicating that this metric is distorted due to the route switch and is not eligible for inclusion in the statistical scope.<br><br>* Rewrite the js error plugin by reusing the listening method, so that users do not need to be aware of it.<br><br>* Due to the `'script error'` error, it is not possible to obtain valid error type and stack trace information, so the business cannot follow up to locate the issue, and this error will no longer be reported.<br><br>* Due to static resource errors with `src= ''` that cannot be located or reproduced, this error will no longer be reported. |


<span id="b71ca941"></span>
## 2.0.1


|Change type |Release Month |Change |
|---|---|---|
|Optimize |2023\-03\-15 |Fix the potential issue in hash routing mode where the underlying use of history by the routing framework may result in missed PV reports. |


<span id="6929ff38"></span>
## 2.0.0


|Change type |Release Month |Change |
|---|---|---|
|Optimize |2023\-03\-15 |* Rewrote the xhr, fetch, resource, resource error, and other plugins by reusing listeners. This major upgrade updates the SDK architecture and introduces no breaking changes. |
|Add ||* The blank screen plugin now includes three new configuration options: mask, partialShot, and quality. For details on their specific uses, you can view the [configuration plugin](https://docs.byteplus.com/en/docs/apmplus/Plugin_configuration).<br><br>* The Action plugin allows you to specify the action name using the value of the data\-apm\-action attribute of the nearest element. Additionally, a new optional field, pure, has been added, which enables configuration of a pure action and allows reporting without waiting to associate. |


<span id="1.7.0（2022-12-14）"></span>
## 1.7.0


|Change types |Release Month |Change |
|---|---|---|
|Add new |2022\-12\-14 |* Added support for listener reuse, allowing different plugins to reuse listeners.<br><br>* The Performance plugin and PV plugin have been rewritten using the capability to reuse listeners. PV data is expected to remain unchanged, while some performance metrics, such as LCP, may experience an increase in reporting volume. |


<span id="1.6.0（2022-12-06）"></span>
## 1.6.0


|Change types |Release Month |Change |
|---|---|---|
|Add |2022\-12\-06 |Provide a standalone lightweight entry point, allowing users to package only the plugin capabilities they need. |


<span id="1.5.0（2022-11-29）"></span>
## 1.5.0


|Change type |Release Month |Change |
|---|---|---|
|Add |2022\-11\-29 |* The method for obtaining timing in xhr has been changed from xhr.responseURL to xhr's original request path. This change can fix the issue where timing cannot be obtained for some redirect services.<br><br>* Fix the issue where pages or components cannot be properly initialized when loaded dynamically. |


<span id="1.4.2（2022-11-02）"></span>
## 1.4.2


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2022\-11\-02 |Token validation has been added, allowing users to configure a token during initialization to prevent theft or misuse of the application's event quota. |


<span id="1.4.0（2022-08-05）"></span>
## 1.4.0


|Change types |Release Month |Change |
|---|---|---|
|Add |2022\-08\-05 |A transport field has been added to the initialization fields, allowing users to manually inject reporting capability. |


<span id="1.3.0（2022-07-30）"></span>
## 1.3.0


|Change type |Release Month |Change |
|---|---|---|
|Add new |2022\-07\-30 |The request monitor plugin adds a trace parameter to support collaboration with server\-side monitoring, enabling end\-to\-end traceability. |


<span id="1.2.4（2022-06-30）"></span>
## 1.2.4


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2022\-06\-30 |* The static resource error plugin adds the includeUrls configuration, allowing you to set a static resource error allowlist.<br><br>* The static resource error plugin adds a dedupe configuration, which is set to true by default. This means that duplicate static resource errors will only be reported once. |


<span id="1.2.0（2022-04-14）"></span>
## 1.2.0


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2022\-04\-14 |* The reporting protocol has been adjusted, and some public parameters are now consistently placed in the query.<br><br>* Remove the reporting of other URL parsing fields; parsing will now be performed by the server side. |


<span id="1.0.0（2022-03-14）"></span>
## 1.0.0


|Change types |Release Month |Change |
|---|---|---|
|Add |2022\-03\-14 |* request monitor<br><br>   * hook xhr<br><br>   * hook fetch<br><br>* PV monitoring<br><br>   * Spa routing<br><br>   * Manually report PV<br><br>* JavaScript error monitoring and static resource error monitoring<br><br>   * Manually report a JavaScript error<br><br>   * Automatically monitoring JavaScript errors and reporting them<br><br>   * Automatically monitor static resource error and report it<br><br>* Performance monitoring for static resources<br><br>* performance monitor<br><br>   * Automatic reporting includes performance metrics such as FP, FCP, FMP, TTI, FID, MPFID, LCP, CLS, and more.<br><br>   * Customize reporting of a single performance metric<br><br>   * Automatically report performance.timing and navigation Timing<br><br>   * Automatically report longtasks related to the first screen<br><br>* Reporting custom logs and custom events<br><br>* Sampling<br><br>* blank screen monitoring<br><br>* Supports listening to all lifecycle events of an instance. For details, refer to [Lifecycle](https://docs.byteplus.com/en/docs/apmplus/The_lifecycle).<br><br>* Support mounting methods on instances |
