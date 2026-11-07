---
title: "JS error"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JS_error"
---

JS error provides JavaScript error monitoring and analysis capabilities, and also supports reporting custom errors. Overall, it is divided into an overview of dashboard metrics and an analysis of issue details.

JS error capturing logic: Capture global errors using window.addEventListener('error').

<span id=".SlPplJnor6_otovlir8="></span>
## JavaScript error trends

JavaScript error trend provides four metrics: error count, error rate, number of impacted users, and impacted users rate.

Below the trend chart, the issue list aggregated by message is displayed. The error type, start and end time, error count, and number of affected users for the issue are displayed simultaneously. You can assign someone to this issue and modify its status.

<span id=".SlPplJnor6_liJfooag="></span>
## JavaScript error list

The Actions bar allows selection of the handling status of issues, facilitating tracking and batch management.

<span id=".SlPplJnor6_or6bmg4U="></span>
## JavaScript error details

On the issue details page, you can view summary information for the issue and analyze error metrics by dimension.

The center of the page displays the detailed distribution and reporting trends of this error type across various dimensions.

If you find that, in one dimension, a single value is significantly higher than the values in other dimensions, you may have successfully pinpointed the key factor causing the error. For example, a certain error is concentrated on pages that start with /page.

By observing error trends, you can infer the time period when errors occurred and recall whether a certain change operation may have caused the issue, providing additional clues.

You can also query the user's device information, version information, and many other details for each error event in this issue. Click the UUID or session ID to navigate to single point tracing, where you can view detailed logs for the user or the individual session. Additionally:


* Error stack trace: The obfuscated stack trace where the error occurred; if the symbol table is uploaded, you can view the raw stack trace.

* Breadcrumbs: Records of user actions before and after an error, including request types automatically collected by the system as well as custom interaction event types tracked via user\-defined tracking points.

* Custom dimension: In addition to dimensions automatically collected by the system, reporting of custom dimensions is supported.


You can also post a comment on this issue.

<span id=".57u05bqm"></span>
## Subnamespace

The following are dimensions automatically collected by the system:


* Platforms currently covered by monitoring: WeChat Mini Program, ByteDance Mini Program, and Alipay Mini Program

* Country/region: The country or region where the user is located when an error occurs while locating the user by IP.

* Operating system version number: The model and version number of the operating system

* Platform app version: APP version number

* Page (PID): the page where an error occurred

* network type: 4G, WiFi, 3G, and more

* Custom error type for issue

* Device model: The device that reports information

* Mini Program SDK version

* Show only errors with a stack trace: Some reported JavaScript error events may not include a stack trace. You can select whether to view only errors with a stack trace.

* Custom dimension: a dimension independently reported by users


It also supports manual error capture and reporting.

<span id=".5omL5Yqo5o2V6I636ZSZ6K-v5bm25LiK5oql"></span>
## Manually capture and report errors

For certain expected errors, or asynchronous errors returned through promise rejection and similar mechanisms, it may not be possible or convenient to obtain these errors using global capture methods. In such cases, you can manually capture and report these errors.

```Plain Text
Rangers.capture(new Error('manually captured')) // Manual capture
```


<span id=".56ym5Y-36KGo77yIU291cmNlbWFw77yJ"></span>
## Symbol table (Sourcemap)

The symbol table for frontend monitoring supports manual and automatic upload. For details, refer to the description in "Sourcemap management".
