---
title: "View details of DDoS attack protection"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/View_dashboard_details"
---

The traffic report page provides detailed security data for your Cloud DDoS Protection instances, helping you monitor security posture and analyze attack patterns to verify protection effectiveness. Use this page for routine security audits or to investigate specific incidents after receiving an attack alert. This document guides you through accessing the traffic report and interpreting its key metrics, charts, and event details.

<span id="c3341d3a"></span>
## Prerequisites

You have added an EIP to your Cloud DDoS Protection (Premium Edition) instance.

<span id="573cab92"></span>
## Procedure


1. Log in to the [Cloud DDoS Protection console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select **Native DDoS protection\>Traffic report**.

3. At the top, select the Cloud DDoS Protection (Premium Edition) instances and the time range you want to view.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you select an instance, all domains protected by it are displayed by default.   </div>
   

4. View the data and reports.

   * **Data overview**: Displays the number of protected IPs, peak traffic, peak service packet rate, and the number of attacks on the selected instance within the selected time period.

   * **Trend chart**: Displays the inbound traffic and business traffic trends of the selected instance within the selected time period. Hover over a node to view its value at that point in time.

   * **DDoS attack event**: Displays details of attack events for the current instance within the selected time period.

      
      |Parameters |Description |
      |---|---|
      |Protected IP |The IP addresses of the protected EIP instances. You can filter attack events by IP address. |
      |Attack types |The type of attack. |
      |Status |Current attack status, including **Ended** and **Attacking**. |
      |Start time |The start time of the attack. |
      |End time |The end time of the attack. |
      |Duration |The duration of the attack. |
      |Attack bandwidth (Peak) |The maximum attack bandwidth during the attack duration. |
      |Attack packet rate (Peak) |The maximum attack packet rate during the attack duration. |
      |Actions |Click **Details** to view specific information about the attack event. |
      


<span id="98718ab2"></span>
## Optional actions

<span id="6492b0cf"></span>
### View attack event details

Viewing attack event details provides basic information, an event overview, and attack data to help you analyze the attack's characteristics and choose effective protection measures.

<span id="cc93efc4"></span>
### Set a custom threshold

By default, the platform records attack events and sends alert notifications when it detects that an attack peak exceeds 100 Mbps or 50,000 pps. You can also set custom alert thresholds for individual instances. For more information about setting custom thresholds, refer to [Set alert thresholds](https://docs.byteplus.com/docs/byteplus-ddos-protection/Set_alert_thresholds).
