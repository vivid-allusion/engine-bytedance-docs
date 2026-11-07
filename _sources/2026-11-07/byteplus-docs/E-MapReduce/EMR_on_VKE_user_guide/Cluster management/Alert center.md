---
title: "Alert center"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/vke_alert_center"
---

This article describes the purpose of the EMR on VKE Alarm Center page and provides parameter descriptions. The EMR on VKE alarm module is managed by the Cloud Monitoring product, providing you with context\-related alarm views and simplifying troubleshooting. For detailed usage, refer to the documentation: [Configure alarm policies in Cloud Monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

On the [EMR on VKE Console ](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/vke-cluster-management/cluster-list) **\> Cluster Details \>**  **Alert center**page, you can quickly view the alarm history for the corresponding cluster. This is suitable for scenarios such as cluster troubleshooting and routine health checks. Displayed as follows:

**Explanation of table parameters:** 


|Parameter |Description |
|---|---|
|Rule name |Corresponds to the alarm rule name configured in Cloud Monitoring and is hyperlinked. You can click the rule name to view its definition. |
|Dimension |The dimension category in which the alarm was generated, specific to the service itself. |
|Status |Divided into two types: **Alerting** and **Recovered**. Filtering is supported. |
|Rule description |Indicates the configuration details of the rule. |
|Affected resource |Indicates the resource associated with the alarm, such as a specific host. |
|First alarm occurrence time |Indicates the time when this alarm history was generated after the resource triggered the alarm. |
|Duration |* If the alarm status is **Recovered**, it indicates the duration from when the resource triggered this alarm history to when it returned to normal.<br><br>* If the alarm status is **In alarm**, it indicates the duration from when the resource triggered this alarm history to the current time. |
|Alarm level |Divided into **notice, warning, critical** levels. Filtering is supported. |
