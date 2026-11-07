---
title: "Enabling or disabling private network egress (new version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-New-version"
---

Private Network Egress enables ArkClaw to access internal enterprise network resources via Virtual Private Cloud (VPC), providing enhanced security and control. The private network egress is disabled by default​ after the ArkClaw Enterprise service is enabled. This topic describes how to enable and configure a private network egress.

<div data-tips="true" data-tips-type="default">Notes</div>


<div data-tips="true" data-tips-type="default">If you are unable to use the new version of Network Configuration, go to <a href="https://console.byteplus.com/arkclaw/enterprise">the ArkClaw Enterprise console</a> to find your Space ID, and <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to upgrade the Space.</div>


<span id="CnJYS7cH"></span>
## **Use limits**


* The private network egress cannot be enabled​ if the VPC hosting your enterprise services is already connected to the ArkClaw VPC via Transit Router (TR) or Cloud Enterprise Network (CEN).

* After the private network egress is configured, if you need to modify the VPC or subnet, you must first disable the private network egress and then re\-enable it.


<span id="DBV9f4Ya"></span>
## Procedure


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the Network Configuration page, click the "Space Egress \> Private network egress" tab.

4. Click "Edit" to the right of "Private network egress", and configure the private network information based on the table below.

   
   |Configuration item |Description |
   |---|---|
   |Configure private network egress |Specify whether to enable private network egress.<br><br><br>* If enabled, ArkClaw instances communicate with enterprise services over the private network, ensuring more secure and controllable access.<br><br>* If disabled, no additional parameters need to be configured. |
   |**Basic information** ||
   |VPC |Select the VPC to which the enterprise service belongs. |
   |Availability zone and subnet |Select the two availability zones and subnets to which the private network egress belongs. Subnets are used to allocate private IP addresses for the private network egress. Private network egress will occupy 6 private IP addresses in each subnet to ensure access performance. |
   |Security group |Select the security group associated with the private network egress. You can configure up to 4 groups simultaneously.<br><br><br>* The private network egress only carries outbound traffic initiated by ArkClaw. Therefore, only outbound rules in the security group apply to it.<br><br>* When private network egress instances are deployed across two availability zones, they share the same security group configuration. For more information, see [Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). |
   |**Specify access destination** ||
   |Specify destination IP range |Enter the IP address or CIDR block where your enterprise services are located.<br><br><br>* The specified addresses or blocks must not fall within the following ranges: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/0`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, or `169.254.0.0/16`.<br><br>* You can specify up to 50 entries at a time. Separate multiple addresses or blocks with commas (,). |
   

5. Click "OK" to complete the action.
