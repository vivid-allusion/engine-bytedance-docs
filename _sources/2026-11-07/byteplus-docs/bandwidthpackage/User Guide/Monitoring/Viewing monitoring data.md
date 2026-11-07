---
title: "Viewing monitoring data"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Viewing-monitoring-data"
---

You can view monitoring data through the Bandwidth Package console or the Cloud Monitor console. For details on specific monitoring metrics of the Bandwidth Package, see [Monitoring metrics of Bandwidth Package](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_BandwidthPackage).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Identity and Access Management (IAM) users cannot directly view monitoring data of Bandwidth Package. To view it, the IAM user needs to be granted CloudMonitor permissions by its root account. For specific procedure, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf">Why can't IAM users view monitoring data</a>.</div>


<span id=".5YWx5Lqr5bim5a695YyF5o6n5Yi25Y-w5p-l55yL"></span>
## View data via the Bandwidth Package console

<span id=".5p-l55yL5YWx5Lqr5bim5a695YyF55uR5o6n5oyH5qCH"></span>
### View monitoring data of Bandwidth Package

You can view monitoring data of Bandwidth Package within a specific period by this procedure.


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fed8c20937b7c69e69997eca49fb2c3.png) </span>monitor icon in the **Monitor** column of the target Bandwidth Package, and the Data monitoring window will pop up.

4. On the **Data monitoring \> instance** tab, you can view the monitoring metric data of the current Bandwidth Package.

   * Supports viewing Bandwidth Package metrics, such as inbound/outbound traffic, inbound/outbound data packets, inbound/outbound bandwidth, inbound/outbound packet rate, inbound/outbound rate\-limiting packet loss rate, and inbound/outbound bandwidth utilization.

   * Click the **Period** and **Method** (default, average, maximum, minimum, and sum) dropdowns to customize the monitoring data display.

   * Click the **Legend** dropdown on the right side of the page **, ** and select **Table** to view the extremes of each monitoring metric.


<span id=".5p-l55yLSVAvSVB2Nua1gemHj-ebkeaOpw=="></span>
### View IP/IPv6 traffic monitoring

If an EIP in a Bandwidth Package experiences traffic exception, it may occupy the bandwidth of the Bandwidth Package, affecting the use of other cloud resources. You can query the top\-ranked EIPs by certain metrics (such as, inbound/outbound bandwidth) within a specific period to quickly identify cloud resources with traffic exceptions.


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. In the Bandwidth Package instance list, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fed8c20937b7c69e69997eca49fb2c3.png) </span>monitor icon in the **Monitor** column of the target Bandwidth Package instance, and the Data monitoring window will pop up.

4. In the Data monitoring window, select the **IP traffic**/**IPv6 traffic** tab as needed.

5. Set a query period as needed. You can select 1 hour, 3 hours, 6 hours, 12 hours, 1 day, or a custom period. The granularity for custom periods is minutes, with a minimum of 1 minute and a maximum not exceeding 1 day.

6. Click the sorting icon (descending or ascending) next to the target metric to sort and display EIPs based on that metric, with a maximum of 50 EIPs supported.

   **Monitoring metrics** include inbound and outbound bandwidths.


<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
## View data via the Cloud Monitor console

View monitoring data of the Bandwidth Package in the Cloud Monitor console. For specific procedure, see [Viewing cloud service monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor).
