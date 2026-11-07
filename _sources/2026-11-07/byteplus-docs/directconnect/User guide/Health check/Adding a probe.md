---
title: "Adding a probe"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Adding_a_probe"
---

<span id="mrLdzmf1"></span>
## Scenarios

After creating a health check instance, you also need to add a probe to the instance. Direct Connect probes collect link delay and packet loss data in real time by continuously sending ICMP packets from a specific source IP within the Virtual Private Cloud (VPC) to a specified destination IP on\-premises.

<span id="mrLdzmf1"></span>
## Procedure


1. Log in to [the Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select your target region.

3. Select **Health Check** in the left\-side navigation pane.

4. Click the target instance name, then click the **Probe** tab.

5. Click **Add Probe** and configure the probe based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Source configuration** |||
   |VPC |Select the VPC where the probe is located. |vpc\-01 |
   |Subnet |Select the subnet where the probe is located. Changes are not supported after selection. The source IP will be randomly assigned within the subnet. Please choose carefully. |subnet\-01 |
   |**Destination configuration** |||
   |Destination configuration |Add the destination IP of the probe.<br><br><br>* IP address: Currently supports only IPv4 format.<br><br>* Protocol: Currently supports ICMP.<br><br>* Packet size: Set the packet size based on actual business requirements to allocate bandwidth resources reasonably. You can enter an integer in the range of 56 to 8500. |10.XX.XX.4\|ICMP\|56 |
   

6. Click **Add** to complete the action.
