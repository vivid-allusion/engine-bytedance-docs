---
title: "Viewing alert events"
product: "Network Detection and Response"
product_code: "nta"
source: "https://docs.byteplus.com/en/docs/nta/Viewing-alert-events"
---

To monitor and respond to security threats detected by Network Detection and Response (NDR), you can use the alert section to view and analyze security events in real time. This guide explains how to access alert statistics, trends, and detailed lists, and how to handle them to ensure your data security.

<span id="38e980ad"></span>
## Prerequisites

Risk detection is already enabled for your assets.

<span id="b6a25d52"></span>
## Procedure


1. Log in to the NDR console.

2. Select **Threat center** \> **Alarm perspective** on the left side of the page.

3. View alert information.

   Alert data in the last 24 hours is displayed by default. You can change the time range in the upper\-right corner of the page.

   * Alert statistics: This section provides statistics for different alert types based on the number of alerts. You can sort security events by the number of alerts in descending order and collapse or hide certain alerts.

   * Alert trend:You can view the alert trend in real time and select a day with an abnormal number of alerts for targeted analysis. You can also collapse and hide certain alerts.

   * Alert list: The alert list includes details such as the time of the last occurrence, threat type, attack status, risk level, asset IP address, external IP address, port, protocol, attack direction, HTTP status code, and processing status.

4. Click a threat type in the list to open its alert details page.

   You can view all events of this alert type and follow the suggested solution to resolve them.

   * Handled manually: Manually resolve the alert based on the provided suggestions, and then mark it as handled.

   * Add to allowlist: Add the source and destination IP addresses and destination port to the allowlist. Once this rule is configured, traffic from the source IP address to the specified destination IP address and port will not be inspected.
