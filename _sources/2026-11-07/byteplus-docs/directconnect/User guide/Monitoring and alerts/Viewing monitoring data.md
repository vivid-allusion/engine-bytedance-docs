---
title: "Viewing monitoring data"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Viewing-the-indicator-monitoring-data"
---

Direct Connect (DC) has integrated with Cloud Monitor, supporting real\-time monitoring of business metrics for DC Connection, DC Gateway, Global Direct Exchange Gateway (DXGW), and Virtual Interface. You can configure alarm strategies, set alert thresholds for metrics, and define notification rules. This allows you to be promptly informed of metric exceptions, ensuring stable service operation. For detailed monitoring metrics of Direct Connect, see [Direct Connect metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectConnectConnection), [Direct Connect Gateway metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectConnectGateway), [Global Direct Exchange Gateway metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectExchangeGateway), [Virtual Interface metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectConnectVIF), [QoS management metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectConnectQoSQueue), and[Health check metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectConnectHealthCheck).

<div data-tips="true" data-tips-type="tip">Note</div>


<div data-tips="true" data-tips-type="tip">Identity and Access Management (IAM) users cannot directly view DC monitoring data. To view it, the IAM user needs to be granted CloudMonitor permissions by its root account. For procedure, see <a href="https://docs.byteplus.com/en/docs/directconnect/IAM_FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf">Why can't IAM users view monitoring data</a>.</div>


<span id=".5LiT57q_6L-e5o6l5o6n5Yi25Y-w5p-l55yL"></span>
## View data via the Direct Connect console


1. Log in to the[ Direct Connect console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select the region where the target DC is located.

3. Select and enter the instances page of the target feature.

   * **DC Connection**/**DC Gateway**/**DXGW**/**Virtual Interface**/**health check**: In the left navigation pane, select **DC Connection**/**DC Gateway**/**Direct Exchange Gateway**/**DC Virtual Interface**/**Health Check**, then click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_307c6187a7a3ad73387e65985a1d22a4.png) </span> monitor icon of the target instance.

   * **QoS policy**: In the left navigation pane, select **QoS Policy**. Click the name of the target policy, select the **Traffic queue** tab, and click the target queue's <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_307c6187a7a3ad73387e65985a1d22a4.png) </span>monitor icon.

4. On the **Data monitoring** page, you can view various metric monitoring data of the instance.

   * Monitoring metrics for DC Connection include port connection status, inbound/outbound bandwidth, inbound/outbound packet rate, port error packets, inbound/outbound bandwidth utilization.

   * Monitoring metrics for DC Gateway include inbound/outbound bandwidth, inbound/outbound traffic, inbound/outbound packet rate.

   * DXGW monitoring metrics include:

      * Layer 2 interconnection: Inbound/outbound bandwidth between access points, rate\-limited packet loss rate between access points.

      * Layer 3 interconnection: Inbound/outbound rate to/from DXGW, inbound/outbound packet count to/from DXGW, inbound/outbound traffic volume to/from DXGW.

   * Monitoring metrics for DC Virtual Interface include inbound bandwidth, outbound bandwidth, inbound traffic, outbound traffic, inbound packet rate, outbound packet rate, interface status, limited bandwidth.

   * Monitoring metrics for QoS management include average bandwidth rate and average packet loss rate of the QoS traffic queue.

   * Monitoring metrics for health check include packet loss rate and average delay.


<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
## View data via the Cloud Monitor console

View monitoring data of DC Connections, DC Gateways, DXGWs and Virtual Interfaces, QoS management, and health checks on the Cloud Monitor console. For procedure, see [Viewing cloud product monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData): Query time\-series data aggregated for specified metrics within a specified period.
