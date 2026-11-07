---
title: "iOS crash protection"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/iOS_crash_protection"
---

Crash protection provides protection against exception crashes, effectively prevents app termination for users, avoids large\-scale crashes caused by common issues, increases app stability, and improves user experience. The integration of exception protection is completely non\-intrusive to business code, effectively prevents issues, and reports issues to the platform to help you identify them in a timely manner.

<span id="5bd9574c"></span>
## crash protection configuration

<span id="69b8297e"></span>
### Crash protection submodule switch

The crash protection submodules include USEL, Container, Notification, KVO, KVC, and NSUserefaults. Correspondence between modules and values:


|**Submodule features** |**Value to be sent** |**Meaning** |
|---|---|---|
|USEL |1（1<<0） |The Unrecognized Selector protection.<br><br>Protect against crashes caused by calling unimplemented methods. |
|Container |2（1<<1） |Protection for containers<br><br>Common methods for safeguarding Foundation base types (NSString, NSMutableString, NSAttributedString, NSMutableAttributedString, NSArray, NSMutableArray, NSDictionary, NSMutableDictionary) can prevent crashes caused by improper parameter passing, such as array out\-of\-bounds, null parameters, and more. |
|Notification |4（1<<2） |Notification center protection. |
|KVO |8（1<<3） |The operating system provides a feature for monitoring changes in an object's properties, but there may be many hidden issues during use. KVO protection is designed to safeguard against problems of this type. |
|KVC |16（1<<4） |A method for obtaining and setting parameters at runtime; if the object being acted upon does not have the corresponding key during use, this will cause a crash. KVC protection is designed to safeguard against this type of issue. |
|NSUserefaults |32（1<<5） |Protect NSUserDefaults to prevent crashes caused by writing non\-standard types. |


Calculation formula for all feature values:

finalValue = issued value for turning on feature 1 + issued value for turning on feature 2 + ... + issued value for turning on feature 6

For example:


* Turn on all features: finalValue=63 (0b 0011 1111)

* Turn off all features: finalValue=0 (0b 0000 0000)

* Only turn off container protection: finalValue=61 (0b 0011 1101)


<span id="aa5b73df"></span>
### Rules for array protection logic

During data creation, if the passed\-in object contains nil, the operating system will crash. After crash protection is integrated, the operating system will not experience a crash; however, by default, the returned array is nil.


|**Modes** |**Platform fields** |**Default status** |
|---|---|---|
|Strict mode |Prioritize ensuring the correctness of array indices. When creating an array, if the input values contain null values, the created array will be empty.<br><br>```Java```<br>```NSString *strValue = nil;```<br>```NSArray *arr = @[strValue, @"str1"];```<br>```// The result of arr is nil```<br> |✔ |
|Compatibility mode |Give priority to ensuring successful array creation. When creating an array, if the input values contain empty values, remove the empty values and then create the array.<br><br>```Java```<br>```NSString *strValue = nil;```<br>```NSArray *arr = @[strValue, @"str1"];```<br>```// The result of arr is @[@"str1"]```<br> |✘ |


<span id="b74ecd8f"></span>
## crash protection

Statistical data in crash protection can help applications intercept exceptions, but subsequent handling and resolution of the issue are still required.

<span id="f3c1d5a8"></span>
### Prerequisites


