---
title: "JS monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JS_monitoring_minipro"
---

JS Monitoring displays error\-related information that occurs within the application, and allows filtering by mini program type, device, system, region, user, access information, error status, and other attributes. Through this feature, you can better understand and observe exceptions that occur at runtime and handle them effectively.

<span id=".SlPplJnor6_otovlir_lm74="></span>
## JS error trend chart

The JS error trend chart is displayed at the top of the page, showing trends for four metrics: number of errors, number of affected users, error rate, and affected user rate. Additionally, if you have recently specified new version information on the SDK, it will also appear in the trend chart. For numerical data or ratio data, you can click to select multiple specific indicators for observation, but you cannot select both numerical data and ratio data at the same time.

Each metric displays its fluctuation compared to the previous period. For example, if the chart above selects the most recent three days (from the 5th to the 8th), the error count shows the fluctuation relative to the previous three\-day period (from the 2nd to the 5th).


|**Metric** |**Calculation rules** |
|---|---|
|Number of JS errors |Total JS errors |
|Affected user count |The total number of unique visitors who encountered JavaScript errors |
|Error rate |Page views with JavaScript errors / total page views |
|User impact rate |Number of UVs with JS errors / total UVs |


<span id=".6ZSZ6K-v5Y-K6aG16Z2i5YiX6KGo"></span>
## Error and page list

The error list displays the specific error name, error stack, and error message for each Issue. In addition, the start and end times, error count, affected user count, and their trends are also displayed.


* By default, the error list is aggregated by error type and error stack.

* Support assigning the appropriate handler to the issue and updating the current status of the issue. The assignee can be selected from administrators or members of the current application.

* By selecting multiple JS errors, you can quickly modify the status of issues.


<span id=".SlPplJnor6_or6bmg4U="></span>
## JS error details

The error details page helps you further explore the cause of the Issue and the scope of its impact.

The top of the error details page displays a summary of the issue, including the error name, error message, error stack, error count, affected user count, issue owner, and issue status.

Click **Go to Data Exploration** to access detailed information on all reported events under the current error type and error message.

The error stack displays the specific stack trace. 'original' shows the stack trace after source mapping, while 'minified' shows the stack trace before source mapping (compressed). After completing the **sourcemap configuration**, you can obtain the de\-obfuscated original code stack trace, allowing you to identify the root cause of the error.

Upload the Source Map file corresponding to the current JS file name, select the correct version, and then click **confirm**. The platform will extract the context of the current code.

Click **Manage sourcemap** to navigate to the sourcemap management page for the corresponding version. In the minified stack, click the upload icon on the right side of the stack to upload the missing sourcemap.

The action history displays the issue's handling details and user comments.
