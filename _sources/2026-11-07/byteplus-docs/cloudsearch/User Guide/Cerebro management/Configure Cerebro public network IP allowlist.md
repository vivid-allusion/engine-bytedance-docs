---
title: "Configure Cerebro public network IP allowlist"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configure_Cerebro_public_network_IP_allowlist"
---

After enabling Cerebro public network access, all public IPs are blocked by default. It is recommended to configure a public network IP allowlist to restrict which public IPs can access Cerebro. This topic explains how to configure the Cerebro public network IP allowlist.

<span id="yAzK7K7z"></span>
## Precautions

When configuring the IP allowlist, you can specify a single IP address or an IP subnet. Pay attention to the following format requirements:


* IP address format: must be a valid IPv4 address consisting of four integers between 0 and 255, separated by dots.

* CIDR subnet: must follow the standard format with a matching IP and mask.

   * The IP part must be the network address, the first address in the subnet; all host bits must be zero.

   * Network prefix length range is `0–32`. `/0` is valid, representing the entire IPv4 address space (`0.0.0.0/0`); `/32` denotes a single host address.

   * Reserved IP ranges such as the loopback address 127.0.0.0/8 must not be used.

   * Configuration as 0.0.0.0/x is not allowed.

   
   |**Valid CIDR examples** |**Invalid CIDR examples** |
   |---|---|
   |* 192.168.0.0/24: valid Class C network address<br><br>* 10.0.0.0/8: valid Class A network address<br><br>* 172.16.0.0/12: valid Class B network address |* 192.168.1.1/24: not a network address (last octet is not 0);<br><br>* 192.168.0.0/33: invalid prefix length (exceeds 32);<br><br>* 256.0.0.0/24: invalid IP address (first octet exceeds 255);<br><br>* 192.168.01.0/24: format error (third octet has leading zero). |
   


<span id="7w3qLQe0"></span>
## Procedure


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **Cerebro** in the left navigation bar, then click **IP allowlist configuration** next to the **Public access address**.

4. In the **IP allowlist configuration** dialog, add the IP address that needs continued access to the visualization tool, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to understand the following when configuring the IP allowlist:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The IP allowlist supports configuration as single IP addresses or IP ranges, separated by commas (,).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Quantity up to 300 supported for IP addresses and ranges.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using CIDR ranges, use the standard format with matching IP and mask. For detailed format requirements, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Configure_Cerebro_public_network_IP_allowlist#yAzK7K7z">Precautions</a>.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, <code>192.168.0.0/16</code> is correct; <code>192.168.1.0/16</code> is incorrect.   </div>
