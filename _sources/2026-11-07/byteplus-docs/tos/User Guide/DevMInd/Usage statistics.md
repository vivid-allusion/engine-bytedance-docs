---
title: "Usage statistics"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Usage-statistics"
---

Usage statistics is ideal for routine inspections and quick comparisons. It allows you to view basic metric trends for buckets in time\-series line charts. These metrics include storage and retrieval capacity, as well as request status codes. You can observe them within a time range from one hour to 30 days. This topic describes the metrics available in this module and explains how to view them.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Usage statistics is currently in closed beta. Please contact your account manager for access.</div>


<span id="2o27hUfR"></span>
## Notes


* The underlying data comes from Cloud Monitor, so there is a delay in the data statistics. This information is intended for monitoring purposes only and should not be used for metering references.

* To view usage statistics, you must have read\-only access to Cloud Monitor. For authorization steps, see [Granting read-only access to Cloud Monitor](https://docs.byteplus.com/docs/tos/Grant_read-only_permission_for_account_cloud_monitoring).


<span id="QBKQt8Vr"></span>
## Viewing bucket usage statistics


<Tabs>
<Tab zoneid="DfXh9SWS" title="From DevMind">
<TabTitle>From DevMind</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the **DevMind** page, click **Usage statistics** in the left navigation pane.

4. On the **Usage statistics** page, you can view **basic data** and **request status code**.


</Tab>
<Tab zoneid="tiV62ssI" title="From Overview">
<TabTitle>From Overview</TabTitle>

The **Overview** page provides a comprehensive view of the total usage of all buckets.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Overview**. In the **Usage overview** section, view the TOS storage usage by storage type.


</Tab>
</Tabs>


<span id="nSLU2Dd2"></span>
## View options

On the Basic data/Status codes page, you can configure the following sections to change the views.


|Section |Description |
|---|---|
|Time range |You can select one hour, six hours, one day, seven days, or 30 days, and you can also customize a time range. |
|Radio mode |The line chart has a **radio mode** that simplifies the view by displaying one metric at a time. When this mode is enabled, clicking a legend below the chart shows only the corresponding metric curve. To switch to a different metric, click a different legend. To return to the full view, double\-click the currently selected legend.<br><br>You can configure this section when viewing **basic data**. |
|Metric |Select status code metrics from the drop\-down list. Each selected metric corresponds to a line chart. |


<span id="T6XIE8yn"></span>
## Supported metrics

TOS provides visibility to the following data.


|**Category** |**Description** |
|---|---|
|Storage capacity |Specifies the raw and billable capacities by storage type within a given time period. You can change the reference period at the top of the page. The details are as follows:<br><br><br>* Raw Capacity: The actual physical storage space used by a given storage type.<br><br>* Billing Capacity: The amount of storage space billed for a given storage type.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A minimum charge applies to objects in Standard Storage, Infrequent Access Storage, Flashback Archive, Archive, Cold Archive, and Deep Cold Archive based on object size. Objects smaller than 64 KiB are charged as if they were 64 KiB. If you store objects smaller than 64 KiB in Infrequent Access Storage, Flashback Archive, Archive, or Cold Archive, the billing capacity will exceed the raw capacity.   </div><br>    |
|Retrieve Capacity |Specifies the volume of data retrieved over a given period. The details are as follows:<br><br><br>* IA storage data retrieval capacity: Retrieval of data from TOS when the client accesses objects in Infrequent Access Storage.<br><br>* Flashback Archive data retrieval capacity: Retrieval of data from TOS when the client accesses objects in Flashback Archive.<br><br>* Archive storage data retrieval capacity: Data retrieval when restoring objects from Archive.<br><br>* Cold Archive quick retrieve capacity: Data retrieval when restoring objects from Cold Archive in quick retrieval mode.<br><br>* Cold Archive standard retrieval capacity: Data retrieval when restoring objects from Cold Archive in standard retrieval mode.<br><br>* Cold Archive batch retrieval capacity: Data retrieval when restoring objects from Cold Archive in batch retrieval mode.<br><br>* Deep Cold Archive Standard Retrieval Capacity: Data retrieval when restoring objects from Deep Cold Archive in standard retrieval mode.<br><br>* Deep Cold Archive batch retrieval capacity: Data retrieval when restoring objects from Deep Cold Archive in batch retrieval mode. |
|Traffic |Specifies the volume of data transferred under different scenarios over a given period. The details are as follows:<br><br><br>* Outflow Traffic from Public Network: Data transfer out from TOS to internet clients.<br><br>* Public Network Inflow Traffic: Data transfer in from internet clients to TOS.<br><br>* Intranet Outflow Traffic: Data transfer out from TOS to BytePlus clients.<br><br>* Intranet Inflow Traffic: Data transfer in from BytePlus clients to TOS.<br><br>* CDN Back\-to\-Origin Outflow Traffic: Data downloads from TOS to BytePlus's Content Delivery Network (CDN) via an accelerated domain name.<br><br>* CDN Back\-to\-Origin Inflow Traffic: Data uploads from CDN to TOS via an accelerated domain name.<br><br>* CRR Traffic: Data transfer when replicating data across buckets in different regions via cross region replication (CRR) rules.<br><br>* Transfer Acceleration Inflow Traffic (Chinese mainland to Chinese mainland).<br><br>* Transfer Accelerated Outflow Traffic (Chinese mainland to Chinese mainland).<br><br>* Transfer Accelerated Inflow Traffic (outside Chinese mainland to Chinese mainland):<br><br>* Transfer Accelerated Outflow Traffic (outside the Chinese mainland to Chinese mainland)<br><br>* Transfer Accelerated Inflow Traffic (Chinese mainland to outside Chinese mainland).<br><br>* Transfer Accelerated Outflow Traffic (Chinese mainland to outside Chinese mainland).<br><br>* Transfer Accelerated Inflow Traffic (outside Chinese mainland to outside Chinese mainland).<br><br>* Transfer Accelerated Outflow Traffic (outside Chinese mainland to outside Chinese mainland). |
|Number of requests |Specifies the total number of write and read requests in the bucket within a given time period. |
