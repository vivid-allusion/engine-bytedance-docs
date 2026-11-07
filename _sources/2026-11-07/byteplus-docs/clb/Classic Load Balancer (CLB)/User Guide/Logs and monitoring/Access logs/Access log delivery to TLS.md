---
title: "Access log delivery to TLS"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Access-Log-Delivery-to-TLS"
---

This topic introduces how to deliver the access logs of the Layer 7 (HTTP/HTTPS) listener to the Torch Log Service (TLS).

> **warning**

> This feature does not apply to HTTP/HTTPS requests on Layer 4 TCP listeners.

## Enable the access log feature

### Action description

* Ensure that the CLB has created an HTTP or HTTPS listener. If not created, see [Creating an HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener) or [Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener).

* Torch Log Service (TLS):

   * Make sure you have enabled Torch Log Service (TLS),  and created a log project and log topic.

   * **After enabling the access log delivery to TLS feature, the log topic will default to key\-value index configuration, which will overwrite the original index configuration of the log topic. Proceed with caution.**

   * Please properly plan log service resources and use clear naming to avoid accidentally deleting access log resources in the log service console.

* After enabling the access log delivery to TLS feature, it will take approximately 1 minute for log data to be collected and uploaded to the log service before it becomes available for viewing.

### Procedures

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target CLB instance name.

4. On the Access Log Analysis (7 Layers) tab, click Instant configuration.

5. Turn on the **Access Log Delivery TLS** switch and select the log project and log topic.

6. Click **Configure** to complete the action.

## View and modify the index

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target CLB instance name.

4. In the Access Log Analysis (7 Layers) tab, click Index configuration on the right.

5. View the key\-value index configured by the system by default. You can also modify it as needed.

## Analyze access log

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target CLB instance name.

4. In the Access Log Analysis (7 Layers) tab, input the search and analysis statement.

   A search and analysis statement consists of a search statement and an SQL analysis statement, separated by a pipe symbol (|). This syntax indicates that data statistics and analysis are performed on the results that match the search conditions.

5. Click **Search** to view the analysis results Displayed in charts.

## Disable the access log feature

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. In the Access Log Analysis (7 Layers) tab, click Edit configuration on the right to open the configuration window.

5. Disable the switch for Access Log Delivery TLS.

6. Click **Configure** to complete the action.

## Related documents

* [EnableAccessLog](https://docs.byteplus.com/en/docs/clb/EnableAccessLog)

* [DisableAccessLog](https://docs.byteplus.com/en/docs/clb/DisableAccessLog)
