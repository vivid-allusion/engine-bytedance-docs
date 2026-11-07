---
title: "Viewing monitoring data"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Viewing-monitoring-data"
---

Elastic IP Addresses (EIPs) are integrated with Cloud Monitor, enabling real\-time monitoring of service metrics and Cloud DDoS Protection_Basic events for the EIP.


* Metric monitoring: View traffic, packets, bandwidth utilization, and other metrics of EIP instances via the EIP console or CloudMonitor console. You can configure alert policies for key services of the EIP by setting metric thresholds and alert notifications to promptly detect metric exceptions and ensure stable business operations. For specific monitoring metrics of an EIP, see [EIP monitoring metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_EIP).

* Event monitoring: Record and notify EIP event information. When an instance triggers a system event (e.g., DDoS attack begins), you can promptly view the event details and take action.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IAM users cannot directly view EIP monitoring data. To view it, the toor account associated with the IAM user must grant CloudMonitor permissions to the IAM user. For procedure, see <a href="https://docs.byteplus.com/en/docs/eip/EIP-FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf">Why can't IAM users view monitoring data</a>.</div>


<span id=".5p-l55yL5oyH5qCH55uR5o6n"></span>
## View metric monitoring

<span id=".5YWs572RSVDmjqfliLblj7Dmn6XnnIs="></span>
### View data via the EIP console


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fed8c20937b7c69e69997eca49fb2c3.png) </span>monitor icon under the **Monitoring** column of the target EIP, and the Data monitoring window will pop up.

4. In the Data monitoring window, you can view various monitoring metrics of the current EIP.

   * Support viewing EIP metrics, such as outbound/inbound traffic, outbound/inbound data packets, outbound/inbound bandwidth, outbound/inbound packet rate, outbound/inbound rate\-limiting packet loss rate, and outbound/inbound bandwidth utilization.

   * Click the **Period** and **Method** (default, average, maximum, minimum, sum) dropdowns to customize the monitoring data view.

   * Click the **Legend** dropdown on the right side of the page **,**  and select **Table** to view the extremes of each monitoring metric.


<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
### View data via the Cloud Monitor console

View the monitoring data of an EIP in the Cloud Monitor console. For detailed steps, see [Viewing cloud product monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor).
