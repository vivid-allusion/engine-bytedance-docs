---
title: "Enabling or disabling private network egress (old version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-Old-version"
---

Private Network Egress enables ArkClaw to access internal enterprise network resources via Virtual Private Cloud (VPC), providing enhanced security and control. The private network egress is disabled by default​ after the ArkClaw Enterprise service is enabled. This topic describes how to enable and configure a private network egress.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic provides the instructions for the old version of the network configuration interface. We recommend upgrading to the new version for more management capabilities. To upgrade, find your Space ID in <a href="https://console.byteplus.com/arkclaw/enterprise">the ArkClaw Enterprise console</a> and <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


<span id="a0OPOpxd"></span>
## **Use limits**


* The private network egress cannot be enabled​ if the VPC hosting your enterprise services is already connected to the ArkClaw VPC via Transit Router (TR) or Cloud Enterprise Network (CEN).

* After the private network egress is configured, if you need to modify the VPC or subnet, you must first disable the private network egress and then re\-enable it.


<span id="Ih9f2YzL"></span>
## Procedure


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the "Network Configuration" page, click the "Configuration" tab.

4. Click "Edit" to the right of "Private network egress".

5. In the Private network egress section, configure the private network information based on the table below.

   
   |Configuration item |Description |
   |---|---|
   |Configure private network egress |Specify whether to enable private network egress.<br><br><br>* After enabling the private network egress, ArkClaw instances communicate with enterprise services over the private network, ensuring more secure and controllable access.<br><br>* If disabled, no additional parameters need to be configured. |
   |**Basic information** ||
   |VPC |Select the VPC to which the enterprise service belongs. |
   |Availability zone and subnet |Select the two availability zones and subnets to which the private network egress belongs. Subnets are used to allocate private IP addresses for the private network egress. Private network egress will occupy 6 private IP addresses in each subnet to ensure access performance. |
   |Security groups |Select the security group associated with the private network egress. You can configure up to 4 groups simultaneously.<br><br><br>* The private network egress only carries outbound traffic initiated by ArkClaw. Therefore, only outbound rules in the security group apply to it.<br><br>* When private network egress instances are deployed across two availability zones, they share the same security group configuration. For more information, see [Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). |
   |**Specify access destination** ||
   |Specify destination IP range |Enter the IP address or CIDR block where your enterprise services are located.<br><br><br>* The specified addresses or blocks must not fall within the following ranges: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/0`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, or `169.254.0.0/16`.<br><br>* You can specify up to 50 entries at a time. Separate multiple addresses or blocks with commas (,). |
   |**DNS resolution configuration** ||
   |DNS resolution configuration |Specify whether to enable DNS resolution.<br><br><br>* If disabled, ArkClaw forwards DNS queries from the Space to BytePlus DNS servers (`100.96.0.2` and `100.96.0.3`).<br><br>* If enabled, ArkClaw forwards DNS queries from the Space to the specified external DNS server. This is suitable for resolving enterprise internal domains (e.g., \*.internal.corp). |
   |External DNS system IP address and port |Specify the IP address and port of the external DNS server.<br><br><br>* Currently only IPv4 addresses are supported. Up to 10 external DNS server addresses are allowed.<br><br>* The DNS server address cannot be set to system\-reserved addresses: `100.96.0.2` and `100.96.0.3`.<br><br>* "Port" is optional. It defaults to 53 (standard DNS port) if left blank. Manual input is required only when the listening port is not 53 for the enterprise DNS server. |
   |Forwarding domain |Specify the domain that needs to be resolved by an external DNS server, and press Enter to confirm. Domains not specified will still be resolved by BytePlus DNS server.<br><br><br>* Batch pasting of multiple domains is supported. Separate the domains with commas (,).<br><br>* A maximum of 500 domains can be added for forwarding.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If cross\-border public acceleration is enabled, we recommend that the forwarding domains do not overlap with the acceleration domains. If a domain is configured for both forwarding and public acceleration, requests for that domain will be prioritized to go through the acceleration path. This may cause access failures as requests bypass internal DNS resolution. Run <code>nslookup <domain></code> inside the Claw instance to verify the resolution path. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-cross-border-acceleration-policy-new-version">Learn more</a></div><br> |
   

6. Click "OK" to complete the action.
