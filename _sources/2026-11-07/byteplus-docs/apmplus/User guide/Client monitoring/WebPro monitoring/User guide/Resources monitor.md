---
title: "Resources monitor"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/resources_monitor"
---

The static resources monitoring feature consists of two parts: overview and list. Through dashboards such as trend charts, list data, and load heatmaps, combined with data explore to view static resources details, you can troubleshoot static resource error and load time issues on the page.

<span id="0168b14d"></span>
## resources overview

<span id="f801e13d"></span>
### All resources

<span id="0391b44c"></span>
##### Static resources trend chart


* The static resources trend chart displays metrics such as load count, user count, slow load count, slow load rate, slow resource affected user, and slow resource affected user rate for all static resources under the current filter conditions, providing an overview of site resources monitor information. To learn more about metric meanings, refer to [resources monitor](https://docs.byteplus.com/en/docs/apmplus/WebPro_client_metric_description#54ae29f4).

* If Release information has been set in the setting, the chart will also display the Release launch version information.


<span id="d60529fa"></span>
##### Slow\-loading sorted lists


* On the slow\-loading list page, you can specify the sorting criterion and view the sorted list of all static resources.

* On the slow load list page, metrics such as load time, slow load rate, and impacted user count are provided for static resources, reflecting the load time and slow load rate for different static resources.

* Click the static resources path to view details of the current static resources. The operating system automatically uses the static resource name as a search condition, and you can view information such as the trend chart, distribution chart, and heatmap for the current static resource.

* Click **data explore** to navigate to the data explore page for further analysis of the slow loading of static resources. The operating system automatically populates static resource names and loading times into the search criteria of data explore. Then, by clicking on a single data entry within a specific time period, you can view a waterfall chart showing the distribution of resource loading times under a particular view.


<span id="8ee7d654"></span>
### Error resources

<span id="97cade21"></span>
##### Static resource error trend chart


* The static resource error trend chart displays metrics such as error count, error rate, impacted user count, impacted user rate, and other metrics for the currently selected time range, providing an overview of the overall static resource error status for the site.

* If Release information has been set, the Release launch version information will also be displayed in the chart.


<span id="6afea970"></span>
##### List of error resources


* The error resource list displays the error count and impacted user count for different static resources.

* Click the static resources path to navigate to the **data explore** page, where you can further view error resource details. The operating system automatically populates static resource paths and domain names into the search criteria of data explore. Then, by clicking on a single data entry within a specific time period, you can view a waterfall chart showing the distribution of resource load times for a particular view, as well as analyze the root cause of errors.


<span id="f2a77336"></span>
## resource


* On the left side of the static resources list, a sorted list of different static resources is displayed. The sorting method depends on the criteria you set, such as sorting by slow resource rate, slow resource count, resource load count, total load time, and other metrics.

* Click static resources to expand the static resources details on the right side of the list. You can view summary metric information such as load count, user count, and slow load count, as well as the SLA for slow resources and bar and ring charts showing the proportion of slow resources.

* Trend and distribution charts display the current timing information for static resource requests and the distribution of request times.

* The resource loading heatmap provides feedback on the loading status of current static resources at different times. Hover the mouse over the heatmap to view the load count for different time periods.

   In the figure below, it is clear that the amount of data loaded is highest between 14:00 and 18:00.
