---
title: "Data explore"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/data_explore_minipro"
---

In the Mini Pro Monitoring module of Application Performance Management Plus, data exploration supports access to fine\-grained information on all reported events, helping you explore all data collected and reported by the application.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature overview


* Query all reported information for a specific user and a specific session in chronological order

* View all reported information for a specific type of event within a certain time period

* Thoroughly and accurately restore user visits through the multi\-level structure of `Session` \- `View` \- `Event`, resolving online issues.

* Investigate the specific resources, requests, setData, or user behaviors that affect mini program startup and loading, and perform targeted optimization.

* Trace the cause of page exceptions by using detailed context

* View distribution information of specific events across different dimensions


<span id=".55WM6Z2i6K-05piO"></span>
## Interface description


* Filter criteria vary for different types of filter items. After you click **filter condition** under a certain event type and configure it, your configuration will be saved. When you switch to another event type and then switch back, the previous filter condition will still be retained.

* The left side displays the distribution of each dimension and can also be used for filtering. You can freely select the dimensions you are interested in to be displayed by default.

* The main area on the right displays the various event types.

   * The top of the main area displays the reporting trend chart. You can select a subregion to further view the reporting status for the selected time period.

      * The top displays the specific event type of this event and supplementary information, such as occurrence time, region, device, user_id, session_id, env, release, and more.

      * By filtering events by specific type, you can search event keywords to filter events.

      * Click the event list to directly expand the secondary menu and further inspect lower\-level reports.

   * Below the main section is a table listing specific event reports in reverse chronological order. Each column displays selected reporting information for each event. Click **Custom columns** to select the reported information you are interested in for display. Drag a specific column to adjust its width. The table scrolls horizontally when its width exceeds the available space.

* The system provides the ability to export data, Currently, up to 5,000 records can be exported at one time. If the export limit is exceeded, adjust the filter range and export in batches; otherwise, the export will be truncated.


<span id=".5LqL5Lu26K-m5oOF"></span>
## Event details


* Each event contains all relevant reporting information.

* In the middle section of the event details for all events except Session events, hierarchical relationship information is displayed. This information indicates which Session and which View the current event originates from. Click a specific row to directly trace back from an individual report entry to its aggregated report information.

* By default, all events retain both the complete JSON report and the specific parsed report details.

* All events include context information.

* Reporting information is displayed, grouped by the default dimensions, that is, the reporting fields specific to this event. Click the content of a specific field. If the field is filterable, you can add to filter.

   * Dimensional data: supports inclusion and exclusion filtering. For example, city, device brand, and device model.

   * Metric data: Supports greater than and less than filtering. For example, page build time and page render time.


<span id="Session"></span>
### Session


* Aggregation of reports linked by session_id, including the View event, the request, the JavaScript error, and the startup performance metric.

* For Session events, each specific event is composed of a series of Views, along with errors and polling requests interspersed among them. Click the specific session to see a list of events reported in sequence. Caution: Not all of these events are necessarily the final reported events. For example, View is an aggregation of some `http`, `page_perf`, and `request` events.

* Click any part of the JSON page to copy its information to the clipboard.


<span id="View"></span>
### View


* A pageView event within a Session links together the related requests and page load performance, and also displays the associated reported metrics.

* A View event is essentially an instance of PageView. Each time a page visit occurs, APM assigns a global `view_id` to the current visit. Before any new access occurs, the page, startup performance metrics reporting, requests, JS exceptions, and setData information will all carry the global `view_id`. This method categorizes scattered individual reports under a single page visit, making it easier to clearly analyze the relationship between these reports and the loading performance and errors of a specific page.

* You can view details of timing metrics in formats such as waterfall charts. By switching tabs, you can also view information related to requests, JS exceptions, and other information for the corresponding View events.


<span id="JS Error"></span>
### JS Error


* Displays all JavaScript error reporting events, allowing you to view the specific stack trace and the context associated with each report.

* If you want to view statistical information, you can navigate to the error details page.


<span id="Http"></span>
### Http


* Request data reporting is supported, and you can view the request list sorted by time. Click a request to view the Timing information for that request.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Alipay Mini Program and the Lark Mini Program do not have Timing information.</div>


**Exception scenarios**


* Request status code in the list is \-1

   When a request fails and the status code for the current request cannot be obtained, set the status code to \-1.

* TCP Connection Time in Timing does not precede request time.

   The HTTP profile in mini programs draws on, but does not strictly adhere to, the [W3C Resource Timing](https://w3c.github.io/resource-timing/#dom-performanceresourcetiming) specification regarding response fields. As a result, some data may differ from what is displayed by xhr and fetch on the Web.


<span id="SetData"></span>
### SetData


* All data reporting related to setData


<span id="Custom Event"></span>
### Custom Event


* Report all custom events


<span id="Custom Log"></span>
### Custom Log


* All custom log reports
