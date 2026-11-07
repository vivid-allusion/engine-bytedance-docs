---
title: "Available APIs"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Available_APIs_minipro"
---

Mini Pro Monitoring provides OpenAPIs for services such as general capabilities, JavaScript errors, and alerts. By calling these APIs, you can use the corresponding features of Mini Pro.

## General

|API name |Feature |
|---|---|
|[MiniProGetFieldValues](https://docs.byteplus.com/en/docs/apmplus/MiniProGetFieldValues) |Get the values of the specific filter conditions. |
|[MiniProGetFieldKeys](https://docs.byteplus.com/en/docs/apmplus/MiniProGetFieldKeys) |Get filter criteria. |

## JS error

|API name |Feature |
|---|---|
|[MiniProJsErrDetailDistribution](https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailDistribution) |Get JavaScript error distribution details. |
|[MiniProJsErrDetailReleaseList](https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailReleaseList) |Get the JavaScript error release information. |
|[MiniProJsErrDetail](https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetail) |Get JavaScript error details. |
|[MiniProJsErrDetailStartEndInfo](https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailStartEndInfo) |Get the start and end events of JavaScript errors. |
|[MiniProJsErrDetailStack](https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailStack) |Get JavaScript error stack trace information. |
|[MiniProJsTrendOverview](https://docs.byteplus.com/en/docs/apmplus/MiniProJsTrendOverview) |View the JavaScript error trend overview. |
|[MiniProJsErrList](https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrList) |View the JavaScript issue list. |

## Alert

|API name |Feature |
|---|---|
|[MiniProAddAlarm](https://docs.byteplus.com/en/docs/apmplus/MiniProAddAlarm) |Add a new alert task. |
|[MiniProUpdateAlarm](https://docs.byteplus.com/en/docs/apmplus/MiniProUpdateAlarm) |Modify an alert task. |
|[MiniProDeleteAlarm](https://docs.byteplus.com/en/docs/apmplus/MiniProDeleteAlarm) |Delete an alert task. |
|[MiniProAlarmMeta](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMeta) |Get metadata such as the alert category and corresponding metrics. |
|[MiniProAlarmMetaMeasure](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMetaMeasure) |Get detailed metrics of an event. |
|[MiniProAlarmEventMeta](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmEventMeta) |Get alert event name metrics. |
|[MiniProAlarmMetricsMeta](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMetricsMeta) |Get filter, grouping, and attribution dimensions based on metrics. |
|[MiniProAlarmTrend](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmTrend) |View the alert count trend chart (alert overview). |
|[MiniProAlarmDetail](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmDetail) |Get alert task details. |
|[MiniProAlarmMetricsCandidate](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMetricsCandidate) |Get the available values of specific filter criteria under the specified alert metric. |
|[MiniProAlarmList](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmList) |Get the alert task list. |
|[MiniProAlarmDistribution](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmDistribution) |Get the alert type distribution. |
|[MiniProAlarmMetricsTrend](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMetricsTrend) |View the overview of metrics related to the alert task. |
|[MiniProAlarmAttribution](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmAttribution) |Get alert attribution information. |
|[MiniProDownloadAlarmHistory](https://docs.byteplus.com/en/docs/apmplus/MiniProDownloadAlarmHistory) |Download alert history data. |
|[MiniProAlarmHistory](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmHistory) |Get the alert history of the specified task. |
|[MiniProAlarmAckStatus](https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmAckStatus) |Get alert task ACK status. |
|[MiniProAckAlarm](https://docs.byteplus.com/en/docs/apmplus/MiniProAckAlarm) |Set the alert task ACK. |
|[MiniProUnAckAlarm](https://docs.byteplus.com/en/docs/apmplus/MiniProUnAckAlarm) |Cancel alert task ACK. |

## Performance monitor

|API name |Feature |
|---|---|
|[MiniproPerfDatumChart](https://docs.byteplus.com/en/docs/apmplus/MiniproPerfDatumChart) |View the details of the performance monitor metric data. |
|[MiniproPerfMetricKeyList](https://docs.byteplus.com/en/docs/apmplus/MiniproPerfMetricKeyList) |View the performance monitor metric list. |

## Page list

|API name |Feature |
|---|---|
|[MiniproUrlListUrlList](https://docs.byteplus.com/en/docs/apmplus/UrlListUrlList) |View page list metric data. |
|[MiniproUrlListOverviewMetrics](https://docs.byteplus.com/en/docs/apmplus/UrlListOverviewMetrics) |Query the available items for page list metrics. |
