---
title: "Creating a health check"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating_a_health_check"
---

<span id="V8AbZUHz"></span>
## Scenarios

Direct Connect Health Check offers monitoring of the link quality between the cloud Virtual Private Cloud (VPC) and the remote network. By actively sending probe requests, the health check monitors network link status in real\-time. By integrating with CloudMonitor metrics and alerts, it promptly identifies issues and takes corresponding measures to ensure stable business operations.

<span id="zSr81xo7"></span>
## Limits

Each health check instance supports specifying only one subnet as the monitoring source. The source IP is randomly allocated within the specified subnet and cannot be specified manually. For more about quota limits, see [Limits](https://docs.byteplus.com/en/docs/directconnect/Limits#.6YWN6aKd6ZmQ5Yi2).

<span id="zSr81xo7"></span>
## Procedure


1. Log in to [the Direct Connect console.](https://console.byteplus.com/dc/PhysicalConnection)

2. In the top menu bar, select your target region.

3. Select **Health Check** in the left\-side navigation pane.

   > When you use Health Check for the first time, follow the interface guidance to complete VPC cross\-service authorization.   
   

4. Click **Configure Health Check** and configure the health check parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region from where the data center accesses the cloud ingress (i.e. DC Gateway).<br><br>Private networks in different regions are isolated. We recommend selecting a region closest to your business for lower network delays and faster access. |China (Beijing) |
   |Name |Set the name of the health check instance. |JKJC\-01 |
   |**Source configuration** |||
   |DC Gateway |Select the DC Gateway associated with the target DC Connection. |China (Beijing) \| Dcg\-123 |
   |VPC |Select the VPC where the target monitoring source IP is located.<br><br>Only the VPC in the same region as the health check instance is supported. |vpc\-01 |
   |Subnet |Select the subnet where the target monitored source IP is located. Changes are not supported after selection. Proceed with caution. |subnet\-01 |
   |**Destination configuration** |||
   |Destination configuration |Add a destination IP, supporting up to 4 IPs.<br><br><br>* IP address: Currently supports only IPv4 format.<br><br>* Protocol: Currently supports ICMP.<br><br>* Packet size: Set the packet size based on actual business requirements to allocate bandwidth resources reasonably. You can enter an integer in the range of 56 to 8500. |10.XX.XX.4\|ICMP\|56 |
   

5. Click **Create** to complete the action.


<span id="fUy3Tnxi"></span>
## What to do next


* [Add probe](https://docs.byteplus.com/en/docs/directconnect/Adding_a_probe): Add a probe to collect network traffic data.

* [Set CloudMonitor event alerts](https://docs.byteplus.com/en/docs/directconnect/Configuring-event-monitoring-alerts): When network link status deteriorates and poses a risk, you can receive CloudMonitor alerts and take timely action.
