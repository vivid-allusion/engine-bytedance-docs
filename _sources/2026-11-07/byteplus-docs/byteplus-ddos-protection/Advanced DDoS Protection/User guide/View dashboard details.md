---
title: "View dashboard details"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-viewing-ddos-attack-protection-information"
---

The DDoS attack protection dashboard presents statistical data regarding bandwidth and DDoS attack incidents. It enables you to monitor bandwidth trends and examine the specifics of each attack incident. Based on the DDoS protection data of the instance, you can modify the DDoS protection policy to achieve accurate protection and enhance the security level of your assets.

<span id="e624da15"></span>
## Before you begin

Subscribe to BytePlus Advanced DDoS Protection.

<span id="b5a79ee1"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Dashboard**.

3. Select the **DDoS attack protection** tab.

4. Select your instance and set the time duration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can select a single instance or all instances.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system can display data from the last hour, the past 24 hours, the last 7 days, and the last 30 days. Additionally, you can customize a time range of up to 90 days within the previous 180 days.   </div>
   

5. View the statistical data and trend charts.

   * **Overview**: The overview data displays Attack bandwidth(Peak), Back\-to\-origin bandwidth(Peak), Outbound bandwidth(Peak), and the number of DDoS attacks within the selected time range.

      * **Attack bandwidth(Peak)** : The maximum attack bandwidth from the client to the instance.

      * **Back\-to\-origin bandwidth(Peak)** : The maximum bandwidth from the instance to your origin server.

      * Outbound bandwidth(Peak): The maximum bandwidth from the origin server passing through the instance and returned to the client.

      * DDoS attack: The total number of detected DDoS attacks.

   * **Bandwidth trend**: The chart shows the bandwidth changes within the selected time range, including back\-to\-origin bandwidth and outbound bandwidth.

   * DDoS attack event: The list provides detailed information about each DDoS attack, including the type of attack, current status, start and end times, duration, and maximum attack bandwidth.


<span id="f763f020"></span>
## Related operations

By default, the platform logs attack events and sends an alert to your account when the attack traffic exceeds 100 Mbps. You can customize a threshold value to receive alerts only for DDoS attacks that exceed a specific bandwidth.

On the Dashboard page, select an instance, and click Custom alarm threshold to configure the threshold.
