---
title: "Migrate from the old version"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Migrate_from_the_old_version"
---

This document records the update history of the Monitoring SDK version for the WebPro side.

<span id="c3272a94"></span>
## 2.8.0


|Change type |Release Month |Change |
|---|---|---|
|Optimize |2024\-07\-04 |Remove default reporting of the performance metrics FID and MPFID |


<span id="be8d976f"></span>
## 2.2.0


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-06\-08 |Optimize the sampling logic When a user hits total sampling, the monitoring instance is automatically destroyed. When an individual monitoring sample is hit, the corresponding monitoring plugin is immediately destroyed. |


<span id="888e019c"></span>
## 2.1.1


|Change types |Release Month |Change |
|---|---|---|
|Add |2023\-05\-25 |The storageExpires field has been added; the expiration time of storage can be configured via `client.init({storageExpires: boolean \| number})`. |


<span id="01556af5"></span>
## 2.1.0


|Change type |Release Month |Change |
|---|---|---|
|Optimize |2023\-05\-18 |Values stored in localStorage are encoded in base64.<br><br><br>* Upgrade from the old version to the new version: fully compatible.<br><br>* Downgrade from the new version to the old version: UV and PV will be regenerated, which may result in temporarily elevated UV and PV values. |


<span id="7dc45d05"></span>
## 2.0.5


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-05\-09 |* When an event (pageview, http, js_error, and so on) interrupts the blank screen retest task, perform blank screen detection again at the end of the retest.<br><br>* When html2canvas returns data:, set it to a blank image of 192 x 108 pixels.<br><br>* Use the context when an event occurs in the http, action, and performance plugins.<br><br>* If the FMP metric has not been finalized when a second\-hop route switch occurs, set isSupport to false. This indicates that the metric is distorted due to the route switch and should not be included in statistical analysis.<br><br>* The userId returned by the server side is no longer used, and users do not need to be aware of this. |


<span id="8790c850"></span>
## 2.0.3


|Change type |Release Month |Change |
|---|---|---|
|Optimize |2023\-04\-12 |* If the TTI metric has not been completed when a second\-hop route switch occurs, it is marked as isSupport false, indicating that this metric is distorted by the route switch and is not supported for inclusion in the statistical scope.<br><br>* The JS error plugin is rewritten by reusing the listener method, with none of the changes visible to users.<br><br>* Due to `'script error'`, it is not possible to obtain valid error type and stack trace information, so the business cannot follow up or locate the issue, and this error will no longer be reported.<br><br>* Due to the inability to locate and reproduce the `src= ''` static resource error, this error will no longer be reported. |


<span id="b71ca941"></span>
## 2.0.1


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-03\-15 |Fix the issue in hash routing mode where missed PV reports may occur because the underlying routing framework uses history. |


<span id="6929ff38"></span>
## 2.0.0


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2023\-03\-15 |* Rewrote plugins such as xhr, fetch, resource, and resource error by reusing the listening method. This major upgrade is an SDK architecture upgrade, with no breaking changes. |
|Add ||* The blank screen plugin now includes three new configuration options: mask, partialShot, and quality. For details on their usage, view [the plugin configuration](https://docs.byteplus.com/en/docs/apmplus/Plugin_configuration).<br><br>* The Action plugin allows you to specify the action name using the value of the nearest element's data\-apm\-action attribute. Additionally, a new optional field, pure, has been added, which enables configuration of a pure action that can be reported without waiting to associate. |


<span id="1.7.0（2022-12-14）"></span>
## 1.7.0


|Change types |Release Month |Change |
|---|---|---|
|Add |2022\-12\-14 |* Added the capability to reuse listeners, allowing different plugins to reuse listeners.<br><br>* The Performance plugin and PV plugin have been rewritten using the capability for multiplexed listening. PV data is expected to remain unchanged, while some performance metrics, such as LCP, may experience an increase in reporting volume. |


<span id="1.6.0（2022-12-06）"></span>
## 1.6.0


|Change type |Release Month |Change |
|---|---|---|
|Add |2022\-12\-06 |Provide a separate lightweight entry point, allowing users to package only the plugin capabilities they need. |


<span id="1.5.0（2022-11-29）"></span>
## 1.5.0


|Change types |Release Month |Change |
|---|---|---|
|Add new |2022\-11\-29 |* The method for obtaining timing from xhr has been changed from using xhr.responseURL to using the original request path of xhr, which can fix the issue where timing cannot be obtained in some redirect service scenarios.<br><br>* Fixed the issue where pages or components failed to initialize correctly when loaded dynamically. |


<span id="1.4.2（2022-11-02）"></span>
## 1.4.2


|Change types |Release Month |Change |
|---|---|---|
|Optimize |2022\-11\-02 |Token validation has been introduced. Users can configure a token during initialization to prevent unauthorized use of application event volume. |


<span id="1.4.0（2022-08-05）"></span>
## 1.4.0


|Change type |Release Month |Change |
|---|---|---|
|Add |2022\-08\-05 |A transport field has been added to the initialization parameters, allowing users to manually inject reporting capabilities. |


<span id="1.3.0（2022-07-30）"></span>
## 1.3.0


|Change type |Release Month |Change |
|---|---|---|
|Add |2022\-07\-30 |Request to add a trace parameter to the monitoring plugin to support integration with server\-side monitoring and enable end\-to\-end traceability. |


<span id="1.2.4（2022-06-30）"></span>
## 1.2.4


|Change type |Release Month |Change |
|---|---|---|
|Optimize |2022\-06\-30 |* The static resource error plugin adds the includeUrls configuration, allowing the setting of a static resource error allowlist.<br><br>* The static resource error plugin adds a dedupe configuration, which is set to true by default. This means that duplicate static resource errors are reported only once. |


<span id="1.2.0（2022-04-14）"></span>
## 1.2.0


|Change type |Release Month |Change |
|---|---|---|
|Optimize |2022\-04\-14 |* Reporting protocol adjustment: some public parameters are now consistently included in the query.<br><br>* Remove reporting of other parsed URL fields and change to parsing by the server side. |


<span id="1.0.0（2022-03-14）"></span>
## 1.0.0


|Change type |Release Month |Change |
|---|---|---|
|Add |2022\-03\-14 |* request monitor<br><br>   * hook xhr<br><br>   * hook fetch<br><br>* PV monitoring<br><br>   * SPA routing<br><br>   * Manually report PVs<br><br>* JavaScript error monitoring && static resource error monitoring<br><br>   * Manually report JavaScript error<br><br>   * Automatically monitor and report JavaScript errors<br><br>   * Automatically monitor static resource errors and report<br><br>* Static resource performance monitoring<br><br>* performance monitor<br><br>   * Automatic reporting includes FP, FCP, FMP, TTI, FID, MPFID, LCP, CLS, and other performance metrics.<br><br>   * Custom reporting of a single performance metric<br><br>   * Automatically report performance.timing and Navigation Timing<br><br>   * Automatically report first screen\-related longtasks<br><br>* Reporting of custom logs and custom events<br><br>* Sampling<br><br>* blank screen monitoring<br><br>* Supports monitoring of all instance lifecycles. For details, refer to [Lifecycle](https://docs.byteplus.com/en/docs/apmplus/The_lifecycle).<br><br>* Support mounting methods on instances |
