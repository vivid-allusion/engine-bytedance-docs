---
title: "User experience"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/User_experience"
---

For the analysis of issues regarding how application performance affects user experience, Application Performance Monitoring Full\-Link Edition provides two features: start analysis and page experience. In general, user experience issues during the application start process and the time required to access pages can have a critical impact on a company's revenue and reputation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* User experience has been integrated. For details, refer to [Application integration with Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) and [Application integration with iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* The user experience has been configured. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id=".5ZCv5Yqo5YiG5p6Q"></span>
## Start analysis

Start analysis monitors the time consumption for different start types. By using trend and distribution charts of start\-related metrics, you can understand the time consumption data during the application's start process.

<span id="2d55c4a2"></span>
### Filter conditions

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android system:

   Time, Device ID, User ID, Start type, System version, App version, App minor version, Device model, APM SDK version, Download channel, Custom dimension.

* Filter dimensions supported by iOS:

   Time, Device ID, User ID, Prewarm start, Start type, Jailbreak status, System version, App version, App minor version, Device model, APM SDK version, Download channel, Custom dimension.


<span id="1a9ededb"></span>
#### Start type


|Start type |Definition |Android calculation method |iOS data definition |
|---|---|---|---|
|**First launch** |The first cold start after app installation, including version upgrade, uninstall, and reinstall. |Activity's onResume() \- Application constructor |From process creation to the first UIViewController.didAppear method call |
|**Cold start** |The process of starting an app process from scratch |The Activity onResume() method – the Application constructor |From process creation to the first UIViewController.didAppear method call |
|**Warm start** |The process of re\-entering the App while its process is still alive (re\-entering after exiting with the back button) |onResume() of Activity minus onCreate() of Activity |Not applicable |
|**Warm start** |The process of triggering start again when the App process is alive (switching from background to foreground) |Activity.onResume() \- Activity.onRestart() |From willEnterForeground to didBecomeActive |


<span id="c3840568"></span>
#### iOS Prewarm

In systems running iOS 15 or later, there is a Prewarm policy that advances part of the application's start process, resulting in the platform overestimating the application's start time.

In this situation, the platform adopts the following approach: if Prewarm is triggered, the platform calibrates the measured start duration by ignoring a portion of the start time. As a result, the reported start duration will be slightly shorter than the actual time, and the reported start Trace may be missing the execToLoad or loadToDidFinishLaunching time segments.

If you wish to obtain a more accurate start time, please upgrade the SDK to version 2.11.1 or later, and perform the following actions:


1. Call `[RangersAPM prewarmCheckStart]` in the main method, and at the same time, in the `application:willFinishLaunchingWithOptions:` method, call `[RangersAPM prewarmCheckEnd]`.

   If your main method or the `application:willFinishLaunchingWithOptions:` method contains complex logic, this action is not recommended.

2. Initialize the SDK at the very beginning of `application:didFinishLaunchingWithOptions:`.

   If early initialization is not possible due to special reasons, please first call `[RangersAPM applicationDidFinishLaunching]`.


<span id="163c82de"></span>
### Start overview

<span id=".5ZCv5Yqo5oOF5Ya15qaC6KeI"></span>
#### Start time and number of starts

On the start time and count page, you can view trend charts of average start time and start count based on filter criteria.

<span id="13a04dee"></span>
#### **Start time distribution**

The start time distribution page allows you to view the distribution of start times under filter conditions.

<span id="f3987105"></span>
#### **Performance breakdown**

Trend charts for various metrics during the startup phase are provided in the performance breakdown to help identify the specific factors affecting startup duration.


|Monitoring side |DescriptionS |
|---|---|
|Android client |* init_time_avg: Time consumed by the Application.attachbaseContext() method<br><br>* build_avg: From the end of Application.attachbaseContext() to the end of Application.onCreate()<br><br>* load_avg: From the end of Application.onCreate() to the end of MainActivity.onResume() |
|iOS client |* from_exec_to_load: The stage from when the process begins with the exec function to when the specified +load is executed<br><br>* from_load_to_didFinishLaunching: The stage from the start of execution of the specified +load method to the start of execution of the didFinishLaunching function.<br><br>* from_didFinishLaunching_to_first_render_time: The period from the execution of the didFinishLaunching function to the completion of the first render (when CoreAnimation completes its first commit).<br><br>* from_vc_loadView_to_didAppear: The stage from FirstVC.loadView() to the completion of FirstVC.viewDidAppear() |


