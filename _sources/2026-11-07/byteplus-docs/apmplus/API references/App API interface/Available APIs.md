---
title: "Available APIs"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Available_APIs_app"
---

The OpenAPIs for event, log, alert, and other services are available on the app side. By calling these APIs, you can use the corresponding app\-side features.

<span id=".5LqL5Lu2"></span>
## General


|API name |Feature |
|---|---|
|[GetAppCustomTagValues](https://docs.byteplus.com/en/docs/apmplus/GetAppCustomTagValues) |Get custom dimension values. |
|[GetAppCustomTagKeys](https://docs.byteplus.com/en/docs/apmplus/GetAppCustomTagKeys) |Get custom dimension keys. |


<span id=".5LqL5Lu2"></span>
## Event


|API name |Feature |
|---|---|
|[AnalyseSummary](https://docs.byteplus.com/en/docs/apmplus/AnalyseSummary) |View the event overview. |
|[AnalyseRank](https://docs.byteplus.com/en/docs/apmplus/AnalyseRank) |View the event list. |
|[AnalyseDimensionValues](https://docs.byteplus.com/en/docs/apmplus/AnalyseDimensionValues) |View the available value list for the event dimension. |
|[AnalyseMetricList](https://docs.byteplus.com/en/docs/apmplus/AnalyseMetricList) |View the list on the metric detail page. |
|[AnalyseDimensionList](https://docs.byteplus.com/en/docs/apmplus/AnalyseDimensionList) |View the list on the event dimension detail page. |
|[AnalyseEventList](https://docs.byteplus.com/en/docs/apmplus/AnalyseEventList) |View the list on the event detail page. |


<span id=".5pel5b-X"></span>
## Logs


|API name |Feature |
|---|---|
|[AppTraceLogs](https://docs.byteplus.com/en/docs/apmplus/GetTraceLog) |Query a single log. |


<span id=".5oql6K2m"></span>
## Alerts


|API name |Feature |
|---|---|
|[GetAppAlarmRuleList](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmRuleList) |Get app alert task list. |
|[GetAppAlarmMetricsConf](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmMetricsConf) |Get app alert\-related metadata. |
|[SetAppAlarmRule](https://docs.byteplus.com/en/docs/apmplus/SetAppAlarmRule) |Create or update an app alert task. |
|[GetAppAlarmTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmTrend) |Get the app alert trend. |
|[GetAppAlarmHistory](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmHistory) |Get app alert history. |
|[GetAppAlarmEventMetricsConf](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmEventMetricsConf) |Get alert configurations for app custom events. |
|[UpdateAppAlarmStatus](https://docs.byteplus.com/en/docs/apmplus/UpdateAppAlarmStatus) |Update app alert task status. |


<span id=".5byC5bi45ZKM5bSp5rqD"></span>
## Exceptions and crashes


|API name |Feature |
|---|---|
|[GetAppTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppTrend) |Get data trends for app\-side crash analysis, MetricKit, crash protection, custom errors, and lag analysis\-related data, for example, the number of crash analyses, crash rate, number of crash users, crash user rate, PV, and UV. |
|[GetAppSummaryData](https://docs.byteplus.com/en/docs/apmplus/GetAppSummaryData) |Get app\-side crash analysis, MetricKit, crash protection, custom errors, and lag analysis data, for example, the number of crashes, crash rate, number of crash users, and crash user rate. |
|[GetAppPvUv](https://docs.byteplus.com/en/docs/apmplus/GetAppPvUv) |Get PV and UV of the app. |
|[GetAppExceptionIssueList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueList) |Get the issue list related to app\-side crash analysis, MetricKit, crash protection, custom errors, and lag analysis. |
|[GetAppExceptionIssueDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueDetail) |Get issue details related to app\-side crash analysis, MetricKit, crash protection, custom errors, and lag analysis. |
|[GetAppExceptionIssueEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueEventList) |Get the event list of a designated crash issue related to app\-side crash analysis, MetricKit, crash protection, custom errors, and lag analysis. |
|[GetAppFieldValues](https://docs.byteplus.com/en/docs/apmplus/GetAppFieldValues) |Get available values for app filter criteria. |


<span id=".5ZCv5Yqo5YiG5p6Q"></span>
## Startup analysis


|API name |Feature |
|---|---|
|[GetAppStartupMultiTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppStartupMultiTrend) |Obtain the trend of application startup analysis. |


<span id=".5YaF5a2Y55uR5o6n"></span>
## Memory monitoring


|API name |Feature |
|---|---|
|[GetAppMemoryDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryDetail) |Get the summary of a single memory event. |
|[GetAppMemoryEventDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryEventDetail) |Get details of a single memory event. |
|[GetAppMemoryList](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryList) |Get the list of memory leaks or large objects. |
|[GetAppMemoryEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryEventList) |Get memory event list. |


<span id=".Q1BV55uR5o6n"></span>
## CPU monitoring


|API name |Feature |
|---|---|
|[GetAppExceptionalCPUTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUTrend) |Get the trend of CPU anomalies. |
|[GetAppCPUTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppCPUTrend) |Get trends of various CPU metrics. |
|[GetAppExceptionalCPUIssueList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUIssueList) |Get the CPU issue list. |
|[GetAppExceptionalCPUSummaryData](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUSummaryData) |Get CPU abnormal metrics. |
|[GetAppExceptionalCPUIssueDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUIssueDetail) |Get CPU issue details. |
|[GetAppThreadCPUUsageList](https://docs.byteplus.com/en/docs/apmplus/GetAppThreadCPUUsageList) |Get the CPU utilization of each thread. |


<span id=".572R57uc55uR5o6n"></span>
## Network monitoring


|API name |Feature |
|---|---|
|[GetAppHttpFieldValues](https://docs.byteplus.com/en/docs/apmplus/GetAppHttpFieldValues) |Get available values for HTTP filter criteria for the app network. |
|[GetAppHttpTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppHttpTrend) |Get metric trends for HTTP network monitoring. |


<span id=".55S16YeP55uR5o6n"></span>
## Battery monitoring


|API name |Feature |
|---|---|
|[GetAppBatteryTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryTrend) |Get trends of foreground current and battery temperature related to app power consumption. |
|[GetAppBatteryConsumptionFactorsEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryConsumptionFactorsEventList) |Get app power consumption event list. |
|[GetAppBatteryPageList](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryPageList) |Get app battery foreground list. |
|[GetAppBatteryConsumptionFactorsTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryConsumptionFactorsTrend) |Get trends of current and battery temperature related to app power consumption. |
|[GetAppExceptionalBatteryTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryTrend) |Get the trend of app battery anomalies. |
|[GetAppBatteryFieldValues](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryFieldValues) |Get available values for battery filter criteria. |
|[GetAppExceptionalBatteryIssueEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueEventList) |Get app battery abnormal events. |
|[GetAppExceptionalBatteryIssueDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueDetail) |Obtain the details of the app battery anomalies. |
|[GetAppExceptionalBatteryIssueList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueList) |Get the list of app battery anomalies. |
|[GetAppExceptionalBatterySummaryData](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatterySummaryData) |Get app battery metrics. |
