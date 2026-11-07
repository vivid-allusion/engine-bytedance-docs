---
title: "Viewing monitoring data"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Viewing_monitoring_data"
---

IPv6 Gateway supports real\-time monitoring of all service metrics through CloudMonitor. Through customizable metric thresholds and alert notifications, anomalies are detected promptly to ensure stable business operations. For details on specific monitoring metrics of the IPv6 Gateway and IPv6 Internet bandwidth, see [Monitoring metrics of IPv6 Gateway](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_Ipv6Gateway) and [Monitoring Metrics of IPv6 Internet bandwidth](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_Ipv6AddressBandwidth).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IAM users cannot directly view IPv6 Gateway monitoring data. To view it, the main account of the IAM user must grant CloudMonitor permissions to the IAM user. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/IPv6/FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf">Why can't IAM users view monitoring data</a>.</div>


<span id=".5p-l55yLSVB2Nue9keWFs-ebkeaOpw=="></span>
## View IPv6 Gateway monitoring data

<span id=".SVB2Nue9keWFs-aOp-WItuWPsOafpeeciw=="></span>
### View data via the IPv6 Gateway console


1. Log in to [the IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fed8c20937b7c69e69997eca49fb2c3.png) </span>monitor icon in the **Monitor** column of the target IPv6 Gateway, and the Data monitoring window will pop up.

4. In the Data monitoring window, you can view all monitoring metric data of the IPv6 Gateway.

   * Monitor IPv6 Gateway metrics for both directions: outbound/inbound traffic volume, packet count, bandwidth, packet rate, and rate limit for packet loss.

   * Click the **Period** and **Method** (default, average, maximum, minimum, and sum) dropdowns to customize the monitoring data display.

   * Click the **Legend** dropdown on the right side of the page **, ** and select **Table** to view the extremes of each monitoring metric.


<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
### View data via the Cloud Monitor console

To view monitoring data of an IPv6 Gateway in the Cloud Monitor console, see [Viewing cloud service monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor) for detailed steps.

<span id="7NyE085d"></span>
## View IPv6 Internet bandwidth monitoring data

<span id="iTwPmVpB"></span>
### View data via the IPv6 Gateway console


1. Log in to [the IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. Click the name of the target IPv6 Gateway and select the **IPv6 Internet bandwidth** tab.

4. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fed8c20937b7c69e69997eca49fb2c3.png) </span>monitor icon in the **Monitor** column of the target IPv6 Gateway to pop up the Data monitoring window.

5. You can view all monitoring metric data of the IPv6 Internet bandwidth in the Data monitoring window.

   * Monitor IPv6 Internet bandwidth metrics for both directions: outbound/inbound traffic volume, packet count, bandwidth, packet rate, bandwidth utilization, and rate\-limit induced packet loss rate.

   * Click the **Period** and **Method** (default, average, maximum, minimum, and sum) dropdowns to customize the monitoring data display.

   * Click the **Legend** dropdown on the right side of the page **, ** and select **Table** to view the extremes of each monitoring metric.


<span id="KUBVCz3T"></span>
### View data via the Cloud Monitor console

View IPv6 Internet bandwidth monitoring data in the CloudMonitor console. For procedure, see [Viewing cloud product monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor).
