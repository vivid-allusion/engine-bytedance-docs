---
title: "Configure Cerebro private network IP allowlist"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/private-IPallowlist-Cerebro"
---

The instance supports private network access by default, allowing all devices within the same VPC environment to access the visualization tool. It is recommended to configure a private network IP allowlist to restrict access to the visualization tool from specific private network IP addresses.

<span id="dcc3d51b"></span>
## Precautions

When configuring the IP allowlist, you can specify a single IP address or an IP subnet. Please follow the format requirements:


* IP address format: must be a valid IPv4 address consisting of four integers between 0 and 255, separated by dots.

* CIDR subnet: should be in standard format, with the IP and mask matching.

   * The IP address must be a network address, which is the first address in the subnet; all host bits must be zero.

   * The network prefix length ranges from `0 to 32`. `/0` is valid, representing the entire IPv4 address space (0.0.0.0/0); `/32` indicates a single host address.

   * Reserved IP ranges such as the loopback address 127.0.0.0/8 must not be used.

   * Configuration of 0.0.0.0/x is not allowed.

   
   |**Example of a valid CIDR** |**Example of an invalid CIDR** |
   |---|---|
   |* 192.168.0.0/24: a valid Class C network address;<br><br>* 10.0.0.0/8: a valid Class A network address;<br><br>* 172.16.0.0/12: a valid Class B network address. |* 192.168.1.1/24: not a network address (the last octet is not 0);<br><br>* 192.168.0.0/33: invalid prefix length (exceeds 32);<br><br>* 256.0.0.0/24: invalid IP address (the first octet exceeds 255);<br><br>* 192.168.01.0/24: format error (the third octet has leading zeros). |
   


<span id="f552d83d"></span>
## Configure private network IP allowlist


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation bar, select **Instance management \> Visulization configuration**, then click **IP allowlist configuration** after the **Private network access address** on the **Cerebro** card.

5. In the **IP allowlist configuration** dialog, add the IP addresses that need continued access to the visualization tool, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring the IP allowlist, you need to understand the following precautions:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cerebro and Kibana/Dashboards share one IP allowlist configuration; adding or deleting an entry applies to both simultaneously.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">IP allowlist configuration supports single IP addresses or IP subnet formats, with multiple IP addresses separated by commas.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports up to 300 IP addresses and network segments in the allowlist.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using CIDR segments, ensure the format is standard and the IP matches the mask. For detailed format requirements, see <a href="https://docs.byteplus.com/docs/cloudsearch/private-IPallowlist-Cerebro#dcc3d51b">Precautions</a>.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example: <code>192.168.0.0/16</code>, if you enter <code>192.168.1.0/16</code>, it is incorrect.   </div>
   

6. View IP allowlist configuration progress.

   Return to the Instances page, the instance status shows as **Updating**. When the status shows **Running**, it means the IP allowlist configuration is successful. Only IP addresses added to the allowlist can access the visualization tool.
