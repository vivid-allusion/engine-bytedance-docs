---
title: "Viewing monitoring data"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Viewing-monitoring-data-vpcnat"
---

This topic describes how to view the monitoring data of an Internet NAT gateway and a Virtual Private Cloud (VPC) NAT gateway. For more information, see [the Internet NAT gateway metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_NAT) and [the VPC NAT Gateway metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_PrivateNAT).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">VPC NAT Gateway is a beta feature and is available for trial only to accounts that have completed <a href="https://docs.byteplus.com/en/docs/6261/64937">enterprise authentication</a>. To request a trial, first complete real\-name authentication, then contact your account manager to enable feature permissions.</div>


* <div data-tips="true" data-tips-type="tip">Identity and Access Management (IAM) users cannot directly view the monitoring data of the Internet or VPC NAT gateways. To view the data, the primary account of the IAM user must grant CloudMonitor permissions to the IAM user. For specific operations, see <a href="https://docs.byteplus.com/en/docs/natgateway/Identity-and-Access-Management-FAQ#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf">Why IAM users cannot view monitoring data</a> .</div>



<span id=".5YWs572RL-engee9kU5BVOaOp-WItuWPsOafpeeciw=="></span>
## View monitoring data on the Internet/VPC NAT Gateway console

Following this procedure, you can view the connection counts, outbound/inbound monitoring metrics of Internet/VPC NAT gateways during a specified period. Support viewing IP traffic monitoring, helping you quickly identify the ECS instances with traffic exceptions.


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats) or [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select a target region and project.

3. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fed8c20937b7c69e69997eca49fb2c3.png) </span> icon in the **Monitor** column of the target Internet/VPC NAT Gateway instance.

4. Switch tabs to view different monitoring metric data of the current Internet/VPC NAT gateway respectively.

   * **Connection: ** Supports viewing maximum connections, new connections per second (CPS), connection drops, CPS drops, port allocation errors, and connection utilization.

   * **Outbound: ** Supports viewing outbound traffic, outbound bandwidth, outbound bandwidth usage, outbound packet count, outbound packet rate, outbound scheduling bandwidth, and outbound rate\-limiting packet loss.

   * **Inbound: ** Supports viewing inbound traffic, inbound bandwidth, inbound bandwidth usage, inbound packet count, inbound packet rate, inbound scheduling bandwidth, and inbound rate\-limiting packet loss.

   * **IP traffic monitoring**

      * Set a query period as needed. You can select 1 hour, 3 hours, 6 hours, 12 hours, 1 day, or a custom period. The granularity for custom periods is minutes, with a minimum of 1 minute and a maximum not exceeding 1 day.

      * Click the sorting icon (ascending or descending) next to the target metric. The page displays up to 50 IP addresses sorted in a descending or ascending order based on the metric.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When no data is collected for a monitoring metric of an IP address within a specified time period, 0 is displayed for that metric. In this case, if you sort IP addresses based on this metric, the IP address with a metric value of 0 is not displayed.      </div>
      

<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
## View data via the Cloud Monitor console

View the monitoring data of Internet/VPC NAT gateway in the CloudMonitor console. For details, see [Viewing cloud product monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor).
