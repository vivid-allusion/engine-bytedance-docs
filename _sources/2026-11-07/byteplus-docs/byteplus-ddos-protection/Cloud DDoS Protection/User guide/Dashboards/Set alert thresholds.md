---
title: "Set alert thresholds"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Set_alert_thresholds"
---

To make DDoS alerts more relevant to your business, you can customize the default alert thresholds. This guide shows you how to set custom thresholds for attack peak bandwidth or packet rate, helping you reduce false positives and ensure alerts align with your operational needs.

<span id="c1dae69e"></span>
## Important notes

Set alert thresholds based on your specific business needs, and keep the following in mind:


* If the threshold is set too high, your business may face a higher risk of attacks.

* A lower threshold may cause false positives, resulting in frequent alert notifications.

* You should dynamically adjust the alert threshold to match changing business conditions. For example, for an e\-commerce business, raise the threshold during a new product launch or a large\-scale promotional event to reduce alert noise.


<span id="5ef16a1d"></span>
## Steps


1. Log in to [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select **Cloud DDoS Protection \> Dashboard**.

3. At the top of the page, select the target instance, domain name, and time period.

4. Click **Custom alert threshold** at the top of the DDoS attack event list to configure the threshold for logging attack events and sending alerts. The parameters are described below.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1aa52965b25449e7bd68d8760bcfb751) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Alert configuration |* Default: The system logs the attack event and sends an alert notification when the attack peak exceeds 100 Mbps (or 50,000 pps).<br><br>* Custom threshold: Allows you to set a custom threshold. An attack event is logged and an alert is sent when the attack peak exceeds this value. |
   |Threshold |Allows you to configure a threshold based on either peak attack bandwidth or peak attack packet rate. |
