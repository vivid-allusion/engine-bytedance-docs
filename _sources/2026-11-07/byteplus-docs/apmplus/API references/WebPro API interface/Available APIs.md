---
title: "Available APIs"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Available_APIs_webpro"
---

WebPro provides OpenAPIs for alerts, blank screen monitoring, custom monitoring, and other related services. By calling these APIs, you can use the corresponding features on the WebPro side.

## General

|API name |Feature |
|---|---|
|[GetFieldKeys](https://docs.byteplus.com/en/docs/apmplus/GetFieldKeys) |Get filter criteria. |
|[GetFieldValues](https://docs.byteplus.com/en/docs/apmplus/GetFieldValues) |Get the available values for specific filter dimensions. |

## Action list

|API name |Feature |
|---|---|
|[GetActionOverviewList](https://docs.byteplus.com/en/docs/apmplus/GetActionOverviewList) |Get the action event list. |
|[GetTrendPerAction](https://docs.byteplus.com/en/docs/apmplus/GetTrendPerAction) |Get the quantity trend for the specified action. |
|[GetDurationTrendPerAction](https://docs.byteplus.com/en/docs/apmplus/GetDurationTrendPerAction) |Get the duration trend of the specified action. |
|[GetReqListPerAction](https://docs.byteplus.com/en/docs/apmplus/ActionDetailReqList) |Get the list of requests triggered by the specified action. |
|[GetJsErrorListPerAction](https://docs.byteplus.com/en/docs/apmplus/GetJsErrorListPerAction) |Get the list of JavaScript errors associated with the specified action. |

## Alert

|API name |Feature |
|---|---|
|[GetAlarmMeta](https://docs.byteplus.com/en/docs/apmplus/GetAlarmMeta) |Get the alert metric metadata for all types. |
|[GetAlarmEventMeta](https://docs.byteplus.com/en/docs/apmplus/GetAlarmEventMeta) |Get the list of custom event names. |
|[GetAlarmEventMetaMetric](https://docs.byteplus.com/en/docs/apmplus/GetAlarmEventMetaMetric) |Get the alert metrics for a specified custom event. |
|[GetAlarmMetricRelatedMeta](https://docs.byteplus.com/en/docs/apmplus/GetAlarmMetricRelatedMeta) |Get the filtering conditions, grouping dimensions, and attribution dimensions supported by the specified metric. |
|[GetAlarmMetricCandidate](https://docs.byteplus.com/en/docs/apmplus/GetAlarmMetricCandidate) |Get the available values of specific filter criteria under the specified alert metric. |
|[AddAlarm](https://docs.byteplus.com/en/docs/apmplus/AddAlarm) |Create an alert task. |
|[UpdateAlarm](https://docs.byteplus.com/en/docs/apmplus/UpdateAlarm) |Update alert task. |
|[DeleteAlarm](https://docs.byteplus.com/en/docs/apmplus/DeleteAlarm) |Delete an alert task. |
|[GetAlarmRuleList](https://docs.byteplus.com/en/docs/apmplus/GetAlarmRuleList) |Get the alert task list. |
|[AckAlarm](https://docs.byteplus.com/en/docs/apmplus/AckAlarm) |Set the alert task acknowledgment. |
|[UnackAlarm](https://docs.byteplus.com/en/docs/apmplus/UnackAlarm) |Clear the acknowledgment status of an alert task. |
|[GetAlarmAckStatus](https://docs.byteplus.com/en/docs/apmplus/GetAlarmAckStatus) |Get alert task ACK status. |
|[GetAlarmTaskDetail](https://docs.byteplus.com/en/docs/apmplus/GetAlarmTaskDetail) |Get the details of the specified alert task. |
|[GetAlarmTrend](https://docs.byteplus.com/en/docs/apmplus/GetAlarmTrend) |Get alert trend. |
|[GetAlarmRelatedMetricTrend](https://docs.byteplus.com/en/docs/apmplus/GetAlarmRelatedMetricTrend) |Get the metric trend chart related to the alert task. |
|[GetAlarmAttribution](https://docs.byteplus.com/en/docs/apmplus/GetAlarmAttribution) |Get attribution information. |
|[GetAlarmHistory](https://docs.byteplus.com/en/docs/apmplus/GetAlarmHistory) |Get the alert history of the specified task. |
|[GetAlarmAllHistory](https://docs.byteplus.com/en/docs/apmplus/GetAlarmAllHistory) |Get all alert histories. |
|[DownloadAlarmAllHistory](https://docs.byteplus.com/en/docs/apmplus/DownloadAlarmAllHistory) |Download alert history. |
|[GetAlarmDistribution](https://docs.byteplus.com/en/docs/apmplus/GetAlarmDistribution) |Get the alert type distribution. |

## Blank screen monitoring

|API name |Feature |
|---|---|
|[BlankScreenOverviewTrend](https://docs.byteplus.com/en/docs/apmplus/BlankScreenOverviewTrend) |Get the blank screen overview trend and attribution distribution. |
|[BlankScreenOverviewList](https://docs.byteplus.com/en/docs/apmplus/BlankScreenOverviewList) |Get the blank screen list for different attribution types. |

## Custom monitoring

|API name |Feature |
|---|---|
|[EventList](https://docs.byteplus.com/en/docs/apmplus/EventList) |Get the custom event list. |
|[EventTypeTrend](https://docs.byteplus.com/en/docs/apmplus/EventTypeTrend) |Get the report trend for a specific custom event. |
|[EventTypeDetail](https://docs.byteplus.com/en/docs/apmplus/EventTypeDetail) |Get the category and metric aggregation list of a specific custom event. |

## Data exploration

|API name |Feature |
|---|---|
|[DataEvTypeCount](https://docs.byteplus.com/en/docs/apmplus/DataEvTypeCount) |Get overview values of reports for each type. |
|[DataTrend](https://docs.byteplus.com/en/docs/apmplus/DataTrend) |Get the report trend for a specific type. |
|[DataList](https://docs.byteplus.com/en/docs/apmplus/DataList) |Get the report details list for a specific type. |
|[SessionList](https://docs.byteplus.com/en/docs/apmplus/SessionList) |Get trace details under the specified session. |
|[ResourceTiming](https://docs.byteplus.com/en/docs/apmplus/ResourceTiming) |Get the resource loading duration Gantt chart. |
|[JsBreadcrumbs](https://docs.byteplus.com/en/docs/apmplus/JsBreadcrumbs) |Get the breadcrumbs under a specific JS error. |
|[ViewDetail](https://docs.byteplus.com/en/docs/apmplus/ViewDetail) |Get the performance and resource loading status under the specified view. |
|[ActionDetail](https://docs.byteplus.com/en/docs/apmplus/ActionDetail) |Get the resource loading status under a specific action. |

## JS error monitoring

|API name |Feature |
|---|---|
|[JSOverviewTrend](https://docs.byteplus.com/en/docs/apmplus/JSOverviewTrend) |Get the JS error overview value and trend. |
|[JSOverviewErrorList](https://docs.byteplus.com/en/docs/apmplus/JSOverviewErrorList) |Get JS error aggregation list. |
|[JSOverviewPageList](https://docs.byteplus.com/en/docs/apmplus/JSOverviewPageList) |Get the list of pages where JavaScript errors occurred. |
|[JSOverviewErrorMessageList](https://docs.byteplus.com/en/docs/apmplus/JSOverviewErrorMessageList) |Get the list of error messages. |
|[JSErrDetail](https://docs.byteplus.com/en/docs/apmplus/JSErrDetail) |Get JS error details. |
|[JSErrDetailStack](https://docs.byteplus.com/en/docs/apmplus/JSErrDetailStack) |Get JavaScript error stack traces. |
|[JsErrDetailBlankScreenCount](https://docs.byteplus.com/en/docs/apmplus/JsErrDetailBlankScreenCount) |Get the list of blank screens caused by JavaScript errors. |

## Performance monitoring

|API name |Feature |
|---|---|
|[PerfMetricsList](https://docs.byteplus.com/en/docs/apmplus/PerfMetricsList) |Get the performance metric change trend. |
|[WorstPerf](https://docs.byteplus.com/en/docs/apmplus/WorstPerf) |Get the list of the top 5 pages with the worst performance. |
|[ImprovedPerf](https://docs.byteplus.com/en/docs/apmplus/ImprovedPerf) |Get the list of the top 5 pages with optimized performance. |
|[DeteriorationPerf](https://docs.byteplus.com/en/docs/apmplus/DeteriorationPerf) |Get the list of top 5 pages with performance deterioration. |
|[PageOverview](https://docs.byteplus.com/en/docs/apmplus/PageOverview) |Get the page performance metric overview. |
|[GetSingleMetricChart](https://docs.byteplus.com/en/docs/apmplus/GetSingleMetricChart) |Get performance metric distribution. |
|[GetDatumLinekeys](https://docs.byteplus.com/en/docs/apmplus/GetDatumLinekeys) |Get the performance monitoring metric baseline. |

## Version management

|API name |Feature |
|---|---|
|[ReleaseList](https://docs.byteplus.com/en/docs/apmplus/ReleaseList) |Get the list of versions. |
|[ReleaseDetail](https://docs.byteplus.com/en/docs/apmplus/ReleaseDetail) |Get the details of the specified version. |

## Request monitoring

|API name |Feature |
|---|---|
|[ReqOverviewTrend](https://docs.byteplus.com/en/docs/apmplus/ReqOverviewTrend) |Get the request overview trend. |
|[ReqOverviewErrTrend](https://docs.byteplus.com/en/docs/apmplus/ReqOverviewErrTrend) |Obtain the request error overview trend. |
|[ReqErrorList](https://docs.byteplus.com/en/docs/apmplus/ReqErrorList) |Get the request error list. |
|[ReqSlowList](https://docs.byteplus.com/en/docs/apmplus/ReqSlowList) |Get the top 10 slow requests. |
|[ReqList](https://docs.byteplus.com/en/docs/apmplus/ReqList) |Get request list. |
|[ReqItemDashboard](https://docs.byteplus.com/en/docs/apmplus/ReqItemDashboard) |Get the dashboard for the specific request. |
|[ReqItemTrend](https://docs.byteplus.com/en/docs/apmplus/ReqItemTrend) |Get the specific request duration trend. |
|[ReqItemHeatMap](https://docs.byteplus.com/en/docs/apmplus/ReqItemHeatMap) |Get the specific request heat map. |
|[ReqItemBlankScreenCount](https://docs.byteplus.com/en/docs/apmplus/ReqItemBlankScreenCount) |Get the list of blank screens caused by request errors. |

## Resource monitoring

|API name |Feature |
|---|---|
|[ResourceOverviewTrend](https://docs.byteplus.com/en/docs/apmplus/ResourceOverviewTrend) |Get the overall trend of static resources. |
|[ResourceOverviewErrTrend](https://docs.byteplus.com/en/docs/apmplus/ResourceOverviewErrTrend) |Get the static resource error trend. |
|[ResourceErrorList](https://docs.byteplus.com/en/docs/apmplus/ResourceErrorList) |Get the static resource error list. |
|[ResourceSlowList](https://docs.byteplus.com/en/docs/apmplus/ResourceSlowList) |Get the top 10 slow\-loading static resource list. |
|[ResourceList](https://docs.byteplus.com/en/docs/apmplus/ResourceList) |Get static resource list. |
|[ResourceItemDashboard](https://docs.byteplus.com/en/docs/apmplus/ResourceItemDashboard) |Get the specified static resource dashboard. |
|[ResourceItemTrend](https://docs.byteplus.com/en/docs/apmplus/ResourceItemTrend) |Get the trend of specified static resources. |
|[ResourceItemHeatMap](https://docs.byteplus.com/en/docs/apmplus/ResourceItemHeatMap) |Get the heat map for the specified static resource. |
|[ResourceItemBlankScreenCount](https://docs.byteplus.com/en/docs/apmplus/ResourceItemBlankScreenCount) |Get the list of blank screens caused by static resource errors. |

## Page list

|API name |Feature |
|---|---|
|[UrlOverview](https://docs.byteplus.com/en/docs/apmplus/UrlOverview) |Get the overview values for all pages. |
|[UrlOverviewMetrics](https://docs.byteplus.com/en/docs/apmplus/UrlOverviewMetrics) |Get page\-related metrics. |
|[UrlList](https://docs.byteplus.com/en/docs/apmplus/UrlList) |Get the page list. |

## New error alert

|API name |Feature |
|---|---|
|[CreateWebProNewErrorAlertRule](https://docs.byteplus.com/en/docs/apmplus/CreateWebProNewErrorAlertRule) |Create an alert rule for new errors. |
|[DeleteWebProNewErrorAlertRule](https://docs.byteplus.com/en/docs/apmplus/DeleteWebProNewErrorAlertRule) |Delete an alert rule for new errors. |
|[UpdateWebProNewErrorAlertRule](https://docs.byteplus.com/en/docs/apmplus/UpdateWebProNewErrorAlertRule) |Update the new error alert rule. |
|[OpenWebProNewErrorAlertRule](https://docs.byteplus.com/en/docs/apmplus/OpenWebProNewErrorAlertRule) |Enable alert rules for new errors. |
|[GetWebProNewErrorAlertRuleDetail](https://docs.byteplus.com/en/docs/apmplus/GetWebProNewErrorAlertRuleDetail) |Get details of new error alert rules. |
|[CloseWebProNewErrorAlertRule](https://docs.byteplus.com/en/docs/apmplus/CloseWebProNewErrorAlertRule) |Disable alert rules for new errors. |
|[GetWebProNewErrorAlertTrend](https://docs.byteplus.com/en/docs/apmplus/GetWebProNewErrorAlertTrend) |Get the overview and trend chart of new error alerts. |
|[ListWebProNewErrorAlertRules](https://docs.byteplus.com/en/docs/apmplus/ListWebProNewErrorAlertRules) |Get the list of alert rules for new errors. |
|[GetWebProNewErrorAlertHistory](https://docs.byteplus.com/en/docs/apmplus/GetWebProNewErrorAlertHistory) |Get the trigger history of new error alerts. |
