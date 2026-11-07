---
title: "View alarm history"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_alarm_history"
---

This topic describes how to view alarm history in Milvus for VectorDB.

<span id="qmZaIXTr"></span>
## Background

The alarm history displays the policies triggering alarms and the corresponding resource information. The fields in the alarm history list are described as follows.


|**Column name** |**Description** |
|---|---|
|Policy name |Name of the alarm policy that generated this alarm. You can click the name to copy it. |
|Failure resource |Name of the resource triggering the alarm. Click the name to view the detailed metric dashboard of the resource. |
|Dimension |Select the resource dimension of the cloud product that triggered the alarm, such as instance and disk. |
|Status |Current status of this alarm history. Valid values: **Alarming** and **Recovered**. |
|Alarm rule |The metric type and trigger condition configured in the alarm rule. |
|Alarm first trigger time |Time when the resource first triggered this alarm history after the alarm was activated. |
|Duration |* If the alarm state is **Recovered**, the duration starts from when the resource triggered this alarm history to when the alarm is recovered.<br><br>* If the alarm status is **Alarming**, the duration starts from when the resource triggered this alarm to the present. |
|Alarm level |Severity of the alarm. Valid values:  **Serious**, **Warning**, and **Notification**. |
|Region |Region where the alarm resource is located. |
|Actions |Supported operations for alarm history. Click **Details** in the **Actions** column to view detailed alarm information. |


<span id="IpRy4L1r"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. On the top navigation bar, select the target project and region.

3. Click **Alarm management** in the left navigation pane.

4. Click the **Alarm policy** tab at the top of the page to view the alarm history for the current region.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can filter alarm history by policy name, status, resource ID, alarm level, and specified time period.</div>
