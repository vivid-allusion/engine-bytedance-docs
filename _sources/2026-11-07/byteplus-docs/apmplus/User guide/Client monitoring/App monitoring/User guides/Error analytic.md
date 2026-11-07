---
title: "Error analytic"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Error_analytic_app"
---

The App Monitoring feature of Application Performance Management Plus provides an error analysis feature, supporting the collection and analysis of multiple error types across iOS and Android platforms to help you resolve issues more accurately.

Custom error provides analysis views from four dimensions and perspectives—error trend, error distribution, error list, and error details—making it easier for you to more comprehensively analyze different error types in your application.

<span id="e8fe157c"></span>
## Filter criteria

You can filter data using the following filter criteria.


* Filter criteria supported by Android:

   Time, error details, Device ID, User ID, exception type, issue new status, error type, Foreground/Background State, OS version, device model, app version, app minor version, APM SDK Version, download channel, ROM Information, province, usage duration, process name, manufacturer, parsing status, issue status, assignee, tag, custom dimension, PV custom dimension.

* Supported filter criteria for iOS:

   time, error details, Device ID, User ID, issue new status, error type, Foreground/Background State, jailbreak status, OS version, device model, APP version, APP minor version, APM SDK Version, download channel, province, usage duration, parsing status, APP page, issue status, assignee, tag, custom dimension, PV custom dimension.


<span id="5787242b"></span>
## Error trends

The error trend displays the metric trend chart for custom errors under filter conditions. You can also display the trend chart by grouping dimension(s). On the right side of the metric data, you can view changes in custom error data compared to the previous period.

Metric description:


|Metric |DescriptionS |
|---|---|
|Error counts |Error count under filter conditions |
|error rate |Number of errors under filter conditions / total number of launches under filter conditions |
|Number of people with errors |Deduplicated UV count with errors under filter conditions |
|error Impacted Users rate |Deduplicated UV count with errors under filter conditions / total deduplicated UV count under filter conditions |


<span id="125bf002"></span>
## Error distribution

Error distribution supports multidimensional analysis to help understand the distribution of errors and locate problems.


* Hovering over the distribution chart allows you to view the full name of the current category and its proportion within this metric type.

* By default, the distribution of errors is shown across four dimensions: **OS version**, **device model**, **APP version**, and **APP minor version number**. You can click the settings button to select other dimensions, such as error type, download channel, and more.

* By default, the distribution of errors is displayed according to **report volume**. You can also configure it to display the distribution of errors according to **user volume**.


<span id="acc7b4d3"></span>
## Error list

The error list displays the quantity of errors for a given network error code, the error rate, the number of impacted users, the impacted user rate, the year\-over\-year data for these metrics, and the start and end versions.

Click a specific aggregated error code to navigate to the error details, where you can view detailed information about this type of error.

<span id="f73f8a16"></span>
## Error details

On the error details page, you can view the field attributes for a specific type of aggregated error.

<span id="5b231e2b"></span>
### Error summary

The error summary displays the issue title, key stack trace information, latest report time, latest occurrence time, first occurrence time, error description, error count, number of affected users, error rate, and error user ratio. It also supports configuring custom tags for issues; for details, refer to [tag management](https://docs.byteplus.com/en/docs/apmplus/Platform_setting#.5qCH562-566h55CG).

<span id="d79af868"></span>
### Error trends

The error trend shows the changes in error count and impacted user count for this issue. Supports grouping by dimensions such as app version, app minor version, error type, and Foreground/Background State. You can view the trends in error count and impacted user for each grouping dimension.

<span id="56fa19d8"></span>
### Error distribution

Error distribution supports multidimensional analysis to understand how issues are distributed across different dimensions.


* By default, the distribution of errors is displayed across four dimensions: **OS version**, **device model**, **APP version**, and **APP minor version number**. You can click the settings button to select other dimensions, for example, error type, download channel, and more.

* By default, the error distribution is displayed based on **report volume**, but it can also be configured to display the error distribution based on **user volume**.


<span id="b43d4efd"></span>
### Detailed information

Within the detailed information, you can look up the specific field attributes of a single error.


* Trace: Click to go to the **log query** page. Query log details for DID and UserID where the log attribute is custom error.

* Switch error details: The error count for this issue is displayed in the upper right corner. Click to switch to the next error and view field details.


<span id="60662409"></span>
### Raw stack trace & Retrace

The display of stack trace information differs between Android and iOS:


* Android: If the symbol table is not uploaded, an obfuscated stack trace is displayed. After uploading and parsing the symbol table, the raw stack trace is displayed.

* iOS: If the symbol table is not uploaded, the raw stack trace is displayed, which is the stack trace information from the client's original log. If the symbol table has been uploaded, the displayed Retrace is the symbolicated stack trace.


Page description:


* Copy stack trace: After clicking, you can copy the stack trace information to another text editor, making it easier to search and find.

* Retry Retrace: If a symbol table parsing error occurs, click to reparse according to the symbol table.


<span id="abf3989b"></span>
### symbol table


* Upload: If the symbol table has not been uploaded, click to manually upload the symbol table.

* Re\-upload: If a symbol table has already been uploaded, click to manually re\-upload the symbol table.

* Download: If the symbol table has been uploaded, click to download the symbol table.


<span id="39f101f3"></span>
### on\-site data

On\-site data includes custom data present when an error occurs.
