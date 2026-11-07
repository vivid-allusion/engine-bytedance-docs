---
title: "Configure Cerebro private network IP allowlist"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configure_Cerebro_private_network_IP_allowlist"
---

Cerebro supports private network access by default, allowing all devices within the same VPC to access Cerebro. It is recommended to configure a private network IP allowlist to restrict private network IP addresses that can access Cerebro.

<span id="AtZECnXc"></span>
## Precautions

When configuring the IP allowlist, you can specify a single IP address or an IP subnet. Please follow the required format:


* IP address format: must be a valid IPv4 address consisting of four integers from 0 to 255 separated by dots.

* CIDR subnet: must follow the standard format, with matching IP and mask.

   * The IP address must be the network address, which is the first address in the subnet; all host bits must be zero.

   * The network prefix length ranges from `0 to 32`. `/0` is valid and represents the entire IPv4 address space (`0.0.0.0/0`); `/32` represents a single host address.

   * Reserved IP ranges such as the loopback address 127.0.0.0/8 are not allowed.

   * Configuration of 0.0.0.0/x is prohibited.

   
   |**Example of valid CIDR notation** |**Example of invalid CIDR notation** |
   |---|---|
   |* 192.168.0.0/24: correct class C network address;<br><br>* 10.0.0.0/8: correct class A network address;<br><br>* 172.16.0.0/12: correct class B network address. |* 192.168.1.1/24: not a network address (the last octet is not 0);<br><br>* 192.168.0.0/33: invalid prefix length (exceeds 32);<br><br>* 256.0.0.0/24: invalid IP address (first octet exceeds 255);<br><br>* 192.168.01.0/24: format error (third octet has leading zero). |
   


<span id="zLynrBIv"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **Cerebro** in the left navigation bar, then click **IP allowlist configuration** after the **Private network access address**.

4. In the **IP allowlist configuration** dialog, add the IP addresses that need continued access to the visualization tool, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to be aware of the following when configuring the IP allowlist:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The IP allowlist supports configuration for single IP addresses or IP subnets, separated by commas (,).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The allowlist supports a quantity of up to 300 IP addresses and subnets.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using CIDR subnets, ensure they follow the standard format with correct matching of IP and mask.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example: <code>192.168.0.0/16</code>, if you enter <code>192.168.1.0/16</code>, it is incorrect.   </div>
