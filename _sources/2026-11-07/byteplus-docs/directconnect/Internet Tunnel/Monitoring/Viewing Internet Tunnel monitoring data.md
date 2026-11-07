---
title: "Viewing Internet Tunnel monitoring data"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/View_Internet_Tunnel_monitoring_information"
---

The Internet Tunnel (IT) is now integrated with CloudMonitor, supporting real\-time monitoring of key business metrics of the IT Bandwidth and the IT Virtual Interface. You can configure alarm strategies for critical services, set thresholds for alert metrics, and define notification rules. This allows you to be promptly informed of metric exceptions, ensuring stable service operation. For details of specific Internet Tunnel monitoring metrics, access [Internet Tunnel Bandwidth](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_InternetTunnelBandwidth) and [Internet Tunnel Virtual Interface](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_InternetTunnelVirtualInterface).

<span id=".5LqS6IGU572R6YCa6YGT5o6n5Yi25Y-w5p-l55yL"></span>
## View data via the Internet Tunnel console


1. Log in to the [Internet Tunnel console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the target region.

3. Access the monitoring data page.

   * **Internet Tunnel Bandwidth**:

      1. In the left\-side navigation pane, select **IT Gateway**.

      2. In the IT Gateway list, click the name of the target IT Gateway.

      3. Click the **IT Bandwidth** tab on the details page.

      4. In the IT Bandwidth list, click the<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_542a28104606682d84fb33e2b6c1c723.png) </span> icon of the target IT Bandwidth, and view the monitoring data in the **Data monitoring** panel that pops up on the right.

   * **Internet Tunnel Virtual Interface**:

      1. In the left\-side navigation pane, select **IT Virtual Interface**.

      2. In the IT Virtual Interface list, click the<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_542a28104606682d84fb33e2b6c1c723.png) </span> icon of the target IT Virtual Interface, and view the monitoring data in the **Data monitoring** panel that pops up on the right.

4. In the **Data monitoring** panel, you can view various monitoring metrics for the current IT Bandwidth and IT Virtual Interface.

   * **Monitoring metrics for IT Bandwidth**: Inbound/outbound traffic, inbound/outbound packet count, inbound/outbound bandwidth, inbound/outbound packet rate, inbound/outbound rate\-limiting packet loss rate, and inbound/outbound bandwidth utilization.

   * **Monitoring metrics for IT Virtual Interface**: Network inbound/outbound bandwidth, network inbound/outbound traffic, network inbound/outbound packet rate, and interface operational status.


<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
## View data via the Cloud Monitor console

View the monitoring date of IT Bandwidth and IT Virtual Interface in the Cloud Monitor console. For procedure, see [View Cloud Service Monitoring Data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData): Query time\-series data aggregated for specified metrics within a specified period.
