---
title: "Alert overview"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Alert_overview"
---

The alert overview aggregates alert data across the Cloud Monitor, VMP, and Server\-side Monitoring product lines. It provides a clear view of overall failure risks and alert sources. Alert trends help identify alert surges and changing patterns, enabling O&M personnel to quickly understand the overall alert landscape, troubleshoot issues more efficiently, reduce alert noise, and support routine O&M governance. This topic describes how to view the alert overview dashboard.

<span id="lfVODyGJ"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select **Alert Center \-\> Alert overview** to go to the "Alert overview" page.

3. Filter the data by product, alert type, and region.

   
   |Serial number |Filter item |Description |
   |---|---|---|
   |1 |Product filter |Filters data by product. Products currently supported in the alert overview include Cloud Monitor, VMP, and Server\-side Monitoring. |
   |2 |Switch dashboard |Filters data by alert type. Two dashboards are currently available: "Alerting" and "Historical dashboard".<br><br><br>* Alerting: Shows only data for active alerts, mainly displaying metric data from the last 24 hours.<br><br>* Historical dashboard: Shows data for up to the past two weeks and supports filtering by a relative or absolute time range. |
   |3 |Region filter |Filters data by region. |
   

4. After applying the filters, view the "Alert overview" dashboard.

   
   |Metric |Description |
   |---|---|
   |Total active alerts |The total number of active alerts and the total number of alerts that have not recovered. This helps you quickly assess the overall scale of failures and determine whether the system is in an abnormally high\-risk state. |
   |Active alerts by product |The number of active alerts by product. This helps you quickly identify which products are affected by the failure and assign response responsibilities by business unit. |
   |New alert trend (last 24h) |A trend chart of newly added alerts in the last 24 hours. Use alert growth trends to determine whether failures occur suddenly or worsen gradually and to evaluate remediation effectiveness. |
   |Top 10 alert regions (last 24h) |The top 10 regions by alert volume in the last 24 hours. This helps you quickly identify data center\- or region\-level failures and distinguish localized failures from global failures. |
   |Top 10 alert policies (last 24h) |The top 10 alert rules by alert volume in the last 24 hours. This helps you identify high\-frequency alert rules, distinguish real failures from alert storms, and optimize alert rules for noise reduction.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click an alert policy name to go to the alert rule details page for more information.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>View</strong> in the "Actions" column for the target policy to go to the alert event page and view the alert history related to the current alert.</div><br> |
   |Top 10 cloud product alerts (last 24h) |The top 10 cloud products by alert volume in the last 24 hours. This helps the O&M team identify the underlying cloud components associated with the failure and quickly locate the resources causing it.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click the target cloud product name or <strong>View</strong> in the "Actions" column to go to the alert event page and view the alert history for that cloud product.</div><br> |
   |Top 10 cloud product events (last 24h) |The top 10 cloud products by event volume in the last 24 hours. Correlate event and alert data to determine whether alerts were triggered by O&M changes, helping you prevent change\-induced failures.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click the target cloud product name or <strong>View</strong> in the "Actions" column to go to the alert event page and view the event history for that cloud product.</div><br> |
   |Total alerts |The total number of alerts and the total number of alerts that have not recovered within the specified time range. This reflects the overall alert volume during the period and is used for failure scale assessment and O&M health evaluation. |
   |Alerts by product |The number of alerts triggered by each product within the specified time range. This helps you measure alert frequency across business cycles, quantify product stability, and prioritize improvements for less stable products. |
   |Alert trend |A trend chart of triggered alerts within the specified time range. Review historical alert fluctuation patterns to identify periodic failures and failure risks during business peak hours. |
   |Top 10 alert regions |The top 10 regions by alert volume within the specified time range. This helps you identify regions with persistently high failure rates and provides a basis for data center expansion and regional O&M resource allocation. |
