---
title: "Data explore"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/data_explore"
---

Data explore can help you explore all data collected and reported by your application. On the data explore page, you can access detailed information about all report time.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature overview


* Query all reported information for a specific user and a specific session in chronological order

* View all reported information for a specific event type within a given time period

* By leveraging the multi\-level structure of `Session` \- `View` \- `Action` \- `Event`, user visits can be deeply and accurately reconstructed to resolve online issues.

* Investigate the specific resources, requests, `longTask`, or user behaviors that affect page loading, and optimize in a targeted manner.

* Trace the cause of page exceptions through detailed context.

* View distribution information of specific events across different dimensions


<span id=".55WM6Z2i6K-05piO"></span>
## Interface description


* General filters are located at the top of the page, and the filter options vary depending on the type. After you click **filter conditions** under a specific event type and configure them, the configuration will be saved. When you switch to another event type and then switch back, the previous filter configuration is retained.

* The left side of the page displays the distribution of each dimension and can also be used for filtering. You can freely select the dimensions you are interested in to be displayed by default.

* The topics on the right display various event types.

   * The top displays the reporting trend chart. You can select a subregion to further view the reporting status for the selected time period.

      * The top displays the specific event type and some related information, such as occurrence time, region, device, user_id, session_id, env, release, and so on.

      * By filtering specific event types, you can search for event keywords to filter events.

      * Click the event list to directly expand a secondary menu and further inspect deeper\-level reports.

   * Below is a table listing specific event reports in chronological order from the present to the past. Each column in the table displays partial reporting information for the current event. Click **Custom Columns** to freely select the reporting information you want to display. Drag a specific column to adjust its width. The table will scroll horizontally if it exceeds the available width.


<span id=".5LqL5Lu26K-m5oOF"></span>
## Event details


* Each event includes all relevant reporting information.

* In the middle section of all event details except those for Session events, hierarchical relationship information appears. This information indicates which Session and which View the current event originates from. Click a specific row to directly trace back from an individual report entry to its aggregated report information.

* By default, all events retain both their complete JSON report and the parsed report content.

* All events include context information.

* Reporting information will be displayed, grouped by the default dimensions—that is, by the reporting fields specific to the event. If you click a specific field that is filterable, you can add it to the filter.

   * Dimension data supports both inclusion and exclusion filtering. For example, city, device brand, and device model.

   * Metric data: Supports greater than and less than filtering. For example, page build time and page render time.


<span id="Session"></span>
### Session


* Aggregation of reports linked by session_id, which includes View events, requests, JavaScript errors, and page load performance metrics.

* For Session events, each specific event consists of a series of Views, along with errors and polling requests interspersed among them. Click a specific Session, and you will see the list of events reported in chronological order.

   These events are not necessarily all final reported events. For example, View is an aggregation of some `http`, `page_perf`, and `request` events.

* Click any part of the JSON page to copy it to the clipboard.


<span id="View"></span>
### View


* A pageView event within a session connects the requests and page load performance related to the event, and displays the relevant reported metrics.

* A View event is essentially a PageView. Each time a page is accessed, APM assigns a global `view_id` to the current visit. Before any new visit occurs, page load performance metric reporting, requests, JS exceptions, static resources, and longtask information will all carry the global `view_id`. This method groups scattered individual reports into a single page visit, enabling clearer analysis of the relationship between these reports and the loading performance and errors of a specific page.

* You can view the details of timing metrics in formats such as waterfall charts. By switching tabs, you can also view information such as the requests, JS exceptions, and other information associated with the View event.


<span id="Actions"></span>
### Actions

Click session details to quickly view the current user's behavior path. This helps reconstruct the user's operation path and assists in troubleshooting.

<span id="JS Error"></span>
### JS Error


* Displays all JavaScript error reporting events, allowing you to view the specific stack trace and the context associated with each reported event.

* If you want to view statistical information, you can go to the error details page.


<span id="Request"></span>
### Request

All `Resource timing` reports.

<span id="Resource"></span>
### Resource

Timing is reported for all static resources.

<span id="Resource Errors"></span>
### Resource Errors

All static resource errors are reported.

<span id="Custom Event"></span>
### Custom Event

All custom event reports.

<span id="Custom Log"></span>
### Custom Log

All custom log reporting

<span id="LongTasks"></span>
### LongTasks

All longtask reporting information

<span id="Blank Screen"></span>
### Blank Screen

The Blank Screen page displays all blank screen reporting data.
