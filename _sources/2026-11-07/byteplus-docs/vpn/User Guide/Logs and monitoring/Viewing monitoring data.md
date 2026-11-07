---
title: "Viewing monitoring data"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Viewing-monitoring-data"
---

The VPN Connect is integrated with Cloud Monitor, supporting real\-time monitoring of various business metrics for VPN Connect.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IAM user cannot directly view the monitoring data of the VPN Connect product. To view it, the main account must authorize CloudMonitor permission for the IAM user. For detailed operations, refer to <a href="https://docs.byteplus.com/en/docs/vpn/Identity-and-Access-Management-FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf">Why can't the IAM user view monitoring data?</a></div>


<span id=".5qaC6L-w"></span>
## Overview

<span id=".VlBO6L-e5o6l5pWw5o2u55qE55uR5o6n5Yqf6IO9"></span>
### Monitoring features for VPN Connect data


* **Monitor VPN gateways and IPsec\-VPN connection business metrics in real time**.

   Monitor over a dozen metrics related to VPN gateways and IPsec\-VPN connections, such as inbound bandwidth of VPN gateways, outbound bandwidth of VPN gateways, inbound packet rate of IPsec\-VPN connections, and outbound packet rate of IPsec\-VPN connections. You can configure alarm strategies for key VPN Connect by setting alarm metric thresholds and alarm notifications to quickly detect metric anomalies and ensure stable business operation.

* **Real\-time IP traffic monitoring**.

   Displays the top 50 data entries with the highest bandwidth traffic for VPN gateway inbound (peer VPC or IDC to local cloud VPC), VPN gateway outbound (local cloud VPC to peer VPC or IDC), TR\-IPsec connection inbound, and TR type IPsec connection outbound directions. This allows direct viewing of the Top 50 IP addresses and their traffic status during sudden traffic spikes, helping you quickly locate and analyze issues.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Top 50 IPs shown in real\-time traffic monitoring are <strong>cloud IPs</strong>. For VPN gateway inbound direction, the top 50 <strong>destination IPs</strong> rankings are displayed, while for VPN gateway outbound direction, the top 50 <strong>source IPs</strong> rankings are shown.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Destination IP: The IP address on the peer VPC or local IDC accessible from the local VPC through the IPsec\-VPN connection.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Source IP: The IP address on the local VPC accessible from the peer VPC or local IDC through the IPsec\-VPN connection.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When multiple IPsec\-VPN connections are established under the same VPN gateway, the real\-time traffic monitoring shows the aggregated traffic of all IPsec\-VPN connections under that VPN gateway.   </div>
   


<span id=".VlBO6L-e5o6l5pWw5o2u55qE55uR5o6n5L-h5oGv"></span>
### VPN Connect monitoring data 


|Attachment type |Attach type |Data monitoring types |Monitoring metrics |
|---|---|---|---|
|IPsec\-VPN connection |VPN gateway |* VPN gateway data monitoring<br><br>* IPsec\-VPN connection data monitoring<br><br>* IP traffic monitoring |* VPN gateway inbound bandwidth, VPN gateway outbound bandwidth, VPN gateway inbound packet rate, VPN gateway outbound packet rate, VPN gateway inbound traffic, VPN gateway outbound traffic, VPN gateway inbound packets, VPN gateway outbound packets, VPN gateway outbound bandwidth utilization, VPN gateway inbound bandwidth utilization, VPN gateway SSL max connections.<br><br>* IPsec\-VPN connection inbound packet rate, outbound packet rate, inbound bandwidth, and outbound bandwidth.<br><br>* Top 50 resources for VPN gateway outbound to cloud, top 50 resources for VPN gateway inbound from cloud. |
||Transit Router |* IPsec\-VPN connection data monitoring<br><br>* IP traffic monitoring |* IPsec\-VPN connection inbound packet rate, outbound packet rate, inbound bandwidth, and outbound bandwidth.<br><br>* Top 50 resources for TR\-IPsec connection inbound to cloud, and top 50 resources for outbound to cloud. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>The collection objects and methods differ among metrics; some metrics collect encapsulated traffic while others collect original traffic before encapsulation. For details, see the description sections in </strong><a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_VPN"><strong>VPN connection monitoring metrics</strong></a><strong> and </strong><a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_IPsec"><strong>IPsec connection monitoring metrics</strong></a><strong>.</strong></div>


<span id=".5p-l55yL55uR5o6n5pWw5o2u"></span>
## Viewing monitoring data

<span id=".VlBO6L-e5o6l5o6n5Yi25Y-w5p-l55yL"></span>
### View data via the VPN Connect console


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click **VPN Gateway** or **VPN Connection** in the left navigation pane to enter the target resource console.

4. Click the **monitor** icon in the target resource's row to access the monitoring data page.

5. On the **data monitoring** page, view various monitoring metrics data.

   * **VPN gateway**

      Switch tabs to view monitoring data related to the VPN gateway, IPsec\-VPN connection, and IP traffic monitoring.

   * **IPsec\-VPN connection**

      If the IPsec\-VPN connection is attached to a TR, switch to the **IP traffic monitoring** tab to view the related monitoring data.


<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
### View data via the Cloud Monitor console

View VPN gateway and IPsec\-VPN connection monitoring data in the Cloud Monitor console. For detailed steps, see [View cloud product monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy): Create an alarm strategy to monitor the data status of resources related to the VPN connection. To configure an alarm strategy for VPN gateway bandwidth limit, choose monitoring metrics that include packet encapsulation overhead as the trigger condition, such as VPN gateway outbound bandwidth utilization rate or VPN gateway inbound bandwidth utilization rate.

* [Create alarm template](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-template): Create an alarm template for quick creation of alarm strategies later.

* [Cloud product event](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-events): Monitor cloud product events to promptly track status changes and exceptions, ensuring business health and stability.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateRule): Create an alarm strategy.

* [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData): Query time\-series data aggregated for specified metrics within the specified period.
