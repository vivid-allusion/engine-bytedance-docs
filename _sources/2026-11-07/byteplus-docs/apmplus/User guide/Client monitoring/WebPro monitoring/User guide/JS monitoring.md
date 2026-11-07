---
title: "JS monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JS_monitoring"
---

JS Monitoring displays information related to errors that occurred in your application. Filtering can also be performed by attributes such as browser, device, system, region, user, access information, and error status. With this feature, you can better understand and monitor exceptions that occur at runtime and handle them effectively.

<span id=".SlPplJnor6_otovlir_lm74="></span>
## Js error trends


* The top of the page displays a JS error trend chart, which provides trends for four metrics: error count, affected user count, error rate, and affected user rate.

* Each metric displays its fluctuation compared to the previous period. For example, as shown above, if you select the most recent three days (from the 11th to the 14th), the error count decreased by 52.8% compared to the previous period (from the 8th to the 11th).

* If you have recently specified new version information for the SDK, it will also appear in the trend chart.

* For numerical data or ratio data, you can select multiple indicators for observation by clicking them, but you cannot select numerical data and ratio data at the same time.



|Metric |DescriptionS |
|---|---|
|Error count |Number of JavaScript errors in the current time range |
|Impact on the number of users |Number of unique visitors who encountered JS errors in the current time range |
|Error rate |Page views with JS errors / total page views |
|Impact on user adoption rate |Unique visitors with JS errors / unique visitors |


<span id=".SlPplJnor6_liJfooag="></span>
## List of JS errors

The lower section of the page displays a list of JavaScript errors, which is aggregated by default based on error type and error stack. You can also switch to view the error status for each PID of the current site or to a list aggregated by error message.


* **Project settings** menu JS error aggregation is, by default, based on error type and error stack. At this time, the JS error list is displayed according to this aggregation method, and the error message list is displayed in an aggregated manner by error message.

* If you select to aggregate by error message, both the JS error list and the error message list are displayed aggregated by error message.

* In the table, for each Issue in the error list, the specific error name, error stack, and error message are displayed. In addition, the start and end times, error count, number of affected users, and their trends are displayed.

* On the far right, you can assign a handler to the Issue and change the current Issue status. The assignee can be selected from among the administrators or members of the current application.


<span id=".SlPplJnor6_or6bmg4U="></span>
## JS error details


* The error details page helps you further explore the cause of the Issue and the scope of its impact.

* The top of the page displays a summary of the current Issue, including the error name, error message, and the stack trace where the error occurred. Number of errors and number of affected users. Below is the current error status and handler information.

* The right side displays the start and end information for current errors, the trends of each metric, and the distribution across versions and pages.

* Navigating to Data Exploration allows you to access detailed information on all reported events under the current error type and error message. For more information, see [Data Exploration](https://docs.byteplus.com/en/docs/apmplus/data_explore).

* The main content of the page is the detailed information about the error. The left side of the main area displays the specific page stack, while original displays the page stack after reverse parsing. "minified" refers to the page stack information in its compressed state before de\-obfuscation. After completing [sourcemap configuration](https://docs.byteplus.com/en/docs/apmplus/SourceMap_upload_and_reverse_mapping), you can obtain the source\-mapped stack trace. Thus, the original cause of the error can be pinpointed.

* At the top left of the stack, the dropdown allows you to switch between versions and observe changes in the error stack for different versions. Click the **sourcemap management** button to the left of the dropdown to navigate to the sourcemap management page for the selected version. In the minified stack, click the upload icon on the right side of the stack to upload missing sourcemaps.

* Below the change history is the Actions section. Information about assignees manually set by users, as well as user comments on this Issue, will appear here.

* The white screen list displays the URL, DOM score, screenshot, PID, and the reporting time associated with each white screen occurrence. Click **Go to Data Exploration** to view detailed reported data.
