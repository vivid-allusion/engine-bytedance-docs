---
title: "Viewing traffic analysis data"
product: "Network Detection and Response"
product_code: "nta"
source: "https://docs.byteplus.com/en/docs/nta/Viewing-traffic-analysis-data"
---

The Traffic Center provides comprehensive analysis of all non\-attack traffic to your protected assets. This guide shows you how to use the Traffic Center to view risky internet\-facing ports and analyze outbound connection behaviors. By following the steps, you can effectively identify potential security threats, trace attack sources, and inspect for policy violations.

<span id="c096954c"></span>
## Viewing risky ports

The risky port page displays all your risky ports that are exposed to the internet. Once a cloud asset opens a port for internet access, internet IP addresses can access the asset, which is convenient but also entails a risk of intrusion. Therefore, you should minimize the number of exposed ports or protect them with security controls, such as cloud firewalls, to ensure secure access.


1. Log in to the NDR console.

2. Select **Analysis center** ＞ **Traffic analysis** on the left side of the page.

3. Select the **Risk port** tab to view the data and list of risky ports.

4. If you confirm that a risky port is still needed to provide external services, click **Add allowlist** to exclude this traffic from detection.

   Once a risky port is added to an allowlist, NDR won't detect the traffic to this port.


<span id="613c6a01"></span>
## Viewing outbound connection analysis

The outbound connection page displays all outbound connections from your assets. You can use this information to identify policy violations or other abnormal activity.


1. Log in to the NDR console.

2. Select **Analysis center** ＞ **Traffic analysis** on the left side of the page.

3. Select the **Outbound analysis** tab to view the data and list of risky assets with outbound traffic.

   The outbound traffic details are aggregated by access source IP address and destination IP address. You can view outbound traffic details between two IP addresses, including details such as the source IP address, destination service, connection count, traffic volume, time, and protocol.

4. Click **Detail** to view the log details of outbound actions.
