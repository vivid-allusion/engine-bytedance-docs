---
title: "Enable alarm configuration"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Enable_alarm_configuration"
---

This topic describes how to enable preset alarm policies in Milvus for VectorDB using alarm configuration.

<span id="hMbQSGGA"></span>
## Precautions

Only Dedicated and Serverless instances support enabling alarm configuration.

<span id="kUliYbRv"></span>
## Background

To easily monitor the running state of Milvus for VectorDB instances, Milvus for VectorDB presets a series of alarm policies and supports one\-click settings. The table below summarizes the preset alarm policies of Milvus for your reference.


<Tabs>
<Tab zoneid="gaoamVDkFW" title="Dedicated instance">
<TabTitle>Dedicated instance</TabTitle>


|**Name** |**Alarm level** |**Trigger condition** |**Dimension** |**Region** |**Affiliated project** |
|---|---|---|---|---|---|
|[Alarm configuration] StreamingNode CPU utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/StreamingNode CPU usage maximum value \> 70%, lasting 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] StreamingNode CPU utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/StreamingNode node CPU usage maximum value \> 90% in the last 1 cycle, with 1 occurrence meeting the condition within 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] MixCoord Memory utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/MixCoord memory usage maximum value \> 70%, lasting 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] MixCoord Memory utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/MixCoord node Memory usage rate maximum value \> 90% within the last 1 cycle, and the condition is met once within 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] Proxy Memory utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/Proxy node Memory usage maximum value \> 70%, lasting 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] MixCoord CPU utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/MixCoord node CPU usage maximum value \> 70% in the last 1 cycle, with 1 occurrence meeting the condition within 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] MixCoord CPU utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/MixCoord node CPU usage maximum value \> 90% within the latest 1 cycle, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] QueryNode CPU utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/QueryNode node CPU usage maximum value in the last 1 cycle \> 70%, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] QueryNode CPU utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/QueryNode node CPU usage maximum value \> 90% in the last 1 cycle, with 1 occurrence meeting the condition within 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] QueryNode Memory utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/QueryNode node Memory usage maximum value \> 70%, lasting 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] QueryNode Memory usage \- serious |Serious |Single metric alarm: [Serious] Resource/QueryNode node Memory usage maximum value \> 90% within the latest 1 cycle, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] DataNode Memory usage \- Warning |Warning |Single metric alarm: [Warning] Resource/DataNode node Memory usage maximum value \> 70%, lasting 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] DataNode Memory utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/DataNode node Memory usage maximum value \> 90% within the latest 1 cycle, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] IndexNode Memory utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/IndexNode node memory usage rate maximum value \> 70% in the last 1 cycle, with 1 occurrence meeting the condition in 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] IndexNode Memory utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/IndexNode node memory usage maximum value \> 90%, lasting for 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] Proxy CPU utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/Proxy node CPU usage maximum value \> 70%, lasting for 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] Proxy CPU utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/Proxy node CPU usage rate maximum value \> 90% in the last 1 cycle, with 1 occurrence meeting the condition in 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] IndexNode CPU utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/IndexNode node CPU usage maximum value \> 70% in the last 1 cycle, with 1 occurrence meeting the condition within 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] IndexNode CPU utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/IndexNode CPU usage maximum value \> 90%, lasting 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] StreamingNode Memory usage \- Warning |Warning |Single metric alarm: [Warning] Resource/StreamingNode node memory usage maximum value within the last 1 cycle \> 70%, and the condition is met once in 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] StreamingNode Memory utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/StreamingNode node memory usage maximum value \> 90% within the last 1 cycle, with 1 occurrence meeting the condition in 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] DataNode CPU utilization \- Warning |Warning |Single metric alarm: [Warning] Resource/DataNode node CPU usage maximum value \> 70% in the last 1 cycle, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] DataNode CPU utilization \- Serious |Serious |Single metric alarm: [Serious] Resource/DataNode node CPU usage maximum value \> 90%, lasting 1 cycle (1 cycle = 1 minute) |Resource |ALL |default |
|[Alarm configuration] Write Latency P99 \- Warning |Warning |Single metric alarm: [Warning] performance/Write Latency P99 maximum value \> 1000 ms within the last 1 cycle, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Performance |ALL |default |
|[Alarm configuration] Query Latency P99 \- Warning |Warning |Single metric alarm: [Warning] Performance/Query Latency P99 maximum value \> 1000 ms in the last 1 cycle, with 1 occurrence meeting the condition within 1 cycle (1 cycle = 1 minute) |Performance |ALL |default |
|[Alarm configuration] Search Latency P99 \- Warning |Warning |Single metric alarm: [Warning] Performance/Search Latency P99 maximum value within the last 1 cycle \> 1000 ms, and the condition is met once in 1 cycle (1 cycle = 1 minute) |Performance |ALL |default |
|[Alarm configuration] Write Failures \- Warning |Warning |Single metric alarm: [Warning] Performance/Write Failed count maximum value \> 100 in the last 1 cycle, with 1 occurrence meeting the condition in 1 cycle (1 cycle = 1 minute) |Performance |ALL |default |
|[Alarm configuration] Read Failures \- Warning |Warning |Single metric alarm: [Warning] Performance/read failed Quantity maximum value \> 100Count in the last 1 cycle, with 1 occurrence meeting the condition within 1 cycle (1 cycle = 1 minute) |Performance |ALL |default |



