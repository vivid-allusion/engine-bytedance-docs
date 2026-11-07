---
title: "NAT Gateway smart scheduling"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/NAT_Gateway_smart_scheduling"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When an Internet NAT Gateway is bound to Elastic IP Addresses (EIPs) from multiple line operators, you can enable the smart scheduling feature. This allows the gateway to prioritize allocating an EIP from the same line operator as the destination IP as the source IP address, thereby avoiding cross\-line operator network latency.

Before enabling smart scheduling: When an Elastic Compute Service (ECS) accesses the internet, the Internet NAT Gateway randomly selects an EIP. This may result in network latency due to cross\-line operator access.

After enabling smart scheduling: When an ECS accesses the internet, the Internet NAT Gateway identifies the line operator of the destination and precisely assigns an EIP from the corresponding line operator, avoiding network latency caused by cross\-line operator access.

<span id=".5pON5L2c6K-05piO"></span>
## Scheduling process

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* Enabling or disabling smart scheduling on the Internet NAT Gateway does not affect established connections; it only applies to newly created connections.

* The Internet NAT Gateway must be bound to at least two different types of EIPs from the following: China Mobile, China Telecom, China Unicom, and BGP Multi\-line, in order to enable the smart scheduling feature.

* After enabling Smart scheduling on the Internet NAT Gateway, the logic for selecting EIP will change. If the bandwidth of the configured EIP is too small, packet loss may occur due to rate limiting.


<span id=".5byA5ZCv5pm66IO96LCD5bqm"></span>
## Enable smart scheduling


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. Click  **... \> Smart scheduling** at the right of the target Internet NAT Gateway.

4. Turn on the smart scheduling switch.

5. (Optional) Select the ISP and configure the scheduling policy.

   * Supports China Mobile, China Unicom, China Telecom, and BGP Multi\-line.

   * The priority is determined by the selection order of the ISP by default, and the priority order can be manually adjusted.

6. Click **OK** to complete the action.


<span id=".5YWz6Zet5pm66IO96LCD5bqm"></span>
## Disable smart scheduling

Disabling smart scheduling will automatically delete the scheduling policy.


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. Click  **···\> Smart scheduling** at the right of the target Internet NAT Gateway

4. Turn off the smart scheduling switch: click **Disable** to complete the action.