* Crash protection has been integrated. Add **CrashProtector** module to Podfile. For details, refer to [iOS SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* The crash protection sampling rate, crash protection submodule switch, and array creation protection logic rules have been configured. For details, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration) and [crash protection configuration](https://docs.byteplus.com/en/docs/apmplus/iOS_crash_protection#5bd9574c).


<span id="e05a1841"></span>
### Filter criteria

You can filter data for the iOS operating system using the following filter criteria:

time, crash details, Device ID, User ID, issue new status, Foreground/Background State, jailbreak status, OS version, device model, app version, app minor version, APM SDK Version, download channel, province, usage duration, parsing status, app page, issue status, assignee, tag, custom dimension, PV custom dimension.

<span id=".5bSp5rqD5oum5oiq6LaL5Yq_"></span>
### Crash interception trend

The crash interception trend displays a trend chart of the crash interception metric based on the filter conditions. You can also display the trend chart by grouping dimensions. On the right side of the metric data, you can view changes in crash interception data compared to the previous period.

Metric description:


|**Metric** |**DescriptionS** |
|---|---|
|Intercepted crash count |Number of successfully intercepted crashes |
|Intercepted crash ratio |Number of intercepted crashes under filter conditions / total launch count under filter conditions |
|Number of users whose crashes were intercepted |Number of crash users intercepted for duplicates under filter conditions |
|Intercepted crash Impacted users rate |Number of deduplicated UVs with intercept crash error under filter conditions / total number of deduplicated UVs under filter conditions |
|user count |Deduplicated UV count of intercepted crashes under filter conditions |


<span id=".5bSp5rqD5oum5oiq5YiG5biD"></span>
### Crash interception distribution

The distribution of intercepted crashes is analyzed across multiple dimensions to understand the occurrence of exception\-related crashes and to help define problems.


* When you hover over the distribution chart, you can view the full name of the current category and its proportion within this metric type.

* By default, the distribution of intercepted crashes is displayed across four dimensions: **OS version**, **device model**, **APP version**, and **APP minor version number**. You can click the Settings button to select other dimensions, for example, APM SDK Version, Foreground/Background State, download channel, and more.

* By default, the distribution of errors is displayed based on **report volume**. You can also configure it to display the distribution of intercepted crashes based on **user volume**.


<span id=".5oum5oiq5byC5bi45bSp5rqD5YiX6KGo"></span>
### List of intercepted exception crashes

The intercepted exception crash list displays aggregated issue data for the same type of intercepted exception crashes, including number of impacted users, occurrence count, crash ratio, most recent occurrence time, log report time, status, and assignee.


* Note: Crash description: Click to go to **crash details** to view more crash information.

* Impacted user count: Click the icon after the number to preview the trend chart. Hover over the trend chart to view the corresponding time.

* Occurrence count: Click the icon after the number to preview the trend chart. Hover over the trend chart to view the corresponding time.

* Crash ratio: The number of crashes of this type intercepted as exceptions divided by the total number of launches.

* Latest occurrence time: The time of the most recent intercepted exception crash.

* Log report time: The time when the crash information about intercepted exceptions is reported to the server.

   For example, the interception of an exception crash occurs in version 1.0, but reporting takes place in version 1.2. To avoid information gaps, the list will report all context information from both the time the issue occurred and the time it was reported.

* Sorting: The list is sorted by impacted user count, occurrence count, and crash ratio in descending order by default. Click **latest occurrence time** or **log report time** to sort by time in descending or ascending order.

* Download: Click the download button in the upper right corner to download the first 100 records. The data in the list will be presented in `.xlsx` file format.

* Setting: Click the setting button in the upper right corner to customize the columns displayed in the list. In addition to the default column data, you can also configure the Year\-over\-Year occurrence count, Year\-over\-Year impacted user, Year\-over\-Year crash ratio, affected user rate, Year\-over\-Year affected user rate, and start and end versions.


<span id=".5bSp5rqD6K-m5oOF"></span>
### crash details

<span id=".aXNzdWXmpoLov7A="></span>
#### Issue overview

<span id="5e58b15e"></span>
#### Intercept crash trends

The details interception crash trend displays the changes in two metrics for this type of issue: crash count and impacted user count.

The details crash trend chart and the list crash trend are different; the differences are as follows:


* List of intercepted crash trends: All intercepted exception crashes within the time range.

   For example, with a time period of seven days and an aggregation granularity of one hour, you can view the hourly intercepted crash trend over seven days, with a total of 20 crashes.

* Details of intercepted crash trends: Aggregation of all intercepted exception crashes within the time range.

   For example, with a time period of seven days and an aggregation granularity of one hour, the crash list contains five crash items. This means that the system categorizes twenty crashes into five crash items. When you open one of the crash items, the details panel shows the crash trend for this type of crash over the seven\-day period.


<span id="9d966bb0"></span>
#### Details

Detailed information can be found by querying the field attributes of a single crash.


* Display a custom dimension: Click to display a custom dimension.

* Trace: Click **Trace** next to the device ID or User ID to navigate to log query to query the complete context log stream.

* You can switch to crash using the upper right corner.


<span id="babe615a"></span>
#### Raw stack trace & Retrace


* The raw stack trace display presents the stack trace information from the original log uploaded by the client.

* Retrace displays the stack trace after symbolication.

   * The stack trace of the operating system will be processed.

   * If the symbol table is not uploaded, the client stack trace will not be processed.

   * If the symbol table has already been uploaded but the client stack trace has not been processed, it is possible that the symbol table was not fully uploaded.

* If the symbol table or parsing is incorrect, you can re\-upload the symbol table, and then click **Retry Retrace** in the Retrace interface.

* Copying stack traces makes it easier to collaborate when analyzing stack trace information.


<span id="6785ac60"></span>
#### crash information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f496cf9b819642ebbcca528fdc333b1f~tplv-goo7wpa0wc-image.image) </span>

Parameter description:


|Key |Value |
|---|---|
|reason |Analyze the provided results based on the site conditions. |
|protect_type |The submodule containing the type for crash protection |


<span id="6499c7eb"></span>
#### symbol table

On the symbol table page, manually upload the symbol table.

<span id="ebe79dfa"></span>
#### on\-site data

The on\-site data shows the program running status when crash protection occurs.

<span id="c95b40b3"></span>
#### custom log

Custom log supports recovery and reporting of custom log content, including process\-thread information, log level, and log details, and also supports search and filter.