</Tab>
<Tab zoneid="IBjaFfJXkp" title="Serverless instance">
<TabTitle>Serverless instance</TabTitle>


|**Name** |**Alarm level** |**Trigger condition** |**Dimension** |**Region** |**Affiliated project** |
|---|---|---|---|---|---|
|[Alarm configuration] Write Failure Count \- Warning |Warning |Single metric alarm: [Warning] Write failure count maximum value \> 100 in the last 1 cycle, with at least 1 occurrence meeting the condition in 1 cycle (1 cycle = 1 minute) |Performance |ALL |default |
|[Alarm configuration] Read Failure Count \- Warning |Warning |Single metric alarm: [Warning] Read Failures count maximum value \> 100 within 1 cycle, with 1 occurrence meeting the condition in 1 cycle (1 cycle = 1 minute) |Performance |ALL |default |
|[Alarm configuration] Write Latency P99 \- Warning |Warning |Single metric alarm: [Warning] Write Latency P99 maximum value \> 1000 ms within the last cycle, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Performance |ALL |default |
|[Alarm configuration] Read Latency P99 \- Warning |Warning |Single metric alarm: [Warning] Read Latency P99 maximum value \> 1000 ms in the last 1 cycle, with 1 occurrence meeting the condition (1 cycle = 1 minute) |Performance |ALL |default |



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To avoid alarm interference, not all preset alarm policies are enabled. Only resource dimension policies are enabled by default; performance dimension policies are disabled by default. You can enable, disable, or edit alarm policies anytime based on business needs. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-an-alarm-strategy">Enable an alarm policy</a>, <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Modifying-an-alarm-strategy">Edit an alarm policy</a>, and <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Disabling-an-alarm-strategy">Disable an alarm policy</a>.</div>


<span id="skDMl59B"></span>
## Precautions


* Only one preset alarm policy group can be created by using alarm configuration in a region. When alarm configuration is enabled, Milvus checks existing alarm policies by policy name. If any are missing or inconsistent, Milvus creates the corresponding preset alarm policies.

* When you enable alarm configuration, Milvus for VectorDB simultaneously creates the "Milvus default alarm contact group" and associates it with preset alarm policies. When an alarm policy is triggered, notifications are sent to contacts in this group.

* The Milvus default alarm contact group does not contain valid alarm contacts upon initial creation. You need to add new alarm contacts and maintain the Milvus default alarm contact group. For more information, see [Create a contact](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group) and [Create a contact group](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact).


<span id="jzQszccz"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. On the top navigation bar, select the target project and region.

3. Click **Alarm management** in the left navigation pane.

4. At the top of the page, click the **Alarm policy** tab.

5. On the **Alarm policy** page, choose either **Dedicated** or **Serverless** as needed, then click **Alarm configuration**, and in the popup click **Enable**.