<span id="74e29bb8"></span>
#### **Quantiles**

Quantile values are obtained through statistical analysis of large datasets. Sort by start time to obtain quantile values, and view the proportion of records at that time point whose start time is the highest or lowest value.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Start time: Application's constructor</div>


* <div data-tips="true" data-tips-type="tip">End time: the execution point of the first onResume method</div>


* <div data-tips="true" data-tips-type="tip">Main Activity: The first Activity to execute the onResume method</div>


* The 99th, 95th, 75th, and 50th percentile values are close to each other; long start times are common.

* The 99th and 95th percentile values are close to each other, while the 75th and 50th percentile values are farther apart. Start times vary in length and are distributed relatively evenly.


<span id="c3629c84"></span>
#### **Node startup time**


* Enable initial load page: Supports switching the startup home page in the top right corner to accommodate scenarios with multiple startup home pages.

* Description of key nodes:

   
   |System |Node |DescriptionS |
   |---|---|---|
   |**Android** |totalTime |Total start duration. This is an activity whose onResume method is being executed for the first time. For more information, refer to [start type](https://docs.byteplus.com/en/docs/apmplus/User_experience#1a9ededb).<br><br>The start quantile on the homepage represents the total start time total time. |
   ||app_constructor |Application constructor time |
   ||app_attachBaseContext |Application attachBaseContext() method execution time |
   ||app_onCreate |Application onCreate() method execution time |
   ||initData |Duration of the initData phase when starting custom event tracking |
   ||activity_onCreate |Activity onCreate() method execution time |
   ||activity_onStart |The execution time of the Activity onStart() method |
   ||activity_onResume |Activity onResume() method execution time |
   ||activity_onRestart |The Activity onRestart() method execution time |
   |**iOS** |totalTime |Total start duration |
   ||from_exec_to_load |The stage from the invocation of the process start function exec to the stage where the specified +load is executed. |
   ||from_load_to_didFinishLaunching |The phase from the execution of the specified +load method to the execution of the didFinishLaunching function |
   ||from_didFinishLaunching_to_first_render_time |The phase from the execution of the didFinishLaunching function to the completion of the first rendering (the first commit by CoreAnimation) |
   ||from_vc_loadView_to_didAppear |The stage from FirstVC.loadView() to the completion of FirstVC.viewDidAppear() |
   

* Duration details: Click to view the metric trend chart and the quantile trend chart for this node.


<span id=".5byC5bi457uf6K6h5ZKM6L-96Liq"></span>
### Exception statistics and tracking

<span id="0137adc2"></span>
#### **Slow start analysis**

Slow start analysis displays slow start trends, slow start distribution, and slow start details. Among them, the slow start trend section displays trend charts for the proportion of slow starts, the number of slow starts, and the number of normal cold starts.

<span id="e7dcece8"></span>
#### **Slow start details**

<span id="0ab9b4d3"></span>
##### **Details**

The detailed information records all slow start metrics under this exception, as well as the detailed parameter values, recorded in detail, at the time when slow start occurred.

Indicator description:


|Metric |Android descriptions |iOS descriptions |
|---|---|---|
|Pre\-initialization duration |Not applicable on Android; set to 0. |From the process start function exec to the stage where the specified +load is executed |
|Initialization duration |The execution time of the Application.attachbaseContext() method |The period from the start of the execution of the specified +load method to the start of the execution of the didFinishLaunching function |
|Application build time |From the end of Application.attachbaseContext() to the end of Application.onCreate() |The phase from the start of the execution of the didFinishLaunching function to the completion of the first rendering (the first commit by CoreAnimation) |
|Page load time |From the end of Application.onCreate() to the end of MainActivity.onResume() |The stage from FirstVC.loadView() to the completion of FirstVC.viewDidAppear() |


<span id="e6f31388"></span>
##### **Slow start node duration**

The slow start node elapsed time display shows the elapsed time for each Task when this exception occurs.

<span id="cab5ffd4"></span>
#### Start crash statistics

Startup crash statistics are obtained by viewing crash trends, crash distribution, and crash lists to statistically analyze crash issues that occur during the startup phase. The start phase is defined as the period within 8 seconds after the application starts. Check the crash status of the module page and review the corresponding issue, then use stack traces and other information to perform root cause analysis.


* The crash trend displays the startup crash metrics and trend chart.

* Multidimensional analysis of crash distribution helps to understand the distribution of slow starts, making troubleshooting easier.

* The list of abnormal crashes records issues where a startup exception occurred.


<span id=".6aG16Z2i5L2T6aqM"></span>
## Native page experience

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Native page experience provides dashboard capabilities for three pages: page responsiveness; smoothness and dropped frames; and exception statistics and tracking.</div>


When analyzing page experience, evaluating page response time, stutter occurrences, and stutter\-related crashes helps to understand the overall application's page experience metrics and identify anomalies.

<span id="509c6284"></span>
### Filter conditions

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android system:

   Time, Device ID, User ID, page, system version, App version, App minor version number, device model, APM SDK version, download channel, custom dimension.

* Filter dimensions supported by the iOS system:

   Time, device ID, User ID, jailbreak status, page, system version, app version, app minor version, device model, APM SDK version, download channel, custom dimension.


<span id=".6aG16Z2i5ZON5bqU"></span>
### Page responses

Page response provides a list of metrics for each page.

Indicator descriptions:


|Metric |DescriptionS |
|---|---|
|Trigger count |Number of times this page is triggered under filter conditions |
|Failure percentage |Number of failed pages under filter conditions / number of page views under filter conditions<br><br><br>* For iOS, a page that has executed viewWillAppear: but not viewDidAppear: is considered a failure.<br><br>* For Android, the starting point is the page's onCreate event, and failure is defined as not reaching the end of onResume. |
|Availability percentage |1. Failure proportion |
|Crash rate |Number of page crashes under filter conditions / number of page opens under filter conditions |
|Smooth frame ratio |Number of page opens under filter conditions with load time less than the set threshold / number of page opens under filter conditions |
|The proportion of slow pages |Smoothness percentage |


Click the page name to enter the page details and view the page's load time and count, load time distribution, quantiles, and page load timing diagram.

<span id="bec4a509"></span>
#### **Page details**

On the page details screen, you can view the number of times the page has been loaded, the load duration, a load time distribution chart, and statistics on the number of user visits at each time point after the page goes live.

<span id="60156a46"></span>
##### **Loading times and load counts**

<span id="8e843239"></span>
##### **Load time distributions**

<span id="a2a20b63"></span>
##### **Quantile**

<span id="a9eae120"></span>
##### **Page loading sequence diagrams**

In the page load sequence diagram, you can identify the key Tasks that affect page load time. Once identified, they can be precisely optimized.

<span id=".5rWB55WF5oCn5ZKM5Lii5bin"></span>
### Smoothness and frame drops

Trend charts and distribution charts for FPS on both ends, as well as indicator lists for each page, are provided for fluency and frame drop metrics.

<span id="0cd16323"></span>
#### FPS quantile trend chart

The FPS percentile trend chart displays the distribution trends for the FPS 1%, 5%, 25%, 50%, 75%, 95%, and 99% percentile values, as well as the average value.

<span id="5515a8d9"></span>
#### Distribution of FPS smoothness

The FPS smoothness distribution chart displays the proportion of FPS_FAST, FPS_NORMAL, and FPS_BAD, as well as the growth rate of FPS_BAD.

Parameter descriptions:


* FPS_FAST (slight frame drop): 50 or above

* FPS_NORMAL (normal frame drop): 40–50

* FPS_BAD (severe frame loss): 0~40


<span id="55605528"></span>
#### Detailed information

The detailed information list displays page sample size, average FPS, frame drop attribution, frame drop score, and other information.


* Dropped frame attribution: Click to enter the details page. For example, if the attribution is lag, click to enter the lag trend.

* FPS details: Click to enter the FPS details page and view the FPS percentile trend chart, FPS smoothness distribution, sample size distribution, app version ranking, and device model ranking.

* Frame drop details: Click to enter the frame drop details page and view the severe frame drop rate, frame drop trend, frame drop distribution, and sample size distribution.


<span id=".5byC5bi457uf6K6h5ZKM6L-96Liq"></span>
### Exception statistics and tracking

Page exceptions provide data querying and exception attribution capabilities for three abnormal scenarios: slow page analysis, stutter page analysis, and crash page analysis. You can query the number and distribution of slow visits for pages in this module.


* Slow page analysis: slow page trend chart, slow page distribution, and slow page list

* Page lag analysis: lag trend, lag distribution, lag list

* Crash page analysis: crash trends, crash distribution, and abnormal crash list
