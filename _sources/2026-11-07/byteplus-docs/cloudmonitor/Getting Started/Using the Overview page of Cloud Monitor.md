---
title: "Using the Overview page of Cloud Monitor"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Vitality-Cloud-Monitor-overview"
---

Cloud Monitor provides alert and monitoring dashboards, which display statistics on alerts and the health status of each cloud product. This helps you understand the alert status across all regions within the current account in real time, as well as the alert situation and total number of resources for each cloud product, thus managing resources from a global perspective and promptly making adjustments.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview). 

2. Go to the **Overview** page as shown in the following figure.


<span id=".5ZGK6K2m5qaC6KeI"></span>
## Alert overview

This section displays the total number of resource instances in the **Alerting** state and the number of resource instances at different alert levels, which include **Critical, Warning, and Notice** in all regions within the current account.

If you click the number of instances at a specific level, you are redirected to the **Alert history** page, where instances at the specific level will be automatically displayed in the list. For details, see [Viewing alert records](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history).

<span id="34a6887f"></span>
### Top 5 alert policies in recent 7 days

This section displays the total number of alerts triggered by each alert policy in the last 7 days, and displays brief information about the top five policies with the most alerts, including the alert level, name, resource type, and the number of alerts.

Click the name of the target policy to go to the **alert policy** details page, where you can view details about the alert policy, such as the basic information, alert object, alert rule, and notification method.

<span id=".6L-RN-aXpeWRiuitpuaWsOWinui2i-WKvw=="></span>
### Trend of new alerts in recent 7 days

This section displays the number of new alerts added each day in the last 7 days. The line chart can help you understand the alert trend within the current account.

<span id=".5LqR5Lqn5ZOB5YGl5bq354q25oCB"></span>
### Cloud product health status

Cloud products are categorized by product type, and all products are displayed by default. This section displays the total number of resource instances and alert resources for each cloud service across all regions within the current account. This helps you quickly understand your asset situation and alert status.

You can click a specific product category to quickly retrieve the total number of resource instances and alert resources for each cloud product across all regions within the current account.

Click a cloud product card to go to the monitoring page for the product. For details, see [Viewing cloud product monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor).

<span id="e49c5bbe"></span>
## Alert history

The Alert history section displays alert records that are automatically generated after cloud product resource instances trigger alerts. The records include the resource type, affected resource, dimension, and alert level.

Click Details to go to the **alert record** details page to view basic alert information and alert record details. Basic information includes the time at which the alert was triggered, duration of the alert, alert level, alert policy name, and other information. This allows you to efficiently view and review alert records in a centralized manner.

<span id="3c57155a"></span>
## Cloud product event

The Cloud product event section displays the event occurrence time, event source, and events. By monitoring events for relevant cloud products, you can promptly track status changes and exceptions, maintaining the health and stability of business applications.
