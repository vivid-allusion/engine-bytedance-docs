---
title: "API release notes"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/API_release_records_app"
---

This topic records the changes made to the app\-side OpenAPI after its official release.

<span id=".MjAyNSDlubQgMDEg5pyI"></span>
## January 2025


|API |Release Date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|KuPelU">新增</span> [AnalyseMetricList](https://docs.byteplus.com/en/docs/apmplus/AnalyseMetricList) |2025\-01\-23 |Added an API to view the list from the metric detail page. |Event |
|<span data-api-tag="add\|By4AGR">新增</span> [AnalyseDimensionList](https://docs.byteplus.com/en/docs/apmplus/AnalyseDimensionList) ||Added an API to view the list from the event dimension detail page. ||
|<span data-api-tag="add\|Pc2INH">新增</span> [AnalyseEventList](https://docs.byteplus.com/en/docs/apmplus/AnalyseEventList) ||Added an API to view the list from the event detail page. ||


<span id=".MjAyNCDlubQgMDcg5pyI"></span>
## July 2024


|API |Release Date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|Pf4MPp">新增</span> [GetAppCustomTagValues](https://docs.byteplus.com/en/docs/apmplus/GetAppCustomTagValues) |2024\-07\-16 |Added an API to get custom dimension values. |General |
|<span data-api-tag="add\|2RA9qZ">新增</span> [GetAppCustomTagKeys](https://docs.byteplus.com/en/docs/apmplus/GetAppCustomTagKeys) ||Added an API to get custom dimension keys. ||


<span id=".MjAyNCDlubQgMDQg5pyI"></span>
## April 2024


|API |Release Date |Change |Related feature |
|---|---|---|---|
|[GetAppMemoryDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryDetail) |2024\-04\-16 |Added an API to get the summary of a single memory event. |Memory monitoring |
|[GetAppMemoryEventDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryEventDetail) ||Added an API to get the details of a single memory event. ||
|[GetAppMemoryList](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryList) ||Added an API to get the listed information of memory leaks or large objects. ||
|[GetAppMemoryEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryEventList) ||Added an API to get the memory event list. ||
|[GetAppExceptionalCPUTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUTrend) |2024\-04\-15 |Added an API to get CPU anomaly trends. |CPU monitoring |
|[GetAppCPUTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppCPUTrend) ||Added an API to get CPU metric trends. ||
|[GetAppExceptionalCPUIssueList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUIssueList) ||Added an API to get the CPU issue list. ||
|[GetAppExceptionalCPUSummaryData](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUSummaryData) ||Added an API to get CPU abnormal metrics. ||
|[GetAppExceptionalCPUIssueDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalCPUIssueDetail) ||Added an API to get CPU issue details. ||
|[GetAppThreadCPUUsageList](https://docs.byteplus.com/en/docs/apmplus/GetAppThreadCPUUsageList) ||Added an API to get CPU utilization of each thread. ||
|[GetAppHttpFieldValues](https://docs.byteplus.com/en/docs/apmplus/GetAppHttpFieldValues) ||Added an API to get the optional values for HTTP filter criteria for the app network. |Network monitoring |
|[GetAppHttpTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppHttpTrend) ||Added an API to get metric trends for network HTTP monitoring. ||
|[GetAppBatteryTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryTrend) |2024\-04\-10 |Added an API to get the trends of foreground current and battery temperature related to app power consumption. |Battery monitoring |
|[GetAppBatteryConsumptionFactorsEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryConsumptionFactorsEventList) ||Added an API to get the app power consumption event list. ||
|[GetAppBatteryPageList](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryPageList) ||Added an API to get the app battery foreground list. ||
|[GetAppBatteryConsumptionFactorsTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryConsumptionFactorsTrend) ||Added an API to get trends of current and battery temperature related to app power consumption. ||
|[GetAppConsumerBatteryFieldValues](https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryFieldValues) ||Added an API to get the available values for battery filter criteria. ||
|[GetAppExceptionalBatteryTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryTrend) ||Added an API to get the trend of app battery anomalies. ||
|[GetAppExceptionalBatteryIssueEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueEventList) ||Added an API to get app battery anomaly events. ||
|[GetAppExceptionalBatteryIssueDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueDetail) ||Added an API to get app battery anomaly details. ||
|[GetAppExceptionalBatteryIssueList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueList) ||Added an API to get the app battery anomaly list. ||
|[GetAppExceptionalBatterySummaryData](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatterySummaryData) ||Added an API to get app battery metrics. ||


<span id="5750bcd3"></span>
## March 2023


|API |Release Date |Change |Related feature |
|---|---|---|---|
|[GetAppTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppTrend) |2023\-03\-15 |Added an API to get trends of app crash count, crash rate, crash user count, crash user rate, PV, and UV. |Exceptions and crashes |
|[GetAppSummaryData](https://docs.byteplus.com/en/docs/apmplus/GetAppSummaryData) ||Added an API to get app crash count, crash rate, crash user count, and crash user rate. ||
|[GetAppPvUv](https://docs.byteplus.com/en/docs/apmplus/GetAppPvUv) ||Added an API to get app PV and UV. ||
|[GetAppExceptionIssueList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueList) ||Added an API to get the app crash list. ||
|[GetAppExceptionIssueDetail](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueDetail) ||Added an API to get app crash issue details. ||
|[GetAppExceptionIssueEventList](https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionIssueEventList) ||Added an API to get the event list of a specific app crash issue. ||
|[GetAppFieldValues](https://docs.byteplus.com/en/docs/apmplus/GetAppFieldValues) ||Added an API to get the available values for app filter criteria. ||
|[GetAppStartupMultiTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppStartupMultiTrend) |2023\-03\-13 |Added an API to get app launch analysis trends. |Startup analysis |


<span id="637f4ee6"></span>
## February 2023


|API |Release Date |Change |Related feature |
|---|---|---|---|
|[UpdateAppAlarmStatus](https://docs.byteplus.com/en/docs/apmplus/UpdateAppAlarmStatus) |2023\-02\-28 |Added an API to update alert task status. |Alert |


<span id="0469c46f"></span>
## November 2022


|API |Release Date |Change |Related feature |
|---|---|---|---|
|[GetAppAlarmRuleList](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmRuleList) |2022\-11\-20 |Added an API to get the app alert task list. |Alert |
|[GetAppAlarmMetricsConf](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmMetricsConf) ||Added an API to get app alert\-related metadata. ||
|[SetAppAlarmRule](https://docs.byteplus.com/en/docs/apmplus/SetAppAlarmRule) ||Added an API to create or update app alert tasks. ||
|[GetAppAlarmTrend](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmTrend) ||Added an API to get app alert trends. ||
|[GetAppAlarmHistory](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmHistory) ||Added an API to get app alert history. ||
|[GetAppAlarmEventMetricsConf](https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmEventMetricsConf) ||Added an API to get app custom event alert configurations. ||


<span id="d666c363"></span>
## October 2022


|API |Release Date |Change |Related feature |
|---|---|---|---|
|[APIs](https://docs.byteplus.com/en/docs/apmplus/Available_APIs_app) |2022\-10\-15 |The app\-side OpenAPI documentation is officially released. |None |
